# User & Captain Routes API Documentation

This document describes the `/users` and `/captains` endpoints, including HTTP methods, status codes, request and response bodies.

---

## User Endpoints

### 1. Register

- **Endpoint:** `/users/register`
- **Method:** POST

#### Request Body

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john@example.com",
  "password": "yourpassword"
}
```

#### Responses

- **201 Created**
  ```json
  {
    "token": "<jwt_token>",
    "user": {
      "_id": "user_id",
      "fullname": {
        "firstname": "John",
        "lastname": "Doe"
      },
      "email": "john@example.com",
      "socketId": null,
      "__v": 0
    }
  }
  ```
- **400 Bad Request** (Validation error)
  ```json
  {
    "errors": [
      {
        "msg": "Invalid Email",
        "param": "email",
        "location": "body"
      }
    ]
  }
  ```
- **400 Bad Request** (User already exists)
  ```json
  {
    "message": "User already exist"
  }
  ```

---

### 2. Login

- **Endpoint:** `/users/login`
- **Method:** POST

#### Request Body

```json
{
  "email": "john@example.com",
  "password": "yourpassword"
}
```

#### Responses

- **200 OK**
  ```json
  {
    "token": "<jwt_token>",
    "user": {
      "_id": "user_id",
      "fullname": {
        "firstname": "John",
        "lastname": "Doe"
      },
      "email": "john@example.com",
      "socketId": null,
      "__v": 0
    }
  }
  ```
  - Sets a `token` cookie.
- **400 Bad Request** (Validation error)
  ```json
  {
    "errors": [
      {
        "msg": "Invalid Email",
        "param": "email",
        "location": "body"
      }
    ]
  }
  ```
- **401 Unauthorized**
  ```json
  {
    "message": "Invalid email or password"
  }
  ```

---

### 3. Profile

- **Endpoint:** `/users/profile`
- **Method:** GET
- **Authentication:** Required (JWT token in cookie or Authorization header)

#### Responses

- **200 OK**
  ```json
  {
    "_id": "user_id",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john@example.com",
    "socketId": null,
    "__v": 0
  }
  ```
- **401 Unauthorized**
  ```json
  {
    "message": "Unauthorized"
  }
  ```

---

### 4. Logout

- **Endpoint:** `/users/logout`
- **Method:** GET
- **Authentication:** Required (JWT token in cookie or Authorization header)

#### Responses

- **200 OK**
  ```json
  {
    "message": "Logged out"
  }
  ```
  - Clears the `token` cookie.
- **401 Unauthorized**
  ```json
  {
    "message": "Unauthorized"
  }
  ```

---

## Captain Endpoints

### 1. Register

- **Endpoint:** `/captains/register`
- **Method:** POST

#### Request Body

```json
{
  "fullname": {
    "firstname": "Jane",
    "lastname": "Smith"
  },
  "email": "jane@example.com",
  "password": "yourpassword",
  "vehicle": {
    "color": "Red",
    "plate": "ABC123",
    "capacity": 4,
    "vehicleType": "car"
  }
}
```

#### Responses

- **201 Created**
  ```json
  {
    "token": "<jwt_token>",
    "captain": {
      "_id": "captain_id",
      "fullname": {
        "firstname": "Jane",
        "lastname": "Smith"
      },
      "email": "jane@example.com",
      "status": "inactive",
      "vehicle": {
        "color": "Red",
        "plate": "ABC123",
        "capacity": 4,
        "vehicleType": "car"
      },
      "socketId": null,
      "__v": 0
    }
  }
  ```
- **400 Bad Request** (Validation error)
  ```json
  {
    "errors": [
      {
        "msg": "Invalid Email",
        "param": "email",
        "location": "body"
      }
    ]
  }
  ```
- **400 Bad Request** (Captain already exists)
  ```json
  {
    "message": "Captain already exist"
  }
  ```

---

### 2. Login

- **Endpoint:** `/captains/login`
- **Method:** POST

#### Request Body

```json
{
  "email": "jane@example.com",
  "password": "yourpassword"
}
```

#### Responses

- **200 OK**
  ```json
  {
    "token": "<jwt_token>",
    "captain": {
      "_id": "captain_id",
      "fullname": {
        "firstname": "Jane",
        "lastname": "Smith"
      },
      "email": "jane@example.com",
      "status": "inactive",
      "vehicle": {
        "color": "Red",
        "plate": "ABC123",
        "capacity": 4,
        "vehicleType": "car"
      },
      "socketId": null,
      "__v": 0
    }
  }
  ```
  - Sets a `token` cookie.
- **400 Bad Request** (Validation error)
  ```json
  {
    "errors": [
      {
        "msg": "Invalid Email",
        "param": "email",
        "location": "body"
      }
    ]
  }
  ```
- **401 Unauthorized**
  ```json
  {
    "message": "Invalid email or password"
  }
  ```

---

### 3. Profile

- **Endpoint:** `/captains/profile`
- **Method:** GET
- **Authentication:** Required (JWT token in cookie or Authorization header)

#### Responses

- **200 OK**
  ```json
  {
    "_id": "captain_id",
    "fullname": {
      "firstname": "Jane",
      "lastname": "Smith"
    },
    "email": "jane@example.com",
    "status": "inactive",
    "vehicle": {
      "color": "Red",
      "plate": "ABC123",
      "capacity": 4,
      "vehicleType": "car"
    },
    "socketId": null,
    "__v": 0
  }
  ```
- **401 Unauthorized**
  ```json
  {
    "message": "Unauthorized"
  }
  ```

---

### 4. Logout

- **Endpoint:** `/captains/logout`
- **Method:** GET
- **Authentication:** Required (JWT token in cookie or Authorization header)

#### Responses

- **200 OK**
  ```json
  {
    "message": "Logged out"
  }
  ```
  - Clears the `token` cookie.
- **401 Unauthorized**
  ```json
  {
    "message": "Unauthorized"
  }
  ```