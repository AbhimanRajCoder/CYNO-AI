# 🏥 CYNO Healthcare - Backend API

A robust FastAPI backend for the CYNO Healthcare Platform, designed to support cancer care management with AI-powered features.

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Documentation](#-api-documentation)
- [Database](#-database)
- [Environment Variables](#-environment-variables)
- [Development](#-development)

---

## ✨ Features

- 🔐 **Authentication** - Hospital registration and JWT-based login
- 👥 **Patient Management** - CRUD operations for patient records
- 📄 **Report Upload** - Support for PDF, DICOM, and image uploads
- 🤖 **AI Reports** - AI-generated analysis and recommendations
- 🏛️ **Tumor Board** - Multi-disciplinary case management
- 📝 **Activity Logging** - Complete audit trail for compliance

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **FastAPI** | Modern async web framework |
| **Prisma** | Type-safe ORM with Python client |
| **SQLite** | Development database |
| **PostgreSQL** | Production database (optional) |
| **JWT** | Token-based authentication |
| **bcrypt** | Password hashing |
| **Pydantic** | Data validation |

---

## 📁 Project Structure

```
BACKEND/
├── 📄 main.py              # Application entry point
├── 📄 config.py            # Centralized configuration
├── 📄 database.py          # Database connection management
├── 📄 schemas.py           # Pydantic models for validation
├── 📄 utils.py             # Utility functions (auth helpers)
├── 📄 requirements.txt     # Python dependencies
├── 📄 .env                 # Environment variables (not in git)
├── 📄 .env.example         # Environment template
├── 📄 .gitignore           # Git ignore rules
│
├── 📂 routers/             # API route handlers
│   ├── __init__.py
│   ├── auth.py             # Authentication endpoints
│   ├── patients.py         # Patient management
│   ├── reports.py          # Report upload/management
│   ├── ai_reports.py       # AI report generation
│   ├── tumor_board.py      # Tumor board cases
│   └── activity.py         # Activity logging
│
├── 📂 prisma/              # Database schema & migrations
│   ├── schema.prisma       # Prisma schema definition
│   └── dev.db              # SQLite database (development)
│
├── 📂 uploads/             # Uploaded files storage
│   └── .gitkeep
│
└── 📂 docs/                # Documentation
    └── db.md               # Database documentation
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- Node.js 16+ (for Prisma CLI)

### Installation

1. **Clone the repository**
   ```bash
   cd CYNO/BACKEND
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Setup environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

5. **Setup database**
   ```bash
   # Generate Prisma client
   prisma generate
   
   # Run migrations
   prisma migrate dev --name init
   ```

6. **Run the server**
   ```bash
   uvicorn main:app --reload --port 8000
   ```

The API will be available at `http://localhost:8000`

---

## 📖 API Documentation

Once the server is running, access the interactive documentation:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### API Endpoints Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| **Authentication** |||
| POST | `/api/auth/register` | Register new hospital |
| POST | `/api/auth/login` | Hospital login |
| GET | `/api/auth/me` | Get current hospital info |
| **Patients** |||
| GET | `/api/patients` | List all patients |
| POST | `/api/patients` | Create new patient |
| GET | `/api/patients/{id}` | Get patient details |
| PUT | `/api/patients/{id}` | Update patient |
| DELETE | `/api/patients/{id}` | Delete patient |
| **Reports** |||
| POST | `/api/reports/upload` | Upload new report |
| GET | `/api/reports` | List all reports |
| GET | `/api/reports/{id}` | Get report details |
| **AI Reports** |||
| POST | `/api/ai-reports/generate` | Generate AI report |
| GET | `/api/ai-reports/{id}` | Get AI report |
| **Tumor Board** |||
| POST | `/api/tumor-board` | Create tumor board case |
| GET | `/api/tumor-board` | List cases |
| PUT | `/api/tumor-board/{id}` | Update case |
| **Activity** |||
| GET | `/api/activity` | Get activity logs |

---

## 🗄️ Database

See [docs/db.md](docs/db.md) for comprehensive database documentation.

### Quick Commands

```bash
# Open Prisma Studio (database GUI)
npx prisma studio --url="file:./prisma/dev.db"

# Generate Prisma client after schema changes
prisma generate

# Create new migration
prisma migrate dev --name <migration_name>

# Reset database (WARNING: deletes all data)
prisma migrate reset
```

---

## 🔐 Environment Variables

Create a `.env` file in the BACKEND directory. See `.env.example` for all available options.

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | Database connection string | `file:./prisma/dev.db` |
| `JWT_SECRET_KEY` | Secret for JWT signing | (required) |
| `JWT_ALGORITHM` | JWT algorithm | `HS256` |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | Token expiry time | `1440` (24h) |
| `HOST` | Server host | `0.0.0.0` |
| `PORT` | Server port | `8000` |
| `DEBUG` | Enable debug mode | `true` |
| `FRONTEND_URL` | Frontend URL for CORS | `http://localhost:3000` |
| `ALLOWED_ORIGINS` | Comma-separated CORS origins | `http://localhost:3000,...` |
| `UPLOAD_DIR` | Upload directory path | `./uploads` |
| `MAX_FILE_SIZE_MB` | Max upload size in MB | `50` |

---

## 🔧 Development

### Running in Development Mode

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Code Quality

```bash
# Format code
black .

# Type checking
mypy .

# Linting
flake8 .
```

### Testing

```bash
# Run tests
pytest

# Run with coverage
pytest --cov=.
```

---

## 📝 License

This project is part of the CYNO Healthcare Platform.

---

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Run tests
4. Submit a pull request

---

**Built with ❤️ for better healthcare**
