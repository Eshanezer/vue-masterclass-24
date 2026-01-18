# Vue 3 + Docker Setup

This project demonstrates a **standard Vue 3 (Vite) frontend-only setup using Docker**.

No backend, no database — just Vue running in a Docker container for a consistent development environment.

---

## 📦 Requirements

You need **only these installed on your machine**:

* **Docker** (Docker Desktop or Docker Engine)
* **Git**

> ❗ Node.js is **not required** to run the app with Docker, but **is required** if you want to create or manage the project locally.

---

## 📁 Project Structure

```text
vue-project/
├── Dockerfile
├── .dockerignore
├── package.json
├── package-lock.json
├── vite.config.js
├── index.html
├── src/
│   ├── assets/
│   ├── components/
│   ├── views/
│   ├── App.vue
│   └── main.js
└── README.md
```

---

## 🐳 Docker Setup

### Dockerfile

```dockerfile
FROM node:20.19-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5173
CMD ["npm", "run", "dev", "--", "--host"]
```

### .dockerignore

```text
node_modules
dist
.git
```

---

## ▶️ Run the Project with Docker

### 1️⃣ Build the Docker image

```bash
docker build -t vue-app .
```

### 2️⃣ Run the container

```bash
docker run -p 5173:5173 vue-app
```

> We map **host port 5174 → container port 5173** so multiple Vue apps can run at the same time.

### 3️⃣ Open in browser

```text
http://localhost:5174
```

---

## 🔁 Rebuilding After Changes

If you change:

* `package.json`
* `Dockerfile`

You must rebuild:

```bash
docker build --no-cache -t vue-app .
```

Then run again:

```bash
docker run -p 5174:5173 vue-app
```

---

## 🧠 Important Notes

* Vite **must** run with `--host` inside Docker
* `EXPOSE` does **not** change the port — it only documents it
* Docker port mapping decides which port you access on your machine

---

## 🛠 Common Commands

```bash
# List running containers
docker ps

# Stop all containers
docker stop $(docker ps -q)

# Remove all containers
docker rm $(docker ps -aq)

# View logs
docker logs <container-name>
```

---