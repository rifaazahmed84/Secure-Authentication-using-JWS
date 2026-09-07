# 🔐 Secure Authentication using JWS

A secure authentication system built around **JSON Web Signatures (JWS)** for protecting authentication tokens and verifying their integrity.

The project demonstrates how modern web applications can implement **stateless authentication**, securely validate users, and prevent tampering with authentication tokens.

## 🚀 Features

* 🔑 User registration and login
* 🔒 Password hashing before storage
* 🎫 JWS-based authentication tokens
* ✅ Token signature verification
* 🛡️ Protected API routes
* ⏱️ Token expiration handling
* 🚫 Invalid/tampered token detection
* 🔄 Stateless authentication
* 🌐 REST API architecture
* 📊 Clean authentication flow

## 🧠 How It Works

The authentication flow is simple:

```text
User
  │
  ▼
Login / Register
  │
  ▼
Backend validates credentials
  │
  ▼
Password verified
  │
  ▼
JWS Token Generated
  │
  ▼
Client stores token
  │
  ▼
Client requests protected API
  │
  ▼
Backend verifies JWS signature
  │
  ├── Valid → Allow Request
  │
  └── Invalid → Reject Request
```

The JWS token contains claims such as the user's identity and expiration time. The server signs the token using a secret/private key, allowing the server to detect whether the token has been modified.

## 🛠️ Tech Stack

### Backend

* **Python**
* **FastAPI**
* **JWS / JWT**
* **REST APIs**
* **Pydantic**

### Security

* Password hashing
* Cryptographic signatures
* Token expiration
* Signature verification
* Protected endpoints

### Database

* **MongoDB / PostgreSQL** *(depending on implementation)*

### Frontend

* **React.js**
* HTML
* CSS
* JavaScript

## 📁 Project Structure

```text
secure-auth-jws/
│
├── backend/
│   ├── main.py
│   ├── auth/
│   │   ├── authentication.py
│   │   ├── security.py
│   │   └── dependencies.py
│   │
│   ├── models/
│   ├── routes/
│   └── database/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── services/
│   └── package.json
│
├── .env.example
├── requirements.txt
└── README.md
```

## 🔑 Authentication

After successful login, the server generates a signed token.

Example payload:

```json
{
  "sub": "user_id",
  "username": "user",
  "exp": 1780000000
}
```

The payload is signed before being returned to the client.

On every protected request, the server:

1. Extracts the token.
2. Validates its structure.
3. Verifies the cryptographic signature.
4. Checks token expiration.
5. Extracts the authenticated user's identity.
6. Grants or denies access.

## 🔒 Why JWS?

JWS provides **integrity and authenticity** for signed JSON-based tokens.

If an attacker modifies information inside the token, the signature verification will fail.

For example:

```text
Original Token
     ↓
Signed by Server
     ↓
Client
     ↓
Token modified ❌
     ↓
Signature verification fails
     ↓
Request rejected
```

> **Note:** JWS signs data; it does not encrypt the payload. Sensitive information should therefore not be placed inside a JWS token unless additional encryption is used.

## ⚙️ Environment Variables

Create a `.env` file:

```env
SECRET_KEY=your_secure_secret_key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
DATABASE_URL=your_database_connection
```

**Never commit your real `.env` file to GitHub.**

Add it to `.gitignore`:

```text
.env
__pycache__/
node_modules/
```

## ▶️ Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/secure-auth-jws.git
cd secure-auth-jws
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create `.env` and add your configuration.

### 5. Start the backend

```bash
uvicorn main:app --reload
```

The API will be available at:

```text
http://127.0.0.1:8000
```

FastAPI documentation:

```text
http://127.0.0.1:8000/docs
```

## 📡 Example API Endpoints

| Method | Endpoint     | Description                |
| ------ | ------------ | -------------------------- |
| POST   | `/register`  | Create a new user          |
| POST   | `/login`     | Authenticate user          |
| GET    | `/users/me`  | Get authenticated user     |
| GET    | `/protected` | Access protected resource  |
| POST   | `/logout`    | End authentication session |

## 🧪 Security Testing

The project can be tested against common authentication scenarios:

* Incorrect password
* Non-existent user
* Expired token
* Modified token payload
* Invalid signature
* Missing authentication token
* Accessing protected endpoints without authentication

Example:

```text
Valid credentials       → ✅ Authentication successful
Invalid credentials     → ❌ 401 Unauthorized
Expired token           → ❌ 401 Unauthorized
Modified JWS token      → ❌ 401 Unauthorized
Missing token           → ❌ 401 Unauthorized
```

## 📌 What I Learned

Building this project helped me understand:

* How token-based authentication works
* JWS and cryptographic signatures
* Password hashing
* REST API security
* Authentication middleware
* Token validation and expiration
* Secure environment configuration
* Backend API design

## 🔮 Future Improvements

* Refresh token rotation
* Role-based access control (RBAC)
* OAuth 2.0 / OpenID Connect integration
* Multi-factor authentication
* Rate limiting
* Redis-based session/token management
* Docker deployment
* AWS cloud deployment
* Security logging and monitoring

## 👨‍💻 Author

**Rifaaz Ahmed**

Built as a hands-on project to explore **secure authentication, cryptography, backend APIs, and modern web security**.
