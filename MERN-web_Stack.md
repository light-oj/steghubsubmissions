## MERN web stack
#### What is the MERN Stack?
MERN stands for MongoDB, Express, React, and Node. These technologies form the foundation of a full-stack web application.
- MongoDB: A schema-less, non-relational document-oriented database.
- Express.js: A web application framework for Node.js that simplifies server-side code.
- React: A popular JavaScript library for building dynamic front-end interfaces.
- Node.js: A JavaScript runtime environment for server-side development.

##### Deploy a simple To-Do application
In this task, we will deploy a simple To-Do application.

To start, we create a new instance on AWS:
![](https://lh7-us.googleusercontent.com/rO0k9WoHLRQFKe7OP_WBTEuP0raVqyV44Ome4GGjAq9HtL22CjxYV92Hbhk5axs1S4Xgv9eUazAO9RX-jOtj-_CuhgD59S3KNufL79Nd7jVqyE6RFbx46rUpAVuZ3WjWItmr1tDoLcB8pmEclQ-tfxI)

After successful creation, launch the instance:
![](https://lh7-us.googleusercontent.com/I46s05LLghR68dgFYlpYmJqscxDSjSxBmTvAZeLSocEWdnyUzA6l91onL5XFpdKqdwBXbG0hZ-iT1XnZvlTPJL1qYAVwndH4cYity8JKH1rgVCsApaHQpGKl09zqxe3LDwiOqo0nK-Yb4P2xWHwnCiw)

##### Step 1: Backend Configuration
Run the update command to bring your instance up to speed with the latest updates available.
`sudo apt update`
![](https://lh7-us.googleusercontent.com/BcJqHECvhl1d68khgDUMPFz7F_7e-Hg3GDu1zsHOiG8ob1beuh-SUrjEaIxll8l9mtUOUV85EI9gyNbCEC1uudh6qeEzG8po6avrhQVTokrFIuK3nQL2EGIZFGb9-cM8aj9gfrNX3Gkrkq3zqxcHTUc)

Next, we run the upgrade command as we can see from the update command that there are packages that can be upgraded.
`sudo apt upgrade`
![](https://lh7-us.googleusercontent.com/hjvJCY44sBDBh5-SZ8SnlgyTmmuXulptvcbbyWJvU9rEAL2iSPIA14KtMT0q_KI9OvBmd5eBEKhjw8b4puMYBODZyS1jtImSC7431P0sav-ZfdmjDYDqH9u81W6T1AWCwHvN8ZTKCO_ezzeEJ467MQg)

You will receive a prompt asking if you want to continue, enter `Y` and upgrades will be installed. The system will ask for a reboot after the upgrade, you can run `sudo reboot` to reboot the instance.

After reboot, connect back to the instance. 


#### Install Node.js on the server

We proceed to install node.js on the server using the command below
`sudo apt-get install -y nodejs`

![](https://lh7-us.googleusercontent.com/RpMQQF7ViPYCiUtN20fTe6UMntAOsWGEgzfXkd5Q98Hjds5SM1v8gPsb5e6C4XHidY4CFe-ekmh8UgO3VydItztkJ7odZYmKJi8fiSD9-rtzU3d1QMT5otmbIfvdS_9xbd4nKEuVEkIr2D1qC8iAgL4)

It is important to note that the command above installs both \`nodejs\` and \`npm\`. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

Next, we can verify the node installation with the command
`node -v` & `npm -v`

![](https://lh7-us.googleusercontent.com/tBS4McfClajrwqQkD5Wckv3GYttIuZmJzbboGt720FjVvaAnrqWHFL4ea6uwrj0R6zLwGRgoNVcXfQaNDChg5kbW_vV-zsmeHyZLo29DcgovoKjjoWEs-HRsC_FqOWEgmed29U2SESX-r60QPXJilvg)

##### Application Code Setup

To set up our To-Do project, let’s create a directory for the project.

`mkdir Todo`

We can run the command `ls` to verify that the Todo directory is created
![](https://lh7-us.googleusercontent.com/heOVkLGpFw4DOGD_LhH7JXyNGOQQlzlf3slVwZyYxMzhp2fIjSzOuPxROvly0DHRZNHLDtNmOt2TlPxlpb43aPCFFHGkaytLb5skEzYN8xrbobyDFqcF9-XyLnWokhCTZ7IKJvUOg1_n3PYV51f38q4)

Extra: To see some more useful information about files and directories, you can use following combination of keys `ls -lih` - it will show you different properties and size in human readable format. You can learn more about different useful keys for ls command with ls --help.

Now, let’s change to our newly created Todo directory by using the command `cd Todo`

![](https://lh7-us.googleusercontent.com/mlu_BKaL2V6nlCd6N8GJ6_bcsv_7dGG44uLC3t9ZexsvpxndzSMzKoGUR6t2y1spc8neJLXLbaajqukUwVyEeqMWSHjiERyRC1PE_Zs8lO-SwcqqEEQIk4KRLAWPceoX4dAGLV1wf8QUMHnD8AJFGRA)

Next, we will use the command `npm init` to initialize our project, so that a new file named package.json will be created. This file normally contains information about the application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

![](https://lh7-us.googleusercontent.com/0uAnQAtdV_G0_4zi5iovdi82wprd_0Lh2oJXPCpeJfFFU0l3GSAtXSHvqlSdejGmOduC4x8k2e4tpT8DV1KFVm7pQWkHXFn0Jx-eKH-bXZFNZzWk6WMA5qj7f7vlHFM2MqDZorwWAE26oKbeHQflud0)

To confirm that the package.json file is created, we can run the command \`ls\`.
![](https://lh7-us.googleusercontent.com/QSuNqPYTdk1wTSZGSJ6tJmhRNx02LWt4-XLPQPslYW2G-D0n-s4g2pUkauI-AuomqrdpfffW-07gD1voWgOJv7SSF2J6c2Xl0p8Tsrdr-KdyyAnrJ1NtiuwdS5bIiIxY6MgJp3iXPyAcNRZrZ03Pe8k)

Next, we will Install ExpressJs and create the Routes directory.

#### Install ExpressJS

Express is a framework for Node.js, therefore a lot of things developers would have programmed are already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.

To use express, we install it using `npm` by running the command below:

`npm install express`
![](https://lh7-us.googleusercontent.com/E_tKsX21K90xwN3wOTN7ARYy0wENxbrNu-FQ01MW4o8effRy4HIYz1HZ4p1yWxfYaBSVlYT-IY9KXPn-Sms38X9UDqaQh7ly3qAuXM-M1a0CKbAtyWZOlKYUnuQ9DlW_HKngCNK_D7EJ8VEdPe9Ef8E)

Next, we create a file index.js with the command `touch index.js`

Then, run `ls` to confirm that the `index.js` file is successfully created.
![](https://lh7-us.googleusercontent.com/DIW1aDAAJZRyKtUIGkftSNZO7RgI81FxiJHAz0DbA1KK_qxgSiHdpRfDp7Q07ucliCVbm7t4rJgZ366JrodsUdeAul9HyWBmhOkVQqqUVRd68L9fxfztgJvN1O3kDA93NEL8POhSObn78pKKcomfPrg)

Install the *dotenv* module

To install dotenv module, we run the command \`npm install dotenv\`
![](https://lh7-us.googleusercontent.com/fqWJfRAUvLf2tXpfzr-Sa0KaUolQ-JHdFigJrIcXSXq4L_aEsjkB0R0enICh0_jqHNP2TTerheqYd0WivXXsgj_epPferHmX098rY_x5UJ8GIrE_RilA4o5MD8rK4kYWYlRZK3zs4xTD6B_B3wUSzFE)

Let’s open the index.js file with the command below:
`nano index.js`

Type the code below into it and save. Do not get overwhelmed by the code you see. For now, simply paste the code into the file

```
const express = require('express'); 
require('dotenv').config(); 
const app = express(); const port = process.env.PORT || 5000; 
app.use((req, res, next) => { res.header("Access-Control-Allow-Origin", "\\\*"); 
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept"); 
next(); 
});
app.use((req, res, next) => { res.send('Welcome to Express'); }); 
app.listen(port, () => { 
console.log(\`Server running on port ${port}\`) 
});
```

![](https://lh7-us.googleusercontent.com/3W6Ug0H1s7E37DsFAfqjtjhzzvwIMaqLKOmZVgSxYo-kc0OTLl0L-y9In6w6s3Onf1AD5TOUMoJ2BU_i09DxGIdQ3KpW47Iti2C4o0_4I1-nnHW6PUQ3kW0R6jCh_QbN11WxitZQQKFOc4Fr95vgrv0)

Notice that we have specified to use port 5000 in the code. This will be required later when we go on the browser.

Use `CTRL + O` to save in nano, press `ENTER` to write and use `CTRL + X` to exit nano.

Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:
`node index.js`

If everything goes well, you should see "Server running on port 5000” in your terminal.

![](https://lh7-us.googleusercontent.com/PpcWccZLKByQiwMAC5xnQJVBoCE1Mjs5f5P6WolR4vG4ps6hOGpW54KtCun97svfVGYUqs1DJQ6T2-uf3ShzXQ2XVg8UC4VLCBwILYI_R8H8OXHb53qfyKfcodoNL2sL0ee2RVkAqVIryCwuIUCkLD4)

Now we need to open this port in EC2 Security Groups. There we created an inbound rule to open TCP port 80, you need to do the same for port 5000, like this:
![](https://lh7-us.googleusercontent.com/EZHuRGQFe1OrXVuw_6p4Z3AIwSxQSx5Eo9SUTrv9YlRnQlh4wgxzgjGnIO7KNy9SeXVc_ud9haG5inqyv0vgqe6_89umY0Ej8VIVuOEjES7ijTK3H2CrcJQjPFx0PegHHAAAlxXNWBWRr8I5uzSQGew)

Next, open up your browser and try to access your server's Public IP or Public DNS name followed by port 5000. You should see similar result like below:
![](https://lh7-us.googleusercontent.com/BSwmYUwOKbR2JF7HQZVtNJe4FNkSjIfmXkNsS5kn6zSuZX0JYrlWgJrh-IbbONRBZYNdSYu95n8ZfoHgOKTGB7ER_9bsc7XSNCcHzS7N0WgaEyMhrRjZITQ9ACHojk-N94muTPl-YS0WttStv-ThXb4)

Reminder: To get your server's Public IP and public DNS name:

-   You can find it in your AWS web console in EC2 details
-   Run `curl -s http://169.254.169.254/latest/meta-data/public-ipv4` for Public IP address or `curl -s http://169.254.169.254/latest/meta-data/public-hostname` for Public DNS name.

##### Routes

There are three actions that our To-Do application needs to be able to do:

-   Create a new task
-   Display list of all tasks
-   Delete a completed task

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create ‘routes’ that will define various endpoints that the To-do app will depend on. So let us create a folder ‘routes’

`mkdir routes`

Tip: You can open multiple shells in Putty or Linux/Mac to connect to the same EC2 Change directory to routes folder.

Let’s change directory to ‘routes’ folder by running the command

`cd routes`

Then, we create a file api.js with the command
`touch api.js`

![](https://lh7-us.googleusercontent.com/m1gVBh0s7_2RbaHxSr8j24cReUfnJcbK_VY8pFduzzBD7iJO70CCPk5k-fYZrDdCbhcqZZX7fzCbPHs5dM8dgygpmuS59U31pnLoZGwLT2GORauABDC2b1opXuopJBDyMwGbaPPkDIiozp_xV9igEbQ)

Next, let’s open the file with the command
`nano api.js`

![](https://lh7-us.googleusercontent.com/BF1Sjbz82ZeLrSVIeMGNjvlVROz469mKIxjZ935O3jyT4Gpd3dgA95pDQlfUVRhFvC1JtHtrTeSg3ef37oOBAsq3ZDHJtFpwJkxnwpbVJFoRYHj28B2W7Q0jlXFLwAPx3Yp2wawIw71ldx-A3nTiA6I)

And copy the below code in the file (Don’t worry about the code content)
![](https://lh7-us.googleusercontent.com/VYy3_5qaR8H6Pra8MmbNfgUQ5ZXcShJGyd3fzeuktdgLphmCUTSSuHZDTogjP4uUoSroOofrwx80n0XvIehFdz1dEAdckzS9TckQxkHyAALt_la5L2WPf0alQOsI481DQvqAdL_m_pVb-9doXjKf2KI)

Moving forward let’s create a Models directory.

#### Models
What are Models? A database model defines the logical structure of a database, determining how data can be organized, stored, and manipulated. Think of it as the blueprint for your data storage.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

For our app, we are going to make use of Mongodb which is a NoSQL database, we need to create a model.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document.

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

Change directory back Todo folder with `cd ..` and install Mongoose

`cd Todo`

`sudo install mongoose`

![](https://lh7-us.googleusercontent.com/64gDoseNE4h7ezRumvdkhHecp4WfIFqODBLt0oFBpz8ONLxPiLIhoDbvAvLjZFwnqFZWFK9cKdz8TORp2Z9f9yqWbCHZr3IaITRlfgnEGGTf_FydTkrMMwR3rRY-pnznECo5skVM0YCzso6KkkSarkQ)

Create a new folder with `mkdir models` command

Change directory into the newly created 'models' folder with `cd models`.

Inside the models folder, create a file and name it `todo.js`
![](https://lh7-us.googleusercontent.com/nUsI_R8naZo8mcH4AMv3TTJelTLUSl5nO8lOaEgLZfZ6XmbWa7xkhpWHtpP4XUucBUxPiklN16ySVphltBPS8Q-d5GPh0N1fKJjVwkt-LuUn8giDK1nPnJtazkUxjsnFg4BKkyR1FFZMxK1YdgMMXp0)

Tip: All three commands above can be defined in one line to be executed consequently with help of && operator, like this:

`mkdir models && cd models && touch todo.js`

Open the file created with nano todo.js then paste the code as seen below in the file:

![](https://lh7-us.googleusercontent.com/BoXRpMnFx3JYye9hAcNDinsTF05luWJ5hHfTzTGPdxdjf14qqH3Gn84amCwquHK5J9NEn04vyTg1fPKj9moz51cDPW1CAngUV6w8D9bvZaCLabZzNab91JplLXTwn_9Q7Y5ZV0tjxxzYY90nRHzo0BM)

Now we need to update our routes from the file `api.js` in 'routes' directory to make use of the new model.

In Routes directory, open `api.js` with `nano api.js`, delete the code inside and insert there code below into it then save and exit
![](https://lh7-us.googleusercontent.com/ldewm4nI4Rb3dAx-GlC1V-NqM3o8Yz74aGyi_npt7J3p24_9IxpHG-TVMbH-8lFLgzeurA2pHt9qHNBjHkHvaq1oAhZdIEO8J6I1ueo9yk_PGq-xVXDB7KJgm17ckDcWeNjVmwAONHKB7pnahG4FJ4Y)

The next piece of our application will be the MongoDB Database

#### MongoDB Database

We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up [here.](https://cloud.mongodb.com/) Follow the sign up process, select AWS as the cloud provider, and choose a region near you.

Complete a get started checklist as shown on the image below

Allow access to the MongoDB database from anywhere (Not secure, but it is ideal for testing)
![](https://lh7-us.googleusercontent.com/JQPCTRJLTOsSsXjMJy32L0F1Tq58xGHZeQUpwn5UTjRIblgun-m-lo1tNJtf2IksdaoXgXW3BiMQ45-opJEHdxORRfO8FLWUWNLlrdrqq3m48crKqAcTe4LcmWaBONuVyGa-sY6FRQld24gocwWTEd4)

IMPORTANT NOTE In the image below, make sure you change the time of deleting the entry from 6 Hours to 1 Week

Create a MongoDB database and collection inside mLab
In the `index.js` file, we specified `process.env` to access environment variables, but we have not yet created this file. So we need to do that now.

Create a file in your Todo directory and name it .env.
![](https://lh7-us.googleusercontent.com/hT2cHY5McUg6ODNIEvp1TdQMuMEueftIC79eLv0IoylLCgVp9AE2W0XZkH6FiUkVmC6mJa_ZfEmqrfbkV2fTPQ6Yscm6oOCgG4pcsrE0dYCl0gh1wLD7nsys8BZGHqpm0TamhkLboj2mxLGYylRPOsM)

Add the connection string to access the database in it, just as below:

![](https://lh7-us.googleusercontent.com/JXkJLrlCbz_uescz-AruFFgZRaPlcyjFRlEfI_x8p3z4yJWIOsu1Lnsj7rYZp3rN6Wgj1hJGshuSyoxKxv5EE_mHMIKJMVPvnsZmWz2Qzolk57eAMGzncuVBwefJ6dN9MvR1ynMdTVjZUmXR5AcCDKg)

Ensure to update <username>, <password>, <network-address> and <database> according to your setup
Here is how to get your connection string:
* Select Database
* Chose your database from the list and click connect.

You will see a pop-up like below:
![](https://lh7-us.googleusercontent.com/rQBZq0KZ6EMWMtufRUjiv2HRk3mhvPyHGD_XpzjsTCV8Z3iJ4yoy9c1n0e1pD85msZYJjR0DiJtG_eSyZF4ELmmFA6ws7IP-8kdXUEovwEQ79rlTVTGjM6nVZuwCDg6_4b303RLZKst7Q5PMZXmdEp8)

Next, we need to update the `index.js` to reflect the use of .env so that Node.js can connect to the database.

Let’s update the content in the file, and update it with the entire code as shown below.
![](https://lh7-us.googleusercontent.com/wzhQgGfk7IQMg-GuOZ6r2hGG796AbhrA8sQk5vRIx9m2uhFD3b0zcpG9OIJgzrLaUtQFDiwp3KAe3Gd4NHmiqrg25SurvZQIOZZpJO798nY1UyO4SjMo3-C70X884Q4j-xB6DMWt--WlxjkKAwdpUPI)

Using environment variables to store information is considered more secure and best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the `index.js` application file.

Start your server using the command below:
![](https://lh7-us.googleusercontent.com/gzj44rKSJFjQKe9LaBzQSqqw4zUhsiZWSOL0SVbflOYZwE1CoN5Xc8m84B9JGHTz-ynVKlIH9xncUeOcjMDcfd6HZWTpSlXiLyn1dvl4sv7JQEBBmr1LK2n84IygU-ErUOD6AN-2Zbd9uueeGnyD_AI)

If the response is as shown above, then we have our backend configured.

Let’s test it.

##### Testing Backend Code without Frontend using RESTful API

We have now written the backend part of our To-Do application, and configured a database, but we do not have a frontend UI yet. We need ReactJS code to achieve that. But during development, we will need a way to test our code using RESTfulL API. Therefore, we will need to make use of some API development client to test our code.

In this project, we will use Postman to test our API.

First, we need to download and install postman on our machine: [https://www.postman.com/downloads/](https://www.postman.com/downloads/)

Next, we open send an API request, and create a POST request to our API(make sure your server is running on your terminal)

![](https://lh7-us.googleusercontent.com/d1BSx27-E17rptyzAkovDFrEbYle1YZTRcY9BFAyJJR-VJvHbZ4KHStGydzMJM-ZE0ikP3t6CJJ56yFfItoosPoW_X6cbX7AbGklziDHx9foqxTQgkJwH-ji5UdNZsLTNBvYb6aL9aVkHL250QZrfcE)

### GET Request

1.  Click on the “New” button to create a new request.
2.  Choose the HTTP method as “GET.”
3.  Enter the URL from the previous POST request (e.g., http://<PublicIP-or-PublicDNS>:5000/api/todos).
4.  Click the “Send” button to execute the GET request.

![](https://lh7-us.googleusercontent.com/VqxbdY-LXS0e2mTLdks1MCb77ENXNXg6OOezVW47aYpsbjkvaf3SFcq0ECkB78hfKtgwNWXd6X8sghNH7Nwu9d1IATQA9Uq9chN_nLBO9ZCJMyjGnl2bnKlhF234uwkVCmtZoEWdIydJekRwjXJc5zM)

Let’s send a DELETE request to the API
![](https://lh7-us.googleusercontent.com/oddCpfy23VzLHlEcdDWv4SlbYVeUhyrTqWs00FTANOvc0kdWAtqbq4sZ5L96jGAwgqUv0ofTwf1rQVnkGQdNaih5fBJNN73O-TF8ohoKmoXFPJVvRDDPwtCpMfcHfbyg1xlRA9aC64TRs-eKY2_k4nw)

We can confirm the DELETE operation was successful by running the GET ![](https://lh7-us.googleusercontent.com/PvwoqDbqcW8ubfXH_EjeYldUwlDxDbw4Esrc5TKCIav5fgBxzRc_hRL5Ehnt9UjSiYyMoyfXVNWWFTx1Qu5vtfYA06bixjgecGRoJwJ_FU4D5_vZbSmhXFAzO6DoPzrs-ljNyttGE5QvFTFB7YcWAsg)

We can also confirm from the database as well.
![](https://lh7-us.googleusercontent.com/urAKCcM84VPrazXSFZA7KkrP1DAlSe4Dkcowgpia-n4d2CjpiTZjHtCi9jNRXsAW6N4S0MKEwibfJab5oW1gYHkYVmPOw53uT-VbtxjyplSzFWMFgCm-XTLHrPM2W9bJ5mikXVVK8eki1-3l_daAb0k)

#### FRONTEND CREATION

Now that we have completed the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app.

In the same root directory as your backend code, which is the Todo directory, run:
`npx create-react-app client`

![](https://lh7-us.googleusercontent.com/7xJXLiWJSJ4c7oHMOk417gXv8qdDGo6lvXRTSqggRKwauTuWoPOR7juHBye_yLgromtml2wvBp_pZii5mpMI3ummjbRF4d0Nl8AaDvIrZe7M6gn44WoRcACieD5hsDs3RuPtnqHDUyIT0ql_RFJY5Kg)

This will create a new folder in the Todo directory called client, where we will add all the react code.

#### Running a React App

Before testing the react app, there are some dependencies that need to be installed.

Let’s install concurrently. It is used to run more than one command simultaneously from the same terminal window.

`npm install concurrently --save-dev`

And install nodemon as well. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.

`npm install nodemon --save-dev`

![](https://lh7-us.googleusercontent.com/i1z9cjWjcqS8CPX1xpkx9wp6UrX8fzcbJ4Tt5ovSg-tcbssksIVCVZEwi5UOD38kdAqCw2zImJisczSbhsoAwFV8rtJK6lyZfccF8N4EEUbEEc-aBNVr2yw1stYtUim9UEa30gM2GqY-UsagtRXdK-o)

Next, in the Todo folder open the `package.json` file. Replace it with the code below.
![](https://lh7-us.googleusercontent.com/R-9-hcDCoMg-FcJXUZZKlpKypnopMR1tTz5W37C1dJgbnGI8JChbyuxchgwoUKUmoQoiFQFfyCkxqe5spMYtzq3G9RlMlc3Xown1I7wB5KfjDl19mohv40fyngAit0iQATxT8Y_poKM4RmMFh2NniJk)

##### Configure proxy in package.json

Change directory to client
`cd client`

![](https://lh7-us.googleusercontent.com/08cCDfgyzvkIOLylNexvYnxq5QqKrN-DNjaDXUJzAFTNtPbk_fn8ozNFAaVvE_EdMhF4dHZOPr0qy_lRs-tNujLXRWZAtpoDMOSj-SP2QkG4oqC4b1uMLq800xRkyFcQ5L35Yy_Wafl7x0cDLi5S_Tk)

Open the package.json file
`nano package.json`

Add the key value pair in the package.json file `"proxy": "http://localhost:5000"`

![](https://lh7-us.googleusercontent.com/Uo-8Bjq6qoh_pSBPqXeSJytrhnyzypd0D55lIA70cigWTlW9FdHExKXBZ-HPx0n23NlYJ6ZNCnGVjk-Skl9_Igd4-a6vnO3m2IZmFjYOq73l-jd-lYGn_AnYL3_cE0gqhA6ViJnhqD3p812LBewo_DQ)

The purpose of adding the proxy configuration above is to make it possible to access the application directly from the browser by simply calling the server url like \`[http://localhost:5000](http://localhost:5000)\` rather than always including the entire path like \`http://localhost:5000/api/todos\`

Now, move into the Todo directory, and simply do:

`npm run dev`

Your app should open and start running on \`localhost:3000\` as seen below:
![](https://lh7-us.googleusercontent.com/S3taxI5EC6qwjn2FEfsCFscYWRsxkYsidR3BSOthJmhfsxShSFSSmkq0tJX29405wrG3KH7HECoBL3B_wKwOnlmT3vE8GI4ogGGBV8DuXVyKyAtwJYSdYfMiWeQIanYZ7KdIfyF8WIQNqV774idhWIE)

![](https://lh7-us.googleusercontent.com/nNdnbl9eyToKeJhTA4J9EE8_7Kr8ftKIRGZmagd7-a_v8p7G0xf4DRGLNDLzG9FqgTzKu9zA0_K8njVx8XfuuYhtQPoQkJwX-D-ss3GfoVuZdGG6NS9YL8CL-6veIPQeer_ZbVMhi5zOkcX7TaBX2HM)

Important note: In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2 by adding a new Security Group rule.

##### Creating your React Components

One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component. From our Todo directory run
`cd client`

move to the src directory
`cd src`

Inside your src folder create another folder called components
`mkdir components`

Move into the components directory with `cd components`

Inside 'components' directory create three files Input.js, ListTodo.js and Todo.js.

`touch Input.js ListTodo.js Todo.js`

![](https://lh7-us.googleusercontent.com/OS-eeSF2UVGqKSW_JqRu2M1Nm9P8Lnd-APZRlGTssk7tWHhWa6cz0zFVGj6FzDQUy3rahWwHW9XzGmtSPjQ8_L5Waoo3hhwT5iUCwG7IebjXSnAYcibw37kqus1JPnVUSlepYTVQv5K4tdGNlCjr63o)

Open `Input.js` file and enter the code below:
![](https://lh7-us.googleusercontent.com/9XoiqgMa-G8j-6ydw_MUE8jDCbmMi_L_bf0uLGGzBY-tNFuB1TYSTy4QhH4sVaMOaYIoNpp25EAZvUK6FzNiqu6mnaCfolSYYrPgm0oKA1ybUXGFbDomxvR6hRr-gqUANtLm_McGk-hNgLsePLJIaLk)

To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run `yarn add axios` or `npm install axios`.

Move to the src folder
`cd ..`

Move to clients folder
`cd ..`

Install Axios
`npm install axios`

![](https://lh7-us.googleusercontent.com/uuarOBHKvymcltRD9Kvxc6tLjmXi154YxQIO0Jy8ynv8g5M92SYhArGw293ugNFtp0wW6m-66y1wyBQl8qFmjc0C3_j_1wTRYLJYujPsaOe1-fmgGAN3PAvYLMAQobQy9jeJp6gERVjb5cCXViLIft8)

Let's go to 'components' directory
`cd src/components`

After that open your ListTodo.js
`nano ListTodo.js`

In the ListTodo.js, Insert the following code
![](https://lh7-us.googleusercontent.com/JsOw1T8dq5BMhbUNkWLaYuTNak8alzGKhgrJsIYRGAgvHtgscNFsLP3KEMthDrJqHD8yvhvNt2eVKR39SSQKnwmqNPLAEof-bj7277K9a_CeaoHgctNKBy2-WumhJFPYrzfic3wPZTnzIUP2LIspgHo)

Then in your `Todo.js` file you write the following code
![](https://lh7-us.googleusercontent.com/l0nRif7cK700c9JG2cMONcNYou5qEIBUhvfct4Gd_z_oSxfBKTSEeIEhNqXr6kk-KR_s1jjz8sp5oxM_1ZtqvZhbPOX8uBtZIxAhSw_pPIy0FQX62ghcZoCeyUE4L0eevh5lk68g-w8dW3b0xhiz1-w)

We need to make a little adjustment to our react code.

Move to the src folder
`cd ..`

Ensure that you are in the src folder and run `nano App.js`
Insert the code below into it
![](https://lh7-us.googleusercontent.com/laPzTQzbBJzr8CDKZyu8Ql8IRougP9ES9H2gJlKA3yzqkspOeZ29vfFU_oeQqq5rw9T4jio8JOHh0BXLcWwHN0H-IigHxOVi08fNcugG1W2gpC6bN9pAr0tVu8PaXpvptCLS21S10L9vywhA0rZemg8)

In the src directory open the App.css and insert the code as show in the image below:
![](https://lh7-us.googleusercontent.com/9IildLhpz7pl6OtpPC58WCLAOo_a04tcDpYkqAZxCOUj25zmu2Wp_nAIAncxgBh8tASB4p6mfuxLVeexRD7J5UIsPRId36p7w-IUCohGTn1zw8qU_Y-od5JbOwcA9-3aXfi2glrBGbcDMh7YZHhWRwM)

In the src directory open the `index.css` and enter the code below:
![](https://lh7-us.googleusercontent.com/nw9mgCIhXLN77dwvfYZzVy6y3dEKq948SA2q9lA8TzTEEOIghj3BKmEjsJq6kiFU0WHoAe2VE-dRd_BFQ4rtYXeLt2bed9VSyVJHifZcbRkwLiAT45DSwrUYIp16rSmp_ceLbOAiIve1P8fgSc-yZOs)

Go to the Todo directory
`cd ../..`

When you are in the Todo directory run:
`npm run dev`

![](https://lh7-us.googleusercontent.com/RmWYHYthsdVBFEXrt2LzLBtgtgVZxV2xwA9RJ7mSigCkT_6wsiH4uu2tCp6XgT_EzLvDXqC4CbGgRL8RjMgh5iC9PkX2M5yNwoHK6uByFtIYYGhYOqjCPE7LBBt0DmWarGykRKAtsXQMQ1zhdayPdIU)

Assuming no errors when saving all these files, our To-Do app should be ready and fully functional with the functionality discussed earlier: creating a task, deleting a task and viewing all your tasks.

![](https://lh7-us.googleusercontent.com/rWB-lHqqF_ZDng3bPLBcvqL3maqJYm4TWJoN3rHtXl7tQwemlkS5xXhQIkBcIg_-8uOI3BhrUUNB01B_uCwRhOFpTvpLiZcs-7lo34ScKYMQ0rZOm2DYj91_XAZCx79uZpzSvV7yW-tqGWIIwpUR4qg)
