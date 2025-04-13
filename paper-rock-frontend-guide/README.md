# Paper Rock Scissors Game - Frontend Guide

This guide provides information about connecting a frontend application to the Paper Rock Scissors game API.

## API Overview

The backend API runs on `http://localhost:8080` and provides endpoints for managing users and games.

### Base URL
```
http://localhost:8080/api
```

### Available Endpoints

#### Users API (`/api/users`)
- User management endpoints for player registration and management

#### Games API (`/api/games`)
- Game-related endpoints for creating and managing game sessions

## Data Models

### User Model
```typescript
interface User {
  id: number;
  username: string;
  score: number;
  created_at: string;
}
```

### Game Model
```typescript
interface Game {
  id: number;
  player1_id: number;
  player2_id: number;
  player1_choice: 'paper' | 'rock' | 'scissors';
  player2_choice: 'paper' | 'rock' | 'scissors';
  winner_id: number | null;
  status: 'pending' | 'completed';
  created_at: string;
}
```

## Frontend Setup Recommendations

### Recommended Tech Stack
- React.js or Next.js for the frontend framework
- Axios or fetch for API calls
- TailwindCSS for styling
- TypeScript for type safety

### Example `package.json`
```json
{
  "name": "paper-rock-frontend",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "axios": "^1.6.0",
    "react-router-dom": "^6.22.0",
    "@types/react": "^18.2.0",
    "@types/node": "^20.0.0",
    "tailwindcss": "^3.4.0",
    "typescript": "^5.0.0"
  }
}
```

## API Integration Guide

### Setting up API Client

```typescript
// src/api/client.ts
import axios from 'axios';

const API_BASE_URL = 'http://localhost:8080/api';

export const apiClient = axios.create({
  baseURL: API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});
```

### API Service Example

```typescript
// src/services/gameService.ts
import { apiClient } from '../api/client';

export const gameService = {
  createGame: async (player1Id: number, player2Id: number) => {
    return apiClient.post('/games', { player1Id, player2Id });
  },
  
  makeMove: async (gameId: number, playerId: number, choice: 'paper' | 'rock' | 'scissors') => {
    return apiClient.put(`/games/${gameId}/move`, { playerId, choice });
  },
  
  getGameResult: async (gameId: number) => {
    return apiClient.get(`/games/${gameId}`);
  }
};
```

## Component Structure

Recommended component hierarchy:
```
src/
├── components/
│   ├── Game/
│   │   ├── GameBoard.tsx
│   │   ├── PlayerChoice.tsx
│   │   └── GameResult.tsx
│   ├── User/
│   │   ├── UserProfile.tsx
│   │   └── Leaderboard.tsx
│   └── common/
│       ├── Button.tsx
│       └── Card.tsx
├── pages/
│   ├── Home.tsx
│   ├── Game.tsx
│   └── Profile.tsx
└── services/
    ├── gameService.ts
    └── userService.ts
```

## Error Handling

Implement proper error handling for API calls:

```typescript
try {
  const response = await gameService.makeMove(gameId, playerId, choice);
  // Handle successful response
} catch (error) {
  if (axios.isAxiosError(error)) {
    // Handle API errors
    const errorMessage = error.response?.data?.error || 'An error occurred';
    // Show error to user
  }
}
```

## Authentication

The API currently doesn't implement authentication, but it's recommended to add it for production use. When implemented, you should:

1. Add an auth interceptor to the API client
2. Store tokens in secure storage
3. Implement login/logout functionality
4. Add protected routes

## Development Environment Setup

1. Clone the frontend repository
2. Install dependencies: `npm install`
3. Create a `.env` file:
```env
REACT_APP_API_URL=http://localhost:8080/api
```
4. Start the development server: `npm start`

## Best Practices

1. Use TypeScript for better type safety
2. Implement proper error handling
3. Use loading states for API calls
4. Implement proper form validation
5. Use proper state management (React Context or Redux)
6. Follow responsive design principles
7. Implement proper testing

## Deployment

For production deployment:

1. Build the frontend: `npm run build`
2. Deploy to a static hosting service (Vercel, Netlify, etc.)
3. Update API_BASE_URL to production URL
4. Enable CORS on the backend for your frontend domain

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit changes
4. Create a pull request