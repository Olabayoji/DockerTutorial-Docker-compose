# Docker Compose Tutorial

This repository contains a simple Docker Compose setup to help you understand the basics of containerization with Docker Compose.

## Services

### MongoDB

- **Image:** mongo
- **Volumes:** data:/data/db
- **Environment Variables:** ./env/mongo.env

### Backend

- **Build Path:** ./backend
- **Ports:** 8200:80
- **Volumes:**
  - logs:/app/logs
  - ./backend:/app
  - /app/node_modules
- **Environment Variables:** ./backend/backend.env
- **Depends On:** mongodb

### Frontend

- **Build Path:** ./frontend
- **Ports:** 8100:3000
- **Depends On:** backend
- **Volumes:** ./frontend/src:app/src

## Volumes

- **data:** MongoDB data storage
- **logs:** Backend application logs

## How to Use

1. Clone this repository to your local machine.
2. Navigate to the project directory.
3. Make sure you have Docker and Docker Compose installed on your system.
4. Run `docker-compose up --build` to start the containers.
5. Access the frontend application at `http://localhost:8100`.

## Dockerfile Details

### Backend

```Dockerfile
FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["npm", "start"]
```

### FRONTEND

```Dockerfile
FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["node", "app.js"]
```
