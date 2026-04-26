# Freelance-CONNECT

A full stack freelance marketplace built with the **MERN stack**, where buyers can browse gigs, hire sellers, and manage service requests — all in one place.

---

## Demo Video [Live Demo](https://drive.google.com/file/d/1wkePrZ4b4S8Afvm9qW2IILrV44NBkwv5/view?usp=sharing](https://drive.google.com/file/d/1wkePrZ4b4S8Afvm9qW2IILrV44NBkwv5/view?usp=sharing))
## Code Explaination Video  [Live Demo](https://drive.google.com/file/d/1xtXMcaOcMV8n8dmRZ1sxPiiG-0G28PiM/view?usp=sharing)

## 📸 Features

- 🔐 **JWT Authentication** — Signup & Login with bcrypt password hashing
- 👤 **Role-Based Access** — Users can register as a Buyer, Seller, or Both
- 📋 **Gig Management** — Sellers can create, update, and delete their gigs
- 🖼️ **Image Uploads** — Thumbnail image upload for gigs using Multer
- 🔍 **Search** — Search gigs by keyword (title or description)
- 📬 **Request Lifecycle** — Buyers send requests; sellers accept/reject/complete; buyers confirm delivery
- 👤 **Profile Management** — Users can update their name and email
- 🛡️ **Protected Routes** — Private pages accessible only to authenticated users

---

## 🛠️ Tech Stack

### Backend
| Package | Version | Purpose |
|---|---|---|
| Express | ^5.2.1 | Web framework |
| Mongoose | ^9.5.0 | MongoDB ODM |
| bcrypt | ^6.0.0 | Password hashing |
| jsonwebtoken | ^9.0.3 | JWT authentication |
| multer | ^2.1.1 | File uploads |
| cors | ^2.8.6 | Cross-origin requests |
| dotenv | ^17.4.2 | Environment variables |

### Frontend
| Package | Version | Purpose |
|---|---|---|
| React | ^19.2.5 | UI library |
| React Router DOM | ^7.14.2 | Client-side routing |
| Axios | ^1.15.2 | HTTP requests |
| Tailwind CSS | ^4.2.4 | Styling |
| Lucide React | ^1.11.0 | Icons |
| Vite | ^8.0.10 | Build tool |

---

## 📁 Project Structure

```
freelance-connect/
├── backend/
│   ├── middleware/
│   │   ├── auth.js          # JWT verification middleware
│   │   └── upload.js        # Multer file upload config
│   ├── models/
│   │   ├── User.js          # User schema (buyer/seller/both)
│   │   ├── Gig.js           # Gig schema
│   │   └── Request.js       # Request schema with status lifecycle
│   ├── routes/
│   │   ├── auth.js          # POST /signup, POST /login
│   │   ├── gigs.js          # Full CRUD for gigs
│   │   ├── requests.js      # Request lifecycle routes
│   │   └── users.js         # GET & PUT profile
│   ├── uploads/             # Uploaded gig images (auto-created)
│   ├── .env                 # Environment variables
│   └── server.js            # Express app entry point
│
└── frontend/
    └── src/
        ├── components/
        │   ├── Navbar.jsx
        │   ├── GigCard.jsx
        │   └── RequestCard.jsx
        ├── context/
        │   └── AuthContext.jsx  # Global auth state + Axios instance
        ├── pages/
        │   ├── Home.jsx
        │   ├── Login.jsx
        │   ├── Signup.jsx
        │   ├── Dashboard.jsx
        │   ├── GigDetails.jsx
        │   ├── CreateGig.jsx
        │   ├── MyGigs.jsx
        │   └── Profile.jsx
        └── App.jsx
```

---

## ⚙️ Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v18+)
- [MongoDB](https://www.mongodb.com/) running locally

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/freelance-connect.git
cd freelance-connect
```

---

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file inside the `backend/` folder:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/freelance-connect
JWT_SECRET=your_jwt_secret_here
```

Start the backend server:

```bash
npm run dev
```

The API will be running at `http://localhost:5000`

---

### 3. Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend will be running at `http://localhost:5173` (Vite's default port)

---

## 🔗 API Endpoints

### Auth
| Method | Endpoint | Access | Description |
|---|---|---|---|
| POST | `/api/auth/signup` | Public | Register a new user |
| POST | `/api/auth/login` | Public | Login and get JWT token |

### Gigs
| Method | Endpoint | Access | Description |
|---|---|---|---|
| GET | `/api/gigs` | Public | Get all gigs (supports `?keyword=`) |
| GET | `/api/gigs/:id` | Public | Get a single gig by ID |
| POST | `/api/gigs` | Private | Create a new gig (with image) |
| PUT | `/api/gigs/:id` | Private | Update your gig |
| DELETE | `/api/gigs/:id` | Private | Delete your gig |
| GET | `/api/gigs/user/me` | Private | Get your own gigs |

### Requests
| Method | Endpoint | Access | Description |
|---|---|---|---|
| POST | `/api/requests` | Private | Send a service request |
| GET | `/api/requests/sent` | Private | Get requests sent (buyer view) |
| GET | `/api/requests/received` | Private | Get requests received (seller view) |
| PUT | `/api/requests/:id/accept` | Private | Accept a request (seller) |
| PUT | `/api/requests/:id/reject` | Private | Reject a request (seller) |
| PUT | `/api/requests/:id/complete` | Private | Mark as completed (seller) |
| PUT | `/api/requests/:id/confirm` | Private | Confirm delivery (buyer) |

### Users
| Method | Endpoint | Access | Description |
|---|---|---|---|
| GET | `/api/users/profile` | Private | Get your profile |
| PUT | `/api/users/profile` | Private | Update your profile |

---

## 🔄 Request Status Lifecycle

```
pending → accepted → completed → confirmed
       ↘ rejected
```

- **Buyer** sends a request → status: `pending`
- **Seller** accepts or rejects → status: `accepted` or `rejected`
- **Seller** marks work done → status: `completed`
- **Buyer** confirms delivery → status: `confirmed`

---

## 🔐 Environment Variables

| Variable | Description | Example |
|---|---|---|
| `PORT` | Port for the backend server | `5000` |
| `MONGODB_URI` | MongoDB connection string | `mongodb://localhost:27017/freelance-connect` |
| `JWT_SECRET` | Secret key for signing JWT tokens | `your_secret_key` |

> ⚠️ Never commit your `.env` file to GitHub. Add it to `.gitignore`.

---

## 📌 Recommended .gitignore

```
node_modules/
.env
backend/uploads/
dist/
```

---
