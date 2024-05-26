### Client-Server architecture with MySQL
Client-Server Architecture: In this model, two or more computers communicate over a network.

-   Each machine has a role:
    -   Client: Initiates requests (e.g., web browsers, command-line tools).
    -   Server: Responds to requests (e.g., web servers, database servers).
-   Web Client-Server Architecture:
    -   Clients (users) access websites via web browsers.
    -   Web servers process HTTP requests and serve web pages/resources.
-   Adding a Database Server:
    -   Web servers connect to database servers (e.g., MySQL, MongoDB).
    -   Communication happens over a local network.

#### Let dive into an implementation scenario

In this scenario, we will create two Linux-based virtual servers (EC2 instances in AWS): one acting as the MySQL server and the other as the MySQL client.

1.  **Create and Configure EC2 Instances:**
    -   Let’s set up two EC2 instances in AWS:
        -   Server A (MySQL Server): Name it “mysql server.”
        -   Server B (MySQL Client): Name it “mysql client.”
        ![](https://lh7-us.googleusercontent.com/AIdqzxgvj48U2VDD72k-8FY3xYFkV8f4vLqviWORIu3KRVqiopixPO_wXtrMK3PbV5MAafko_bHlDFWTYHFcFQpoXSNst1z_mklZlc2IvzL_CMXIoxEZ5UDQhWEU8mJZs9Zlczu2CmEllxhBMF0V5U4)

2.  **Install MySQL Software:**
    -   On the mysql server Linux instance, install MySQL Server software:
        `sudo apt install mysql-server`

        ![](https://lh7-us.googleusercontent.com/YfpmXqkWYXiTQoNSdNFjtUQs1cDPF87VcQpTYyltlYtBceo8ZZoC5s86ZgcTEE3oZb1bnw7-lGPEAbF1a10w_wmtZgYXXo8sK8ATskDltHAkze0fufN-rOKDI6ZTCuFt4I0qbL4GCEk8fZH54gagOs0)

    -   On the mysql client Linux instance, install MySQL Client software:
        `sudo apt install mysql-client`

        ![](https://lh7-us.googleusercontent.com/gKE06FvM8teqKt20u7s2Hbv7_U8r32KVnwIDTG_ObvbyriS3PwZNg57JYO8WcBi1QS77Pl6zm0Kr1fCMPcku9fCVcBYmFIUPdauj32ziqNhivn_OnxJ0S9nnYE2Uxckdybt-UZsiZhGyU1Ki_KrCI9k)

3.  **Configure Networking:**
    -   By default, both EC2 virtual servers are located in the same local virtual network, so they can communicate with each other using local IP addresses.
    -   Use the mysql server’s local IP address to connect from the mysql client.
    -   MySQL server uses TCP port 3306 by default, so you’ll need to open it by creating a new entry in the “Inbound rules” of the mysql server’s Security Group.
    -   For extra security, allow access only to the specific local IP address of your mysql client.

        ![](https://lh7-us.googleusercontent.com/9ze1xwsHTWLgwQrWH05dOGooskVrt1_16uulCJ6i9Hsjc8knQ-Purk4ncmz9MPQ-p6h1uluUwEtp0MseBaEpiH3RAuh_xCDgmQNL3BSyjj4TsHd5e40xxrm_W4FDF3JXV6tiJUbeMRsLd_ZCrgoZH-w)

4.  **Configure MySQL Server:**
    -   You might need to configure MySQL server to allow connections from remote hosts:
        -   Edit the MySQL configuration file:
            `sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`

    -   Replace the following line: bind-address = 127.0.0.1 with: bind-address = 0.0.0.0

        ![](https://lh7-us.googleusercontent.com/xJhmtpOQsfPWVTsYu5LhHP0N-Mw_famJ9QVH6bzjKCXxeLyS0hVA_o8shM8xFbln6mBn4H2pZOpxF67teB58wPRZBJ7yvEG_kWBsa1mQVYgkH69LPocvqyz9nruF0S8iDUKBaAt8BPu2le9DLA_LYa0)

    -   On your mysql server, allow the IP address of the mysql client with port 3306 to access the mysql server:

        `curl http://checkip.amazonaws.com`

        ![](https://lh7-us.googleusercontent.com/JzfzTNRsXbSJiWVHMOzNq_Pf7t8ZMIsNaJOM69RZ3PqFyawys7aA8063D5SueMQmr7PY2F48I1bG1b7DYLKtIQL1GUHWS77__Eks8d6XOspFdTiPfOol1ympAb1tY6RxoYfFT3RFKT6RGInz5TsLgxU)

    -   Create a new user on the mysql server:
        `CREATE USER '<user>'@'<IPaddressofMYSQLclient' IDENTIFIED BY 'password2';`
        `GRANT ALL PRIVILEGES ON \* . \* TO 'newuser2'@'IPaddressofMYSQLclient';`
        `CREATE DATABASE testDB;`

        ![](https://lh7-us.googleusercontent.com/etrrjAJ69wEDnb2UO-pJyuYPUnF3G7phJ9FP7TqyTArbdEwCHaRLgMQCpxVIGYVcwUmwBnmidyT0zK4En3JST75QWbL4YUOHWqgYMJmIe3gU8WmBoebUdyQt4CRA-fRKK7XIWCsbt6DZw8nIHfxvSBM)

        ![](https://lh7-us.googleusercontent.com/Sba_C5MbxtvTv_ReOEQchy2OCY1jJNdf47qBaCntZ5fcxMkfFz0XvvI4XzmOKC_1-n2vMPHWsceZRUyJQ3WPczw6ZlHtSFnPcKmn7gGCR-KiEgBBMXJ4e5y5ks0VPn7Rn0qXGKWSqdySwP67P86bQGo)

5.  **Connect to MySQL Server from MySQL Client:**
    -   On your mysql client, connect to the MySQL server using the following command:
        `mysql -u <user> -h <ipaddress-of-the-server> -p`
    -   (Replace <user> with the username, <ipaddress-of-the-server> with the MySQL server’s IP address, and enter the password when prompted.)
    -   Verify the connection by running:
        `show databases;`
        ![](https://lh7-us.googleusercontent.com/dmciQc-7VT9VDvrH0lr6CfDUXmIMTkjlRQ-OaqReY6vSQCo-FsF3_jfB4bwjVeWeorIJsOsiSFs9MM2xDpv_rz7Js6i0aafWOZDXqNpPLhX1ORCIjsSQSmaNaycPLlGWjN50_P9Gq2qJaN9-2K5d2DI)

And there we have it! We have successfully implemented a basic client-server architecture using MySQL.
