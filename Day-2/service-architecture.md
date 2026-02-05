# Service Architecture — Day 2

## Objective

Deploy a **multi-container application** using **Docker Compose** consisting of:

* React Client
* Node.js Server
* MongoDB Database

All services should start using a **single command**:

```bash
docker compose up -d
```

---

## Project Structure

```
WEEK_5/
└── Day-2/
    ├── client/
    │   ├── Dockerfile
    │   ├── package.json
    │   └── src/
    ├── server/
    │   ├── Dockerfile
    │   ├── package.json
    │   └── src/
    ├── docker-compose.yml
    └── service-architecture.md
```

📸 **Screenshot to add here:**

* Terminal showing `ls` inside `Day-2` directory

---

## Services Description

### 1. Client Service (React)

* Built using **Create React App**
* Runs in its own Docker container
* Uses Node.js image internally
* Exposed on **port 3000**

Access URL:

```
http://localhost:3000
```

📸 **Screenshot to add here:**

* Browser showing React app running on `localhost:3000`

---

### 2. Server Service (Node.js)

* Backend API built with Node.js
* Runs in a separate container
* Exposed on **port 5000**
* Connects to MongoDB using Docker internal networking

Server startup logs:

```
Server listening on port 5000
MongoDB connected
```

📸 **Screenshot to add here:**

* Output of `docker compose logs server`

---

### 3. Database Service (MongoDB)

* Uses official `mongo:6` Docker image
* Runs as an isolated service
* Internal port: **27017**
* Uses Docker **named volume** for persistence

Volume used:

```
mongo_data
```

📸 **Screenshot to add here:**

* Output of `docker volume ls`

---

## Docker Compose Networking

* Docker Compose creates a default **bridge network**
* All services are connected automatically
* Containers communicate using **service names**

Example:

```
Server → mongodb://mongo:27017
```

📸 **Screenshot to add here:**

* Output of `docker network ls`

---

## Architecture Flow

```
User Browser
     ↓
React Client (3000)
     ↓
Node Server (5000)
     ↓
MongoDB (27017)
```

---

## Logs & Debugging

Commands used to verify services:

```bash
docker compose ps
docker compose logs client
docker compose logs server
docker compose logs mongo
```

📸 **Screenshot to add here:**

* Output of `docker compose ps`

---

## Data Persistence

* MongoDB data is stored using a Docker named volume
* Data remains intact even after containers are stopped

Stop and remove containers:

```bash
docker compose down
```

Stop and remove containers + volumes:

```bash
docker compose down -v
```

📸 **Screenshot to add here:**

* Output of `docker volume ls` before and after `down -v`

---

## Final Verification Checklist

* ✅ React client running on port 3000
* ✅ Node server running on port 5000
* ✅ MongoDB connected successfully
* ✅ Logs accessible via Docker Compose
* ✅ Data persisted using volumes
* ✅ Single-command startup achieved

---

## Conclusion

This setup demonstrates a **production-style multi-container architecture** using Docker Compose. Each service is isolated, networked internally, and managed using a single orchestration file, fulfilling all Day-2 deliverables.
