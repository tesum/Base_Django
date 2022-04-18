# Сервер-основа для ПРОМа

## Используется Docker-Compose, Django, PostgreSQL, Nginx, Gunicorn

Commands:
  -  delete all: docker system prune -a --volumes
  -  build up: docker-compose up -d --build
  -  build: docker-compose build
  -  up: docker-compose up
  -  down: docker-compose down -v
  -  migrate: docker-compose exec web python3 manage.py migrate --noinput
  -  static: docker-compose exec web python manage.py collectstatic --no-input --clear

