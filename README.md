# 🚀 Getting started with Strapi

Strapi comes with a full featured [Command Line Interface](https://docs.strapi.io/dev-docs/cli) (CLI) which lets you scaffold and manage your project in seconds.

markdown
Copy code
# Strapi App Dockerization Guide

This guide provides step-by-step instructions to dockerize a Strapi app, from setting up Strapi locally to creating Docker configurations and running the app in a Docker container.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/en/download/)
- [Docker](https://www.docker.com/products/docker-desktop)

## Step 1: Set Up Strapi Locally

1. **Install Node.js and npm:**

   Ensure you have Node.js and npm installed. You can download and install them from [Node.js](https://nodejs.org/en/download/).

2. **Create a Strapi Project:**

   Open a terminal and run the following commands to create a new Strapi project.

   ```bash
   npx create-strapi-app my-project --quickstart
Replace my-project with your desired project name.

Navigate to Project Directory:

bash
Copy code
cd my-project
Start the Strapi Application:

bash
Copy code
npm run develop
Your Strapi app should now be running on http://localhost:1337.

Step 2: Dockerize Strapi
Create a Dockerfile:

In the root of your Strapi project, create a file named Dockerfile with the following content:

Dockerfile
Copy code
# Use the official Node.js image
FROM node:18

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose port 1337
EXPOSE 1337

# Start the Strapi application
CMD ["npm", "run", "start"]
Create a .dockerignore File:

In the root directory, create a .dockerignore file to exclude unnecessary files:

plaintext
Copy code
node_modules
.tmp
build
public/uploads
Build the Docker Image:

bash
Copy code
docker build -t strapi-app .
Run the Docker Container:

bash
Copy code
docker run -p 1337:1337 strapi-app
Your Strapi app should now be accessible at http://localhost:1337.

Step 3: Push Docker Image to DockerHub
Tag the Docker Image:

bash
Copy code
docker tag strapi-app:latest yourdockerhubusername/strapi-app:latest
Log In to DockerHub:

bash
Copy code
docker login
Enter your DockerHub username (yourdockerhubusername) and password when prompted.

Push the Docker Image:

bash
Copy code
docker push yourdockerhubusername/strapi-app:latest
Summary
You have successfully dockerized your Strapi application and pushed the Docker image to DockerHub. You can now pull and run your Strapi app from DockerHub on any machine with Docker installed.

markdown
Copy code
docker pull yourdockerhubusername/strapi-app:latest
docker run -p 1337:1337 yourdockerhubusername/strapi-app:latest