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

