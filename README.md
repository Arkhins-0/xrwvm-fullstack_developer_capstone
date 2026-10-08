# Full Stack Developer Capstone — Best Cars Dealership

**Project name:** Best Cars Dealership — a full-stack web application for a national car retailer in the U.S.

The site lists the company's dealership branches across the country. Visitors can browse dealers and
filter them by state, open a dealer to read its customer reviews (each tagged with a sentiment), and
registered users can sign in and post their own reviews.

## Architecture

| Component | Technology | Location |
|---|---|---|
| Web app and user management | Django (SQLite) | `server/djangoproj`, `server/djangoapp` |
| Frontend | React (dealers, dealer detail, post review, login, register) + static Django templates (Home, About, Contact) | `server/frontend` |
| Dealers and reviews API | Node.js / Express + MongoDB | `server/database` |
| Sentiment analyzer | Flask + NLTK VADER | `server/djangoapp/microservices` |
| Car makes and models | Django models + admin | `server/djangoapp/models.py` |
| CI | GitHub Actions (flake8 + JSHint) | `.github/workflows/main.yml` |
| Deployment | Docker + Kubernetes | `server/Dockerfile`, `server/deployment.yaml` |

## Running locally

```bash
# 1. Dealers/reviews API (needs MongoDB; MONGO_URL defaults to mongodb://mongo_db:27017/)
cd server/database && npm install
cd data && MONGO_URL=mongodb://127.0.0.1:27017/ node ../app.js        # port 3030

# 2. Sentiment analyzer
cd server/djangoapp/microservices && pip install -r requirements.txt
NLTK_DATA=. python -m flask run --port 5050

# 3. React frontend build
cd server/frontend && npm install && npm run build

# 4. Django
cd server && pip install -r requirements.txt
python manage.py migrate && python manage.py runserver
```

Service URLs are configured in `server/djangoapp/.env` (`backend_url`, `sentiment_analyzer_url`).
