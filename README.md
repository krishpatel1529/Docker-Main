# DockerFile

# Frontend Dockerfile
1. `FROM node:latest`: This line tells Docker to use an existing Docker image called "node" with the latest version. Docker images are like pre-packaged environments that contain everything needed to run an application.

2. `WORKDIR /app`: This sets the working directory inside the Docker container to `/app`. It's like navigating to a specific folder on your computer before doing anything else.

3. `COPY package*.json ./`: This copies the package.json file (and any other file that starts with "package") from your local machine into the `/app` directory in the Docker container. The package.json file typically lists all the dependencies needed for your Node.js application.

4. `RUN npm install`: This command runs inside the Docker container and installs all the dependencies listed in the package.json file. It's like running `npm install` on your local machine to install all the required libraries for your Node.js application.

5. `COPY . .`: This copies all the files and folders from your local machine into the `/app` directory in the Docker container. This includes your application code.

6. `EXPOSE 3000`: This command tells Docker to expose port 5000 from the container to the outside world. It's like opening a specific door on the container so that other programs can communicate with your Node.js application running inside.

7. `CMD ["npm", "start"]`: This sets the default command to run when the Docker container starts. In this case, it runs `npm start`, which typically starts your Node.js application. It's like setting the initial action when you turn on your computer.


# Backend Dockerfile
1. `FROM node:latest`: This line tells Docker to use an existing Docker image called "node" with the latest version. Docker images are like pre-packaged environments that contain everything needed to run an application.

2. `WORKDIR /app`: This sets the working directory inside the Docker container to `/app`. It's like navigating to a specific folder on your computer before doing anything else.

3. `COPY package*.json ./`: This copies the package.json file (and any other file that starts with "package") from your local machine into the `/app` directory in the Docker container. The package.json file typically lists all the dependencies needed for your Node.js application.

4. `RUN npm install`: This command runs inside the Docker container and installs all the dependencies listed in the package.json file. It's like running `npm install` on your local machine to install all the required libraries for your Node.js application.

5. `COPY . .`: This copies all the files and folders from your local machine into the `/app` directory in the Docker container. This includes your application code.

6. `EXPOSE 3001`: This command tells Docker to expose port 5000 from the container to the outside world. It's like opening a specific door on the container so that other programs can communicate with your Node.js application running inside.

7. `CMD ["npm", "start"]`: This sets the default command to run when the Docker container starts. In this case, it runs `npm start`, which typically starts your Node.js application. It's like setting the initial action when you turn on your computer.


# Compose File
Let's break down the code:

```yaml
version: "3"
```
This specifies the version of the Docker Compose file format being used. In this case, it's version 3.

```yaml
services:
```
This is where you define the services that make up your application.

```yaml
  frontend:
    image: todo-frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend
```
Defines a service named "frontend". It specifies that the frontend application will be built using the Dockerfile located in the "./todo-backend" directory. It also maps port 3000 of the container to port 3000 on the host, allowing access to the frontend application from the host machine.

```yaml
  backend:
    image: todo-backend
    ports:
      - "3001:3001"
    depends_on:
      - database
```
Defines a service named "backend". It specifies that the backend application will be built using the Dockerfile located in the "./todo-backend" directory. It maps port 3001 of the container to port 3001 on the host.

```yaml

  database:
    image: mongo:latest
    ports:
      - "27017:27017"

```
Defines a service named "database". It uses the official MongoDB Docker image from Docker Hub. It sets the environment variable `MONGO_ROOT_PASSWORD` to "my-secret-pw", which will be used as the root password for MongoDB. It maps port 27017 of the container to port 27017 on the host, allowing access to the MongoDB database from the host machine.
