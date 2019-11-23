# :coffee: Full Stack Barista App

# Goal: Recreate the order dynamic between a cashier and barista at any local coffee shop

* **Project Title: The Gardner Roasting Co.**
  - The cashier is able to place orders without having to create an account. While the baristas need to log in, in-order to see the list of drinks they must complete for that given day. Once drinks are completed they can click on the order, causing the computer to automagically say the order out-loud.

* **Image of home Page**
![](public/home.png)

* **Image of SignUp Page**
![](public/signup.png)

* **Image of barista profile Page**
![](public/profile.png)

## How It's Made:

**Tech Used:** HTML5, CSS3, APIs, Javascript, Node.js, mongoDB, Express framework, say.js :speaker:

## How It Works:

  * The index.ejs page contains two forms a login form and an orders form. As well as a signup button that links to a signup page
  * Once the user(cashier) hits the "place order" button it makes a post request to the server, the server creates a document in the 'orders' collection saving that customers name and drink order.(redirecting back to the index.ejs page)
  * The login form has two input requirements 'name' and 'password', once submitted those input values are checked against the database using the passport module
  * If successful the user will be directed to the profile.ejs page
  * if incorrect, the user will be kept on the index.ejs page to try again, or they can click the signup button.
  * The signup button will take the user to the signup page. This page has the same required fields as the login form.
  * If the user does not exist, passport module will encrypt their password, creating a document in the 'user' collection. Once the document is saved the user is directed to the profile page.
  * The profile page will show the Barista that is currently logged in, and a list of orders to be completed
  * The login page also contains a section for 'completed orders'
  * Once the user clicks on one of the orders client-side JS is set up to hear that click, and performs two fetch request.
      * The first fetch makes a post request to the server sending the 'customer's name','order' and 'barista's name' to mongoDB, creating a document in the 'completed' collection
      * The second fetch makes a delete request to the server with the 'customers name' and 'order'.
          * however before accessing the database say module's method is invoked causing the computer to say the following line:
            ```say.speak(`${req.body.name} your ${req.body.order} is ready`)
            ```
          * This request goes into the 'orders' collection deleting that specific document
  * Lastly, the dom is updated displaying the completed order under the 'completed' section of the profile.ejs page

## Lesson Learned:
  This was my first time using say module, so figuring out which API it should be placed in was interesting at first. I was stuck between implementing it in my post or delete API. Putting it inside of my delete API, in the end gave the most seamless outcome. 


## Installation:

1. Clone repo
2. run `npm install`

## How To Use:

1. run `node server.js`
2. Navigate to `localhost:4000`

## Credit

Modified from Scotch.io's auth tutorial
