# API Endpoints Documentation

Base URL: `http://localhost:8080/api`

## Users Endpoints

### 1. Create User
- **Endpoint:** `POST /users`
- **Description:** Create a new user
- **Request Body:**
```json
{
  "username": "string"
}
```
- **Response:** `201 Created`
```json
{
  "id": "number",
  "username": "string",
  "score": "number",
  "created_at": "string"
}
```

### 2. Get All Users
- **Endpoint:** `GET /users`
- **Description:** Retrieve all users
- **Response:** `200 OK`
```json
[
  {
    "id": "number",
    "username": "string",
    "score": "number",
    "created_at": "string"
  }
]
```

### 3. Get User by ID
- **Endpoint:** `GET /users/:id`
- **Description:** Retrieve a specific user by ID
- **Parameters:** `id` (path parameter)
- **Response:** `200 OK`
```json
{
  "id": "number",
  "username": "string",
  "score": "number",
  "created_at": "string"
}
```

### 4. Update User
- **Endpoint:** `PUT /users/:id`
- **Description:** Update a user's information
- **Parameters:** `id` (path parameter)
- **Request Body:**
```json
{
  "username": "string"
}
```
- **Response:** `200 OK`
```json
{
  "id": "number",
  "username": "string",
  "score": "number",
  "created_at": "string"
}
```

### 5. Delete User
- **Endpoint:** `DELETE /users/:id`
- **Description:** Delete a user
- **Parameters:** `id` (path parameter)
- **Response:** `204 No Content`

## Games Endpoints

### 1. Create Game
- **Endpoint:** `POST /games`
- **Description:** Create a new game and play
- **Request Body:**
```json
{
  "username": "string",
  "choice": "string" // "rock", "paper", or "scissors"
}
```
- **Response:** `201 Created`
```json
{
  "id": "number",
  "player_id": "number",
  "player_choice": "string",
  "computer_choice": "string",
  "result": "string",
  "created_at": "string"
}
```

### 2. Get All Games
- **Endpoint:** `GET /games`
- **Description:** Retrieve all games
- **Response:** `200 OK`
```json
[
  {
    "id": "number",
    "player_id": "number",
    "player_choice": "string",
    "computer_choice": "string",
    "result": "string",
    "created_at": "string"
  }
]
```

### 3. Get Game by ID
- **Endpoint:** `GET /games/:id`
- **Description:** Retrieve a specific game by ID
- **Parameters:** `id` (path parameter)
- **Response:** `200 OK`
```json
{
  "id": "number",
  "player_id": "number",
  "player_choice": "string",
  "computer_choice": "string",
  "result": "string",
  "created_at": "string"
}
```

### 4. Get Games by User ID
- **Endpoint:** `GET /games/user/:userId`
- **Description:** Retrieve all games for a specific user
- **Parameters:** `userId` (path parameter)
- **Response:** `200 OK`
```json
[
  {
    "id": "number",
    "player_id": "number",
    "player_choice": "string",
    "computer_choice": "string",
    "result": "string",
    "created_at": "string"
  }
]
```

### 5. Delete Game
- **Endpoint:** `DELETE /games/:id`
- **Description:** Delete a game
- **Parameters:** `id` (path parameter)
- **Response:** `204 No Content`

## Error Responses

All endpoints may return the following error responses:

### 400 Bad Request
```json
{
  "error": "Error message describing the validation error"
}
```

### 404 Not Found
```json
{
  "error": "Resource not found"
}
```

### 500 Internal Server Error
```json
{
  "error": "Internal server error message"
}
```

## API Usage Examples

### Creating a New Game
```javascript
const response = await fetch('http://localhost:8080/api/games', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    username: 'player1',
    choice: 'rock'
  })
});
const game = await response.json();
```

### Getting User History
```javascript
const response = await fetch(`http://localhost:8080/api/games/user/${userId}`);
const games = await response.json();
```

### Creating a New User
```javascript
const response = await fetch('http://localhost:8080/api/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    username: 'newPlayer'
  })
});
const user = await response.json();
```