# Webapp

The webapp consists of a React frontend and a FastAPI backend.

## Frontend

The frontend should be built on your development computer, not directly on the RFSoC board. Building the React app on the board's ARM CPU is slow and can be too resource-intensive.

The update workflow is:

1. Change the frontend code on your computer.
2. Build the React app locally.
3. Upload the generated `dist/` folder to the PYNQ environment.

In this setup, the generated `dist/` folder is uploaded through GitHub by keeping it as part of the application repository. The RFSoC board then uses that already-built frontend instead of building it locally.

## Backend

The backend is a FastAPI service. More backend development notes can be added here later.
