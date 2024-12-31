# Starting the Open WebUI Frontend

This guide explains how to start the Open WebUI frontend server.

## Prerequisites

- Node.js installed (version >=18.13.0 <=22.x.x)
- npm installed (version >=6.0.0)
- Located in the project root directory (`open-webui/`)
- Backend server running (see `starting_backend.md`)

## Starting the Development Server

1. Install dependencies (if not already installed):
   ```bash
   npm install
   ```

2. Start the development server:
   ```bash
   npm run dev
   ```

## Verification

The frontend has started successfully when you see:

1. Pyodide packages being downloaded and installed
2. The following startup messages:
   ```bash
   VITE v5.4.6  ready in XXX ms

   ➜  Local:   http://localhost:5173/
   ➜  Network: http://[your-ip]:5173/
   ➜  press h + enter to show help
   ```

## Important Notes

- Keep the terminal window open while running the frontend
- The frontend typically runs on port 5173 (or next available port if 5173 is in use)
- The backend must be running before starting the frontend
- Changes to frontend code will automatically trigger hot-reloading

## Troubleshooting

If you see port conflicts:
- The development server will automatically try the next available port
- You can manually specify a port using `--port`:
  ```bash
  npm run dev -- --port 3000
  ```

If you encounter dependency issues:
- Try removing `node_modules` and running `npm install` again
- Ensure your Node.js version meets the requirements
- Check for any error messages in the npm output 