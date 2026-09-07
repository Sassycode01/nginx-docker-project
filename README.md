## Nginx Docker Project

## Project Overview

 This project demonstrates how to containerize an Nginx web server using Docker and deploy it on an AWS EC2 Ubuntu server

## Technologies Used

     - AWS EC2
     - Ubuntu Linux
     - Docker
     - Nginx
     - Git
     - Github
     - HTML
     - Dockerhub

## Project Structure

nginx-docker-project/

  |---Dockerfile
  |---index.html
  |---README.md

## Dockerfile

The Dockerfile uses the official Nginx image and copies the HTML page into the Nginx web root

## Docker commands

build the docker image :

docker build -t nginx-docker-project:latest .

Run the container :
 
docker run -d --name nginx-container -p 80:80 nginx-docker-project:latest

check running containers :

docker ps

## Docker Hub

Docker image :

sassy2031/mynginx:latest

Pull the image from Docker Hub :

docker pull sassy2031/mynginx:latest

Run the image :

docker run -d -p 8080:80 --name mynginx-container sassy2031/mynginx:latest


## Docker Compose

start the application :

docker_compose up -d

Checking the running application :

docker-compose ps

Stop the application :

docker-compose down
## AWS Deployment

The Docker container was deployed on AWS EC2 Ubuntu server.
 
port 80 was configured in the EC2 Security Group to allow HTTP traffic.

The application can then be accessed through the EC2 public IP address.


## Result

A custom HTML webpage is successfully served through Nginx running inside a Docker container on AWS EC2
