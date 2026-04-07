
### 1.1 Write requirements.txt

- [ ] Add the following dependencies:
  - flask
  - gunicorn

### 1.2 Write main.py

- [ ] Create a Flask app instance
- [ ] Define a route for `/` that renders `index.html`
- [ ] Make the app listen on `0.0.0.0` port `5000`
- [ ] Add a `/health` route that returns `{"status": "ok"}`

### 1.3 Download SVG Logos

- [ ] Save the Docker logo SVG into `app/static/images/docker-logo.svg`
- [ ] Save the Flask logo SVG into `app/static/images/flask-logo.svg`

### 1.4 Create index.html

- [ ] Add a simple navbar with the text "Docker Learning Sandbox"
- [ ] Display the Docker SVG logo
- [ ] Display the Flask SVG logo
- [ ] Add a heading: "Learning Containerization with Flask"
- [ ] Add basic inline CSS or a style block for the navbar
- [ ] Use Jinja2 url_for to reference static files

### 1.5 Test Locally (Without Docker)

- [ ] Create a virtual environment: `python -m venv venv`
- [ ] Activate it: `source venv/bin/activate`
- [ ] Install dependencies: `pip install -r requirements.txt`
- [ ] Run the app: `python app/main.py`
- [ ] Open browser at `http://localhost:5000` and confirm it works
- [ ] Stop the server with `Ctrl+C`

---

## Phase 2: The Containerization Layer (Docker)

### 2.1 Write the Dockerfile

- [ ] Use `python:3.12-slim` as the base image
- [ ] Set `WORKDIR /app`
- [ ] Copy `requirements.txt` into the image
- [ ] Run `pip install --no-cache-dir -r requirements.txt`
- [ ] Copy the `app/` folder into the image
- [ ] Create a non-root user with `useradd`
- [ ] Switch to the non-root user with `USER`
- [ ] Expose port `5000`
- [ ] Set the CMD to run gunicorn: `gunicorn --bind 0.0.0.0:5000 app.main:app`

### 2.2 Write docker-compose.yml

- [ ] Define a service called `web-app`
- [ ] Set `build: .` to use the local Dockerfile
- [ ] Map port `5000:5000`
- [ ] Add a volume: `./app:/app/app` for live code reloading
- [ ] Add a health check that curls `http://localhost:5000/health`
- [ ] Set `restart: unless-stopped`

---

## Phase 3: Build, Run, and Debug

### 3.1 Build and Start

- [ ] Run: `docker compose up --build`
- [ ] Open browser at `http://localhost:5000`
- [ ] Confirm the page loads with navbar and SVG logos

### 3.2 Explore Docker Commands

- [ ] Run `docker ps` to see the running container
- [ ] Run `docker images` to check the image size
- [ ] Run `docker exec -it <container_id> /bin/bash` to enter the container
- [ ] Inside the container run `whoami` to confirm it is NOT root
- [ ] Exit the container with `exit`
- [ ] Run `docker compose logs -f` to watch live logs

### 3.3 Test Live Reloading

- [ ] Edit `index.html` on your computer (change the heading text)
- [ ] Refresh the browser
- [ ] Confirm the change appears without rebuilding

### 3.4 Cleanup

- [ ] Run `docker compose down` to stop and remove containers
- [ ] Run `docker system prune -f` to clean up unused data

---

## Phase 4: Knowledge Check

After completing all tasks above, answer these questions:

- [ ] Why did we use `0.0.0.0` instead of `127.0.0.1`?
- [ ] What is the difference between a Docker Image and a Container?
- [ ] Why use `python:3.12-slim` instead of `python:3.12`?
- [ ] What does the Volume mapping do in docker-compose.yml?
- [ ] Why do we create a non-root user in the Dockerfile?
- [ ] What is the difference between `flask run` and `gunicorn`?

---

## Success Criteria

- [ ] Page loads in browser with navbar and both SVG logos
- [ ] Docker image size is under 200MB
- [ ] Container runs as a non-root user
- [ ] Health check passes
- [ ] Code changes reflect in browser without rebuilding the image
- [ ] All Phase 4 questions answered
