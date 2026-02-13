# First Step – Today’s Goal

**Goal:** Set up the project foundations so we can start implementing core functionality.

## What we will do today
1. **Initialize a git repository** (if not already created) and create an initial commit.
2. **Create the backend skeleton**:
   - Set up a new Python virtual environment.
   - Install FastAPI, Uvicorn, SQLAlchemy, and Pydantic.
   - Generate a minimal `main.py` that starts the FastAPI app.
   - Add a placeholder `requirements.txt`.
3. **Create the frontend skeleton**:
   - Run `npx create-next-app@latest` (TypeScript and App Router).
   - Install Tailwind CSS and set up basic styling.
   - Add a simple home page that displays "Personal Media Aggregator".
4. **Add Docker Compose basics**:
   - Create a `docker-compose.yml` with services for the backend, frontend, and Redis.
   - Ensure the services can be built and started with `docker compose up`.
5. **Commit the scaffold** to the repository.

By the end of today we will have a runnable project structure, ready for the next phases (authentication, TMDB integration, etc.).