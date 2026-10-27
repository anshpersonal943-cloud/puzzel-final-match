# Multiplayer Sliding Puzzle Game

A fun, colorful multiplayer sliding puzzle game for kids, built with Node.js, Express, Socket.IO, and vanilla JavaScript.

## Features

- **Host-Controlled Game**: Only the host can upload the puzzle image and start the game.
- **Multiplayer Rooms**: Players join using a room ID.
- **Real-Time Updates**: Live rankings and game state synchronization.
- **Progressive Puzzle Difficulty**: Three levels use 4x4, 5x5, and 6x6 tile grids.
- **Timer**: Tracks time during the game.
- **Winner Detection**: First player to solve the puzzle wins.
- **Refresh-Safe**: Players automatically rejoin the game on page refresh.

## How to Play

1. **Join a Room**: Enter a room ID and your name to join or create a room.
2. **Host Uploads Image**: The host uploads an image to use for the puzzle.
3. **Host Starts Game**: Once the image is uploaded, the host starts the game.
4. **Solve the Puzzle**: Click on tiles adjacent to the empty space to move them.
5. **Race to Win**: The first player to arrange the tiles correctly wins!

## Installation

1. Clone the repository.
2. Install dependencies: `npm install`
3. Start the server: `npm run dev`
4. Open your browser to `http://localhost:3000`

## Vercel Deployment

The frontend and `/api/room` endpoint deploy as static assets and a Vercel Function. Room state is stored in Upstash Redis so separate function invocations share the same rooms. Clients poll room state every 1.8 seconds; no long-lived server or Socket.IO connection is required.

1. Create an Upstash Redis database and connect it to the Vercel project, or add `UPSTASH_REDIS_REST_URL` and `UPSTASH_REDIS_REST_TOKEN` to the project's environment variables.
2. Add a long random value as `ROOM_SESSION_SECRET` in the Vercel project's environment variables.
3. Import this repository into Vercel and deploy it with the project root as the root directory.
4. Redeploy after setting all three environment variables. Multiplayer requests return an error until they are configured.

Local development uses temporary in-memory room state when the Upstash variables are absent. Local rooms are not shared across server restarts.

## Technologies Used

- **Backend**: Node.js, Express, Socket.IO
- **Frontend**: HTML, CSS, JavaScript, Canvas API
- **Real-Time Communication**: Socket.IO

## Game Rules

- Each of the three levels contains two image puzzles.
- Grid sizes increase by level: 4x4, 5x5, then 6x6.
- The image is shuffled randomly but remains solvable.
- Players can only move tiles adjacent to the empty space.
- The game ends when the first player solves the puzzle.
- Rankings are updated in real-time as players finish.