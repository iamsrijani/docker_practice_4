# Integrating Git with Docker for Source-Controlled Application Build

## Aim

To develop a Python Flask web application, containerize it using Docker, and integrate Git and GitHub for source code management and version control.

## Technologies Used

- **Python 3.12:** Programming language used to develop the application.
- **Flask:** Python web framework used to create the web application.
- **Docker:** Platform used to containerize and run the application.
- **Git:** Version control system used to track source code changes.
- **GitHub:** Cloud-based platform used to host and manage the source code repository.
- **Ubuntu:** Operating system used for implementation.

## Description

This program demonstrates how to create a simple Python Flask web application, package it into a Docker image, run it inside a Docker container, and maintain the source code using Git and GitHub.

The Flask application displays a welcome message when accessed through a web browser.

Docker is used to create a portable containerized environment for the application, while Git and GitHub are used to maintain different versions of the source code and track modifications.

---

## Prerequisites

- Ubuntu Linux
- Python 3.12
- Docker installed and running
- Git installed
- GitHub account
- Internet connection
- Basic knowledge of Linux commands

---

## Step 1: Update Ubuntu

Update the package repositories:

```bash
sudo apt update
sudo apt upgrade -y
```

## Step 2: Install Required Packages

Install Git, Python and pip:

```bash
sudo apt install git python3 python3-pip python3-venv -y
```

Verify the installations:

```bash
git --version
python3 --version
```

## Step 3: Verify Docker Installation

Check Docker:

```bash
docker --version
```

Check whether Docker is running:

```bash
sudo systemctl status docker
```

If Docker is not running, start it:

```bash
sudo systemctl start docker
```

Enable Docker to start automatically:

```bash
sudo systemctl enable docker
```

## Step 4: Create the Project Directory

Create a directory named `p4`:

```bash
mkdir p4
```

Navigate into the directory:

```bash
cd p4
```

Check the current directory:

```bash
pwd
```

## Step 5: Create the Flask Application

Create the Python application file:

```bash
nano app.py
```

Add the following Python code:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Second commit to app.py file"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=3000)
```

Save the file using:

1. Press `Ctrl + O`.
2. Press Enter.
3. Press `Ctrl + X`.

### Code Explanation

- `from flask import Flask`: Imports the Flask framework.
- `app = Flask(__name__)`: Creates a Flask application.
- `@app.route("/")`: Defines the home page URL.
- `def home()`: Defines the function executed when the home page is accessed.
- `return`: Displays the specified message in the browser.
- `app.run()`: Starts the Flask development server.
- `host="0.0.0.0"`: Allows the application to accept connections from outside the container.
- `port=3000`: Runs the application on port 3000.

## Step 6: Create the Dockerfile

Create a file named `Dockerfile`:

```bash
nano Dockerfile
```

Add the following instructions:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY app.py .

RUN pip install flask

EXPOSE 3000

CMD ["python", "app.py"]
```

Save and exit the file.

### Dockerfile Explanation

| Instruction | Description |
|---|---|
| FROM | Specifies the Python 3.12 slim base image. |
| WORKDIR | Sets the working directory inside the container to `/app`. |
| COPY | Copies the `app.py` file into the container. |
| RUN | Installs the Flask framework. |
| EXPOSE | Documents port 3000 used by the application. |
| CMD | Executes the Python application when the container starts. |

## Step 7: Build the Docker Image

Build the Docker image using:

```bash
sudo docker build -t p4 .
```

### Command Explanation

- `docker build`: Builds a Docker image.
- `-t p4`: Assigns the image name `p4`.
- `.`: Specifies the current directory as the build context.

Verify the image:

```bash
sudo docker images
```

The Docker image named `p4` should appear in the list.

## Step 8: Run the Docker Container

Start the container in detached mode:

```bash
sudo docker run -d -p 3000:3000 --name prg4 p4
```

### Command Explanation

- `docker run`: Creates and starts a container.
- `-d`: Runs the container in the background.
- `-p 3000:3000`: Maps host port 3000 to container port 3000.
- `--name prg4`: Assigns the container name `prg4`.
- `p4`: Specifies the Docker image to run.

## Step 9: Verify the Running Container

Execute:

```bash
sudo docker ps
```

This command displays the currently running Docker containers.

The output should show:

- Container ID
- Image name (`p4`)
- Container name (`prg4`)
- Port mapping (`3000:3000`)
- Container status (`Up`)

## Step 10: Test the Flask Application

Open a web browser and enter:

```text
http://localhost:3000
```

### Expected Output

The browser should display:

```text
Second commit to app.py file
```

This confirms that the Flask application is successfully running inside the Docker container.

## Step 11: Create a GitHub Repository

1. Open GitHub.
2. Log in to your GitHub account.
3. Click **New Repository**.
4. Enter the repository name:

   `program4_docker`

5. Create the repository.

Repository:

https://github.com/iamsrijani/program4_docker

## Step 12: Initialize Git

Navigate to the project directory if you are not already inside it:

```bash
cd ~/p4
```

Initialize the Git repository:

```bash
git init
```

This initializes a new local Git repository.

## Step 13: Add Files to Git

Stage all project files:

```bash
git add .
```

Check the status:

```bash
git status
```

This displays the files staged for committing.

## Step 14: Commit the Files

Create the first commit:

```bash
git commit -m "first commit"
```

This saves the staged changes in the local Git repository.

## Step 15: Rename the Branch to Main

Execute:

```bash
git branch -M main
```

This renames the current branch to `main`.

## Step 16: Connect the Local Repository to GitHub

Add the GitHub remote repository:

```bash
git remote add origin https://github.com/iamsrijani/program4_docker.git
```

If the remote named `origin` already exists, update its URL:

```bash
git remote set-url origin https://github.com/iamsrijani/program4_docker.git
```

Verify the remote connection:

```bash
git remote -v
```

## Step 17: Push the Project to GitHub

Upload the project:

```bash
git push -u origin main
```

If authentication is requested:

- Enter your GitHub username.
- Use a GitHub Personal Access Token (PAT) instead of your regular account password.

After successful execution, the project files will be available in your GitHub repository.

## Step 18: Verify the Uploaded Files

Open the repository:

https://github.com/iamsrijani/program4_docker

Refresh the page and verify that the following files are present:

- `app.py`
- `Dockerfile`
- `README.md`

## Step 19: Modify the Flask Application

Open the application file:

```bash
nano app.py
```

Modify the return message inside the home function.

For example:

```python
@app.route("/")
def home():
    return "Second commit to app.py file"
```

Save the changes.

### Important: Rebuild the Docker Image

Since the application code has been modified, rebuild the image:

```bash
sudo docker build -t p4 .
```

Remove the existing container:

```bash
sudo docker stop prg4
sudo docker rm prg4
```

Run the updated container:

```bash
sudo docker run -d -p 3000:3000 --name prg4 p4
```

Test the updated application again:

```text
http://localhost:3000
```

## Step 20: Commit and Push the Updated Changes

Stage the modified files:

```bash
git add .
```

Create the second commit:

```bash
git commit -m "second commit"
```

Push the changes to GitHub:

```bash
git push
```

The updated source code will now be available in the GitHub repository.

---

## Project Structure

```text
program4_docker/
│
├── README.md
│
├── app.py
│
└── Dockerfile
```

## Important Git Commands

| Command | Description |
|---|---|
| `git init` | Initializes a new Git repository. |
| `git add .` | Stages all project files. |
| `git status` | Displays the current repository status. |
| `git commit -m "message"` | Saves changes in the local repository. |
| `git branch -M main` | Renames the current branch to main. |
| `git remote add origin URL` | Connects the local repository to GitHub. |
| `git remote -v` | Displays configured remote repositories. |
| `git push -u origin main` | Pushes the local main branch to GitHub. |
| `git pull origin main` | Fetches and integrates remote changes. |

## Important Docker Commands

| Command | Description |
|---|---|
| `sudo docker build -t p4 .` | Builds the Docker image named p4. |
| `sudo docker images` | Lists available Docker images. |
| `sudo docker run -d -p 3000:3000 --name prg4 p4` | Creates and starts the container. |
| `sudo docker ps` | Lists running containers. |
| `sudo docker stop prg4` | Stops the running container. |
| `sudo docker start prg4` | Starts an existing stopped container. |
| `sudo docker rm prg4` | Removes the stopped container. |
| `sudo docker logs prg4` | Displays container logs. |

## Expected Output

When the application is accessed through:

```text
http://localhost:3000
```

The browser displays:

```text
Second commit to app.py file
```

The Docker container runs successfully, and the application source files are maintained in the GitHub repository.

## Result

Successfully developed a Python Flask web application, containerized it using Docker, and executed it inside a Docker container. Integrated Git and GitHub for source code management and version control. Demonstrated how to modify application code, create commits, and push updated changes to the remote GitHub repository.

