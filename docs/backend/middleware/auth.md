# Authentication and Authorization Middleware

## Overview
This module provides middleware functions for authenticating and authorizing users in a web application. Its primary purpose is to validate JSON Web Tokens (JWT) to ensure that requests are made by authenticated users and to restrict access based on user types. The module includes security features such as token verification and user type checks to enforce access control.

## How It Fits Together
The `authenticate` function is typically called first to verify the presence and validity of a JWT in the request headers. If authentication is successful, it attaches the user information to the request object and calls the `next` middleware. Following authentication, the `authorize` function can be used to restrict access to certain routes based on the user's type, returning appropriate error responses for unauthorized or forbidden access.

---

## API Reference

### `authenticate` — METHOD /path  ·  <access>
**Purpose** — Validates the JWT token from the request headers and attaches the user payload to the request object. This is essential for ensuring that the user is authenticated before accessing protected routes.

**Request** — No specific request fields detected.

**Responses** — 
| Status | Meaning                |
|--------|-----------------------|
| 401    | Unauthorized          |

**Behavior & side effects** — If the token is missing or invalid, it responds with a 401 status and an error message. If valid, it attaches the user payload (containing `{ id, type, name }`) to `req.user` and calls `next()` to proceed to the next middleware.

**Usage** — 
```javascript
const { authenticate } = require('./middleware/auth');
app.get('/protected', authenticate, (req, res) => {
  res.send(`Hello ${req.user.name}`);
});
```

### `authorize` — METHOD /path  ·  <access>
**Purpose** — Checks if the authenticated user has the required type to access a specific route. This is crucial for enforcing role-based access control.

**Parameters** — 
| Name          | Type     | Required | Description                           |
|---------------|----------|----------|---------------------------------------|
| ...allowedTypes | string[] | Yes      | An array of allowed user types for access. |

**Behavior & side effects** — If the user is not authenticated, it responds with a 401 status. If the user type is not included in `allowedTypes`, it responds with a 403 status and an error message. If the user is authorized, it calls `next()` to proceed.

**Usage** — 
```javascript
const { authorize } = require('./middleware/auth');
app.get('/admin', authenticate, authorize('admin', 'superuser'), (req, res) => {
  res.send('Welcome to the admin panel');
});
```
