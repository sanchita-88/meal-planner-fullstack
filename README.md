# NutriPlan: Personalized Meal Management System

NutriPlan is a full-stack web application designed for dynamic meal planning and user preference adaptation. Unlike static planners, NutriPlan implements a **weighted heuristic feedback loop** that "learns" user tastes through interaction, providing a personalized experience without the overhead of heavy machine learning models.

## 🧠 Core Personalization Logic

The system uses a transparent **Tag-Based Heuristic Scoring Engine** to refine recommendations:

* 
**Preference Matrix**: Every user profile contains a `tagScores` object in MongoDB.


* 
**Feedback Loop**: User actions—**Like**, **Dislike**, or **Reject**—trigger real-time updates to these scores (e.g., +2 for a Like, -2 for a Dislike).


* 
**Adaptive Generation**: The 7-day meal plan generator prioritizes meals by cross-referencing meal metadata tags against the user's highest-weighted scores in the database.



## 🚀 Engineering Highlights: Bypassing Port Restrictions

A major technical milestone of this project was resolving persistent **`ETIMEDOUT` errors** during production deployment on Render.

* **The Problem**: Standard cloud environments often block outbound traffic on SMTP ports (587/465) to prevent spam.
* 
**The Solution**: Migrated the entire email infrastructure from `nodemailer` (SMTP) to the **Brevo (formerly Sendinblue) RESTful HTTP API**.


* 
**Outcome**: By utilizing Port 443 (Standard HTTPS), the system achieved **100% email delivery reliability** for password recovery and OTP flows.



## 🛠️ Tech Stack

* 
**Frontend**: React.js (Vite) 


* 
**Backend**: Node.js, Express.js 


* 
**Database**: MongoDB Atlas (Mongoose ODM) 


* 
**Authentication**: JSON Web Tokens (JWT) & bcryptjs 


* 
**Email Service**: Brevo HTTP API v3 


* 
**Deployment**: Render (Backend) & Vercel (Frontend) 



## 🔌 API Reference

### Authentication

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/api/auth/signup` | Register new user & initialize tag matrix.

 |
| `POST` | `/api/auth/login` | Authenticate and receive JWT.

 |
| `POST` | `/api/auth/forgot-password` | Trigger Brevo API to send recovery OTP.

 |

### User & Planning

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api/generate-plan` | Generate a plan based on heuristic weights.

 |
| `POST` | `/api/user/feedback` | Update tag scores based on Like/Dislike.

 |

## 🛡️ Security & Reliability

* 
**CORS Management**: Configured environment-specific headers to allow secure communication between the Vercel frontend and Render backend.


* 
**Password Hashing**: Utilizes `bcryptjs` for salt-and-hash encryption before database storage.


* 
**Route Protection**: Implemented a custom JWT middleware to verify sessions before accessing planning logic.



## 📦 Environment Setup

To run this project locally, create a `.env` file in the root directory:

```env
PORT=3000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
BREVO_API_KEY=your_v3_api_key_here
EMAIL_USER=your_verified_sender_email

```

---

**Would you like me to add a "Technical Challenges" section detailing the specific code changes used for the Brevo API migration?**
