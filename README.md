# 💼 Job Portal Backend API

A production-ready RESTful API built with Node.js, Express, and MongoDB. Features specific, role-based workflows for Job Seekers, Employers, and Admins organized into feature-scoped directories.

## 📁 Project Architecture
```text
job-portal-backend/
├── Models/
│   ├── job_applicant_model.js
│   ├── employer_model.js
│   └── user_model.js
├── Apis/
│   ├── job_seeker_api.js
│   ├── employer_api.js
│   └── admin_api.js
├── README.md
├── package.json
└── server.js
```

---

## 👥 Roles & Access Constraints

- **Job Seeker**: Access is strictly limited to application tracking. Can only **insert a new application** and **delete an application** by its database ID.
- **Employer**: Responsible for publishing jobs, viewing incoming applicant rosters, and changing application workflows.
- **Admin**: Holds global administrative control to audit system structures and wipe accounts or spam logs.

---

## 🚀 Complete API Routing Matrix

### 1. Job Seeker Endpoints (Strictly Restricted to 'seeker' Role)
- `POST /api/ja` — Insert a new job application.
  - **Payload Example (JSON Body):**
    ```json
    {
      "name": "Alex Mercer",
      "email": "alex@example.com",
      "company": "Tech Corp"
    }
    ```
- `DELETE /api/ja/:id` — Delete a specific job application permanently using its unique database tracking ID.

### 2. Employer Endpoints (Strictly Restricted to 'employer' Role)
- `POST /api/jobs` — Create a new job opening (Automatically maps `postedBy`).
- `GET /api/jobs/:id/applicants` — View seekers who have explicitly applied to their specific job.
- `PUT /api/applications/:id/status` — Change applicant status (`shortlisted` or `rejected`).

### 3. Admin Administration (Strictly Restricted to 'admin' Role)
- `GET /api/admin/users` — Fetch a comprehensive list of all users in the system database.
- `DELETE /api/admin/users/:id` — Completely wipe a user and their cascading data from the platform.

---

## ⚙️ How to Setup and Run Locally

1. **Clone or Download** this repository to your local computer.
2. Open your terminal in the project root folder and run the following command to restore dependencies (recreates your local `node_modules` folder):
   ```bash
   npm install
   ```
3. Create a local `.env` file in the root directory and add your connection variables:
   ```env
   PORT=5000
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_signing_secret
   ```
4. Start your development server with hot-reloading:
   ```bash
   npm run dev
   ```
