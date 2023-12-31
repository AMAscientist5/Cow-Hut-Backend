

# Digital Cow Hut Backend

###  [Project Live Link](https://digital-cow-hut-backend-swart.vercel.app/api/v1/users)

<hr>

### Project Name: Online Cow Selling Backend for Eid Ul Adha
The project has been developed the backend for an Online Cow Selling platform for Eid Ul Adha. The main focus of this project is to implement error handling, CRUD operations, pagination and filtering, transactions (including a simple transaction without a payment gateway), and additional routes as necessary. 

### Technology Stack:

- Use TypeScript as the programming language.
- Use Express.js as the web framework.
- Use Mongoose as the Object Data Modeling (ODM) and validation library for MongoDB.


## Main Part :

### Error Handling:

Implement proper error handling throughout the application.
Use global error handling `middleware` to catch and handle errors, providing appropriate error responses with status codes and error messages.

Error Response Object included the following properties:
- success  →  false
- message → Error Type → Validation Error, Cast Error, Duplicate Entry
- errorMessages 
- stack

### Sample Error Response

```json
   {
    "success": false,
    "message": "E11000 duplicate key error collection: univerity-management.students index: email_1 dup key: { email: \"user2@gmail.com\" }",
    "errorMessages": [
        {
            "path": "",
            "message": "E11000 duplicate key error collection: univerity-management.students index: email_1 dup key: { email: \"user2@gmail.com\" }"
        }
    ],
    "stack": "MongoServerError: E11000 duplicate key error collection: univerity-management.students index: email_1 dup key: { email: \"user2@gmail.com\" }\n    at H:\\next-level-development\\university-management-auth-service\\node_modules\\mongodb\\src\\operations\\insert.ts:85:25\n    at H:\\next-level-development\\university-management-auth-service\\node_modules\\mongodb\\src\\cmap\\connection_pool.ts:574:11\n    at H:\\next-level-development\\university-writeOrBuffer (node:internal/streams/writable:391:12)"
}
```
                  

### Model:

### User Model:
- _id
- phoneNumber
- role   → enums → [‘seller’,’ buyer’]
- password 
- name	
   - firstName
   - lastName
- address
- budget → Savings for buying the cow
- income → money from selling the cow
- createdAt
- updatedAt


### Sample Data: (User as Buyer)
```json
{
  "_id":"ObjectId(“6473c6a50c56d0d40b9bb6a3)",  
  "password":"abrakadabra",
  "role": "buyer",
   "name":{
      "firstName": "Mr. Babull"
      "lastName": "Bro"
    },
  "phoneNumber":"01711111111",
  "address": "Chattogram",
  "budget":70000,
  "income":0,
  "createdAt":"",
  "updatedAt":"",
}
```

### Sample Data: (User as Seller)
```json
{
  "_id":"ObjectId(“6473c6a50c56d0d40b9bb6a3)",  
  "password":"abrakadabra",
  "role": "seller",
   "name":{
      "firstName": "Mr. Babull"
      "lastName": "Bro"
    },
  "phoneNumber":"01711111111",
  "address": "Chattogram",
  "budget":0,
  "income":0,
  "createdAt":"",
  "updatedAt":"",
}
```

### Cow Model:

- name: The name of the cow.
- age: The age of the cow in years.
- price: The price of the cow.
- location: Enums of location
  - Dhaka
  - Chattogram
  - Barishal
  - Rajshahi
  - Sylhet
  - Comilla
  - Rangpur
  - Mymensingh

- breed: The breed of the cow
  - Brahman 
  - Nellore 
  - Sahiwal 
  - Gir 
  - Indigenous 
  - Tharparkar 
  - Kankrej 

- weight: The weight of the cow in kilograms.
- label: The enums of the label.
  - for sale → Default value
  - sold out

- category: An enum representing the category of the cow.
  - Dairy = "Dairy",  // Represents cows bred primarily for milk production.
  - Beef = "Beef", // Represents cows bred primarily for meat production.
  - DualPurpose = "Dual Purpose", // Represents cows bred for both milk and meat production.

- seller: A reference ID that identifies the seller of the cow, allowing for tracking and association with the seller's information.

### Sample Data: (Cow)

```json
{
  "name": "Bella",
  "age": 4,
  "price": 5000,
  "location": "Dhaka",
  "breed": "Brahman",
  "weight": 400,
  "label": "for sale",
  "category": "Beef",
  "seller": "ObjectId(609c17fc1281bb001f523456)"
}

```


## Implement Create, Read, Update, and Delete Operations for Users Listing

### Create a new User 

 Route:  /api/v1/auth/signup (POST)
 
 Request body:
 
 ```json
 {
  "password":"abrakadabra",
  "role": "buyer",
   "name": {
     "firstName": "Kopa",
      "lastName": "Samsu"
   },
  "phoneNumber":"01711111111",
  "address": "Chattogram",
  "budget":30000  // money to buy the cow
  "income":0 // By Default 0
}
```
 
 Response: The newly created user object.
 
 Response Sample Pattern:

```json
 {
      "success": true, 
      "statusCode":200,
      "message": "Users created successfully",
      "data": {}, 
  }
```

           
### Get All Users

 Route:  /api/v1/users (GET)
 
 Request body:
 
 Response: The user's array of objects.
 
 Response Sample Pattern:
 
```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Users retrieved successfully",
      "data": [{},{}], 
  }
```


### Get a Single User

Route:  /api/v1/users/:id (GET)

Request Param: :id

Response: The specified user object.

Response Sample Pattern:

```json
  {
      "success": true, 
      "statusCode":200,
      "message": "User retrieved successfully",
      "data": {}, 
  }
  ```

### Update a Single User

 Route:  /api/v1/users/:id (PATCH)
 
 Request Param: :id
 
 Response: The updated user object.
 
 Response Sample Pattern:
 
```json
  {
      "success": true, 
      "statusCode":200,
      "message": "User updated successfully",
      "data": {}, 
  }
  ```
  
  ### Delete a User

 Route:  /api/v1/users/:id ( DELETE)
 
 Request Param: :id
 
 Response:  The deleted user object.
 
 Response Sample Pattern:
 
```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Uers deleted successfully",
      "data": {}, 
  }
```

## Implement Create, Read, Update, and Delete Operations for COW listings.

### Create a New Cow

 Route:  /api/v1/cows (POST)

Request body:

```json
 {
  "name": "Bella",
  "age": 4,
  "price": 5000,
  "location": "Dhaka",
  "breed": "Brahman",
  "weight": 400,
  "label": "for sale",
  "category": "Beef",
  "seller": "609c17fc1281bb001f523456"
}

```
 
 Response: The newly created cow object.

 Response Sample Pattern:

```json
 {
      "success": true, 
      "statusCode":200,
      "message": "Cow created successfully",
      "data": {}, 
  }
```
           
### Get All Cows

 Route:  /api/v1/cows (GET)

 Request body:

 Response: The cows array of objects.

 Response Sample Pattern:

```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Cows retrieved successfully",
      "meta": {
        "page": 3,
        "limit": 10,
        "count":1050
        }
      "data": [{},{}] , 
  }
  ```


### Retrieve paginated and filtered cow listings:

Route:  /api/v1/cows?

Query parameters:  (Case Insensitive)
- page: The page number for pagination (e.g., ?page=1).
- limit: The number of cow listings per page (e.g., ?limit=10).
- sortBy: The field to sort the cow listings (e.g., ?sortBy=price).
- sortOrder : The order of sorting, either 'asc' or 'desc' (e.g., ?sortOrder=asc).
- location: The location for filtering (e.g., ?location=chattogram).
- searchTerm: The search query string for searching cows (e.g., ?query=Dhaka). (Search Fields should be location, breed, and category) 

Response: An array of cow listing objects that match the provided filters, limited to the specified page and limit.

Response Sample Pattern:
```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Cows retrieved successfully",
      "meta": {
        "page": 3,
        "limit": 10,
        }
      "data": [{},{}], 
  }
```

### Get a Single Cow

Route:  /api/v1/cows/:id (GET)

Request Param: :id

Response: The specified cow object.

Response Sample Pattern:

```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Cow retrieved successfully",
      "data": {}, 
  }
```


### Update a Single Cow

 Route:  /api/v1/cows/:id (PATCH)
 
 Request Param: :id
 
 Response: The updated cow object.

 Response Sample Pattern:

```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Cow updated successfully",
      "data": {}, 
  }

```  
### Delete a Cow

 Route:  /api/v1/cows/:id ( DELETE)
 
 Request Param: :id
 
 Response: The deleted cow object
 
 Response Sample Pattern:

```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Cow deleted successfully",
      "data": {}, 
  }
```

     
### Implement Create, Read Operations for Order History Listings.

Route:  /api/v1/orders  (POST)

Request body:

```json
{

  "cow":"ObjectId(“6473c6a50c56d0d40b9bb6a3)", // cow reference _id
  "buyer":"ObjectId(“6473c6a50c56d0d40b9bb6a3)", // user reference  _id
}
```

Response: The  newly created order object.

Implementation a transactional operation for buying a cow.  When a user requests to buy a cow, simulated a `transaction` process without involving an actual payment gateway. Upon successful transaction simulation, updated the cow's status as sold, transfer money from buyer to seller account, and provided appropriate response messages.

Steps:

- The user initiates a purchase order using the "api/v1/orders" POST API.
- System will Check the user has enough money in their account to buy the cow.
- If the user needs more money, would show an error message.
- If the user has enough money, begin the buying process (would start a transaction). This involves a few steps:
- WIll Change the cow's label from 'for sale' to 'sold out'.
- Deduct the cost of the cow from the buyer's budget
- Put the same amount of  cost into the seller's income
- Make an entry in the orders collection
- Commit transaction
- End transaction session
- If any error happens abort the transaction



Route:  /api/v1/orders  (GET)

Request body:

Response: The ordered array of objects.

Response Sample Pattern:

```json
  {
      "success": true, 
      "statusCode":200,
      "message": "Orders retrieved successfully",
      "data": {}, 
  }
```

### Duration of the project development: 
4 days


  ### Live Link: https://digital-cow-hut-backend-swart.vercel.app/api/v1/users
  ### Application Routes
  All the application routes are available in this project included below

   #### User
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/auth/signup -post
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/users (GET)
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/users/64ab4f81002a381a892f0a61 (Single GET) Included an id that is saved in database
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/users/6177a5b87d32123f08d2f5d4 (PATCH) (Include id that is saved in database)
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/users/6177a5b87d32123f08d2f5d4 (DELETE) Included an id that is saved in database


   #### Cows
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows (POST)
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows (GET)
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows/64ab505a06a1d8953225fec4 (Single GET) Included id that is saved in database
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows/64ab505a06a1d8953225fec4 (PATCH) Included an id that is saved in your database
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows/6177a5b87d32123f08d2f5d4 (DELETE) Included an id that is saved in your database

   ### Pagination and Filtering routes of Cows

   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?pag=1&limit=10
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?sortBy=price&sortOrder=asc
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?location=Chattogram
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?searchTerm=Cha
     
  
   #### Orders
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/orders (POST)
   - https://digital-cow-hut-backend-swart.vercel.app/api/v1/orders (GET)


