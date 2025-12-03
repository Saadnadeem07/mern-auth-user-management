# 🔐 Authentication & Profile Management System

A full-stack user authentication and profile management application built with the MERN stack. This project demonstrates production-ready patterns for user authentication, authorization, file uploads, and CRUD operations.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node](https://img.shields.io/badge/node-%3E%3D14.0.0-brightgreen)
![MongoDB](https://img.shields.io/badge/MongoDB-4.4+-green)

## 🌟 Features

### Authentication & Security
- ✅ User registration with email validation
- ✅ Secure login with JWT tokens
- ✅ Password hashing using bcrypt
- ✅ Protected routes with middleware authentication
- ✅ Token-based authorization
- ✅ CORS configuration for cross-origin requests
- ✅ Input validation and sanitization

### Profile Management
- ✅ View user profile
- ✅ Update user details (name, email, bio)
- ✅ Upload and update profile pictures
- ✅ Image storage via Cloudinary
- ✅ Full CRUD operations on user data

### Technical Highlights
- ✅ RESTful API design
- ✅ Error handling middleware
- ✅ Environment variable configuration
- ✅ Modular architecture with separation of concerns
- ✅ MongoDB database with Mongoose ODM

## 🛠️ Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM for MongoDB
- **JWT** - Token-based authentication
- **Bcrypt** - Password hashing
- **Multer** - File upload handling
- **Cloudinary** - Image hosting and management
- **Cors** - Cross-origin resource sharing
- **Express-validator** - Input validation
- **Dotenv** - Environment variables

### Frontend
- **React.js** - UI library
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **Context API** - State management
- **Tailwind CSS** - Styling (or your choice)

## 📁 Project Structure

```
project-root/
├── backend/
│   ├── config/
│   │   ├── db.js                  # MongoDB connection
│   │   └── cloudinary.js          # Cloudinary configuration
│   ├── models/
│   │   └── User.js                # User schema/model
│   ├── controllers/
│   │   ├── authController.js      # Authentication logic
│   │   └── userController.js      # User CRUD operations
│   ├── middlewares/
│   │   ├── auth.js                # JWT verification middleware
│   │   ├── upload.js              # Multer configuration
│   │   └── errorHandler.js        # Global error handling
│   ├── routes/
│   │   ├── authRoutes.js          # Auth endpoints
│   │   └── userRoutes.js          # User endpoints
│   ├── utils/
│   │   └── validators.js          # Input validation functions
│   ├── .env                       # Environment variables
│   ├── server.js                  # Entry point
│   └── package.json
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Auth/
│   │   │   │   ├── Login.jsx
│   │   │   │   └── Signup.jsx
│   │   │   ├── Profile/
│   │   │   │   ├── ProfileView.jsx
│   │   │   │   └── ProfileEdit.jsx
│   │   │   └── Common/
│   │   │       ├── Navbar.jsx
│   │   │       └── PrivateRoute.jsx
│   │   ├── services/
│   │   │   └── api.js             # Axios configuration
│   │   ├── context/
│   │   │   └── AuthContext.jsx    # Authentication context
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
└── README.md
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (v4.4 or higher)
- npm or yarn
- Cloudinary account (for image uploads)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/auth-profile-system.git
cd auth-profile-system
```

2. **Backend Setup**
```bash
cd backend
npm install
```

3. **Frontend Setup**
```bash
cd frontend
npm install
```

### Environment Variables

Create a `.env` file in the `backend` directory:

```env
# Server
PORT=5000
NODE_ENV=development

# Database
MONGO_URI=mongodb://localhost:27017/auth-system
# Or use MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname

# JWT
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRE=7d

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Frontend URL (for CORS)
CLIENT_URL=http://localhost:5173
```

### Running the Application

1. **Start MongoDB** (if running locally)
```bash
mongod
```

2. **Start Backend Server**
```bash
cd backend
npm run dev
# Server runs on http://localhost:5000
```

3. **Start Frontend**
```bash
cd frontend
npm run dev
# App runs on http://localhost:5173
```

## 📡 API Endpoints

### Authentication Routes

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/auth/signup` | Register new user | No |
| POST | `/api/auth/login` | Login user | No |
| POST | `/api/auth/logout` | Logout user | Yes |

### User Routes

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/users/profile` | Get current user profile | Yes |
| PUT | `/api/users/profile` | Update user details | Yes |
| POST | `/api/users/upload` | Upload profile picture | Yes |
| DELETE | `/api/users/profile` | Delete user account | Yes |

### Example Request/Response

**Signup Request:**
```json
POST /api/auth/signup
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "60d5ec49f1b2c72b8c8e4f3a",
    "name": "John Doe",
    "email": "john@example.com",
    "profilePic": null
  }
}
```

## 🔒 Authentication Flow

1. User signs up → Password is hashed → User saved to DB
2. User logs in → Credentials verified → JWT token generated
3. Token stored in localStorage/cookies on frontend
4. Protected routes verify token via middleware
5. Token included in Authorization header for API requests

## 📸 Profile Picture Upload Flow

1. User selects image file
2. Frontend sends multipart/form-data request
3. Multer middleware processes file
4. File uploaded to Cloudinary
5. Cloudinary returns secure URL
6. URL saved to user document in MongoDB
7. Updated user data returned to frontend

## 🧪 Testing

### Using Postman/Thunder Client

1. Import the provided API collection (if available)
2. Set environment variables:
   - `base_url`: http://localhost:5000
   - `token`: (auto-populated after login)
3. Test each endpoint sequentially

### Manual Testing Steps

1. **Signup**: Create a new user
2. **Login**: Login with credentials, save the token
3. **Get Profile**: Use token to fetch profile (should succeed)
4. **Update Profile**: Update user details
5. **Upload Picture**: Upload a profile picture
6. **Logout**: Test logout functionality

## 🐛 Common Issues & Solutions

### CORS Errors
- Ensure `CLIENT_URL` in `.env` matches your frontend URL
- Check CORS configuration in `server.js`

### JWT Token Issues
- Verify `JWT_SECRET` is set in `.env`
- Check token format: `Bearer <token>`
- Ensure token is not expired

### Cloudinary Upload Fails
- Verify all Cloudinary credentials are correct
- Check file size limits (default: 5MB)
- Ensure file type is allowed (jpg, png, webp)

### MongoDB Connection Issues
- Ensure MongoDB is running
- Check connection string format
- Verify database name and credentials

## 🔐 Security Best Practices Implemented

- ✅ Passwords hashed with bcrypt (salt rounds: 10)
- ✅ JWT tokens with expiration
- ✅ Protected routes with auth middleware
- ✅ Input validation and sanitization
- ✅ CORS properly configured
- ✅ Environment variables for sensitive data
- ✅ Error messages don't leak sensitive info
- ✅ File upload restrictions (type, size)

## 🎯 Future Enhancements

- [ ] Email verification on signup
- [ ] Password reset functionality
- [ ] Two-factor authentication (2FA)
- [ ] Social login (Google, GitHub)
- [ ] Role-based access control (RBAC)
- [ ] Refresh token mechanism
- [ ] Rate limiting
- [ ] User activity logs
- [ ] Profile completion progress
- [ ] Dark mode toggle

## 📚 Learning Resources

This project covers:
- RESTful API design
- JWT authentication
- File uploads and cloud storage
- MongoDB CRUD operations
- React context API
- Protected routing
- Error handling patterns
- Middleware implementation

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your Name](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

## 🙏 Acknowledgments

- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Cloudinary Documentation](https://cloudinary.com/documentation)
- [JWT.io](https://jwt.io/)
- [React Documentation](https://react.dev/)

---

⭐ If you found this project helpful, please give it a star!

**Built with ❤️ for learning and portfolio purposes**# 🔐 Authentication & Profile Management System

A full-stack user authentication and profile management application built with the MERN stack. This project demonstrates production-ready patterns for user authentication, authorization, file uploads, and CRUD operations.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node](https://img.shields.io/badge/node-%3E%3D14.0.0-brightgreen)
![MongoDB](https://img.shields.io/badge/MongoDB-4.4+-green)

## 🌟 Features

### Authentication & Security
- ✅ User registration with email validation
- ✅ Secure login with JWT tokens
- ✅ Password hashing using bcrypt
- ✅ Protected routes with middleware authentication
- ✅ Token-based authorization
- ✅ CORS configuration for cross-origin requests
- ✅ Input validation and sanitization

### Profile Management
- ✅ View user profile
- ✅ Update user details (name, email, bio)
- ✅ Upload and update profile pictures
- ✅ Image storage via Cloudinary
- ✅ Full CRUD operations on user data

### Technical Highlights
- ✅ RESTful API design
- ✅ Error handling middleware
- ✅ Environment variable configuration
- ✅ Modular architecture with separation of concerns
- ✅ MongoDB database with Mongoose ODM

## 🛠️ Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM for MongoDB
- **JWT** - Token-based authentication
- **Bcrypt** - Password hashing
- **Multer** - File upload handling
- **Cloudinary** - Image hosting and management
- **Cors** - Cross-origin resource sharing
- **Express-validator** - Input validation
- **Dotenv** - Environment variables

### Frontend
- **React.js** - UI library
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **Context API** - State management
- **Tailwind CSS** - Styling (or your choice)

## 📁 Project Structure

```
project-root/
├── backend/
│   ├── config/
│   │   ├── db.js                  # MongoDB connection
│   │   └── cloudinary.js          # Cloudinary configuration
│   ├── models/
│   │   └── User.js                # User schema/model
│   ├── controllers/
│   │   ├── authController.js      # Authentication logic
│   │   └── userController.js      # User CRUD operations
│   ├── middlewares/
│   │   ├── auth.js                # JWT verification middleware
│   │   ├── upload.js              # Multer configuration
│   │   └── errorHandler.js        # Global error handling
│   ├── routes/
│   │   ├── authRoutes.js          # Auth endpoints
│   │   └── userRoutes.js          # User endpoints
│   ├── utils/
│   │   └── validators.js          # Input validation functions
│   ├── .env                       # Environment variables
│   ├── server.js                  # Entry point
│   └── package.json
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Auth/
│   │   │   │   ├── Login.jsx
│   │   │   │   └── Signup.jsx
│   │   │   ├── Profile/
│   │   │   │   ├── ProfileView.jsx
│   │   │   │   └── ProfileEdit.jsx
│   │   │   └── Common/
│   │   │       ├── Navbar.jsx
│   │   │       └── PrivateRoute.jsx
│   │   ├── services/
│   │   │   └── api.js             # Axios configuration
│   │   ├── context/
│   │   │   └── AuthContext.jsx    # Authentication context
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
└── README.md
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (v4.4 or higher)
- npm or yarn
- Cloudinary account (for image uploads)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/auth-profile-system.git
cd auth-profile-system
```

2. **Backend Setup**
```bash
cd backend
npm install
```

3. **Frontend Setup**
```bash
cd frontend
npm install
```

### Environment Variables

Create a `.env` file in the `backend` directory:

```env
# Server
PORT=5000
NODE_ENV=development

# Database
MONGO_URI=mongodb://localhost:27017/auth-system
# Or use MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname

# JWT
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRE=7d

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Frontend URL (for CORS)
CLIENT_URL=http://localhost:5173
```

### Running the Application

1. **Start MongoDB** (if running locally)
```bash
mongod
```

2. **Start Backend Server**
```bash
cd backend
npm run dev
# Server runs on http://localhost:5000
```

3. **Start Frontend**
```bash
cd frontend
npm run dev
# App runs on http://localhost:5173
```

## 📡 API Endpoints

### Authentication Routes

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/auth/signup` | Register new user | No |
| POST | `/api/auth/login` | Login user | No |
| POST | `/api/auth/logout` | Logout user | Yes |

### User Routes

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/users/profile` | Get current user profile | Yes |
| PUT | `/api/users/profile` | Update user details | Yes |
| POST | `/api/users/upload` | Upload profile picture | Yes |
| DELETE | `/api/users/profile` | Delete user account | Yes |

### Example Request/Response

**Signup Request:**
```json
POST /api/auth/signup
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "60d5ec49f1b2c72b8c8e4f3a",
    "name": "John Doe",
    "email": "john@example.com",
    "profilePic": null
  }
}
```

## 🔒 Authentication Flow

1. User signs up → Password is hashed → User saved to DB
2. User logs in → Credentials verified → JWT token generated
3. Token stored in localStorage/cookies on frontend
4. Protected routes verify token via middleware
5. Token included in Authorization header for API requests

## 📸 Profile Picture Upload Flow

1. User selects image file
2. Frontend sends multipart/form-data request
3. Multer middleware processes file
4. File uploaded to Cloudinary
5. Cloudinary returns secure URL
6. URL saved to user document in MongoDB
7. Updated user data returned to frontend

## 🧪 Testing

### Using Postman/Thunder Client

1. Import the provided API collection (if available)
2. Set environment variables:
   - `base_url`: http://localhost:5000
   - `token`: (auto-populated after login)
3. Test each endpoint sequentially

### Manual Testing Steps

1. **Signup**: Create a new user
2. **Login**: Login with credentials, save the token
3. **Get Profile**: Use token to fetch profile (should succeed)
4. **Update Profile**: Update user details
5. **Upload Picture**: Upload a profile picture
6. **Logout**: Test logout functionality

## 🐛 Common Issues & Solutions

### CORS Errors
- Ensure `CLIENT_URL` in `.env` matches your frontend URL
- Check CORS configuration in `server.js`

### JWT Token Issues
- Verify `JWT_SECRET` is set in `.env`
- Check token format: `Bearer <token>`
- Ensure token is not expired

### Cloudinary Upload Fails
- Verify all Cloudinary credentials are correct
- Check file size limits (default: 5MB)
- Ensure file type is allowed (jpg, png, webp)

### MongoDB Connection Issues
- Ensure MongoDB is running
- Check connection string format
- Verify database name and credentials

## 🔐 Security Best Practices Implemented

- ✅ Passwords hashed with bcrypt (salt rounds: 10)
- ✅ JWT tokens with expiration
- ✅ Protected routes with auth middleware
- ✅ Input validation and sanitization
- ✅ CORS properly configured
- ✅ Environment variables for sensitive data
- ✅ Error messages don't leak sensitive info
- ✅ File upload restrictions (type, size)

## 🎯 Future Enhancements

- [ ] Email verification on signup
- [ ] Password reset functionality
- [ ] Two-factor authentication (2FA)
- [ ] Social login (Google, GitHub)
- [ ] Role-based access control (RBAC)
- [ ] Refresh token mechanism
- [ ] Rate limiting
- [ ] User activity logs
- [ ] Profile completion progress
- [ ] Dark mode toggle

## 📚 Learning Resources

This project covers:
- RESTful API design
- JWT authentication
- File uploads and cloud storage
- MongoDB CRUD operations
- React context API
- Protected routing
- Error handling patterns
- Middleware implementation

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Your Name**
- GitHub: [@saadnadeem07](https://github.com/saadnadeem07)
- LinkedIn: [saadnadeem07](https://linkedin.com/in/saadnadeem07)
- Email: saadnadeem5509@gmail.com

## 🙏 Acknowledgments

- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Cloudinary Documentation](https://cloudinary.com/documentation)
- [JWT.io](https://jwt.io/)
- [React Documentation](https://react.dev/)

---

⭐ If you found this project helpful, please give it a star!

**Built with ❤️ for learning, professional use and portfolio purposes.**