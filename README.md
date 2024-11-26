# LibraryAPI

A powerful and flexible API for managing library resources, designed to streamline the processes of user, author, and book management for libraries of all sizes.

## Table of Contents
- [Description](#description)
- [Features](#libraryapi-features)
  - [User  Management](#user-management)
  - [Author Management](#author-management)
  - [Book Management](#book-management)
  - [Book-Author Relationship Management](#book-author-relationship-management)
  - [Security](#security)
  - [Error Handling](#error-handling)
- [API Endpoints and Sample JSON](#api-endpoints-and-sample-json)
  - [User  Management](#user-management-1)
  - [Author Management](#author-management-1)
  - [Book Management](#book-management-1)
  - [Book-Author Relationship Management](#book-author-relationship-management-1)


## Description

LibraryAPI is a comprehensive RESTful API that facilitates seamless interaction with library data. It is specifically designed to address common challenges faced by libraries, such as inefficient resource management and complex user interactions. By leveraging the power of APIs, LibraryAPI provides a robust solution for integrating library functionalities into various applications, allowing for efficient management of users, authors, and books. This API streamlines processes and enhances the overall user experience, making it an essential tool for libraries of all sizes.

# LibraryAPI Features

## User Management
- Users can register and authenticate themselves.
- User sessions are managed securely with JWT tokens.
- Users can update their profiles and delete their accounts.

## Author Management
- Libraries can create, read, update, and delete authors.

## Book Management
- Users can add new books to the library's collection.
- Books can be retrieved, updated, and deleted as needed.
- Each book is linked to its respective author.

## Book-Author Relationship Management
- Establish relationships between books and authors.
- Retrieve and manage these relationships effectively.

## Security
- Implements JWT middleware for secure access to protected endpoints.
- Tokens are revoked after use to prevent replay attacks.

## Error Handling
- Provides meaningful error messages for various failure scenarios.
- Ensures that users receive clear feedback on their actions.


# API Endpoints and Sample JSON

## User Management

### Register User: POST /user/register
**Request**
```
{
  "username": "gun_park",
  "password": "password123"
}
```
**Response (Success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": null
}
```

**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Username and password must be at least 5 characters long and not empty"
}

```

### Authenticate User: `POST /user/authenticate`
**Request**
```
{
  "username": "gun_park",
  "password": "password123"
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": null
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Authentication Failed!"
}
```

### View Users: GET /user/read (requires JWT)
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": [
    {
      "userid": 1,
      "username": "gun_park"
    },
    {
      "userid": 2,
      "username": "vasco"
    }
  ]
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "No users found"
  }
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Authentication Failed!"
}
```
### Update User: PUT /user/update (requires JWT)
**Request**
```
{
  "userid": 1,
  "username": "gun_park_updated",
  "password": "strongerpassword"
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "User  updated successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "User  with ID 1 does not exist."
  }
}
```

### Delete User: DELETE /user/delete (requires JWT)
**Request**
```
{
  "userid": 1
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "User  deleted successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "User  with ID 1 does not exist."
  }
}
```
## Author Management
### Create Author: POST /authors/create (requires JWT)
**Request**
```
{
  "name": "J.K. Rowling"
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Author created successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Author name must be more than 4 characters and cannot be blank."
  }
}
```

### Update Author: PUT /authors/update (requires JWT)
**Request**
```
{
  "authorid": 1,
  "name": "J.K. Rowling Updated"
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Author updated successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Author with ID 1 does not exist."
  }
}
```
### Get All Authors: GET /authors/read (requires JWT)
**Request**
```
No request body
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": [
    {
      "authorid": 1,
      "name": "J.K. Rowling"
    },
    {
      "authorid": 2,
      "name": "George R.R. Martin"
    }
  ]
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "No authors found"
  }
}
```
### Delete Author: DELETE /authors/delete (requires JWT)
**Request**
```
{
  "authorid": 1
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Author deleted successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Author with ID 1 does not exist."
  }
}
```
## Book Management
### Create Book: POST /books/create (requires JWT)
**Request**
```
{
  "title": "Harry Potter and the Sorcerer's Stone",
  "authorid": 1
}
```
**Response (success)*
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Book created successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Book title must be more than 4 characters and cannot be blank."
  }
}
```
### Get All Books: GET /books/read (requires JWT)
**Request**
```
no request body
```
**Response (success)*
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": [
    {
      "bookid": 1,
      "title": "Harry Potter and the Sorcerer's Stone",
      "authorid": 1,
      "author_name": "J.K. Rowling"
    },
    {
      "bookid": 2,
      "title": "A Game of Thrones",
      "authorid": 2,
      "author_name": "George R.R. Martin"
    }
  ]
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "No books found"
  }
}
```
### Update Book: PUT /books/update (requires JWT)
**Request**
```
{
  "bookid": 1,
  "title": "Harry Potter and the Chamber of Secrets",
  "authorid": 1
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Book updated successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Book with ID 1 does not exist."
  }
}
```
### Delete Book: DELETE /books/delete (requires JWT)
**Request**
```
{
  "bookid": 1
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Book deleted successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Book with ID 1 does not exist."
  }
}
```
## Book-Author Relationship Management
### Create Book-Author Relationship: POST /book_authors/create (requires JWT)
**Request**
```
{
  "bookid": 1,
  "authorid": 1
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Book-author relationship created successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Book does not exist"
  }
}
```
```
{
  "status": "fail",
  "data": {
    "title": "Author does not exist"
  }
}
```
### Get All Book-Author Relationships: GET /book_authors/read (requires JWT)
**Request**
```
{
  no request body
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": [
    {
      "collectionid": 1,
      "bookid": 1,
      "authorid": 1,
      "book_title": "Harry Potter and the Sorcerer's Stone",
      "author_name": "J.K. Rowling"
    },
    {
      "collectionid": 2,
      "bookid": 2,
      "authorid": 2,
      "book_title": "A Game of Thrones",
      "author_name": "George R.R. Martin"
    }
  ]
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "No book-author relationships found"
  }
}
```
### Update Book-Author Relationship: PUT /book_authors/update (requires JWT)
**Request**
```
{
  "collectionid": 1,
  "bookid": 2,
  "authorid": 2
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Book-author relationship updated successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Book does not exist"
  }
}
```
### Delete Book-Author Relationship: DELETE /book_authors/delete (requires JWT)
**Request**
```
{
  "collectionid": 1
}
```
**Response (success)**
```
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "data": "Book-author relationship deleted successfully"
}
```
**Response (failure)**
```
{
  "status": "fail",
  "data": {
    "title": "Book-author relationship with ID 1 does not exist."
  }
```


