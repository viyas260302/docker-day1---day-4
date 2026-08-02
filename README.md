# docker-day1---day-4
journey of my docker learnings

Hi, I'm Viyas, a B.Com. Business Analytics graduate currently transitioning into DevOps Engineering.

I believe that learning is more valuable when concepts are understood rather than memorized. This repository documents my Docker learning journey with practical exercises, explanations, commands, and observations.

My goal is to build a strong DevOps foundation through hands-on practice before moving on to Kubernetes, Jenkins, Terraform, CI/CD, and AWS.

📅 Day 1 – Docker Images & Containers
Objective

Understand what Docker is and learn the difference between Images and Containers.

What I Learned

Docker is a platform that packages applications with everything they need to run, including dependencies, libraries, and configurations.

Instead of saying:

"It works on my computer."

Docker allows developers to say:

"It works everywhere."

Understanding Images

An Image is a blueprint or template.

It contains:

Application
Dependencies
Required Libraries
Environment

An image is read-only.
Example:
```
Ubuntu Image
```
Understanding Containers

A Container is a running instance of an image.

Think of it like this:
```
Image
      ↓
docker run
      ↓
Container
```
One image can create multiple containers.

Commands Practiced
```
docker pull hello-world
```
Downloads an image from Docker Hub.
```
docker images
```
Lists downloaded images.
```
docker run hello-world
```
Creates and runs a container.
```
docker ps
```
Shows running containers.
```
docker ps -a
```
Shows all containers.

Key Takeaways :
Images are templates.
Containers are running applications.
One image can create many containers.
Containers can be deleted and recreated anytime.

📅 Day 2 – Dockerfile & Custom Website :

Objective

Learn how Docker Images are created.

What I Learned

Instead of downloading an existing image, Docker allows us to create our own custom image using a Dockerfile.

A Dockerfile is simply a text file containing instructions.

Docker reads the instructions from top to bottom and builds an image.

Project

Built and deployed a simple HTML webpage using:

Docker
Nginx
HTML
Dockerfile
```
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```
Understanding Each Line
FROM
```
FROM nginx:latest
```
Uses the official Nginx image as the base.

COPY
```
COPY index.html /usr/share/nginx/html/index.html
```
Copies my webpage into the Nginx web server directory.
Commands Practiced
```
docker build -t my-first-website .
```
Builds an image from the Dockerfile.
```
docker images
```
Lists available images.
```
docker run -d -p 8080:80 --name mywebsite my-first-website
```
Runs the website inside a container.

Key Takeaways : 
Dockerfile automates image creation.
Images become reusable.
Containers can host websites and applications.

📅 Day 3 – Dockerfile Instructions

Objective

Understand important Dockerfile instructions used in real-world projects.

Dockerfile
```
FROM ubuntu:latest

WORKDIR /app

RUN apt update && mkdir docker-learning

ENV COURSE="Docker Day 3"

CMD ["bash"]
```
What I Learned
FROM

Defines the base image.
```
FROM ubuntu:latest
```
WORKDIR

Sets the default working directory.
```
WORKDIR /app
```
Every future command executes inside /app.
RUN

Executes commands while building the image.

Example:
```
RUN apt update
```
The result becomes part of the image.

ENV

Stores environment variables.
```
ENV COURSE="Docker Day 3"
```
Inside the container:
```
echo $COURSE
```
Output:

Docker Day 3

CMD

Defines the default command executed when a container starts.
```
CMD ["bash"]
```
Starts a Bash shell automatically

Key Takeaways :
RUN executes during image creation.
CMD executes when the container starts.
ENV stores configuration values.
WORKDIR sets the working directory.

📅 Day 4 – Docker Volumes

Objective

Understand how Docker stores persistent data.

Problem

Containers are temporary.

If a container is deleted, its internal data is also deleted.

Example:
```
Container

↓

Database

↓

Delete Container

↓

Database Lost
```
Solution

Docker Volumes.

Volumes store data outside containers.
```
Container

↓

Docker Volume

↓

Data
```
Even if the container is deleted:
```
Container ❌

Volume ✅

Data ✅
```
Commands Practiced :

Create Volume
```
docker volume create notes-volume
```
Run Container
```
docker run -it --name ubuntu1 -v notes-volume:/data ubuntu
```
Create File
```
cd /data

echo "Hello Docker Volume" > notes.txt
```
Verify
```
cat notes.txt
```
Delete Container
```
docker rm ubuntu1
```
Create New Container
```
docker run -it --name ubuntu2 -v notes-volume:/data ubuntu
```
Verify Again
```
cd /data

cat notes.txt
```
Output:

Hello Docker Volume

The file remained even after deleting the first container.

Key Takeaways
Containers are temporary.
Volumes provide persistent storage.
Multiple containers can access the same volume.
Databases rely on volumes to prevent data loss.
