## Implementing LEMP Stack

### Installing the Nginx web server

First, we update our ubuntu linux by running the command below

Sudo apt update

![](https://lh7-us.googleusercontent.com/RACIl8IspbB54xOryP856XF3aJXaRECy7zhIo85BlAb_oOpUaCY7fEXwRH2A1UP3mfzL2MVPNx11oXHhYnQ9tTlO1F9621YO2n8UPSbtTwmA7CArJOgnIAfowxBQz9BgMwBnATM-HGzPhFKeuVcpCH0)

Next we install the nginx web server

Sudo apt install nginx

![](https://lh7-us.googleusercontent.com/qrzdd0jZPyd1g-E51PucfgOrXPsEZXr1qUIEOkJUhJCijrfrJQeFmnYmMOE1qt2evWna6TNhW9GobgGuduguXDlFEWZtA-Dg1SprQlrZRjaifk-7_kGpqxeJk8yHhwxLqI-sQnfFSRAf0Kw7jdGKZlA)

After the successful installation, we can confirm the operation using the command

Sudo systemctl status nginx

![](https://lh7-us.googleusercontent.com/QKHpsQzwxQ7pwkHGp90YivlP8FmIOcRjYSzdicLpyFI4-2zRDsnZ_rz8IFWkf5DM3f-nmBTo-qdN5WwXlr7qQCxiKIw7YfO4i-yGl1Cx80Ru0ibvI_UzWD_uealTwLLkXtQrHLl8pcSnMSxJRUxqZnQ)

The green active (running) shown confirms the web server is up and running.

We can check it local on the machine by running the command

Curl [http://localhost:80](http://localhost:80) See output below

![](https://lh7-us.googleusercontent.com/tArC-CuY1tRe52O10WKl2SVqhrbwtLQQXugxFw2mmx-m2J7o1r3NTGu3SLdLNKqS9g8t7YMEf7zTCcZn_OdE0echPPuKu_4zIRYsClJDUQyQxiatn4t6PZ5dpAJxH4IDs6dniHDwAHa6Ebbxfr6DKRo)

We can also check on the browser by visiting the public IP address of the machine

See output below:

![](https://lh7-us.googleusercontent.com/QsJOFR0nInlsX-dLVuJ2lI-k9cqOz_tpR3JSEircQSdd_4eKa3T8c2DZV4O0G9IX0VXdQRHlBeqSSHMkMjIHZiBn2zSyeuQRlDz3kFk--o1bS8rCkjIeKninOcRweCv0arhgVRGDPgWw5GCPA-sEBPA)

Seeing the above page confirms that the web server is correctly installed and accessible through the firewall.

Installing the SQL server

SQL server is an important aspect of web server as it serves to manage and store datafor the site.

To install the sql server we run the command below:

Sudo apt install mysql-server

![](https://lh7-us.googleusercontent.com/Sl_xdWeqEXdxxX6uraSW7m7Cq2NIe3mwTbLHhjXuGHkLwURt-KrU6q3lGlB8HD_WWST3IvZ1Z-0zPv1lSFOP-H4vTkDWVeiV-MoNZ95k0n7f75ycRxvAv7DmTkVgOSh_7kWvEyVs_R7B0IfTYQBw2C4)

We receive a prompt to confirm installation and type Y and Enter.

When installation is complete, we can log into the sql by typing

Sudo mysql

![](https://lh7-us.googleusercontent.com/-CASxn2zbdZ1OEqgREMTKh1dpkOzDJkmbpv-ZicqntnAw6Yp-XoUOHA3VnZtE1reJ2_XpmNCJVN-LWU8W0k4tVhcggeK8ZYM1nmobDfRpuj7Eb5mE-HYAOUWiz8Emloc-J1bzIxJ2da4jSe3ZqdACEQ)

![](https://lh7-us.googleusercontent.com/7OQOQyhn40IATBcmrqKOInVAOdvj3REtwpwmbn6T5TFxV-CzfRIV-mNMjPMiqFwxi0IKRFkt1xML60Wh-KjfJc2oHRrXugqWTX8HRlTRA8QJPUxs_uK4oLKcvH4T2fvzxiOK5_aF0wH7oNBkD_oup4Y)

We continue by starting the interactive script by running:

Sudo mysql\_secure\_installation

![](https://lh7-us.googleusercontent.com/2QXLwGRsfTmMurpAWVANVJbVkLLJ9oMx22JF-QNnPI6i-k34qrw5gMtEFpJO8BzmldO7Ywiog55ZpWP4ua_AmGXBP38eEAIr9kRRlsZdfEQRekB5ewlHfRVO3d1Lv_METtElrhEjfAfViMJ_NqzbAlQ)

![](https://lh7-us.googleusercontent.com/-s6cXtOtEhGf3yKIRQSeOMWqPGNbUh0tg_bN1cotuOkqmnlMicVNc5zUeHzzCC8kSFyQv2PBoWfUXZI206QdceqzMp4SuWX6zNtZIDA_CmZDAP4pyD2yA7OXspJ_LxnwmrFxY37KPvZu2gvd7AkJBng)

Proceed to set up password for the sql

After completing this step, we can test if we able to login into the sql by running the command below:

Sudo mysql -p

By running this command, we get a prompt for password. By entering the correct password, we are able to login

![](https://lh7-us.googleusercontent.com/KC5I-lphPKXIow4EjBsNEEoW9j2gh_D8KK-ne727ZpnP6Xe7VoogzHyfAtA7jNdLUFh3Cz0Cf4V_yHwGy64Yxkd9kqgF6i8Z31X961hOy09NShixVtOBU6NBBjWG_6COweq9Uo4xXZf1xe0y9kU_M5Y)

This confirms that we have successfully completed and configure password for our sql. We can type exit to close the prompt.

### Install PHP

To install php we run the command below:

Sudo apt install php-fpm php-mysql

![](https://lh7-us.googleusercontent.com/AVCUEUsi6Ck5q0v0LtWf-zRECV6iRo_u5eW26Lv2QhSDzBgZ7UqvhUvn4kOt54IVlZ2xiFnTsE5ZyWNjD8AxppOvC3jjkTjB84G-1DICi1zbWeRtHICH_MyWQLHBxNhHYtb03l1z7Ndc8qUVXg7DskU)

I encountered the error E: unable to locate package php-mysql.

To rectify this, I googled the error message and tried out the following commands

sudo add-apt-repository ppa:ondrej/php

sudo apt-get update

![](https://lh7-us.googleusercontent.com/v-kv7D_L6dOPOyGUpxHmQdPKsBge5KBHjTpsX9xHcFmbmY6VbPRxQccauH6XCTPn03MtAjbqYLbWv5hwJNW63bSiYxSZKGo_1Q7ojcPb5nls6T8qFUwUbTkcjocpqQDZGbxkwIW0jqLzEppNYWdOreM)

as it appears this is a known issue on ubuntu. See link below:

["Unable to locate package" while trying to install packages with APT - Ask Ubuntu](https://askubuntu.com/questions/378558/unable-to-locate-package-while-trying-to-install-packages-with-apt)

[linux - Unable to install PHP packages with apt-get, gives "E: Unable to locate package" - Stack Overflow](https://stackoverflow.com/questions/56089537/unable-to-install-php-packages-with-apt-get-gives-e-unable-to-locate-package)

Then, I ran the command again and this time it ran successfully.

![](https://lh7-us.googleusercontent.com/SvjCGAH1_37n_L6s851GwFkavAi4WrWVA0d2BKMxbAKNBHAtYuv2afWZBp0IAaoS-tTABmrd6LHDl00wgREhvJD3dVki_VSc-2EuzMr8rwKZhR-QbXbuI_9JSZyCN5ejoqmEQXxMqgCI33Wo09EUy90)

### Configuring Nginx to use PHP Processor

It is important to note that Nginx has one server block enabled by default on Ubuntu 20.04 and is configured to serve documents out of a directory at /var/www/html.

We will leave that directory and create the root web directory for the domain as follows:

Sudo mkdir /var/www/projectLEMP

Next, we assign ownership of the directory with the $USER permission, which will reference the the current system user.

![](https://lh7-us.googleusercontent.com/2FszfOaClEAekGTl4FPvVMrKXdeABNsL1Wo3vFP8kqKCLkWQ7EBTxin3Slt3porDXDiBQxltGltDKC9JB2JzNNs_E3oHpnDQjNa573Ungt4cjsDoYSYDSXv8Tm_ol1M7e0RAt9rZ7xqW_UNMU-U54W8)

Then, we open a new configuration file in Nginx’s sites-available directory using the preferred CLI. I will use nano here

Sudo nano /etc/nginx/sites-available/projectLEMP

![](https://lh7-us.googleusercontent.com/eCOtugng4qyfuNndWH_tLZXbg_oeJVSUjCQGv2HqbMKtGOqINOj6p_hC7WmNVdvD8GKYpk0eCGEW3At5RcQORh5hmeHRiPRRlBGlC9i5oKE9qvIrZxPXkNnU0dHAXawrJMsQK3Z-079OLTCAuqiOWBQ)

We activate the configuration by linking to the config file from nginx’s sites-enabled directory

Sudo ln -s /etc/nginx/sites-available/ptojectLEMP /etc/nginx/sites-enabled/

This tells nginx to use the configuration next time it is reloaded. Let’s test the configuration for syntax error by typing:

sudo nginx -t

![](https://lh7-us.googleusercontent.com/0pCHfUnPtPLvtYFcdsOpdcl8O0RYXXj5UZwhv_gTd83y4n01x-0E--ZPUqhi_JnlHg3Z8t-0X5tncoKd9KygOEDkQ0Pt82DwkIxqIeR6FYjKYVlsEf5_dPQRsNnxkcnYbgFDC-rE_zgUR8kij7Hp_2g)

I ran into an error. To troubleshoot the errorI ran cat /etc/nginx/nginx.conf to see the configuration file.

Made changes to the nginx.conf file and ran the command again and it was successful.

![](https://lh7-us.googleusercontent.com/ML_rq9WDeuZCcwZnubDSVj_jVl9tNAJhuDpNvidwbXxh7VqwAk0tmHDq3DBp6L-5gNluGtktX8wGfofCVJ73y2eLcVViKj64OG5FLDIuylztMvzybkwqdlDSFQiIhaX-JD0_HxX7I4Qi8XJZWn5zTaY)

I proceed to disable nginx that is listening on port 80

sudo unlink /etc/nginx/sites-enabled/default

Then reload nginx to apply changes

sudo systemctl reload nginx

Let’s create an index.html file in that location so that we can test that the new server block works as expected.

sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
![](https://lh7-us.googleusercontent.com/9xof2LXEL29Ndn9lgg3ho6AXzONt5iGFztw45ceTde79wDUKeMeZE7nLECYfe2TgQgxz921n984kNNGFk8rJCzNVDmKRcNW2xbghoP88Yf1BG_GSCG9SbSxfjiC2xFD5_HexTSJvMK5psRrrNH_E8Hc)

### Testing PHP with nginx

We create a test PHP file called info.php

Sudo nano /var/www/projectLEMP/info.php

The details was updated

<?php

phpinfo();

With the PHP file setup we can now access the webpage in the web browser. We will use the public IP of the instance or the domain name we set up in the NGINX configuration file, followed by/info.php.

![](https://lh7-us.googleusercontent.com/sAmg_v2MfDMthYa8edg_Tv038O4tOzlqu-7LrWnOSKycefrgCRpEJW_siwsGo-Z28TC2rbS1Adarj8l-1EcXIi8ozaqoBQAqPk6jnEN6aQPn-89TJ7kUAJL8sTI3M3OSJsLq6X07SfrK2k9GJ180PVc)

For security reasons, we have to remove our website details.
To do this, run the following command to remove the PHP file:

sudo rm /var/www/your\_domain/info.php

### Gathering Data from MySQL Database with PHP

First things first we will create a dummy database and create a simple “To Do List” and set up in such a way that our website will be able to grab data from the database and display it when we need it.

Secondly, we will name our database “example\_database” and create a dummy user named “example\_user”.

We will connect to the MySQL database by running the following command:

sudo mysql

Create a new database by running the following command:

mysql> CREATE DATABASE \`example\_database\`;

#be sure to remove the quotations to avoid getting an error message.

Create the test user

After successfully creating the database, you will create a test user and grant the user special privileges to access the database. Exit the console to save changes after you are done.

Run the following command:

mysql>  CREATE USER 'example\_user'@'%' IDENTIFIED WITH mysql\_native\_password BY 'PassWord.1';

Let’s test and see if the test user has the proper permissions by logging back into the MySQL console using the user credentials.

Run the following command:

mysql -u example\_user -p

\-p flag will prompt you to enter the password of the user

Our user has the proper permissions, now let’s see if it can access the database created.

Run the following command:

mysql> SHOW DATABASES;

The database output

Create a test table

We will create a test table named todo\_list from the MySQL console.

From the MySQL console run the following script.

CREATE TABLE example\_database.todo\_list (

   item\_id INT AUTO\_INCREMENT,

   content VARCHAR(255),

   PRIMARY KEY(item\_id)

);

Test table is created so we will insert items into it

Run the following command a few times, and be sure to change the values as you go:

mysql> INSERT INTO example\_database.todo\_list (content) VALUES ("My first important item");

Confirmation that all of the items were successfully saved to the table:

mysql>  SELECT \* FROM example\_database.todo\_list;mysql>  SELECT \* FROM example\_database.todo\_list;

exit the MySQL console:

mysql> exit

![](https://lh7-us.googleusercontent.com/7G940ZBr4cb_yDxYPV7II-KNrXXBnX4MHaq8D_sDqIYMvpUN5BGo7MlDlGwdpAcUob7fKhAgjyN8odVpDNR-KQvJ6OmTmOMYuNQCbfF-WfhyAi8bBc4tXX_WAyB-3WV9SUGehQrxigiOvjLijXur59o)

![](https://lh7-us.googleusercontent.com/hHk7CP1nli4G4okt0WiCA6rDtkDC6-5matdtDKrDVmFES5U3JZMBiCPAkEVSpRgP7BQfm9x1JXoD1ag0-ygv92RxarwN5FgeirKk36H78t0bkg_ep5niCpNYHAuvodWgjkNbpdPB91AfLS_wz49bZ3I)


Create a PHP script that will connect to MySQL and pull the data from the table and have it displayed.

Run the following command:


nano /var/www/projectLEMP/todo\_list.php


Copy and paste this into the todo\_list.php script:


<?php

$user = "example\_user";

$password = "PassWord.1";

$database = "example\_database";

$table = "todo\_list";

try {

  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);

  echo "<h2>TODO</h2><ol>";

  foreach($db->query("SELECT content FROM $table") as $row) {

    echo "<li>" . $row\['content'\] . "</li>";

  }

  echo "</ol>";

} catch (PDOException $e) {

    print "Error!: " . $e->getMessage() . "<br/>";

    die();

}


Save and exit the file to save the changes.

![](https://lh7-us.googleusercontent.com/YOutR9L9I9vOMPg6PHc03WxPmlw2RQQKiyLisxKNrToFTWK1RT1M4Hw1viYgEDyXKTU1Q0EwSuUm7U203hHYpgaoC_qGpCvfiz4Q3qygf8LuqOu8LOC5jru3bGl-tC7x2co1c0ZtaDyEXMZ_c7LrAI4)
