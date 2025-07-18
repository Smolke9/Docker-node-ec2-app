# 📦 Dockerized Node.js App on EC2

This project demonstrates how to run a basic Node.js app in a Docker container on an AWS EC2 instance and access it through a browser.

## 📁 Project Structure

```
node-app/
├── app.js
├── package.json
├── Dockerfile
└── README.md
```

## ✅ Steps Summary

1. **Connect to EC2**
2. **Create Node app** (`app.js`, `package.json`, `Dockerfile`)
3. **Build Docker image**
4. **Run container on port 80:3000**
5. **Allow port 80 and 3000 in EC2 Security Group**
6. **Open `http://<ec2-ip>` in browser**

## 🔧 Step-by-Step Instructions

### ✅ Step 1: SSH into EC2 Instance

```bash
ssh -i "your-key.pem" ubuntu@<your-ec2-public-ip>
```

---

### ✅ Step 2: Create Project Directory

```bash
mkdir node-app && cd node-app
```

---

### ✅ Step 3: Create `app.js`

```bash
nano app.js
```

Paste this:

```js
const http = require('http');
const PORT = 3000;

const server = http.createServer((req, res) => {
  res.end('Hello from Node.js app in Docker on EC2!');
});

server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});
```

---

### ✅ Step 4: Create `package.json`

```bash
nano package.json
```

Paste:

```json
{
  "name": "node-app",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  }
}
```

---

### ✅ Step 5: Create `Dockerfile`

```bash
nano Dockerfile
```

Paste:

```Dockerfile
FROM node:14

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install
COPY . .

EXPOSE 3000
CMD [ "npm", "start" ]
```

---

### ✅ Step 6: Build Docker Image

```bash
docker build -t my-nodeapp .
```

📸 Screenshot:

![Docker Build](./1.jpg)

---

### ✅ Step 7: Run Docker Container

```bash
docker run -d -p 80:3000 my-nodeapp
```

Check status:

```bash
docker container ls
```


## 🖼️ Screenshots

### 🔧 Docker Build Output
![Build Output](./1.jpg)

### 🐳 Container Running Confirmation
![Container Running](./2.jpg)

### 🔓 EC2 Security Group Settings
![Security Group Settings](./3.jpg)

### 🔓 Docker Node Output On Browser 
![Output on Browser](./4.jpg)
