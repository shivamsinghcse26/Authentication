# Authentication API

A comprehensive Express.js-based authentication system with JWT tokens, email verification, and OTP support.

## Features

- **User Registration & Login** - Secure user account creation and authentication
- **JWT Authentication** - Token-based authentication with refresh token support
- **Email Verification** - Email-based account verification using OTP
- **Session Management** - Multi-session support with logout capabilities
- **OTP Generation** - Time-based one-time passwords for email verification
- **Secure Password Handling** - Industry-standard password security practices
- **Cookie-based Sessions** - Secure session management with HTTP-only cookies

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose
- **Authentication**: JWT (JSON Web Tokens)
- **Email Service**: Nodemailer
- **Middleware**: Morgan (logging), Cookie-parser
- **Environment**: Dotenv for configuration

## Project Structure

```
├── server.js                 # Entry point
├── package.json             # Dependencies and scripts
├── src/
│   ├── app.js              # Express app configuration
│   ├── config/
│   │   ├── config.js       # Application configuration
│   │   └── database.js     # MongoDB connection setup
│   ├── controller/
│   │   └── authController.js   # Authentication logic
│   ├── models/
│   │   ├── userModel.js    # User schema
│   │   ├── otp.model.js    # OTP schema
│   │   └── SessionModel.js # Session schema
│   ├── routes/
│   │   └── authRoutes.js   # Authentication routes
│   ├── services/
│   │   └── email.service.js    # Email sending service
│   └── utils/
│       └── util.js         # Utility functions
└── controller/
    └── authController.js   # (Duplicate - consider removing)
```

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd AUTHENTICATION
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file with required environment variables:
```env
# Database
MONGODB_URI=mongodb://localhost:27017/authentication

# JWT
JWT_SECRET=your_jwt_secret_key
JWT_REFRESH_SECRET=your_refresh_token_secret

# Email Service
EMAIL_SERVICE=gmail
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password

# Server
PORT=3000
NODE_ENV=development
```

4. Start the server:
```bash
npm start
```

The server will run on `http://localhost:3000`

## API Endpoints

### Authentication Routes (`/api/auth`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/register` | Register a new user |
| POST | `/login` | Login with email and password |
| GET | `/verify-email` | Verify email with OTP |
| GET | `/get-me` | Get current user details |
| GET | `/refresh-token` | Refresh JWT token |
| GET | `/logout` | Logout from current session |
| GET | `/logout-all` | Logout from all sessions |

### Register
```bash
POST /api/auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123",
  "name": "John Doe"
}
```

### Login
```bash
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

### Get Current User
```bash
GET /api/auth/get-me
Authorization: Bearer <jwt_token>
```

### Refresh Token
```bash
GET /api/auth/refresh-token
Cookie: refreshToken=<refresh_token>
```

### Logout
```bash
GET /api/auth/logout
Authorization: Bearer <jwt_token>
```

### Logout All Sessions
```bash
GET /api/auth/logout-all
Authorization: Bearer <jwt_token>
```

### Verify Email
```bash
GET /api/auth/verify-email?otp=123456&email=user@example.com
```

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `MONGODB_URI` | MongoDB connection string | `mongodb://localhost:27017/auth` |
| `JWT_SECRET` | Secret key for JWT signing | `your_secret_key` |
| `JWT_REFRESH_SECRET` | Secret key for refresh tokens | `your_refresh_secret` |
| `EMAIL_SERVICE` | Email service provider | `gmail` |
| `EMAIL_USER` | Email account username | `your_email@gmail.com` |
| `EMAIL_PASSWORD` | Email account password/app password | `your_app_password` |
| `PORT` | Server port | `3000` |
| `NODE_ENV` | Environment | `development` |

## Database Models

### User Model
- Email (unique)
- Password (hashed)
- Name
- Email verification status
- Created and updated timestamps

### OTP Model
- Email
- OTP code
- Expiration time
- Status (used/unused)

### Session Model
- User ID
- Refresh token
- Device information
- Created and updated timestamps

## Security Features

- ✅ Password hashing
- ✅ JWT token-based authentication
- ✅ Refresh token rotation
- ✅ Email verification with OTP
- ✅ Session management
- ✅ HTTP-only secure cookies
- ✅ CORS and CSRF protection ready

## Development

### Scripts

```bash
# Start development server
npm start

# Run tests (not yet configured)
npm test
```

### Dependencies

- **express**: Web framework
- **mongoose**: MongoDB ODM
- **jsonwebtoken**: JWT handling
- **nodemailer**: Email service
- **morgan**: HTTP request logger
- **cookie-parser**: Cookie parsing middleware
- **dotenv**: Environment variable management

## Author

Shivam Kumar Singh

## License

ISC

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Submit a pull request

## Troubleshooting

### MongoDB Connection Issues
- Ensure MongoDB service is running
- Check connection string in `.env`
- Verify network connectivity

### Email Verification Not Sending
- Check email credentials in `.env`
- Enable "Less secure app access" (if using Gmail)
- Use app-specific password for Gmail

### JWT Token Errors
- Verify JWT_SECRET is set in `.env`
- Check token expiration
- Ensure token format is correct in Authorization header

## Support

For issues and questions, please create an issue in the repository.

---

**Last Updated**: April 2026
