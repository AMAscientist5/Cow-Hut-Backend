### Live Link: https://digital-cow-hut-backend-swart.vercel.app/api/v1/users

### Application Routes

##### User

POST https://digital-cow-hut-backend-swart.vercel.app/api/v1/auth/signup

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/users

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/users/6177a5b87d32123f08d2f5d4 (Single GET) Include an id that is saved in your database

PATCH https://digital-cow-hut-backend-swart.vercel.app/api/v1/users/6177a5b87d32123f08d2f5d4 (Include an id that is saved in your database)

DELETE https://digital-cow-hut-backend-swart.vercel.app/api/v1/users/6177a5b87d32123f08d2f5d4 (Include an id that is saved in your database)

##### Cows

POST https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows/6177a5b87d32123f08d2f5d4 (Single GET) Include an id that is saved in your database

PATCH https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows/6177a5b87d32123f08d2f5d4 (Include an id that is saved in your database)

DELETE https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows/6177a5b87d32123f08d2f5d4 (Include an id that is saved in your database)

##### Pagination and Filtering routes of Cows

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?pag=1&limit=10

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?sortBy=price&sortOrder=asc

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?location=Chattogram

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/cows?searchTerm=Cha

##### Orders

POST https://digital-cow-hut-backend-swart.vercel.app/api/v1/orders

GET https://digital-cow-hut-backend-swart.vercel.app/api/v1/orders

Please note that the routes above represent the endpoints available in the application.
