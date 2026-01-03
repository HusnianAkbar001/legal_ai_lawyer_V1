# LegalAI Project Setup (Windows) Guide 

This document explains the exact, step-by-step procedure to set up and run the **LegalAI** project on **Windows**.
The project consists of a **Flask backend**, **Celery workers**

> **Important:**
>
> * Backend is implemented in **Flask (Python)**

---

## Prerequisites

Ensure the following are installed on your system:

* Python 3.10
* pip
* Git
* Docker Desktop (required for Redis)

---

## Backend Setup (Flask)

### First-Time Setup

1. Navigate to the backend directory:

```bash
cd legalai-backend
```

2. Create a virtual environment:

```bash
python -m venv venv
```

```bash
C:\Users\Zbook\AppData\Local\Programs\Python\Python310\python.exe -m venv venv
```

3. Activate the virtual environment (Windows):

```bash
venv\Scripts\activate
```

4. Install backend dependencies:

```bash
pip install -r requirements.txt
```

5. Apply database migrations:

```bash
flask db upgrade
```

6. Start the backend server:

```bash
python run.py
```

---

### Subsequent Backend Runs

```bash
cd legalai-backend
```

```bash
venv\Scripts\activate
```

```bash
python run.py
```

---

## Celery Worker Setup

> **Important:** Docker Desktop must be running and Redis must be active before starting Celery.

```bash
cd legalai-backend
```

```bash
venv\Scripts\activate
```

### Celery Worker

```bash
celery -A app.celery_worker:celery worker --loglevel=info --pool=solo
```

### Celery Beat

```bash
celery -A app.celery_worker.celery beat --loglevel=info
```


## Notes

* Backend, Celery Worker must be run in **separate terminals**
* Redis must be running for Celery tasks
* `.env` files must be correctly configured

---

## Recommended Startup Order

1. Backend Server
2. Celery Worker

Following this sequence prevents runtime and dependency issues.
