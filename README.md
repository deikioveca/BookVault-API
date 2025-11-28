BookVault API
- 
BookVault-API is a RESTful backend service for managing an online bookstore.
It provides functionality for user management, book catalog management, shopping cart operations, order processing, and book reviews.
The API is designed to be modular, secure, and scalable, making it suitable for building a complete e-commerce platform for books.

Features
- 
* User Management:
  * Register and authenticate users

  * Role-based access (admin and user)

  * Manage user details
* Book Management:

  * Add, view, and update books

  * Search books by title or author

  * Manage stock
* Shopping Cart:

  * Add and remove books from the cart

  * Update book quantities

  * Clear cart
* Orders:

  * Create and cancel orders

  * View orders by user or status

  * Update order status
* Reviews:

  * Add, update, and delete reviews for books

  * Fetch reviews by book or by user
 

Technologies Used
-
* Go
* GORM
* PostgreSQL
* Docker

Running Guide
- 
* Prerequisites

  * Go 1.25+ installed (for local testing)

  * Docker & Docker Compose (for containerized setup)

  * PostgreSQL (for local setup)

Running locally
-
* clone the repo
* go mod download
* start postgresql and ensure databases bookvault and bookvault_test exist
* create .env file, write database config variables and jwt secret -> DB_HOST, DB_PORT, DB_USER, DB_PASSWORD, DB_NAME, DB_NAME_TEST, DB_SSLMODE, JWT_SECRET
* go run main.go

Running with Docker
-
* docker compose up -> this command will start two services: app(bookvault-api) and db(PostgreSQL)
* to run tests inside the container you must open a shell inside the app container with the command -> docker compose exec app sh
* to test services: cd tests/services -> go test -v
* to test handlers: cd tests/handlers -> go test -v

API Endpoints
-
| Method     | Endpoint                                                  | Description                                                                        |
| -----------| ----------------------------------------------------------| -----------------------------------------------------------------------------------|
| **GET**    | `/`                                                       | Not found                                                                          |
| **GET**    | `/user`                                                   | Home endpoint for user                                                             |
| **GET**    | `/admin`                                                  | Endpoint only for admin                                                            |
| **POST**   | `/user/register`                                          | User registration                                                                  |
| **POST**   | `/user/login`                                             | User login                                                                         |
| **POST**   | `/user/createDetails/{userID}`                            | Create user details                                                                |
| **GET**    | `/user/getById/{userID}`                                  | Get user information                                                               |
| **POST**   | `/book/create`                                            | Create book                                                                        |
| **GET**    | `/book?title={bookTitle}`                                 | Get book by title                                                                  |
| **GET**    | `/book/all`                                               | Get all books                                                                      |
| **GET**    | `/book/author?author={bookAuthor}`                        | Get books by author                                                                |
| **PATCH**  | `/book/updateStock/{bookID}`                              | Update book stock by                                                               |
| **POST**   | `/cart/add/{userID}/{bookID}`                             | Add book to user cart                                                              |
| **DELETE** | `/cart/clear/{userID}`                                    | Delete user cart                                                                   |
| **DELETE** | `/cart/remove/{userID}/{bookID}`                          | Remove book from user cart                                                         |
| **PATCH**  | `/cart/update/{userID}/{bookID}?quantity={quantity}`      | Update book quantity in user cart                                                  |
| **GET**    | `/cart/{cartID}`                                          | Get cart                                                                           |
| **POST**   | `/order/create/{userID}?address={address}`                | Create order by user id with address                                               |
| **PATCH**  | `/order/cancel/{orderID}`                                 | Cancel order                                                                       |
| **GET**    | `/order/{orderID}`                                        | Get order                                                                          |
| **GET**    | `/order/user/{userID}`                                    | Get user orders                                                                    |
| **GET**    | `/order/status/?status={status}`                          | Get orders by status                                                               |
| **PATCH**  | `/order/update/{orderID}?status={status}`                 | Update order status                                                                |
| **POST**   | `/review/add/{userID}/{bookID}`                           | Add review                                                                         |
| **GET**    | `/review/get/{bookID}`                                    | Get book reviews                                                                   |
| **GET**    | `/review/getByUser/{userID}`                              | Get reviews from user                                                              |
| **PATCH**  | `/review/update/{userID}/{bookID}`                        | Update book review                                                                 |
| **DELETE** | `/review/delete/{reviewID}`                               | Delete review                                                                      |