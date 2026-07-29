# Input Validation Middleware
This module is a collection of input validation functions for various types of requests, including user registration, product creation, requests, and messages. Its primary purpose is to ensure that the data sent in the request body conforms to certain rules and standards, such as valid email addresses, non-empty strings, and positive numbers. The module uses a stateless approach, relying on the request and response objects to perform validation.

## Overview
The module exports four validation functions: `validateUserRegistration`, `validateProduct`, `validateRequest`, and `validateMessage`. Each function checks the request body for specific fields and returns an error response if any of the fields are invalid. The functions are designed to be used as middleware in an Express.js application, allowing for flexible and modular validation of incoming requests. The module does not perform any authentication or authorization checks, focusing solely on input validation.

## How It Fits Together
The validation functions are designed to be used independently, depending on the type of request being made. For example, the `validateUserRegistration` function would be used when a new user is registering, while the `validateProduct` function would be used when a new product is being created. The functions follow a similar pattern, checking the request body for required fields and returning an error response if any of the fields are invalid. The `next()` function is called if the validation is successful, allowing the request to proceed to the next middleware or route handler. The call-chain is typically initiated by the Express.js router, which calls the validation function as part of the request handling process. 

Since there are no environment variables used in this module, the Configuration section is omitted.

---

## API Reference

### validateUserRegistration — METHOD / · 
**Purpose** — Input validation middleware for user registration.
**Request** 
| Field | Required |
| --- | --- |
| type | Yes |
| name | Yes |
| email | Yes |
| password | Yes |
**Responses** 
| Status | Meaning |
| --- | --- |
| 400 | Validation failed |
**Behavior & side effects** — Validates user registration input data, checking for valid user type, name, email, and password. If any validation fails, returns a 400 response with an error message and a list of validation errors.
**Usage** — Example usage in a router file: `app.use('/register', validateUserRegistration, registerUser);`

### validateProduct — METHOD / · 
**Purpose** — Input validation middleware for product creation.
**Request** 
| Field | Required |
| --- | --- |
| farmerId | Yes |
| name | Yes |
| category | Yes |
| quantity | Yes |
| unit | Yes |
| price | Yes |
**Responses** 
| Status | Meaning |
| --- | --- |
| 400 | Validation failed |
**Behavior & side effects** — Validates product creation input data, checking for valid farmer ID, product name, category, quantity, unit, and price. If any validation fails, returns a 400 response with an error message and a list of validation errors.
**Usage** — Example usage in a router file: `app.use('/products', validateProduct, createProduct);`

### validateRequest — METHOD / · 
**Purpose** — Input validation middleware for requests.
**Request** 
| Field | Required |
| --- | --- |
| productId | Yes |
| farmerId | Yes |
| vendorId | Yes |
| quantity | Yes |
**Responses** 
| Status | Meaning |
| --- | --- |
| 400 | Validation failed |
**Behavior & side effects** — Validates request input data, checking for valid product ID, farmer ID, vendor ID, and quantity. If any validation fails, returns a 400 response with an error message and a list of validation errors.
**Usage** — Example usage in a router file: `app.use('/requests', validateRequest, createRequest);`

### validateMessage — METHOD / · 
**Purpose** — Input validation middleware for messages.
**Request** 
| Field | Required |
| --- | --- |
| senderId | Yes |
| recipientId | Yes |
| text | Yes |
**Responses** 
| Status | Meaning |
| --- | --- |
| 400 | Validation failed |
**Behavior & side effects** — Validates message input data, checking for valid sender ID, recipient ID, and message text. If any validation fails, returns a 400 response with an error message and a list of validation errors.
**Usage** — Example usage in a router file: `app.use('/messages', validateMessage, createMessage);`
