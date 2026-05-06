# ☁️ Cloud-Based Student Record Management System

A full-stack **MERN** (MongoDB, Express, React, Node.js) web application to store and manage student records, built for easy deployment on **AWS EC2**.

## Features

- **CRUD Operations** — Add, View, Update, and Delete student records
- **Search & Filter** — Search by name/roll/email, filter by department and year
- **Dashboard** — Stats overview with department breakdown and recent students
- **Responsive UI** — Works on desktop, tablet, and mobile
- **Production Ready** — Backend serves React build in production (single port deployment)

## Tech Stack

| Layer     | Technology                  |
|-----------|-----------------------------|
| Frontend  | React 19 + Vite             |
| Backend   | Node.js + Express           |
| Database  | MongoDB + Mongoose          |
| Styling   | Vanilla CSS (Dark Theme)    |

## Project Structure

```
student-records/
├── backend/
│   ├── config/db.js          # MongoDB connection
│   ├── controllers/          # Request handlers
│   ├── models/Student.js     # Mongoose schema
│   ├── routes/               # API routes
│   ├── seeder.js             # Sample data seeder
│   ├── server.js             # Express server
│   └── .env                  # Environment variables
├── frontend/
│   ├── src/
│   │   ├── components/       # Navbar, Toast, Modal
│   │   ├── pages/            # Dashboard, StudentList, StudentForm, StudentDetail
│   │   ├── api.js            # Axios API service
│   │   └── index.css         # Global styles
│   └── vite.config.js        # Vite config with proxy
└── README.md
```

## Local Development

### Prerequisites
- Node.js 18+
- MongoDB running locally (or MongoDB Atlas URI)

### 1. Backend Setup
```bash
cd backend
npm install
npm run dev
```
Backend runs on `http://localhost:5000`

### 2. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```
Frontend runs on `http://localhost:5173` (proxies API calls to port 5000)

### 3. Seed Sample Data (Optional)
```bash
cd backend
npm run seed
```

## API Endpoints

| Method | Endpoint             | Description                |
|--------|----------------------|----------------------------|
| GET    | /api/students        | Get all students (+ search/filter) |
| GET    | /api/students/:id    | Get single student         |
| POST   | /api/students        | Create new student         |
| PUT    | /api/students/:id    | Update student             |
| DELETE | /api/students/:id    | Delete student             |
| GET    | /api/students/stats  | Get aggregated statistics  |
| GET    | /api/health          | Health check               |

---

## 🚀 AWS EC2 Deployment Guide

### Step 1: Launch EC2 Instance
- AMI: Ubuntu 22.04 LTS
- Instance Type: t2.micro (free tier)
- Security Group: Allow **HTTP (80)**, **HTTPS (443)**, **SSH (22)**, and **Custom TCP 5000**

### Step 2: SSH into EC2
```bash
ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

### Step 3: Install Node.js & MongoDB
```bash
# Node.js 18
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# MongoDB
sudo apt-get install -y gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
sudo systemctl enable mongod
```

### Step 4: Clone & Setup Project
```bash
git clone <YOUR_REPO_URL> student-records
cd student-records

# Backend
cd backend
npm install
# Edit .env file
nano .env
```

Set in `.env`:
```
NODE_ENV=production
PORT=5000
MONGO_URI=mongodb://localhost:27017/student_records
```

### Step 5: Build Frontend
```bash
cd ../frontend
npm install
npm run build
```

### Step 6: Seed Data (Optional)
```bash
cd ../backend
npm run seed
```

### Step 7: Run with PM2
```bash
sudo npm install -g pm2
cd ~/student-records/backend
pm2 start server.js --name student-records
pm2 save
pm2 startup
```

### Step 8: Access the App
Open `http://<EC2_PUBLIC_IP>:5000` in your browser.

---

## Environment Variables

| Variable    | Description                    | Default                                      |
|-------------|--------------------------------|----------------------------------------------|
| NODE_ENV    | Environment mode               | development                                  |
| PORT        | Server port                    | 5000                                         |
| MONGO_URI   | MongoDB connection string      | mongodb://localhost:27017/student_records     |
