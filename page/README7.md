To deploy multi-service applications using Docker Compose.
2. Procedure
Step 1: Install Docker Desktop

1. Download Docker Desktop for Windows.
2. Install it using the default settings.
3. Restart your computer.
4. Open Docker Desktop and wait until Docker Engine is running.

Step 2: Check Docker installation

docker --version
docker compose version


Step 3: Create the project folders
Create this folder structure on your Desktop:

compose-demo
├── docker-compose.yml
├── app
└── nginx


Open the compose-demo folder in VS Code.
Step 4: Create app.py
Inside the app folder, create app.py and write:

from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "<h1>Hello from Docker Compose!</h1>"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)



Step 5: Create requirements.txt
Inside the app folder, create requirements.txt:

Flask


Step 6: Create Dockerfile
Inside the app folder, create Dockerfile:

FROM python:3.10
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python","app.py"]


Step 7: Create default.conf
Inside the nginx folder, create default.conf:

server {
    listen 80;

    location / {
        proxy_pass http://app:5000;
    }
}


Step 8: Create docker-compose.yml
Inside the main compose-demo folder, create docker-compose.yml:

services:
  app:
    build: ./app

  nginx:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - app


Step 9: Open the terminal
In VS Code, select Terminal → New Terminal.

Make sure the terminal is inside the compose-demo folder.
Step 10: Build the application-

docker compose build


Step 11: Start the application-

docker compose up


This starts both Flask and Nginx services.
Step 12: Check the containers
Open another terminal and run:

docker ps


Step 13: Test the application
Open your browser and enter:

http://localhost

Expected output:
Hello from Docker Compose!


Step 14: Stop the application
Press Ctrl + C, then run:

docker compose down