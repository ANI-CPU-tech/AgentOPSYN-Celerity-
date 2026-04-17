
# AgentOPSYN

## Overview

AgentOPSYN is an agentic developer experience platform that integrates with developer tools such as GitHub, monitoring systems, Slack, Jira, and internal documentation. It provides a unified interface to query operational data, automate workflows, and assist engineering teams.

The project uses:

* Django for the backend API
* Next.js for the frontend
* PostgreSQL as the database
* Docker for local development and service orchestration

---

## Environment Variables

Create a `.env` file inside the `backend/` directory with the following contents:

```
# Django
SECRET_KEY=your-secret-key
DEBUG=True

# Database
DB_NAME=agentopsynvectorbase
DB_USER=agent_user
DB_PASSWORD=strongpassword123
DB_HOST=db
DB_PORT=5432

# CORS
CORS_ALLOWED_ORIGINS=http://localhost:3000
```

### Generating a Django Secret Key

Run the following command in your terminal:

```
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

Copy the output and set it as the value of `SECRET_KEY` in your `.env` file.

---

## Running the Project with Docker

### Build and start services

```
docker compose up --build
```

### Access the application

* Frontend: [http://localhost:3000](http://localhost:3000)
* Backend: [http://localhost:8000](http://localhost:8000)

---

## Database Setup

After the containers are running, apply migrations:

```
docker exec -it django_backend python manage.py migrate
```

### Create a superuser (optional)

```
docker exec -it django_backend python manage.py createsuperuser
```

Admin panel:

```
http://localhost:8000/admin
```

---

## Project Structure

```
project-root/
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── .env
│   └── (Django project)
├── frontend/
│   ├── Dockerfile
│   └── (Next.js app)
└── docker-compose.yml
```

---

## Troubleshooting

### Database connection issues

* Ensure `DB_HOST=db` when using Docker
* Verify that the database container is running

### Port conflicts

* Update port mappings in `docker-compose.yml`

### Backend not starting

Check logs:

```
docker logs django_backend
```

---

## Next Steps

* Connect the frontend to backend APIs
* Add authentication (JWT)
* Integrate vector search capabilities (pgvector)

---

This setup is intended for local development. For production, additional configuration such as a WSGI server, reverse proxy, and environment hardening will be required.
