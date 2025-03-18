---
title: "Django on vercel"
date: "2025-03-18"
tags: ["python", "django", "vercel"]
---

# 🚀 Deploying Your Django Project to Vercel

Follow these steps to convert your Django project to work on Vercel seamlessly!

## Step 1: Set Up Your Django Project 🛠️

1. **Install Dependencies**:
   First, make sure you have Pipenv installed. If not, you can install it using pip:

   ```bash
   pip install pipenv
   ```

2. **Create a Pipfile**:
   Navigate to your Django project directory and create a Pipfile:

   ```bash
   pipenv install django gunicorn
   ```

   This will create a Pipfile and install Django and Gunicorn, which are essential for running your application on Vercel. 🎉

3. **Create a `requirements.txt`**:
   If your project requires additional packages, generate a `requirements.txt`:

   ```bash
   pipenv lock -r > requirements.txt
   ```

## Step 2: Configure Your Project ⚙️

1. **Modify `wsgi.py`**:
   Ensure your `wsgi.py` file is set up correctly, like so:

   ```python
   import os
   from django.core.wsgi import get_wsgi_application

   os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'NAME.settings')
   application = get_wsgi_application()
   app = application
   ```

2. **Configure Static Files**:
   Vercel needs your static files to be served properly. In your `settings.py`, add:

   ```python
   STATIC_URL = '/static/'
   STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
   ```

   Then run:

   ```bash
   python manage.py collectstatic
   ```

   This collects all your static files! 📦

3. **Set Environment Variables**:
   Create a `.env` file at the root of your project to store sensitive info:

   ```
   DJANGO_SECRET_KEY=your_secret_key
   DATABASE_URL=your_database_url
   ```

   Install `python-decouple` to load these variables easily:

   ```bash
   pipenv install python-decouple
   ```

   Update your `settings.py` to use them:

   ```python
   from decouple import config

   SECRET_KEY = config('DJANGO_SECRET_KEY')
   DATABASE_URL = config('DATABASE_URL')
   ```

## Step 3: Deploy to Vercel 🌍

1. **Install Vercel CLI**:
   If you haven’t already, install the Vercel CLI:

   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel**:
   Use the CLI to log in:

   ```bash
   vercel login
   ```

3. **Create a Vercel Project**:
   In your project directory, run:

   ```bash
   vercel
   ```

   Follow the prompts to set up your project. 🥳

4. **Configure `vercel.json`**:
   Create a `vercel.json` file in your project root to specify build settings:

```json
{
    "builds": [{
        "src": "NAME/wsgi.py",
        "use": "@vercel/python",
        "config": { "maxLambdaSize": "15mb" }
    }],

    "routes": [
        {
            "src": "/(.*)",
            "dest": "NAME/wsgi.py"
        }
    ]
}
```

## Step 4: Deploy Your Application 🚢

1. **Deploy to Production**:
   Once everything is set up, deploy your application:

   ```bash
   vercel --prod
   ```

   This will deploy your Django application to production on Vercel! 🎊

## Step 5: Verify Deployment ✔️

1. **Check Logs**:
   After deployment, check the logs to ensure everything is working correctly:

   ```bash
   vercel logs <your-deployment-url>
   ```

2. **Visit Your Application**:
   Navigate to the URL provided by Vercel to see your deployed application in action! 🌟

---
