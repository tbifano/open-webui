# Starting the Open WebUI Backend

This guide explains how to start the Open WebUI backend server.

## Prerequisites

- Python virtual environment (venv) activated
- Located in the project root directory (`open-webui/`)

## Method 1: Using the Development Script

This is the recommended method:

1. Navigate to the backend directory:

bash
cd backend

2. Make the development script executable:
bash
chmod +x ./dev.sh


## Method 2: Using Uvicorn Directly

Alternatively, you can start the server using uvicorn directly:

bash
cd backend
python -m uvicorn open_webui.main:app --host 0.0.0.0 --port 8080 --reload



## Verification

The backend has started successfully when you see:

1. The Open WebUI ASCII art banner
2. The version number
3. The following startup messages:
   ```bash
   INFO:     Uvicorn running on http://0.0.0.0:8080 (Press CTRL+C to quit)
   INFO:     Application startup complete.
   ```


## Important Notes

- Keep the terminal window open while running the backend
- The backend must be running on port 8080 for the frontend to communicate with it
- Use CTRL+C to stop the server when needed
- The `--reload` flag enables auto-reloading during development when code changes are made

## Troubleshooting

If you encounter permission issues with `dev.sh`:
- Verify you're in the correct directory
- Ensure the script has executable permissions
- Try running with sudo if necessary (not recommended for development)

If the port is already in use:
- Check for other processes using port 8080
- Kill the existing process or use a different port