## MEAN stack development

The MEAN stack is a popular framework for developing scalable web applications. It consists of the following:

1.  **MongoDB**: A NoSQL, object-oriented database designed for use with cloud applications.
2.  **Express.js**: A web application framework for Node.js that supports interactions between the front end (client side) and the database.
3.  **Angular.js**: Often referred to as the “front end,” Angular.js is a client-side JavaScript framework used to create dynamic web applications with interactive user interfaces.
4.  **Node.js**: The premier JavaScript web server used to build scalable network applications.

#### Step 1: Install NodeJs

Node.js is a powerful JavaScript runtime that allows you to run JavaScript code outside the browser. It’s commonly used for server-side development, and it’s a key component of the MEAN stack you mentioned earlier. In this project, we will use Node.js to set up the Express routes and AngularJS controllers.

First, let’s update our ubuntu
`sudo apt update`
This ensures that your system has the latest information about available packages.

Next, we upgrade ubuntu
`sudo apt upgrade`
This step ensures that your system is up to date.

Then, we add certificates
These are necessary installation packages for secure communication:
`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates`

`curl -sL https://deb.nodesource.com/setup\_12.x | sudo -E bash -`

After running the code above, we might get a similar information as below warning us about deprecation.
![](https://lh7-us.googleusercontent.com/XFJTquggpHfOVEBcGkKSfkSxVXVm7Yy05Yft_xgu__Njzx3Z2whMGTL3VcbDKgEqaBeyHkuH1Oqh5-LYstQB_XS_0HTGErc0i-8bMrqqRb8c6Oi0lgvXoFe4dXIySGk3qJe0RUN3imARqhtJdPS5qgQ)

To fix this we can visit the link in the image to find the latest distribution compatible with the distribution.
![](https://lh7-us.googleusercontent.com/PT-SOLF9eC6CGe82-9khcCvNh14hbiAqQkCEKFc9cYIo21ElU96KjfKe8X9OLKpDWK_083c6FMuSOonqfNE0LG9fahWvH2onRAQqb_6AjwQpZsdd4m5mBKAFY4eXAblFpz_Wbb5h1R9rydgyT1AmMC8)
Then run the command below:
`curl -fsSL https://deb.nodesource.com/setup\_22.x | sudo -E bash -`
![](https://lh7-us.googleusercontent.com/_acd72gOgI9Wn0SkuQ_DqlQR1JbZD_Zbc5Ae4WB7FY2JwTV9jGQVNd-5sXhPBHbzNk_D1rV5gyjOasvqTnXIqzWG9EvXysKOqbrM6a-VwM9-E_e46YOl9CVoAUbbi5bcW1vhpO6e0r_jq5t9ES_HfR0)

Now, that we have fixed that, let’s Install NodeJS
`sudo apt install -y nodejs`
![](https://lh7-us.googleusercontent.com/NxrV65mJHXzgYynWncYA4oK9eMI-uEpnco3q04vmm9Z5c4LtA5egYrFNLIq6bCjrfXEV4y2iFhTfTrUTRsDKB4N3t-aLn13rPRGGJ68tobyiCCd0nfe34QoQVnomWnOsRnOIw3Vdqjgych-RZA4f5Pk)

#### Step 2: Install MongoDB
MongoDB is a powerful NoSQL database that stores data in flexible, JSON-like documents. For our example application, we will add book records to MongoDB that contain book name, isbn number, author, and number of pages..

##### Add MongoDB Repository Key:

Run the following command to add the MongoDB repository key:
`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`
![](https://lh7-us.googleusercontent.com/eKphOn4WKzxIAVZodE8L6Yieo0kaY2Nyj-xVpAHcgvx0GTkyb5DFQGvrao4idFhk5EKczOgRTbqhTJ8J5Vhu7rZTFhZ_jgB0VXKeRE5Lb6VSi1HmmFE-NtyJSVq12m7sQeqJhIoi9o9DNjMIQJIZjcI)

This step ensures that your system trusts the MongoDB repository.

##### Add MongoDB Repository:

Next, add the MongoDB repository to your system:
`echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`
![](https://lh7-us.googleusercontent.com/_mQOQ1JCgd7nTBKIrIKBxGroYCRocQoIh5f2wGT7C7NdcK5KQjRumpeqldQjoSwbjwr_XSwuJCHkS0xD6a2uSi_06Z6uZAobf5j8ex_6FRs57vDtiQO0SveXDRWaQGXktfkf6Zc2A42j0y5tlLjxwhA)
This line specifies the repository URL for MongoDB 3.4.

##### Install MongoDB:

`sudo apt install -y mongodb`
![](https://lh7-us.googleusercontent.com/NozbvEJKKidJdwtsxbloHtfIggxw2mRjyN015lpQBRQ3lM2NFs5Upy9xIGlWv_ZHZOaGCRo2TzXz-WBwaKuQwqHLay6AMCnWCTjorKp6Oz5KXylaIyowBJOy75KWu0KJcGgv4vdZ7_9qZD0gAQ5_zbg)
This command installs MongoDB on your system. From the image above, we got an error “Package ‘mongodb’ has no installation candidate”
##### Fixing error on MongoDB installation
To fix this, let’s Import the public key used by the package management system.
`wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -`

The operation should respond with an OK.
![](https://lh7-us.googleusercontent.com/NxskWspS8opWr3tEPy3HEIRTh9iiNapTBxhxuDphH0X56ZCVO8cPXdGp0vU_4u9vEg5HfNsxAlu7qM9klosBLkj5pfY4ezuYWJZkOTpGezqbQJwkW6WRZ4NktmIaiArh5jKdOaaquWDuApjDPBax8oc)

Next, create a list file for MongoDB
`echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list`

Reload local package database and install MongoDB
`sudo apt-get update`
`sudo apt-get install -y mongodb-org`
`sudo systemctl start mongod.service`

If you receive an error similar to the following when starting mongod:

`"Failed to start mongod.service: Unit mongod.service not found."`

Run the following command:
`sudo systemctl daemon-reload`
`sudo systemctl status mongod`
`sudo systemctl enable mongod.service`
`sudo systemctl restart mongod.service`
![](https://lh7-us.googleusercontent.com/yeQZbv6DqC1wBhVs3OLblUP7QoTaQvd6clONldR2ADRWP-CBSqGKGmK7CbpvA63oeUk_iSwaI5xQP6gzeCVAUEKxOgd-6QNc7iKp7z86YOf9VLGxJMGq4vbEqJYer9qI511-rlKx2Mn2vTDQVzOt3Pg)

Check if it's running or not using the command below:
`mongosh`
![](https://lh7-us.googleusercontent.com/l2fTtUOC7XWVlafNpDC-0gdkKvtzBemAGWdlv-ijZZE-H76hNBjvkogXoMHKJ5_Mf7hA37R2Jme8NZ6J25p1hKQKrDbsjnx-xJ1wgKD6daovB6oRxtXbHi5gbPtMV8RLca3ke6TQFTqLb3ZBNF0hpOI)

Type `exit` to quit the mongodb.

##### Verify MongoDB Service:
Check if the MongoDB service is active:
`sudo systemctl status mongod`
![](https://lh7-us.googleusercontent.com/IdTToAuNmDVA74h1VJseyhvMUUy0jKsRH8JtII00SUrLIqbu4-vteD3W3zWMfNwULBYswQ2rCi85zfVsrAyQRU3DxFvnJbEQw6Y9NUqDezj9S-f47TNmoJ3gZn7nDocPx0Em9yIP5UK6p843pnUohBA)

You should see information indicating that MongoDB is active(running).

##### Install npm (Node Package Manager):

Install npm, which is essential for managing Node.js packages:
`sudo apt install -y npm`
![](https://lh7-us.googleusercontent.com/SPXkYdGWk3Gg0BtfrmAnBqVWDLQp3XPDGR6sutR66uolcrm_98k1sBPzTXhm_hDCI40d4VnURewa6xpbEgMBsqBPcvj5I5kBKZVxoitPcQZueEKOM2RwPA1AA0BqRrPp-KUbr3K1UzHtribaxDaN6Jw)

If you encounter an error as seen above.

Install NVM simply by doing:
`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash`
![](https://lh7-us.googleusercontent.com/U8myN2T_pIwVCH9tbEtT6bAznQSOmt3g0atqfx6qXKfkI2LijWtYl9ZjZSicmbxvsD_aU604mqxq0Zz5KuDUNCDpvlfUGUln53Ib3FOBmrf6WI5Tx4upxtPFk8QDxyIgteLhP4gYiSujq52nBs9-TFM)

Next, let’s Install ‘body-parser’ Package:
We need the ‘body-parser’ package to process JSON files passed in requests to the server:
`sudo npm install body-parser`
![](https://lh7-us.googleusercontent.com/LSxptUkzPt7pWDwH7PxBKwHNRijbwDHkp_CiHzEYDyv3KzmBRBUOn2Zn1MUhPFYY5rm0JmFVWMGYS5730D8rdJN274Gl7wFvIGyHnNak7G3TFSG-PcTKd5Qde7L9f6K4VfvBP8MzkzSzV77yWdEjXuY)

Let's create a Folder for our Project:

Create a directory named ‘Books’:
`mkdir Books && cd Books`
![](https://lh7-us.googleusercontent.com/Yx0_Dp0b-rp95COfuCN6HeEc5L9ej79g3tgZp9_rLhxhcP7q8jK7BIsHy2hPAoNLs5TGyJHfHw_Q67iRnyzWDBKecqk2s2Pnrjl4lTJmwvUQFTm0n1f52zF1S6UzKzOe67pVCW7BU8ltK_w51PJJJyI)

Initialize npm Project:
Initialize an npm project in the ‘Books’ directory:
`npm init`
![](https://lh7-us.googleusercontent.com/sZsj2RD4uFRcSv0kRAt8PivT7d7_CUL5s3bPZzS8v1tSjpgnsQ0xYdhdKRw7Csut-8IoqyiMgHtdU4rYxs16LQhgcfoh-o3hExvbeAjEViWxYfsemDcKkxYSnFp6fqS79lszvCUtVdmtwvDc2TzB1MQ)

Create a Server File:
Add a file named server.js to the ‘Books’ directory:
`nano server.js`

Copy and paste the following web server code into server.js:

```
var express = require('express');
var bodyParser = require('body-parser');

var app = express();

app.use(express.static(\_\_dirname + '/public'));
app.use(bodyParser.json());

require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});
```
![](https://lh7-us.googleusercontent.com/NdY8bFppu6t67EhBBEX73JU71V38Aosn7c4DLjjBa86YWA8KODMuEJ_59qaLZ4aCjHVPkrlb0-HXFdv1iZAu7bsEGAtaXKMvkaEZeZ3YVbGc2lRqsYDf8Kr98TYaCXeQQWxk-gCQCjH-Tq_qBjIWwdY)

##### Step 3: Install Express and set up routes to the server
Express is a minimal and flexible Node.js web application framework that provides features for web and mobile applications. We will use Express in order to pass book information to and from our MongoDB database.

We also will use the Mongoose package which provides a straight-forward, schema-based solution to model your application data. We will use Mongoose to establish a schema for the database to store data from our book register.

You can do this by running the following command:
`sudo npm install express mongoose`
![](https://lh7-us.googleusercontent.com/kSXlRPProogVqJK94c5k2FK7Qm1V_eT89M7IyrzV6gE_t4291cDD6zf--QKm1NIJsKx-9cFDJBNAYjKfwne2UqjFDTjmwCGrqII6-qD4Cs97Hbs3ox3ta7c4l-QShBWOIoACUZqvKMkovW2oOTT9dxU)

Folder Structure: In your project directory, create a folder named “apps”:
`mkdir apps && cd apps`
![](https://lh7-us.googleusercontent.com/PL1lZGrzCIwNHuNQtcQSpkOHvv2ocv9oumE2A3Wz3dW0e9DK5PC5CUs_NPYZG1XTCABSlhBOMz0FWceEsFBXSaBEAUrfo9QfvSn9gvfq7WyX7vSghHBHtMAQDBS2KCgh3AGJH6fgG-GC1QSOHNX97iU)

Create Routes: Inside the “apps” folder, create a file named “routes.js”.
This file will define the routes for your application.

Copy and paste the code below:

```
// routes.js
var Book = require('./models/book');

module.exports = function(app) {
  // GET all books
  app.get('/book', function(req, res) {
    Book.find({}, function(err, result) {
      if (err) throw err;
      res.json(result);
    });
  });

  // POST a new book
  app.post('/book', function(req, res) {
    var book = new Book({
      name: req.body.name,
      isbn: req.body.isbn,
      author: req.body.author,
      pages: req.body.pages
    });

    book.save(function(err, result) {
      if (err) throw err;
      res.json({
        message: "Successfully added book",
        book: result
      });
    });
  });

  // DELETE a book by ISBN
  app.delete("/book/:isbn", function(req, res) {
    Book.findOneAndRemove(req.query, function(err, result) {
      if (err) throw err;
      res.json({
        message: "Successfully deleted the book",
        book: result
      });
    });
  });
  // Serve index.html for all other routes
  var path = require('path');
  app.get('\*', function(req, res) {
    res.sendFile(path.join(\_\_dirname, 'public', 'index.html'));
  });
};
```

Create Models: Inside the “apps” folder, create another folder named “models”:
`mkdir models && cd models`
![](https://lh7-us.googleusercontent.com/kYSj8Bkkz3qxrP3OMxUTdDgoNPFiN9f1arCoOGSdsXQeBIq7MAX_q04zLOki4cqYWySyR-Xcr0UoCgklHdlslC4d7a-hV6O00QdM7eDFMh4UYftfnLS2Yc56Lll00WFm39VrrJ-zyuTyYv0EoJeItsE)

Define Book Schema: Create a file named “book.js” inside the “models” folder.

This file will define the schema for your book data.

```
var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';

mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);

var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);
```

![](https://lh7-us.googleusercontent.com/OewOG_DSetvGryK3uBovYqBTT91Ks18rJM-rNn0cN6dMU8XyI0k1ZDvcFfPB6W_tpPzSQet-MlRMYK54Ekze63aX-98OAKb14rp5ZBtSytnCU9Gra99Gv2k79V5TmO0wQgFwQe6SKwULAPr9EC5W8yY)

##### Step 4 - Access the routes with AngularJS

AngularJS provides a web framework for creating dynamic views in your web applications.
We will set up the AngularJS controller configuration to connect your web page with the Express server and perform actions on your book register.

Change Directory Back to ‘Books’:
Run the following command to navigate back to the ‘Books’ directory:
`cd ../..`

Create a ‘public’ Folder:

Create a new folder named ‘public’:
`mkdir public && cd public`

Add a File Named ‘script.js’:
Create a file named ‘script.js’ within the ‘public’ folder:
`nano script.js`

Copy and Paste the Controller Configuration Code:
Copy the following code and paste it into the ‘script.js’ file:

```
var app = angular.module('myApp', \[\]);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del\_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };

  $scope.add\_book = function() {
    var body = '{ "name": "' + $scope.Name +
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author +
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});
```

![](https://lh7-us.googleusercontent.com/VSjLsc-LCZkRV1Gmi0rBqFucJMoTZtpSjLp095T0RtpnxXt_C8brpwuvl1scvWGvK3HSLoxo3kRIC9D5umeAt4KA6SBzgM7AtR2PBrb_UKMIEphtCf9hABa2om2Z_TUO8tjfJ7jxadSBdmRWEgX_fbs)

Let’s proceed with creating the \`index.html\` file in the public folder by following the steps below:

Create the ‘index.html’ File:
Navigate to the ‘public’ folder (where you previously created the ‘script.js’ file):
`cd public`

Create a new file named ‘index.html’:
`nano index.html`

Copy the following code and paste it into the ‘index.html’ file:

```
<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add\_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>
        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>
          <td><input type="button" value="Delete" data-ng-click="del\_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>

```
![](https://lh7-us.googleusercontent.com/f-HrnCUVh6U_JSgDBzc1TZJ6bzvjc5opbliYxgzj86sVk_Tuig63_Jq_Rfj7H1xwnLtTmU7sLs74IknYyj5PUc0zepZunIJl04_u2z0BqNiEDp0aJXx6B6gUmIHtlbYM5_YA6kP1DUHD6_QlmyeWtMs)
Change Directory Back to ‘Books’:
Navigate back to the ‘Books’ directory:
`cd ..`

Start the Server:
Run the following command to start your server using the server.js file:
`node server.js`

![](https://lh7-us.googleusercontent.com/1bWG_Vu15JVKPgjVeK9266TsWeWIVd9FDqQTxEeahEiSpCtKx2uZqXHznGmMl639GHan_T1Ey32GneHWIPwUW6VM_DMVUcPqyaSf0YZKUCUNhbBBIF_fNm-hiHiCE4wpZ5eLLvXncqlBc2eCFjwwnWo)

This will launch your Express.js server, and it should now be running.

Test Locally with curl:

-   Open a separate terminal or console window.
-   Use the following curl command to test your server locally:
        curl -s http://localhost:3300

This command will make an HTTP request to your server at port 3300. It should return an HTML page (although it might be difficult to read in the terminal).

We can also access from the Internet:
-   To access your server from the internet, you’ll need to open TCP port 3300 in your AWS Web Console for your EC2 Instance.
-   Log in to your AWS account and navigate to the EC2 dashboard.
-   Locate your EC2 instance and configure the security group associated with it.
-   Add an inbound rule to allow traffic on port 3300.
-   Once configured, you should be able to access your server using your EC2 instance’s public IP or DNS name followed by port 3300 (e.g., http://your-instance-ip:3300).

![](https://lh7-us.googleusercontent.com/x5B46rOfJmySzQvNux3l2IwcDWrotjGupJ_zV_Q9L60hyN985UtyudNqf879G2olZTTqLra2NcsWXl3sf8tUyCtCxi5x8DN8Io_J0uJstInqWUlB5jj_ldypoWzYYqpM5Q63XtaKle_GwdMa0Sxazn0)
