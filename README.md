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
├── server.js                      # Entry point
├── package.json                   # Dependencies and scripts
├── README.md                      # Project documentation
├── .env                           # Environment variables (not tracked)
└── src/
    ├── app.js                     # Express app configuration
    ├── config/
    │   ├── config.js             # Application configuration
    │   └── database.js           # MongoDB connection setup
    ├── controller/
    │   └── authController.js     # Authentication business logic
    ├── models/
    │   ├── userModel.js          # User schema and model
    │   ├── otp.model.js          # OTP schema and model
    │   └── SessionModel.js       # Session schema and model
    ├── routes/
    │   └── authRoutes.js         # Authentication API routes
    ├── services/
    │   └── email.service.js      # Email sending service (Nodemailer)
    └── utils/
        └── util.js               # Utility helper functions
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

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---|
| POST | `/register` | Register a new user | No |
| POST | `/login` | Login with email and password | No |
| GET | `/verify-email` | Verify email with OTP | No |
| GET | `/get-me` | Get current user details | Yes |
| GET | `/refresh-token` | Refresh JWT token | Yes |
| POST | `/logout` | Logout and clear session | Yes |

### Request/Response Examples

#### Register
```bash
POST /api/auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123",
  "name": "John Doe"
}
```

#### Login
```bash
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

## Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Server Configuration
PORT=3000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/authentication

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_change_this
JWT_REFRESH_SECRET=your_super_secret_refresh_key_change_this
JWT_EXPIRE=7d
JWT_REFRESH_EXPIRE=30d

# Email Service Configuration
EMAIL_SERVICE=gmail
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_specific_password

# OTP Configuration
OTP_EXPIRE=600000
```

## Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or Atlas)
- npm or yarn package manager

### Quick Start

1. **Clone and Setup**
   ```bash
   git clone <repository-url>
   cd AUTHENTICATION
   npm install
   ```

2. **Configure Environment**
   - Copy `.env.example` to `.env` (or create `.env` manually)
   - Update with your MongoDB URI and email credentials

3. **Start Development Server**
   ```bash
   npm start
   ```
   
   Server runs at: `http://localhost:3000`

## Development

### Running Tests
```bash
npm test
```

### Code Organization
- **Models**: Define database schemas and validation
- **Controllers**: Handle business logic and request/response
- **Routes**: Define API endpoints
- **Services**: Reusable utilities (email sending, etc.)
- **Config**: Configuration files and database connection
- **Utils**: Helper functions and middleware

## Error Handling

The API returns standardized error responses:

```json
{
  "success": false,
  "message": "Error description",
  "error": "error_code"
}
```

## Security Considerations

- Passwords are hashed before storage
- JWT tokens are signed with secure secrets
- Email verification prevents unauthorized access
- Session tokens are stored in HTTP-only cookies
- Environment variables keep sensitive data secure

## Troubleshooting

### MongoDB Connection Issues
- Ensure MongoDB service is running
- Verify `MONGODB_URI` in `.env`
- Check network connectivity

### Email Not Sending
- Verify email credentials in `.env`
- For Gmail, use app-specific passwords (not your account password)
- Check email service configuration

### Port Already in Use
- Change `PORT` in `.env`
- Or kill the process using port 3000

## Contributing

1. Create a feature branch
2. Commit changes with clear messages
3. Push to repository
4. Open a pull request

## License

ISC

## Author

Shivam Kumar Singh

## Support

For issues and questions, please open an issue in the repository.
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
