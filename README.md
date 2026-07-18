# Laravel Docker Environment

Laravel 13 + PHP 8.4 + Nginx + PostgreSQL + Redis + Node/Vite

## Requirements

- Docker
- Docker Compose

## Start project

Clone:

```bash
git clone git@github.com:DmitryBDA/laravel-project.git
cd laravel-project

docker compose build

docker compose exec php composer install

cp src/.env.example src/.env

docker compose exec php php artisan key:generate

docker compose exec php php artisan migrate

docker compose exec node npm install

docker compose up -d node


---

# Шаг 42. Commit и push

Проверяем:

```bash
git status
