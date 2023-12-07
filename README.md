# Marketplace #

## How to compile and run Marketplace ##
In order to run our program ensure that all text files have been cleared of the workspace to guarantee a clean and new run. Then, proceed by first running ServerMarketplace.java (server side), then running Marketplace.java (client side). Go ahead and use the program as intended. Once a user logs out, ServerMarketplace.java (server side) will still be running but Marketplace.java (client side) will stop. In order to continue using the program, Marketplace.java is the only class that needs to be rerun.

## Who submitted what ##
Steven will submit the written report and video to Brightspace. Allison will submit the copied repository onto Vocareum.

## All classes and functionality ##

### ServerMarketplace Class ###
This is the server side of our application. Becuase of that the main functions of it are to store data, take inputted data from the client side application, process that data, and return it to the client. There are only a few methods, which all deal with information storage in the event that the server is shut down (which it should never be).
* readSeller, 
reads in all of the sellers from a file and creates new seller objects from those usernames and password
* readCustomer, 
same thing as above, but for customers and adds them to the customer list
* createCSV, 
creates a new CSV file to export if the user desires
* readCSV, 
reads in a CSV if the user decides to and adds it to the product list

### Marketplace Class ###
The marketplace class is the command center of our project. It is the client's side of the application and where the user inputs data, writes it to the server, gets the processed data returned, and displays it. There aren't really and methods in the class as it's mostly jsut displaying GUIs and whatnot aside from some small things dealing with connecting to the server.

### Product Class ###
This class is interacted with by nearly every class in the program. This class is used to create products with then can be interected with by both customers and sellers. There aren't too many important methods in here. Mostly just getters and setters so that we can view and change each aspect of a product depending on what we need. A couple of interesting methods are:
* toString, 
this is used when we write to a file, instead of the default toString, we overrode it with our own version becasue we realized there might be issues if the description or title contains spaces.
* modifiedtoString, 
same as above, just for the CSV writing
* saveProductInfo, 
ability to save a list of all products. We ended up not really using this as we went with a different method for product storage.

### User ###
a simple class that creates a new user given an email and password. Main features are getters and setters for each user, but also some checks:
* saveAccount, 
writes emails and passwords to a file, also didn't end up using this one really as we decided to keep customers and sellers separate (even with files).
* checkEmail, 
checks if the email entered is unique or not, returns a boolean accordingly
* login, 
checks if the email and password combo corresponds to a user. this is called when a user is logging in so it essentially checks if the inputs match an account. returns a boolean accordingly

### Seller ###
class that takes user input from Marketplace, and runs processing methods on it in order to deliver the necessary information.
* constructor, 
checks if a file exists that contains sellerItems and sales, if so, they are read in and added to the apporporite lists.
* viewProducts, 
allows the seller to view a list of all of their products, shows name, id, description, price, quantity.
* addSellerItems, 
when a product is created, the item is added to the list of sellerItems
* viewCustomerCarts, 
a triple loop that runs through 3 things: seller items, customers, and items in customer's carts. if the id's match between an item in the customer's cart and the seller's item then it is added to a string that's returned to the main method
* addSale, 
if an item is sold, it adds the item and customer information to a list of previous sales
* viewPreviousSales, 
returns a string of all previous sales to the main method
* create, 
takes input of a product and the old list of products, makes sure the product is unique. If so, it's added to the list of products and this is returned to the main method as well as the list of seller items, else, you get a rejection notice.
* edit, 
takes a product and the edit desired, makes the edit and returns an update list to the main method and edits the product in the seller's list
* delete, 
takes the product id, matches it with the index in the list of sellerItems and overall products, and deletes it from both lists
* login, 
checks if the seller's login matches a seller specifically (and not a customer)
* saveSellerItems, 
writes all of the items that a seller has to a file so that it can be read in once the program is rerun.
* saveAccount, 
saves the seller's email and password to a file to be read in later once the program is rerun
* saveSales, 
same as saveSellerItems, but with objects from the previousSales list instead.
#### Subclass: SellerPreviousSale ####
a file that creates a new object after a customer buys something, just has the standard getters and setters. One thing to note: it also takes in the email of the customer which is stored in the object, so the seller can view which customer purchased the item

### Customer ###
this is the main interaction functionality for everything customer related, taking inputs from the main method and processing the data in order to make the correct outputs and return them to the main method.
* constructor, 
checks if the customer has an active shopping cart and if they have previous purchase history. if so, the information is read in and stored to the correct files. 
* getShoppingCart, 
needed for the viewCustomerCart method in seller, simply returns the shoppingCart arrayList
* viewMarket, 
takes in a list of all the products, and lists them in no particular order
* sortMarket, 
takes in a list of all products, and the desired sort method. The method then runs through the list of proucts and returns a list of the product sorted in one of four ways: quantity (high to low/low to high) or price (high to low/low to high).
* searchMarket, 
takes a string input and checks the product name, description, and store for matches. if there is it's added to a string and sent back to the main method
* viewProduct, 
allows a customer to select a specific product (via the id) and see more information on it that's not displayed in the overall market view. information such as quantity and description are shown here
* viewCart, 
after an item is added to the shopping cart, a customer is able to see a printout of all items in their cart
* addToCart, 
takes a product id and the desired quantity and adds the item to the shopping cart (via a new object called CustomerShoppingCartProduct
* removeFromCart, 
a customer can put in the id of a product that they would like to remove from the cart, if the id matches an item in the cart it is removed
* purchaseShoppingCart, 
runs through each item in the shopping cart and calls the purchase method on it, deletes and/or updates quantities if needed
* purchase, 
takes a product id and does some error checking before adjusting the product list and the sellerItems list. if all of the quantity is purchase, the item is deleted, if there is still some quantity left, the value is update and lists are returned
* updateHistory, 
a private method that adds a new CustomerHistoryProduct to the customer history list after an item is purchased
* viewHistory, 
runs through each item in the customer's history and returns a string to be printed in the main method
* saveCart, 
saves the customer's shopping cart to a file containing their email and the identifying string "cart"
* saveHistory, 
same thing as above, just with all of the items in the customer's purchaseHistory list
* saveAccount, 
saves the customer's information to a file containing all other user's information
#### Subclass: CustomerHistoryProduct ####
an object that's created with the standard getters and setters once a customer purchases and item
#### Subclass: CustomerShoppingCartProduct ####
same as above, except for when a a customer adds a product to their cart
