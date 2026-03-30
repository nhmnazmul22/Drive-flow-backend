<div align="center">

# 🚗 Drive Flow — Backend API

**A robust and secure RESTful API for a car rental platform**

[![Node.js](https://img.shields.io/badge/Node.js-v18+-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-v4-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-v6+-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/License-ISC-blue?style=for-the-badge)](LICENSE)

---

*Drive Flow connects car owners (hosts) with renters (users) through a seamless platform — managed by a powerful admin dashboard.*

</div>

---

## 📖 Summary

**Drive Flow** is a full-featured car rental backend built with **Node.js**, **Express**, and **MongoDB**. It implements a **three-role architecture** — **User**, **Host**, and **Admin** — each with dedicated routes, controllers, and services.

### ✨ Key Highlights

- 🔐 **JWT Authentication** with cookie-based sessions for all three roles
- 📧 **Email Verification** via OTP on signup (powered by Nodemailer)
- 🛡️ **Production-grade Security** — Helmet, XSS protection, HPP, MongoDB sanitization, rate limiting
- 🚘 **Car Management** — Hosts can list, update, and remove cars
- 📝 **Booking & Request System** — Users can book or request cars; hosts accept/reject
- ⭐ **Review System** — Car reviews with ratings
- 📰 **Blog System** — Hosts create blogs; users read them
- 🏷️ **Admin CMS** — Full CRUD for brands, types, services, testimonials, users, and hosts

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Runtime** | Node.js (ES Modules) |
| **Framework** | Express.js v4 |
| **Database** | MongoDB + Mongoose ODM |
| **Authentication** | JSON Web Tokens (JWT) + bcrypt |
| **Email** | Nodemailer |
| **File Upload** | Multer |
| **Security** | Helmet, CORS, express-rate-limit, hpp, xss-clean, express-mongo-sanitize |
| **Dev Tools** | Nodemon, Morgan (HTTP logger), dotenv |

---

## 📁 Folder Structure

```
Drive-flow-backend/
├── app.js                        # Entry point — Express app, middleware & DB connection
├── package.json
├── .env                          # Environment variables (not committed)
├── .gitignore
│
├── routes/
│   ├── user.js                   # User-facing public & protected routes
│   ├── host.js                   # Host (car owner) routes
│   └── admin.js                  # Admin management routes
│
└── src/
    ├── controller/
    │   ├── UserController.js     # User auth & profile handlers
    │   ├── HostController.js     # Host auth & profile handlers
    │   ├── CarController.js      # Car CRUD, booking, requests, reviews
    │   ├── BlogController.js     # Blog CRUD handlers
    │   ├── BrandController.js    # Read brands (public)
    │   ├── TypeController.js     # Read types (public)
    │   ├── ServiceController.js  # Read services (public)
    │   ├── TestimonialController.js
    │   └── adminController/      # Admin-specific controllers
    │       ├── AdminController.js
    │       ├── UserController.js
    │       ├── HostController.js
    │       ├── BlogController.js
    │       ├── BrandController.js
    │       ├── TypeController.js
    │       ├── ServiceController.js
    │       └── TestimonialController.js
    │
    ├── model/
    │   ├── UsersModel.js         # User schema
    │   ├── HostsModel.js         # Host schema
    │   ├── AdminsModel.js        # Admin schema
    │   ├── CarsModel.js          # Car listing schema
    │   ├── BookedCarsModel.js    # Booked cars records
    │   ├── RequestCarsModel.js   # Car rental requests
    │   ├── CarReviewsModel.js    # Car reviews & ratings
    │   ├── HostReviewsModel.js   # Host reviews
    │   ├── BlogsModel.js         # Blog posts
    │   ├── BrandsModel.js        # Car brands
    │   ├── TypesModel.js         # Car types / categories
    │   ├── ServicesModel.js      # Platform services
    │   └── TestimonialsModel.js  # User testimonials
    │
    ├── services/
    │   ├── UserServices.js       # User business logic
    │   ├── HostServices.js       # Host business logic
    │   ├── CarServices.js        # Car, booking & review logic
    │   ├── BlogServices.js       # Blog business logic
    │   ├── BrandServices.js
    │   ├── TypeServices.js
    │   ├── ServicesService.js
    │   ├── TestimonialServices.js
    │   └── adminServices/        # Admin-specific business logic
    │       ├── AdminServices.js
    │       ├── UserServices.js
    │       ├── HostServices.js
    │       ├── BlogServices.js
    │       ├── BrandServices.js
    │       ├── TypeServices.js
    │       ├── ServicesService.js
    │       └── TestimonialServices.js
    │
    ├── middleware/
    │   └── AuthMiddleware.js     # JWT verification (User, Host, Admin)
    │
    └── utility/
        ├── TokenUtility.js       # JWT token generation & encoding
        ├── Validation.js         # Input validation helpers
        ├── VerifyEmail.js        # OTP email sender via Nodemailer
        └── commonUtility.js      # Shared helper functions
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** v18 or higher → [Download](https://nodejs.org/)
- **MongoDB** (local or [Atlas](https://www.mongodb.com/atlas)) running instance
- **Git** → [Download](https://git-scm.com/)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/nhmnazmul22/Drive-flow-backend.git

# 2. Navigate into the project
cd Drive-flow-backend

# 3. Install dependencies
npm install

# 4. Create your environment file
cp .env.example .env   # or create .env manually (see below)

# 5. Start the development server
npm start
```

The server will start at `http://localhost:5080` (or your configured `PORT`).

---

## ⚙️ Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Server
PORT=5080

# Database
DATABASE_URI=mongodb://localhost:27017/drive-flow

# Client
CLIENT_URL=http://localhost:3000

# JWT Secret
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRATION=24h

# Rate Limiting
REQUEST_TIME=15 * 60 * 1000
REQUEST_LIMIT=100

# Body Parser
MAX_JSON_FILE=50mb

# Email (Nodemailer)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
```

---

## 📡 API Endpoints

### 👤 User Routes (`/`)

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/signupUser` | ✗ | Register a new user |
| `POST` | `/verifyUser/:email` | ✗ | Verify user email via OTP |
| `POST` | `/loginUser` | ✗ | Login and receive JWT cookie |
| `GET` | `/readUser` | ✓ | Get authenticated user profile |
| `POST` | `/updateUser` | ✓ | Update user profile |
| `POST` | `/logoutUser` | ✓ | Logout and clear session |
| `DELETE` | `/removeUser` | ✓ | Delete user account |
| `GET` | `/readCars` | ✗ | Browse all available cars |
| `GET` | `/readCar/:carID` | ✗ | View car details |
| `POST` | `/bookCar/:carID` | ✓ | Book a car |
| `POST` | `/requestCar/:carID` | ✓ | Request to rent a car |
| `GET` | `/getBookedCars` | ✓ | Get user's booked cars |
| `GET` | `/getRequestedCars` | ✓ | Get user's requested cars |
| `POST` | `/setCarReviews/:carID` | ✓ | Submit a car review |
| `GET` | `/getCarReviews/:carID` | ✓ | Get reviews for a car |

### 🏠 Host Routes (`/host`)

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/signupHost` | ✗ | Register as a host |
| `POST` | `/verifyHost/:email` | ✗ | Verify host email |
| `POST` | `/loginHost` | ✗ | Host login |
| `GET` | `/readHost` | ✓ | Get host profile |
| `POST` | `/updateHost` | ✓ | Update host profile |
| `POST` | `/logoutHost` | ✓ | Host logout |
| `DELETE` | `/removeHost` | ✓ | Delete host account |
| `POST` | `/createCar` | ✓ | List a new car |
| `POST` | `/updateCar/:carID` | ✓ | Update car listing |
| `GET` | `/readHosterCars` | ✓ | Get host's cars |
| `DELETE` | `/deleteCar/:carID` | ✓ | Remove a car listing |
| `POST` | `/acceptRequest/:carRequestID` | ✓ | Accept a rental request |
| `POST` | `/rejectRequest/:carRequestID` | ✓ | Reject a rental request |
| `POST` | `/createBlog` | ✓ | Write a blog post |
| `POST` | `/updateBlog/:blogID` | ✓ | Edit a blog post |
| `DELETE` | `/removeBlog/:blogID` | ✓ | Delete a blog post |

### 🔑 Admin Routes (`/admin`)

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/signupAdmin` | ✗ | Register admin |
| `POST` | `/loginAdmin` | ✗ | Admin login |
| `GET` | `/readAdmin` | ✓ | Get admin profile |
| `GET` | `/readUsers` | ✓ | List all users |
| `DELETE` | `/removeUser/:userID` | ✓ | Remove a user |
| `GET` | `/readHosts` | ✓ | List all hosts |
| `DELETE` | `/removeHost/:hostID` | ✓ | Remove a host |
| `POST` | `/createBrand` | ✓ | Add car brand |
| `POST` | `/createType` | ✓ | Add car type |
| `POST` | `/createServices` | ✓ | Add platform service |
| `POST` | `/createTestimonial` | ✓ | Add testimonial |

> 📌 *Admin routes also include full CRUD (read, update, delete) for brands, types, services, testimonials, and blogs.*

---

## 🔒 Security Features

| Feature | Package | Purpose |
|---------|---------|---------|
| **Helmet** | `helmet` | Sets secure HTTP headers |
| **CORS** | `cors` | Restricts cross-origin requests |
| **Rate Limiting** | `express-rate-limit` | Prevents brute-force attacks |
| **XSS Protection** | `xss-clean` | Sanitizes user input against XSS |
| **HPP Protection** | `hpp` | Prevents HTTP parameter pollution |
| **NoSQL Injection** | `express-mongo-sanitize` | Sanitizes MongoDB query operators |
| **Password Hashing** | `bcrypt` | Hashes passwords with salt rounds |

---

## 📄 License

This project is licensed under the **ISC License**.

---

<div align="center">

**Built with ❤️ by [Nhm Nazmul](https://github.com/nhmnazmul22)**

</div>
