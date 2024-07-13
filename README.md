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
   ```
   git clone https://github.com/StephCurry07/gridrnddjango
   cd gridrnddjango
   ```
2. **Set up a virtual environment:**
   ```
   python3 -m venv env
   source env/bin/activate
   ```
3. **Install the dependencies:**
   ```
   pip install -r requirements.txt
   ```
4. **Database setup:**

   - **Using SQLite (default):** Ensure `DATABASES` in `settings.py` is configured for SQLite.
   - **Using MySQL:** Update the `DATABASES` setting in `settings.py`:
     ```
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
     ```
5. **Run migrations:**
   ```
   python manage.py migrate
   ```
6. **Create a superuser (optional but recommended):**
   ```bash
   python manage.py createsuperuser
   ```

## Usage

1. **Start the development server:**
   ```
   python manage.py runserver
   ```
2. **Access the admin interface to add job postings:**

   - Navigate to `http://127.0.0.1:8000/admin`
   - Log in with your superuser credentials.
   - Add job postings under the `Job` model.
3. **Access the XML job feed:**

   - Navigate to `http://127.0.0.1:8000/jobs/feed/`

## Automatic Updates

To ensure the XML feed updates automatically when a new job is posted, Django signals are used.

- **Signal configuration:** The `post_save` signal for the `Job` model triggers the XML feed regeneration.
- **In `models.py`:**
  ```
  from django.db.models.signals import post_save
  from django.dispatch import receiver
  from .models import Job

  @receiver(post_save, sender=Job)
  def update_feed(sender, instance, created, **kwargs):
  if created:
  # Logic to update XML feed
  pass
  ```

## Documentation

### Dependencies and Configuration

- Ensure all dependencies listed in `requirements.txt` are installed.
- Configure the database settings in `settings.py` as per your choice of database (SQLite or MySQL).

### Adding New Job Postings

1. Access the Django admin interface at `http://127.0.0.1:8000/admin`.
2. Log in with your superuser credentials.
3. Navigate to the `Job` model and add new job postings.

### Verifying the XML Feed Updates

- After adding a new job posting, navigate to `http://127.0.0.1:8000/jobs/feed/` to verify the XML feed reflects the new job listing.

---

For further information on Indeed's XML feed specifications, refer to the official Indeed documentation.
