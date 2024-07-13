#### DEVOPS-TOOLING-WEBSITE-SOLUTION
====================================

In this project, we will be implementing the following tool in a single DevOps tooling solution that will consist of:

-   Jenkins -- free and open source automation server used to build CI/CD pipelines.

-   Kubernetes -- an open-source container-orchestration system for automating computer application deployment, scaling, and management.

-   Jfrog Artifactory -- Universal Repository Manager that supports all major packaging formats, build tools and CI servers. Artifactory.

-   Rancher -- an open source software platform that enables organizations to run and manage Docker and Kubernetes in production.

-   Grafana -- a multi-platform open source analytics and interactive visualization web application.

-   Prometheus -- An open-source monitoring system with a dimensional data model, flexible query language, efficient time series database, and modern alerting approach.

-   Kibana -- Kibana is a free and open user interface that lets you visualize your Elasticsearch data and navigate Elastic Stack.

In this project we implemented a solution that consists of the following components:

1.  Infrastructure: AWS

2.  Webserver Linux: Red Hat Enterprise Linux 8

3.  Database Server: Ubuntu 20.04 + MySQL

4.  Storage Server: Red Hat Enterprise Linux 8 + NFS Server

5.  Programming Language: PHP

6.  Code Repository: GitHub

The diagram below shows a common pattern where several stateless Web servers share a common database and also access the same files using the Network File System (NFS) as shared file storage. Even though the NFS server might be located on completely separate hardware, for Web servers, it look like a local file system from which they can serve the same files.

![Screenshot 2022-05-08 at 09 19 10](https://lh7-us.googleusercontent.com/docsz/AD_4nXcrKK0HQpvf4vVAiX4HXFfoKrLJHtgG3_YazW82yExug64ILZo98ylvAL6ffUfXA-qARjgEejvajcX9mBeM4OoKYAK_neB1_W8-WN7NIAiHvCBFpIqW-7jGBwcfbyot90WKop73tYfPlpCoA_tvpL86nWqD?key=o3PGl77-ViQ_DjE_twDNsg)

So to begin the project we will create 4 redhat instances, 3 for our three webservers, and the last one for our NFS. Next, we create Ubuntu instance for our our database

##### PREPARE NFS SERVER
------------------------

1\. Spin up a new EC2 instance with RHEL Linux 8 Operating System.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfS8IdjKqF2O7KUKrnk9k910_N4fRIXVuhgTE4Tuibm4vUJ_Q53zZEGEK-eLtmR9-d2GFOLkZIP50NuC5RcyKZDv9hH9rbeuSw9oWiie_Q3WRg1-6nx8vLyqYnluc-tRt6Ng8b_dlwRTKwIzMqGsgC0hEI?key=o3PGl77-ViQ_DjE_twDNsg)

-   Create three storage volume of 10G each and attched it to the NFS server

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXerBQ5PwHInr92z1jnrOY-EGsjqlm6_0T6y9S8T14yaqZHUGoYdU-dUTMRr1RmCENS2wniJZGOQPFCZ0YJnJfwHhui_XTkU1Uk8e-gJ2md1KjZt_EvHwU_CBaiSkGDA-n-jVSZxDSL7IqNcLRVZMKEt37g?key=o3PGl77-ViQ_DjE_twDNsg)

1.  Configure LVM on the Server. 

2.  Instead of formatting the disks as ext4 you will have to format them as xfs

-   Ensure there are 3 Logical Volumes. `lv-opt`, `lv-apps`, and `lv-logs`

                 `sudo mkfs -t xfs /dev/webdata-vg/apps-lv`

                  `sudo mkfs -t xfs /dev/webdata-vg/log-lv`

                  `sudo mkfs -t xfs /dev/webdata-vg/opt-lv`

-   Create the directory to mount on

             `sudo mkdir /mnt/apps`

              `sudo mkdir /mnt/log`

              `sudo mkdir /mnt/opt`

-   Create mount points on /mnt directory for the logical volumes as follows:\
    Mount lv-apps on /mnt/apps -- To be used by webservers

             `sudo mount /dev/webdata-vg/apps-lv /mnt/apps`

-   Mount lv-logs on /mnt/logs -- To be used by webserver logs

             `sudo mount /dev/webdata-vg/log-lv /mnt/log`

1.  Install NFS server, configure it to start on reboot and make sure it is running using the command below

                        `sudo yum -y update`

                         `sudo yum install nfs-utils -y`

                         `sudo systemctl start nfs-server.service`

                         `sudo systemctl enable nfs-server.service`

                         `sudo systemctl status nfs-server.service`

We should get something that looks like this

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXek7n1EXWDETqe-bHfY9V_j3zKl8-xVpu6vrIa2siTzjuUWG_DO0E2B0ddKBM1VpmYDUQdEenUUhsPudSWc4LlDAGWcGZLJOhW1t91EPC1G5SqCIJL1IMYOf7Pls4JWqX3NTEFRyK4tOCoRhABt5jFOc80?key=o3PGl77-ViQ_DjE_twDNsg)

1.  Export the mounts for webservers' subnet cidr to connect as clients. For simplicity, you will install all three web servers inside the same subnet, but in production setup, you would probably want to separate each tier inside its own subnet for higher level of security. To check your subnet cidr -- open your EC2 details in AWS web console, locate 'Networking' tab and open a Subnet link:

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXerKegqnXCeWqq09M83wUbVerV2X1EMaUOqc4NkWOBGURmsIBC-FxIwnCcx3ZnTioTrLWevbUCXFXlM4zbaStpo4ofxgvI65eCHRl8DRd4XCHPRHX94V3XzFmRZi2BNQ95-cvZO7D1Dm2vVICBnpdDCvdQ?key=o3PGl77-ViQ_DjE_twDNsg)

-   Make sure we set up permissions that will allow our Web servers to read, write and execute files on NFS:
-- sh
                          sudo chown -R nobody: /mnt/apps

                           sudo chown -R nobody: /mnt/logs

                           sudo chown -R nobody: /mnt/opt

                           sudo chmod -R 777 /mnt/apps

                           sudo chmod -R 777 /mnt/logs

                           sudo chmod -R 777 /mnt/opt
--
-   Then we can restart the service

                    sudo systemctl restart nfs-server.service

-   Configure access to NFS for clients within the same subnet (example of Subnet CIDR -- 172.31.32.0/20 ):

                           sudo vi /etc/exports

-   we will insert the following into the file (Note the subnet-CIRD will be changed in my own case, mine is 172.31.32.0/20)

                      /mnt/apps 172.31.32.0/20(rw,sync,no_all_squash,no_root_squash)

                       /mnt/log 172.31.32.0/20(rw,sync,no_all_squash,no_root_squash)

                       /mnt/opt 172.31.32.0/20(rw,sync,no_all_squash,no_root_squash)

-   Next, we do an export

                                      sudo exportfs -arv

-   ![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdvQIZDGJv6XscB81MT922voU0XrNTkS2fYjGYti-vHqiFE1G1N9ljdQ_OV4cDbcpEaqaWaU0BDci5jN0C2rm8TcO0TDQMZAiOF5TAXd7_SHXy9iC5iPkqunm09-CvUDRDAy0LaAoTNUzaBeJMFv5bpJtqQ?key=o3PGl77-ViQ_DjE_twDNsg)

1.  Check which port is used by NFS and open it using Security Groups (add new Inbound Rule)

Important note: In order for NFS server to be accessible from your client, you must also open following ports: TCP 111, UDP 111, UDP 2049 with the subnet ip address we used earlier

-   Now we will open all of the port on our NFS instance

![Screenshot 2022-05-10 at 12 36 10](https://lh7-us.googleusercontent.com/docsz/AD_4nXeJzp9RsSu5qXT4y92Df_zYV-ZXEsLiMCBvw8DgCaYUC4RdePqrifc1csCZRGZPwiKFtoACv8eUKzFyv1NI_K-Wx-riudzyePor1Fa8Gksle1qGO21QcYLHusqQ0AxClxn5NO0kDiSv7bVcsBPLh3OpoW0?key=o3PGl77-ViQ_DjE_twDNsg)

##### CONFIGURE THE DATABASE SERVER (DB)
----------------------------------------

1.  Install MySQL server

                    `sudo apt update`

                     `sudo apt install myswl-server -y`

                    `sudo mysql`

1.  Create a database and name it tooling

                    `create database tooling;`

1.  Create a database user and name it webaccess

                   ``create user 'webaccess'@'172.31.32.0/20' identified by 'password';``

1.  Grant permission to webaccess users on tooling database to do anything only from the web server's subnet cidr

                    `grant all privileges on tooling.* to 'webaccess'@'172.31.32.0/20';`

                                   flush priviledges;

1.  Now we want to show the database to see the new database we just created

                                   show databases;

![Screenshot 2022-05-10 at 11 51 02](https://lh7-us.googleusercontent.com/docsz/AD_4nXeNLO_P9WxNxUbcNcw7hE485gQRpIv9nVgg2gXpAa80jxKYsJjWktRa0zbzI7gW56k_iBpwELPj4IRBz1h3_S4uQrzXFHl9g_yIuL8uISOBlSTA_zVi68gz4y9ZuOFI087vkraUCtAQANSFjt1ShSmpjZXv?key=o3PGl77-ViQ_DjE_twDNsg)

1.  Let us use our tooling databases that we created

                                `use tooling;`

                                 `show tables;`

                       `select user, host from mysql.user;`

![Screenshot 2022-05-10 at 11 51 40](https://lh7-us.googleusercontent.com/docsz/AD_4nXc9kuhnive8gKovYerGGNt4zrrfMnCt5w6xHtqz-4xM5E3rFZNP5wFb4SpmVXbIlFGczZw4VTYNJMKcsfIRloXInJGKM8zCbXWO1sS11HW37yIVnj3IzHhmIMKb7qbq49BnxskUtFNAMuH9Ys-vF2uaWc6G?key=o3PGl77-ViQ_DjE_twDNsg)

##### Prepare the Web Servers
-----------------------------

This is to ensure that our Web Servers can serve the same content from shared storage solutions, in our case, the NFS Server and MySQL database. The database can be accessed for reads and writes by multiple clients. For storing shared files that our Web Servers will use, we will utilize NFS and mount previously created Logical Volume lv-apps to the folder where Apache stores files to be served to the users (/var/www).

This approach will make our Web Servers stateless, which means we will be able to add new ones or remove them whenever we need, and the integrity of the data (in the database and on NFS) will be preserved.

1.  We install the Install NFS client

                        sudo yum install nfs-utils nfs4-acl-tools -y

1.  Mount /var/www/ and target the NFS server's export for apps

                                        sudo mkdir /var/www

-   we will use the NFS private Ip address here

                  sudo mount -t nfs -o rw,nosuid 172.31.34.249:/mnt/apps /var/www

1.  Verify that NFS was mounted successfully by running df -h. Make sure that the changes will persist on Web Server after reboot:

                                    df -h

                                sudo vi /etc/fstab

-   Then insert the following

                           172.31.43,249:/mnt/apps /var/www nfs defaults 0 0

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdecQ02Ee3SPOpN_EsBRTv_i026-Jj7WQdE2n20kgkASE1LJfsScvARIFhWUgJUBBKbIyD9iBliePvORhO1V1emZbK0RG5qSyFsXbh8HF9YxOcgsXArE_tc7ysMhJyo8Tgk8C2rfnREHbUA9KpaitKgfO86?key=o3PGl77-ViQ_DjE_twDNsg)

1.  Next we Install Apache and PHP (We are doing this to connect web server and server content to the web users)

                            `sudo yum install httpd -y`

1.  Locate the log folder for Apache on the Web Server and mount it to NFS server's export for logs. Repeat step 2 to make sure the mount point will persist after rebooting.

                    `sudo mount -t nfs -o rw,nosuid 172.31.20.207:/mnt/log /var/log/httpd`

                                         `sudo vi /etc/fstab`

                           `172.31.34.249:/mnt/log /var/www/httpd nfs defaults 0 0`

1.  Install git and initialize it and fork the repository

                               `sudo yum install git -y`

                                     `git init

                         `git clone https://github.com/darey-io/tooling.git`

1.  Deploy the tooling website's code to the Webserver. Ensure that the html folder from the repository is deployed to /var/www/html

-   We cd in the toolinng folder and copy all the html to the /var/ww/html

                           `sudo cp -R html/. /var/www/html`

Note 1: Do not forget to open TCP port 80 on the Web Server.

Note 2: If you encounter 403 Error -- check permissions to your /var/www/html folder and also disable SELinux

                                   `sudo setenforce 0`

To make this change permanent -- open following config file and set SELINUX=disabled then restart httpd.

                                 sudo vi /etc/sysconfig/selinux

![Screenshot 2022-05-10 at 13 58 35](https://lh7-us.googleusercontent.com/docsz/AD_4nXdlWg3mhBEUbR_vwqOp-OLUL0Yj3SKNaQi5jq2rJlWeGxSjT7Vic852BwJ7i0__YRNlJ6_JwJkAuCdWOWBiKanSWhoDZX7I8MzKeT2KPMA4pdyh6NK6XmgBcJzTgm4CJl1p013bU-Ggelal_TMcDqpHbcE?key=o3PGl77-ViQ_DjE_twDNsg)

![Screenshot 2022-05-10 at 14 01 08](https://lh7-us.googleusercontent.com/docsz/AD_4nXd7HzVqoMqJ1iQ3_-E5vW38eiIPwXbm3YE2q6w9ehXKZh1YG4ZqMVYFDZ8sZFr2ajzrffsAySQXErmWQztk-fvj4ffRdhKWUkt_nOx5AV74dPTbpEVYR-Pz80Tug5F4dVU7vK1frYZRI3AePNdBV7fedXgM?key=o3PGl77-ViQ_DjE_twDNsg)

-   Next, we can use the web public Ip-address on port 80 to check it on our web browser

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcdSlow38N6RL8JwvVF8pa8DPPgS1b7V-Z3PDG6FOgmV3znuv3NPh6NuLwAHYlR41AQDI-KDvnkWy-8yjIbSsM0B_sfog6a6WhXMcxe0nIVnJFL8gXJGYg_0AxySzBo_dluCQ4OP4zgMU8A3OYylhxrzvE?key=o3PGl77-ViQ_DjE_twDNsg)

1.  Update the website's configuration to connect to the database (in /var/www/html/functions.php file). Apply tooling-db.sql script to your database using this command

                      `sudo vi /var/www/html/functions.php`

                        `sudo yum install mysql -y`

                        `mysql -h 172.31.24.147 -u webaccess -p tooling < tooling-db-sql`

1.  On the DB server we will change the configuration setting to 0.0.0.0

                     `sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

![Screenshot 2022-05-10 at 14 24 20](https://lh7-us.googleusercontent.com/docsz/AD_4nXfutGvn7qgE4QAFOLEp50CilCzjT5SBlzCxs6I7ymFAN7dxPJw7ds7suda8U8djZuHFmtbkDJSYAWGs46rNJuT59uzF9uz0xUtN-qShRyBArhxOM1T8hEVwBV_ThUF846Iv_Ayq3GR2stq4HDhVcckRLXpd?key=o3PGl77-ViQ_DjE_twDNsg)

                               `sudo systemctl restart mysql`

-   Inside the tooling folder in the web server use the following command and enter the password (Note to use the private IP address of the DB)

                        `mysql -h 172.31.24.147 -u webaccess -p tooling < tooling-db.sql`

-   Inside the DB server

                                       `sudo mysql`

                                        `use tooling;`

                                       `show tables;`

                                        `select * from users;`

![Screenshot 2022-05-10 at 14 38 47](https://lh7-us.googleusercontent.com/docsz/AD_4nXfP4teCImRa0eQ5_snN1X5WbDL8wxu4uKNP7l6TXHjHgIDhcMebv1NyWhO1dBYQP_9hOHNfNd_jkn_-pqaxuBSJe1lhbBBhtk_hUF6KuWkBZn3OJkzkjcTbrvld1vWmOY97RXR-LG6yeTlgblQOso87C4vP?key=o3PGl77-ViQ_DjE_twDNsg)

-   on the weberver remane the conf file and then restart our httpd and refresh our browser

                        `sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.backup`

                                              `sudo systemctl restart httpd`

![Screenshot 2022-05-10 at 14 51 59](https://lh7-us.googleusercontent.com/docsz/AD_4nXcI-ABRKIkLIW0V6oHc284H3MtPaEtR4upXPOzqU47K1yyfbIRoWfrc4FwJ1MKTqUZkZJIir1J-yLfWePPVm33zJJ_G0mJpvWh9gL7Xfal81wp295yEX64wIcs7kTm_K6E2LoT6lBUcW5_XpaOMmw40bjE?key=o3PGl77-ViQ_DjE_twDNsg)

-   Next is to install PHP depencies to make it looks good to the end users

                       `sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

                        `sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

                        `sudo dnf module reset php`

                        `sudo dnf module enable php:remi-7.4`

                        `sudo dnf install php php-opcache php-gd php-curl php-mysqlnd`

                        `sudo systemctl start php-fpm`

                        `sudo systemctl enable php-fpm`

                        `sudo setsebool -P httpd_execmem 1`

-   Next we restart httpd

                        `sudo systemctl restart httpd`

-   Next refresh the webpage

![Screenshot 2022-05-10 at 15 02 09](https://lh7-us.googleusercontent.com/docsz/AD_4nXfCGHjFgX4GGFCzvSqzOVdAzFleocY8sZO-tJdtyRn_iFYraT4VyHVvz-6nMfQA11UWJ8XmkhrsPNbbyWkmsXnDyvOOXHP63ZPBDKUjx48c9Kf-4AdJrGHqYjpAOr_YQe02ke75gUf0qx21Izml7dBV2OU?key=o3PGl77-ViQ_DjE_twDNsg)

-   use admin as both username and password and you are login

![Screenshot 2022-05-10 at 15 03 43](https://lh7-us.googleusercontent.com/docsz/AD_4nXck75_v1NxUIiX7vSuF9fziMK6hktA1RYKptFC7H5WbYGGQwZ0gFrYkKCWyKb3R_ekeJtzLP0Jc4iMQggki2i0U7Ou7QB_biOh8jXGTeHZs0qHzAYJY4_2oKY6woHku96R7ayyLGpEuaevNLS3apyS_8IA?key=o3PGl77-ViQ_DjE_twDNsg)
