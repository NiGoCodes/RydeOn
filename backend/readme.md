# User API Endpoints

## POST /users/register

- **HTTP Method:** POST
- **Status Codes:**
  - `201 Created`: User registered successfully
  - `400 Bad Request`: Validation failed or user already exists

### Request Body

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

### Successful Response (`201 Created`)

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

### Error Response (`400 Bad Request`)

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
or
```json
{
  "message": "User already exist"
}
```

---

## POST /users/login

- **HTTP Method:** POST
- **Status Codes:**
  - `200 OK`: Login successful
  - `400 Bad Request`: Validation failed
  - `401 Unauthorized`: Invalid email or password

### Request Body

```json
{
  "email": "john@example.com",
  "password": "yourpassword"
}
```

### Successful Response (`200 OK`)

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

### Error Response (`400 Bad Request`)

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

### Error Response (`401 Unauthorized`)

```json
{
  "message": "Invalid email or password"
}
```