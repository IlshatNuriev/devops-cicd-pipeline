# DevOps CI/CD Pipeline

Учебный проект, демонстрирующий настройку CI pipeline для контейнеризированного приложения с использованием GitHub Actions, Docker Compose, Nginx и PostgreSQL.

## Описание

Проект показывает, как автоматизировать проверку приложения и инфраструктурного окружения при каждом push и pull request.

Pipeline выполняет следующие шаги:

- получает код из репозитория
- создает файл переменных окружения
- валидирует docker compose конфигурацию
- собирает контейнеры
- запускает окружение
- проверяет доступность приложения через endpoint /health
- завершает работу и удаляет окружение

## Архитектура приложения

```text
Client -> Nginx -> Flask App -> PostgreSQL
```

## Стек технологий

- GitHub Actions
- Docker
- Docker Compose
- Nginx
- Python Flask
- PostgreSQL

## Структура проекта

```text
.
├── .github/
│   └── workflows/
│       └── ci.yml
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── db/
│   └── init.sql
├── nginx/
│   └── default.conf
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

## Локальный запуск

Создать файл переменных окружения:

```bash
cp .env.example .env
```

Запустить проект:

```bash
docker compose up --build
```

Проверить работу приложения:

```bash
curl http://localhost:8080/
curl http://localhost:8080/health
curl http://localhost:8080/users
```

Остановить проект:

```bash
docker compose down
```

Удалить контейнеры и volume:

```bash
docker compose down -v
```

## CI pipeline

Workflow расположен в файле:

```text
.github/workflows/ci.yml
```

Pipeline запускается при:

- push в ветку main
- pull request в ветку main

## Что проверяет pipeline

- корректность docker compose конфигурации
- успешную сборку контейнеров
- успешный запуск сервисов
- доступность приложения по endpoint /health

## Как посмотреть результат

В GitHub:
- открыть вкладку Actions
- выбрать workflow CI Pipeline
- открыть последний запуск

## Полезные команды

Проверка compose-конфигурации:

```bash
docker compose config
```

Сборка сервисов:

```bash
docker compose build
```

Запуск окружения:

```bash
docker compose up -d
```

Просмотр контейнеров:

```bash
docker ps
```

Просмотр логов:

```bash
docker compose logs -f
```

Остановка и очистка:

```bash
docker compose down -v
```

## Что демонстрирует проект

- настройку CI через GitHub Actions
- автоматическую сборку контейнеризированного приложения
- автоматическую проверку доступности сервиса
- работу с инфраструктурным стеком в CI

## Возможные улучшения

- добавить публикацию Docker image в registry
- добавить этапы lint и unit tests
- добавить CD и деплой на удаленный сервер
- добавить уведомления о статусе pipeline

## Автор

Ильшат Нуриев  
https://github.com/IlshatNuriev