# Task Management System - Full Stack Application

A scalable REST API with authentication, role-based access control, and CRUD operations built with Django REST Framework and React.

## 🚀 Features

### Backend (Django REST Framework)
- ✅ User registration & login with JWT authentication
- ✅ Password hashing using Django's built-in security
- ✅ Role-based access control (User vs Admin)
- ✅ CRUD operations for Task management
- ✅ API versioning (`/api/v1/`)
- ✅ Input validation and error handling
- ✅ SQLite database (easily switchable to PostgreSQL/MySQL)

### Frontend (React.js)
- ✅ User registration and login interface
- ✅ Protected dashboard (JWT required)
- ✅ Task CRUD operations with real-time updates
- ✅ Success/error message handling
- ✅ Responsive UI design
- ✅ Secure token management (localStorage)

### Security Features
- ✅ JWT token-based authentication
- ✅ Password hashing (PBKDF2 algorithm)
- ✅ CORS configuration
- ✅ Input validation and sanitization
- ✅ Protected API endpoints

---

## 📁 Project Structure
```
## 📁 Project Structure
```
backend-assignment/
├── api/                       # Django app (models, views, serializers, urls)
├── backend/                   # Django project settings
├── venv/                      # Python virtual environment (not in git)
├── manage.py                  # Django management script
├── db.sqlite3                 # SQLite database (not in git)
├── requirements.txt           # Python dependencies
│
├── frontend/                  # React Frontend Application
│   ├── src/
│   │   ├── components/       # React components
│   │   │   ├── Register.js
│   │   │   ├── Login.js
│   │   │   ├── Dashboard.js
│   │   │   └── ProtectedRoute.js
│   │   ├── services/         # API integration
│   │   │   └── api.js
│   │   ├── utils/            # Helper functions
│   │   │   └── auth.js
│   │   └── App.js
│   ├── public/
│   ├── node_modules/         # (not in git)
│   └── package.json
│
├── README.md                  # Project documentation
├── Task_Management_API.postman_collection.json  # API documentation
└── .gitignore                 # Git ignore rules
```
```

---

## 🛠️ Tech Stack

**Backend:**
- Python 3.x
- Django 5.0+
- Django REST Framework
- djangorestframework-simplejwt
- SQLite (default) / MySQL / PostgreSQL

**Frontend:**
- React.js 18+
- React Router DOM
- Axios
- CSS3

---

## 📦 Installation & Setup

### Prerequisites
- Python 3.8 or higher
- Node.js 14+ and npm
- Git

### Backend Setup

1. **Clone the repository**
```bash
git clone 
cd backend-assignment
```

2. **Create and activate virtual environment**
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
```

3. **Install Python dependencies**
```bash
pip install -r requirements.txt
```

4. **Run database migrations**
```bash
python manage.py makemigrations
python manage.py migrate
```

5. **Create superuser (optional - for admin panel)**
```bash
python manage.py createsuperuser
```

6. **Start Django development server**
```bash
python manage.py runserver
```
Backend will run at: `http://localhost:8000`

---
### Frontend Setup

1. **Navigate to frontend folder**
```bash
cd ../frontend
```

2. **Install npm dependencies**
```bash
npm install
```

3. **Start React development server**
```bash
npm start
```

Frontend will run at: `http://localhost:3000`

---

## 🔌 API Endpoints

### Authentication
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/v1/auth/register/` | Register new user | No |
| POST | `/api/v1/auth/login/` | Login user | No |

### Tasks (Protected)
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/tasks/` | Get all tasks | Yes |
| POST | `/api/v1/tasks/` | Create new task | Yes |
| GET | `/api/v1/tasks/{id}/` | Get task detail | Yes |
| PUT | `/api/v1/tasks/{id}/` | Update task | Yes |
| DELETE | `/api/v1/tasks/{id}/` | Delete task | Yes |

### Request/Response Examples

**Register User:**
```json
POST /api/v1/auth/register/
{
  "username": "john",
  "email": "john@example.com",
  "password": "SecurePass123",
  "password2": "SecurePass123",
  "role": "user"
}
```

**Login:**
```json
POST /api/v1/auth/login/
{
  "username": "john",
  "password": "SecurePass123"
}

Response:
{
  "message": "Login successful",
  "tokens": {
    "access": "eyJ0eXAiOiJKV1QiLCJhbGc...",
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGc..."
  },
  "user": {
    "id": 1,
    "username": "john",
    "email": "john@example.com",
    "role": "user"
  }
}
```

**Create Task:**
```json
POST /api/v1/tasks/
Headers: Authorization: Bearer <access_token>

{
  "title": "Complete project",
  "description": "Finish the backend API",
  "status": "pending"
}
```

---

## 🧪 Testing the Application

### Using the UI
1. Open `http://localhost:3000`
2. Register a new account
3. Login with credentials
4. Create, edit, and delete tasks from dashboard

### Using Postman
1. Import the Postman collection (see `postman_collection.json`)
2. Register a user via `/api/v1/auth/register/`
3. Login and copy the access token
4. Add token to Authorization header for protected endpoints
5. Test CRUD operations on tasks

---

## 👥 Role-Based Access Control

- **User Role:** Can only view and manage their own tasks
- **Admin Role:** Can view and manage all tasks from all users

---

## 🔒 Security Implementations

1. **Password Security**
   - Passwords hashed using PBKDF2 algorithm
   - Password validation enabled

2. **JWT Authentication**
   - Access token lifetime: 1 day
   - Refresh token lifetime: 7 days
   - Tokens stored securely in localStorage

3. **CORS Protection**
   - Configured to allow only frontend origin
   - Can be updated for production domains

4. **Input Validation**
   - Django REST Framework serializers
   - Custom validation rules
   - Proper error handling

---

## 📈 Scalability Considerations

### Current Architecture
The application is built with scalability in mind:

1. **Microservices Ready**
   - Modular structure allows easy separation into microservices
   - API versioning enables backward compatibility
   - RESTful design principles followed

2. **Database Scalability**
   - ORM-based (easily switch from SQLite to PostgreSQL/MySQL)
   - Database indexing on frequently queried fields
   - Can implement read replicas for high-traffic scenarios

3. **Caching Strategy**
   - Ready for Redis integration for session management
   - API responses can be cached using Django's caching framework
   - Static files can be served via CDN

4. **Load Balancing**
   - Stateless API design allows horizontal scaling
   - Multiple Django instances can run behind load balancer (Nginx/HAProxy)
   - JWT tokens eliminate need for sticky sessions

5. **Future Enhancements**
   - Implement task queues (Celery + Redis) for async operations
   - Add rate limiting to prevent API abuse
   - Implement GraphQL for flexible data fetching
   - Add WebSocket support for real-time updates
   - Deploy using Docker containers + Kubernetes for orchestration

### Deployment Considerations
- **Backend:** Deploy on AWS EC2, Heroku, or Railway
- **Frontend:** Deploy on Vercel, Netlify, or AWS S3 + CloudFront
- **Database:** Managed PostgreSQL (AWS RDS, Heroku Postgres)
- **File Storage:** AWS S3 for media files
- **Monitoring:** Integration with Sentry, DataDog, or New Relic

---

## 🐛 Troubleshooting

**Backend Issues:**
- Ensure virtual environment is activated
- Check if all migrations are applied: `python manage.py migrate`
- Verify DATABASE settings in `settings.py`

**Frontend Issues:**
- Clear browser cache and localStorage
- Check if backend is running on port 8000
- Verify API_BASE_URL in `src/services/api.js`

**CORS Errors:**
- Add frontend URL to CORS_ALLOWED_ORIGINS in Django settings
- Restart Django server after changes

---

## 📝 Database Schema

### User Model
```python
- id (Primary Key)
- username (Unique)
- email (Unique)
- password (Hashed)
- role (user/admin)
- is_active
- date_joined
```

### Task Model
```python
- id (Primary Key)
- title
- description
- status (pending/in_progress/completed)
- created_by (Foreign Key to User)
- created_at
- updated_at
```

---

## 📧 Contact

**Developer:** [Your Name]  
**Email:** [Your Email]  
**GitHub:** [Your GitHub Profile]

---

## 📄 License

This project is created for internship assignment purposes.

---

## 🙏 Acknowledgments

- Django REST Framework Documentation
- React.js Documentation
- JWT Best Practices
```

---

# STEP 2: Create Postman Collection (10 mins)

### Option A: Manual Export (Recommended)

1. **Open Postman**
2. **Create a new collection** called "Task Management API"
3. **Add these requests:**

#### Request 1: Register User
```
POST http://localhost:8000/api/v1/auth/register/
Body (raw JSON):
{
    "username": "testuser",
    "email": "test@example.com",
    "password": "Test@1234",
    "password2": "Test@1234",
    "role": "user"
}
```

#### Request 2: Login
```
POST http://localhost:8000/api/v1/auth/login/
Body (raw JSON):
{
    "username": "testuser",
    "password": "Test@1234"
}
```

#### Request 3: Get All Tasks
```
GET http://localhost:8000/api/v1/tasks/
Headers:
Authorization: Bearer {{access_token}}
```

#### Request 4: Create Task
```
POST http://localhost:8000/api/v1/tasks/
Headers:
Authorization: Bearer {{access_token}}
Body (raw JSON):
{
    "title": "Sample Task",
    "description": "This is a test task",
    "status": "pending"
}
```

#### Request 5: Update Task
```
PUT http://localhost:8000/api/v1/tasks/1/
Headers:
Authorization: Bearer {{access_token}}
Body (raw JSON):
{
    "title": "Updated Task",
    "description": "Updated description",
    "status": "completed"
}
```

#### Request 6: Delete Task
```
DELETE http://localhost:8000/api/v1/tasks/1/
Headers:
Authorization: Bearer {{access_token}}