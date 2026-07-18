# Laravel Docker Environment

Полноценное окружение для разработки Laravel:

- PHP 8.4 FPM
- Laravel 13
- Nginx
- PostgreSQL 17
- Redis
- Node.js 22
- Vite
- Docker Compose

Проект подготовлен для локальной разработки через WSL + Docker.

---

## Требования

Перед началом должны быть установлены:

- Docker
- Docker Compose
- Git
- WSL2 (для Windows)

Проверка:

```bash
docker --version
docker compose version
git --version
```

---

# Быстрый запуск проекта

## 1. Клонирование репозитория

```bash
git clone git@github.com:DmitryBDA/laravel-project.git

cd laravel-project
```

---

# 2. Запуск Docker контейнеров

Собрать контейнеры:

```bash
docker compose build
```

Запустить:

```bash
docker compose up -d
```

Проверить:

```bash
docker ps
```

Должны работать контейнеры:

```
laravel_nginx
laravel_php
laravel_postgres
laravel_redis
laravel_node
```

---

# 3. Настройка Laravel

Перейти в папку проекта:

```bash
cd src
```

Создать файл окружения:

```bash
cp .env.example .env
```

Если `.env` отсутствует:

```bash
nano .env
```

Добавить:

```env
APP_NAME=Laravel
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8080

DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=secret

CACHE_STORE=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis

REDIS_HOST=redis
REDIS_PORT=6379
REDIS_PASSWORD=null
```

---

# 4. Установка PHP зависимостей

Из корня проекта:

```bash
docker compose exec php composer install
```

---

# 5. Генерация ключа Laravel

```bash
docker compose exec php php artisan key:generate
```

---

# 6. Миграции базы данных

```bash
docker compose exec php php artisan migrate
```

---

# 7. Установка Node зависимостей

```bash
docker compose exec node npm install
```

---

# 8. Запуск Vite

```bash
docker compose restart node
```

Проверить:

```bash
docker compose logs node
```

Ожидаемый результат:

```
VITE ready

Local:
http://localhost:5173
```

---

# Доступ к проекту

Laravel:

```
http://localhost:8080
```

Vite:

```
http://localhost:5173
```

PostgreSQL:

```
localhost:5432
```

Redis:

```
localhost:6379
```

---

# Docker команды

## Запустить проект

```bash
docker compose up -d
```

---

## Остановить проект

```bash
docker compose down
```

---

## Перезапустить контейнеры

```bash
docker compose restart
```

---

## Логи всех контейнеров

```bash
docker compose logs -f
```

---

## Логи Laravel/Nginx

```bash
docker compose logs -f nginx
```

```bash
docker compose logs -f php
```

---

## Войти в PHP контейнер

```bash
docker compose exec php bash
```

---

## Войти в Node контейнер

```bash
docker compose exec node sh
```

---

# Laravel команды

## Очистить кеш

```bash
docker compose exec php php artisan optimize:clear
```

---

## Миграции

```bash
docker compose exec php php artisan migrate
```

---

## Откат миграций

```bash
docker compose exec php php artisan migrate:rollback
```

---

## Создание контроллера

```bash
docker compose exec php php artisan make:controller ExampleController
```

---

## Создание модели

```bash
docker compose exec php php artisan make:model Example
```

---

# Redis проверка

Войти в Laravel:

```bash
docker compose exec php php artisan tinker
```

Проверка:

```php
Cache::put('test','redis works',60);

Cache::get('test');
```

Ответ:

```
redis works
```

---

# Структура проекта

```
laravel-project
│
├── docker
│   ├── nginx
│   │   └── default.conf
│   │
│   └── php
│       ├── Dockerfile
│       └── php.ini
│
├── src
│   ├── app
│   ├── artisan
│   ├── config
│   ├── database
│   ├── public
│   ├── resources
│   ├── routes
│   └── vendor
│
├── docker-compose.yml
├── README.md
└── .gitignore
```

---

# Используемые технологии

| Технология | Версия |
|---|---|
| PHP | 8.4 |
| Laravel | 13 |
| PostgreSQL | 17 |
| Redis | Alpine |
| Node.js | 22 |
| Nginx | Alpine |
| Docker | Compose |

---

# Git workflow

Получить изменения:

```bash
git pull
```

Создать новую ветку:

```bash
git checkout -b feature/example
```

Добавить изменения:

```bash
git add .
```

Commit:

```bash
git commit -m "Описание изменений"
```

Отправить:

```bash
git push origin feature/example
```

---

# Лицензия

Проект используется для разработки и обучения.
