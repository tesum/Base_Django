# Сервер-основа для ПРОМа

## Используется Docker-Compose, Django, PostgreSQL, Nginx, Gunicorn

Commands:
  -  **Delete all:** `docker system prune -a --volumes`
  -  **Build up:** `docker-compose up -d --build`
  -  **Build:** `docker-compose build`
  -  **Up:** `docker-compose up`
  -  **Down:** `docker-compose down -v`
  -  **Migrate:** `docker-compose exec web python3 manage.py migrate --noinput`
  -  **Static:** `docker-compose exec web python manage.py collectstatic --no-input --clear`

