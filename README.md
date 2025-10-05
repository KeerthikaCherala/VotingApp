# VotingApp - Online Voting System

A comprehensive Django-based online voting application that enables secure electronic voting with real-time results, candidate management, and administrative controls.

## 📋 Table of Contents

- [Features](#-features)
- [Project Structure](#-project-structure)
- [Technologies Used](#️-technologies-used)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Database Setup](#️-database-setup)
- [Running the Application](#️-running-the-application)
- [Usage](#-usage)
- [Project Architecture](#️-project-architecture)
- [Key Files](#-key-files)
- [Security Features](#-security-features)
- [Important Notes](#-important-notes)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### User Features
- **User Registration & Authentication**: Secure voter registration with unique Voter ID
- **Election Overview**: View comprehensive election information and guidelines
- **Candidate Details**: Browse candidate profiles, party information, and symbols
- **Live Voting**: Cast votes during active election periods
- **Real-time Results**: View election results after voting closes
- **One Vote Policy**: System ensures each voter can only vote once

### Admin Features
- **Admin Dashboard**: Dedicated admin panel for election management
- **Candidate Management**: Add and remove candidates with complete details
- **Election Scheduling**: Set start and end times for elections
- **Vote Tracking**: Monitor vote counts and election progress

## 📁 Project Structure

```
VotingApp/
├── manage.py                    # Django management script
├── votingproject/               # Main project configuration
│   ├── settings.py             # Project settings
│   ├── urls.py                 # Root URL configuration
│   ├── wsgi.py                 # WSGI configuration
│   └── asgi.py                 # ASGI configuration
├── validation/                  # User authentication & voting app
│   ├── models.py               # UserProfile model
│   ├── views.py                # User views (login, register, voting)
│   ├── urls.py                 # User URL patterns
│   └── migrations/             # Database migrations
├── Candidates/                  # Candidate management app
│   ├── models.py               # Election candidates model
│   ├── views.py                # Admin views
│   ├── urls.py                 # Admin URL patterns
│   ├── admin.py                # Custom admin configuration
│   └── migrations/             # Database migrations
├── templates/                   # HTML templates
│   ├── registration/           # Login & registration pages
│   ├── admin/                  # Admin dashboard pages
│   ├── home.html               # User home page
│   ├── candidateDetails.html   # Candidate listing
│   ├── ElectionsLive.html      # Live voting page
│   ├── ResultsPage.html        # Results display
│   ├── elections_overview.html # Election information
│   └── elections_guidelines.html # Voting guidelines
├── static/                      # Static files (CSS, images)
│   ├── addcands.jpg
│   ├── booth.jpg
│   ├── canddetails.jpg
│   ├── carousel1.jpg
│   ├── carousel2.jpg
│   ├── carousel3.jpg
│   └── [various images]
└── README.md                    # Project documentation
```

## 🛠️ Technologies Used

- **Backend**: Django 5.0
- **Database**: MySQL
- **Frontend**: HTML5, CSS3, JavaScript
- **Frameworks & Libraries**: 
  - Tailwind CSS
  - Bootstrap 5
  - jQuery 3.6.0
  - Font Awesome 5.15.3
- **Security**: bcrypt (password hashing)
- **Image Processing**: Pillow

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Python**: Version 3.8 or higher
- **MySQL Server**: Version 5.7 or higher
- **pip**: Python package manager
- **Git**: (optional, for cloning)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/KeerthikaCherala/VotingApp.git

cd VotingApp
```

### 2. Create Virtual Environment

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```cmd
python -m venv venv
venv\Scripts\activate.bat
```

**Linux/Mac:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install django==5.0
pip install mysqlclient
pip install bcrypt
pip install Pillow
```

**Or install from requirements.txt (if available):**
```bash
pip install -r requirements.txt
```

## 🗄️ Database Setup

### 1. Create MySQL Database

Open MySQL command line or MySQL Workbench and run:

```sql
CREATE DATABASE votingproject;
CREATE USER 'voting_user'@'localhost' IDENTIFIED BY 'your_secure_password';
GRANT ALL PRIVILEGES ON votingproject.* TO 'voting_user'@'localhost';
FLUSH PRIVILEGES;
```

### 2. Configure Database Settings

Update the database configuration in `votingproject/settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'votingproject',
        'USER': 'voting_user',
        'PASSWORD': 'your_secure_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

**⚠️ SECURITY WARNING**: 
- Change the `SECRET_KEY` in `votingproject/settings.py` before deployment!
- Never commit sensitive credentials to version control
- Use environment variables for production settings

### 3. Run Migrations

Apply database migrations to create all necessary tables:

```bash
python manage.py makemigrations
python manage.py migrate
```

Expected output:
```
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying validation.0001_initial... OK
  Applying Candidates.0001_initial... OK
  ...
```

### 4. Create Superuser (Optional)

Create an admin account for Django admin panel:

```bash
python manage.py createsuperuser
```

Follow the prompts to set username, email, and password.

## ▶️ Running the Application

### 1. Start Development Server

```bash
python manage.py runserver
```

You should see output like:
```
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

The application will be available at `http://127.0.0.1:8000/`

### 2. Access Different Interfaces

| Interface | URL | Description |
|-----------|-----|-------------|
| **Home Page** | `http://127.0.0.1:8000/` | Landing page |
| **User Login** | `http://127.0.0.1:8000/login/` | Voter login portal |
| **User Registration** | `http://127.0.0.1:8000/Register/` | New voter registration |
| **Admin Login** | `http://127.0.0.1:8000/ecadmin/` | Election admin panel |
| **Admin Registration** | `http://127.0.0.1:8000/ecadmin/adminRegister/` | Admin account creation |
| **Django Admin** | `http://127.0.0.1:8000/admin/` | Django admin interface |

## 📖 Usage

### For Voters

1. **Register**: 
   - Navigate to `http://127.0.0.1:8000/Register/`
   - Fill in your details (name, email, unique Voter ID, password)
   - Submit the registration form

2. **Login**: 
   - Visit `http://127.0.0.1:8000/login/`
   - Enter your Voter ID and password
   - Access the voter dashboard

3. **Explore**: 
   - **Elections Overview** (`elections_overview.html`): View election information
   - **Guidelines** (`elections_guidelines.html`): Read voting instructions
   - **Candidate Details** (`candidateDetails.html`): Browse all candidates

4. **Vote**: 
   - During active election periods, click "Polling Booth"
   - View candidates and select your choice
   - Submit your vote (one-time only)

5. **Results**: 
   - After election ends, view results showing vote counts
   - See winner announcement with highest votes

### For Administrators

1. **Login**: 
   - Access admin panel at `http://127.0.0.1:8000/ecadmin/`
   - Use admin credentials

2. **Add Candidates** (`addCandidates.html`):
   ```
   Required Information:
   - Candidate ID (unique identifier)
   - Name
   - Age
   - Gender (Male/Female/Other)
   - Education
   - Candidate Photo (upload)
   - Party Name
   - Party Symbol (upload)
   - Election Start Time (YYYY-MM-DD HH:MM:SS)
   - Election End Time (YYYY-MM-DD HH:MM:SS)
   ```

3. **Remove Candidates** (`deleteCandidate.html`):
   - Search by Candidate ID or Name
   - Confirm deletion

4. **Monitor Elections**:
   - View real-time vote counts
   - Track active elections
   - Manage election schedules

## 🏗️ Project Architecture

### Django Apps

#### 1. **validation** App
Handles user authentication and voting functionality:

**Key Files:**
- `validation/models.py`: Defines `UserProfile` model
- `validation/views.py`: Contains view functions:
  - `UserRegister`: User registration logic
  - `UserLogin`: User authentication
  - `polling_booth`: Live voting interface
  - `castVotes`: Vote casting with validation
  - `countingElections`: Results calculation
  - `invalidPage`: Invalid vote handling
- `validation/urls.py`: URL routing for user features

#### 2. **Candidates** App
Manages election candidates and admin operations:

**Key Files:**
- `Candidates/models.py`: Defines `Electioncandidates` model
- `Candidates/views.py`: Admin view functions:
  - `adminHome`: Admin dashboard
  - `add_candidates`: Add new candidates
  - `del_candidates`: Delete candidates interface
  - `candidateDeletion`: Candidate deletion logic
  - `adminRegister`: Admin registration
  - `adminLogin`: Admin authentication
- `Candidates/urls.py`: URL routing for admin features
- `Candidates/admin.py`: Django admin customization

### Database Models

#### UserProfile Model (`validation/models.py`)
```python
class UserProfile(models.Model):
    username = models.CharField(max_length=100)      # Voter's full name
    email = models.EmailField(unique=True)           # Email address
    voter_id = models.CharField(max_length=50, unique=True)  # Unique voter ID
    pass1 = models.CharField(max_length=128)         # Hashed password
    has_voted = models.BooleanField(default=False)   # Voting status tracker
```

#### Electioncandidates Model (`Candidates/models.py`)
```python
class Electioncandidates(models.Model):
    candidateID = models.CharField(max_length=50, unique=True)  # Unique ID
    name = models.CharField(max_length=100)          # Candidate name
    age = models.IntegerField()                      # Age
    gender = models.CharField(max_length=10)         # Gender
    education = models.CharField(max_length=200)     # Education details
    photo = models.ImageField(upload_to='candidates/')  # Candidate photo
    party_name = models.CharField(max_length=100)    # Political party
    party_symbol = models.ImageField(upload_to='party_symbols/')  # Party symbol
    start_time = models.DateTimeField()              # Election start
    end_time = models.DateTimeField()                # Election end
    votes = models.IntegerField(default=0)           # Vote count
```

### URL Configuration

**Main URLs (`votingproject/urls.py`):**
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('validation.urls')),      # User routes
    path('ecadmin/', include('Candidates.urls')),  # Admin routes
]
```

## 🔑 Key Files

| File | Purpose |
|------|---------|
| `manage.py` | Django CLI utility for management commands |
| `votingproject/settings.py` | Project configuration (database, apps, middleware) |
| `votingproject/urls.py` | Root URL routing configuration |
| `validation/views.py` | Core voting logic including vote counting |
| `Candidates/views.py` | Admin operations and candidate management |
| `templates/home.html` | User dashboard landing page |
| `templates/ElectionsLive.html` | Live voting interface with AJAX |
| `templates/ResultsPage.html` | Results display with winner calculation |
| `templates/candidateDetails.html` | Candidate listing and details |
| `templates/admin/index.html` | Admin dashboard |
| `templates/admin/addCandidates.html` | Candidate addition form |
| `templates/admin/deleteCandidate.html` | Candidate deletion interface |

## 🔒 Security Features

- ✅ **CSRF Protection**: All forms include CSRF tokens
- ✅ **Password Hashing**: Secure password storage using Django's built-in hashing
- ✅ **Session Management**: Secure session-based authentication
- ✅ **One-Time Voting**: Database flag prevents multiple votes per user
- ✅ **Time-Bound Elections**: Server-side validation of election start/end times
- ✅ **SQL Injection Prevention**: Django ORM parameterized queries
- ✅ **XSS Protection**: Template auto-escaping enabled

## 📝 Important Notes

### Security Warnings
- ⚠️ Change the `SECRET_KEY` in `votingproject/settings.py` before deployment
- ⚠️ Set `DEBUG = False` in production
- ⚠️ Update `ALLOWED_HOSTS` with your domain name
- ⚠️ Never commit database credentials to version control
- ⚠️ Use environment variables for sensitive configuration

### Production Deployment
```bash
# Collect static files
python manage.py collectstatic

# Run with production settings
python manage.py runserver --settings=votingproject.production_settings
```

### File Permissions
- Ensure proper upload directory permissions for:
  - `media/candidates/` (candidate photos)
  - `media/party_symbols/` (party symbols)
  
### Database Considerations
- Regular backups recommended
- Index on `voter_id` and `candidateID` for performance
- Monitor database connection pool in production

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guide for Python code
- Write descriptive commit messages
- Add tests for new features
- Update documentation as needed

## 📄 License

This project is created by **Keerthika Cherala** © 2024-2025

All rights reserved. This software is provided for educational purposes.

## 📞 Supports

For support, questions, or feedback:
- **GitHub**: [VotingApp](https://github.com/KeerthikaCherala/VotingApp.git)
- **Issues**: Report bugs via GitHub Issues
- **Email**: Contact the project maintainer

---

**Made with ❤️ by Keerthika Cherala**
