# NutriPlan: Personalized Meal Management System

NutriPlan is a production-ready, full-stack application designed to streamline meal planning through data-driven personalization. Rather than relying on static templates, the system implements a **weighted heuristic feedback loop** that adapts to a user's unique dietary profile and taste preferences over time.

## 🧠 Core Personalization Logic
The project uses a transparent, **tag-based scoring engine** rather than a "black-box" AI approach:

* [cite_start]**Heuristic Scoring**: User interactions (Like/Dislike/Reject) trigger real-time updates to a weighted preference matrix[cite: 11, 46].
* **Weighted Tags**: Meals are categorized by metadata tags (e.g., "Keto," "High-Protein"). [cite_start]When a user interacts with a meal, the system adjusts the scores of those specific tags within the user's MongoDB profile[cite: 11, 46].
* [cite_start]**Adaptive Generation**: The 7-day plan generator prioritizes meals with the highest cumulative tag scores, ensuring the system "learns" taste patterns without the overhead of external ML models[cite: 46].



## 🚀 Engineering Highlights: Bypassing Port Restrictions
[cite_start]A major technical milestone was resolving persistent **`ETIMEDOUT` errors** during production deployment on Render[cite: 48].

* [cite_start]**The Problem**: Standard cloud environments (Render, Railway) often block outbound traffic on SMTP ports (587/465) to prevent spam[cite: 12, 48].
* [cite_start]**The Solution**: Migrated the entire email infrastructure from `nodemailer` (SMTP) to the **Brevo (formerly Sendinblue) RESTful HTTP API**[cite: 12, 48].
* [cite_start]**Outcome**: By utilizing Port 443 (Standard HTTPS), the system achieved **100% email delivery reliability** for password recovery and OTP flows[cite: 12, 48].



## 🛠️ Tech Stack
* **Frontend**: React.js (Vite)
* **Backend**: Node.js, Express.js
* [cite_start]**Database**: MongoDB Atlas (Mongoose ODM) [cite: 13, 49, 62]
* [cite_start]**Authentication**: JSON Web Tokens (JWT) & bcryptjs [cite: 10, 49]
* [cite_start]**Email Service**: Brevo HTTP API v3 [cite: 12, 48]
* [cite_start]**Deployment**: Render (Backend) & Vercel (Frontend) [cite: 13, 62]

## 🔌 API Reference

### Authentication
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/auth/signup` | Register new user & initialize tag matrix. |
| `POST` | `/api/auth/login` | Authenticate and receive JWT. |
| `POST` | `/api/auth/forgot-password`| [cite_start]Trigger Brevo API to send recovery OTP[cite: 12]. |

### User & Planning
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/generate-plan` | [cite_start]Generate a 7-day plan based on heuristic weights[cite: 9]. |
| `POST` | `/api/user/feedback` | [cite_start]Update tag scores based on Like/Dislike actions[cite: 11]. |

## 📦 Installation & Configuration

1. **Clone the repository**:
   ```bash
   git clone [https://github.com/sanchita-88/NutriPlan.git](https://github.com/sanchita-88/NutriPlan.git)
   cd NutriPlan

```

2. **Install dependencies**:
```bash
npm install

```


3. **Configure Environment Variables**:
Create a `.env` file in the root directory:
```env
PORT=3000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
BREVO_API_KEY=your_v3_api_key_here
EMAIL_USER=your_verified_sender_email

```


4. **Run the application**:
```bash
# Development mode
npm run dev

# Production mode
npm start

```



## 🛡️ License

Distributed under the MIT License. See `LICENSE` for more information.

```

Would you like me to help you create a **"Technical Challenges"** log to add to this README, specifically documenting how you debugged the SMTP issue?

```
