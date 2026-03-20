Great Vipin 👍 Since you're learning **Node.js deployment on Ubuntu**, Docker will help you a lot in CI/CD and production.

I’ll explain **Docker from basic to advanced commands** with clear examples.

---

# 🔹 1️⃣ Basic Docker Commands (Beginner Level)

## 1. Check Docker Version

```bash
docker --version
```

Shows installed Docker version.

---

## 2. Pull an Image (Download from Docker Hub)

```bash
docker pull node
docker pull nginx
docker pull mongo
```

Downloads image from Docker Hub.

---

## 3. List Images

```bash
docker images
```

Shows all downloaded images.

---

## 4. Run a Container

```bash
docker run nginx
```

Runs nginx container.

Run in background:

```bash
docker run -d nginx
```

Run with custom name:

```bash
docker run -d --name my-nginx nginx
```

Run with port mapping:

```bash
docker run -d -p 3000:80 nginx
```

👉 Host Port 3000 → Container Port 80

---

## 5. List Running Containers

```bash
docker ps
```

Show all containers (including stopped):

```bash
docker ps -a
```

---

## 6. Stop a Container

```bash
docker stop container_id
```

---

## 7. Start a Container

```bash
docker start container_id
```

---

## 8. Restart a Container

```bash
docker restart container_id
```

---

## 9. Remove Container

```bash
docker rm container_id
```

Force remove:

```bash
docker rm -f container_id
```

---

## 10. Remove Image

```bash
docker rmi image_id
```

---

# 🔹 2️⃣ Intermediate Docker Commands

## 1. View Logs

```bash
docker logs container_id
```

Live logs:

```bash
docker logs -f container_id
```

---

## 2. Access Inside Container

```bash
docker exec -it container_id bash
```

Now you're inside container terminal.

---

## 3. Inspect Container Details

```bash
docker inspect container_id
```

---

## 4. Copy Files Between Host & Container

From host to container:

```bash
docker cp file.txt container_id:/app
```

From container to host:

```bash
docker cp container_id:/app/file.txt .
```

---

## 5. Docker Volumes (Important for MongoDB)

Create volume:

```bash
docker volume create myvolume
```

Run with volume:

```bash
docker run -d -v myvolume:/data/db mongo
```

List volumes:

```bash
docker volume ls
```

---

## 6. Docker Networks

List networks:

```bash
docker network ls
```

Create network:

```bash
docker network create mynetwork
```

Run containers in same network:

```bash
docker run -d --name app --network mynetwork node
docker run -d --name db --network mynetwork mongo
```

Now app can access db via hostname: `db`

---

# 🔹 3️⃣ Dockerfile (Build Your Own Image)

Example for Node.js project:

```Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 4000

CMD ["npm", "start"]
```

Build image:

```bash
docker build -t myapp .
```

Run image:

```bash
docker run -d -p 4000:4000 myapp
```

---

# 🔹 4️⃣ Advanced Docker Commands

## 1. Docker Compose (Multiple Containers)

Install docker-compose (if not installed).

Example `docker-compose.yml`:

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "4000:4000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

Run:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

---

## 2. Build with Specific Dockerfile

```bash
docker build -f Dockerfile.dev -t myapp-dev .
```

---

## 3. Prune (Clean System)

Remove stopped containers:

```bash
docker container prune
```

Remove unused images:

```bash
docker image prune
```

Remove everything unused:

```bash
docker system prune -a
```

---

## 4. Tag Image

```bash
docker tag myapp myusername/myapp:v1
```

---

## 5. Push to Docker Hub

```bash
docker login
docker push myusername/myapp:v1
```

---

## 6. Resource Limit (Production)

Limit CPU & memory:

```bash
docker run -d --memory="512m" --cpus="1.0" nginx
```

---

# 🔹 5️⃣ Real-World Production Flow (Node + Mongo + Nginx)

1️⃣ Create Dockerfile for Node app
2️⃣ Create docker-compose.yml
3️⃣ Build image
4️⃣ Run containers
5️⃣ Setup Nginx reverse proxy
6️⃣ Deploy on Ubuntu server

Example:

```bash
docker compose up -d --build
```

---

# 🔥 Most Important Commands for You (As Backend Developer)

Since you’re working with:

* Node.js
* MongoDB
* Ubuntu
* CI/CD

Focus on mastering:

* `docker build`
* `docker run -d -p`
* `docker exec -it`
* `docker logs -f`
* `docker volume`
* `docker compose up`
* `docker system prune`

---

If you want, I can next explain:

* 🐳 Complete production deployment using Docker on Ubuntu
* 🔁 CI/CD using Docker + GitHub Actions
* 🏗 Docker best practices for Node.js project
* 🧠 Interview questions on Docker

Tell me what you want next 🚀
