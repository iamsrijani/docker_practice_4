Practice program 4: Integrate Git with Docker for Source-Controlled Application Build

1. Aim

To develop a Flask application, containerize it using Docker, and integrate Git and GitHub for source code management and version control.

2. Technologies Used

* Python 3.12
* Flask
* Docker
* Git
* GitHub
* Ubuntu

3. Description

This program demonstrates how to create a simple Python Flask web application, package it into a Docker image, run it inside a Docker container, and maintain the source code using Git and GitHub. The application displays a welcome message when accessed through a web browser.

4. Project Structure

p4/
├── app.py
├── Dockerfile
└── README.md

5. Source Code

app.py

from  flask import Flask
app= Flask(__name__)
@app.route("/")
def home():
        return "Second commit to app.py file"
if __name__== "__main__":
        app.run(host= "0.0.0.0", port= 3000)



Dockerfile

FROM python:3.12-slim
WORKDIR /app
COPY app.py .
RUN pip install flask
EXPOSE 3000
CMD ["python", "app.py"]


6. Procedure

Step 1: Create a project directory

mkdir p4
cd p4

Step 2: Create the Flask application

nano app.py

Write the Python Flask code given above and save the file.

Step 3: Create the Dockerfile

nano Dockerfile

Write the Dockerfile instructions given above and save the file.

Step 4: Build the Docker image

sudo docker build -t p4 .

This command builds a Docker image named p4.

Step 5: Run the Docker container

sudo docker run -d -p 3000:3000 --name prg4 p4

This command starts the container in detached mode and maps port 3000 of the host machine to port 3000 of the container.

Step 6: Verify the running container

sudo docker ps

This command displays the running Docker containers.

Step 7: Test the application

Open a web browser and enter:

http://localhost:3000

Expected output:

Hello

Step 8: Create a GitHub repository

1. Open GitHub.
2. Create a new repository.
3. Name the repository program4_docker.
4. Create the repository.

Step 9: Initialize Git

git init

This command initializes a new Git repository in the project directory.

Step 10: Add files to Git

git add .

This command stages all project files for committing.

Step 11: Commit the files

git commit -m "first commit"

This command saves the changes in the local Git repository.

Step 12: Rename the branch to main

git branch -M main

Step 13: Connect the local repository to GitHub

git remote add origin https://github.com/iamsrijani/program4_docker.git

If the remote named origin already exists, use:

git remote set-url origin https://github.com/iamsrijani/program4_docker.git

Step 14: Push the project to GitHub

git push -u origin main

Enter your GitHub username and use a Personal Access Token (PAT) when authentication is requested.

Step 15: Verify the uploaded files

Open your GitHub repository and verify that the project files are uploaded successfully.

Repository: https://github.com/iamsrijani/program4_docker

Step 16: Modify the application

Open the application file:

nano app.py

Modify the return message in the Flask application and save the changes.

Step 17: Commit and push the updated changes

git add .
git commit -m "second commit"
git push

The updated application code will be pushed to GitHub.

7. Dockerfile Explanation

Instruction	Description
FROM	Specifies the Python base image.
WORKDIR	Sets the working directory inside the container.
COPY	Copies app.py into the container.
RUN	Installs Flask.
EXPOSE	Specifies port 3000.
CMD	Executes the Python application.

8. Expected Output

When the application is accessed through http://localhost:3000, the browser displays:

Hello

The Docker container runs successfully, and the application source files are maintained in the GitHub repository.

9. Result

Thus, a Flask web application was successfully developed, containerized using Docker, executed inside a Docker container, and integrated with Git and GitHub for source code management and version control.
