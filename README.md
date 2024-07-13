# Creating an XML Job Feed for Indeed Integration

## Objective
Develop a Django application that generates an XML job feed compatible with Indeed's requirements. The feed should pull job listings from the database and update automatically when a new job is posted.

## Table of Contents
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Automatic Updates](#automatic-updates)
- [Documentation](#documentation)

## Requirements
- Python 3.x
- Django
- MySQL or SQLite (for simplicity)
- Any required Python packages (specified in `requirements.txt`)

## Installation
1. **Clone the repository:**
   \```bash
   git clone <repository_url>
   cd <repository_folder>
   \```

2. **Set up a virtual environment:**
   \```bash
   python3 -m venv env
   source env/bin/activate
   \```

3. **Install the dependencies:**
   \```bash
   pip install -r requirements.txt
   \```

4. **Database setup:**
   - **Using SQLite (default):** Ensure `DATABASES` in `settings.py` is configured for SQLite.
   - **Using MySQL:** Update the `DATABASES` setting in `settings.py`:
     \```python
     DATABASES = {
         'default': {
             'ENGINE': 'django.db.backends.mysql',
             'NAME': 'your_db_name',
             'USER': 'your_db_user',
             'PASSWORD': 'your_db_password',
             'HOST': 'localhost',
             'PORT': '3306',
         }
     }
     \```

5. **Run migrations:**
   \```bash
   python manage.py migrate
   \```

6. **Create a superuser (optional but recommended):**
   \```bash
   python manage.py createsuperuser
   \```

## Usage
1. **Start the development server:**
   \```bash
   python manage.py runserver
   \```

2. **Access the admin interface to add job postings:**
   - Navigate to `http://127.0.0.1:8000/admin`
   - Log in with your superuser credentials.
   - Add job postings under the `Job` model.

3. **Access the XML job feed:**
   - Navigate to `http://127.0.0.1:8000/jobs/feed/`
