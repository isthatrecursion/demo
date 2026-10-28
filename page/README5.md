To containerize applications using Docker.
2. Procedure
Step 1: Check Docker installation
Open the Ubuntu/Linux terminal and run:

docker --version


Information: Checks whether Docker is installed.
- If Docker is installed, the version will be displayed. Continue to Step 2.
- If Docker is not installed, go to Step 1A.
Step 1A: Install Docker (only if not installed)

sudo apt update
sudo apt install docker.io -y


After installation, check the version again:

docker --version


Information: Installs Docker and verifies the installation.
Step 2: Create a project folder

mkdir myapp
cd myapp


Information: Creates a project folder named myapp.
Step 3: Create the application file

nano app.py


Write the following code:

from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello Darshan!"

app.run(host='0.0.0.0', port=5000)



Save using Ctrl + O, press Enter, and then Ctrl + X.

Information: Creates a simple Flask application that displays a message in the browser.
Step 4: Create the requirements file

nano requirements.txt


Write:

Flask


Save the file.

Information: Specifies the Python package required by the application.
Step 5: Create a Dockerfile

nano Dockerfile


Write the following code:

FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]


Save the file.

Information: Defines the instructions to build a Docker image for the Flask application.
Step 6: Build the Docker image

sudo docker build -t myapp .


Information: Builds a Docker image named myapp using the Dockerfile in the current directory.
Step 7: Run the container

sudo docker run -d -p 5000:5000 --name mycontainer myapp


Information: Runs the application inside a container and maps port 5000 to port 5000 on the host machine.
Step 8: Check the container

sudo docker ps


Information: Displays the running Docker containers.
Step 9: Test the application
Open the web browser and enter:

http://localhost:5000

Expected output:
Hello Darshan!


Information: Checks whether the application is running successfully inside the Docker container.