# 🐱 Kittygram

**Kittygram** — социальная сеть для обмена фотографиями любимых питомцев. Проект позволяет пользователям делиться фотографиями своих котов, указывать их достижения и просматривать питомцев других пользователей.

[![Main Kittygram workflow](https://github.com/eqsx000111/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/eqsx000111/kittygram_final/actions/workflows/main.yml)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/eqsx000111/kittygram_final)
[![Live Demo](https://img.shields.io/badge/Live-Demo-green?logo=world)](https://kittylovers.ddns.net)

> **📋 Для проверки проекта**: пользователь **Port-tf** добавлен как коллаборатор для доступа к репозиторию.

## 🚀 Функциональность

- **Регистрация и аутентификация** пользователей
- **Добавление питомцев** с фотографиями и описанием
- **Указание достижений** питомцев из предустановленного списка
- **Просмотр карточек** всех питомцев
- **RESTful API** для взаимодействия с фронтендом
- **Админ-панель** для управления контентом

## 🛠 Технологический стек

### Backend
- **Python 3.11**
- **Django 4.2** — веб-фреймворк
- **Django REST Framework** — для создания API
- **Djoser** — для аутентификации
- **PostgreSQL** — база данных
- **Gunicorn** — WSGI сервер

### Frontend
- **React** — пользовательский интерфейс
- **JavaScript (ES6+)**

### DevOps
- **Docker & Docker Compose** — контейнеризация
- **Nginx** — веб-сервер и прокси
- **GitHub Actions** — CI/CD пайплайн
- **DockerHub** — реестр образов

### Инфраструктура
- **Yandex Cloud** — хостинг
- **SSL-сертификаты** — безопасное соединение

## 📋 Требования

- Docker 20.10+
- Docker Compose 2.0+
- Git

## 🚀 Быстрый запуск

### 1. Клонирование репозитория

```bash
git clone https://github.com/eqsx000111/kittygram_final.git
cd kittygram_final
```

### 2. Создание файла окружения

Создайте файл `.env` в корне проекта:

```bash
# PostgreSQL настройки
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=your_secure_password
POSTGRES_DB=kittygram

# Django настройки
SECRET_KEY=your-super-secret-key-here-make-it-long-and-random
DEBUG=False
ALLOWED_HOSTS=127.0.0.1,localhost,your-domain.com

# База данных для Django
DB_ENGINE=django.db.backends.postgresql
DB_NAME=kittygram
DB_USER=kittygram_user
DB_PASSWORD=your_secure_password
DB_HOST=db
DB_PORT=5432
```

### 3. Запуск проекта

```bash
# Сборка и запуск контейнеров
docker compose -f docker-compose.production.yml up -d

# Выполнение миграций
docker compose -f docker-compose.production.yml exec backend python manage.py migrate

# Сборка статических файлов
docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic --noinput

# Создание суперпользователя (опционально)
docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser
```

### 4. Доступ к приложению

- **Основное приложение**: https://kittylovers.ddns.net/
- **Админ-панель**: https://kittylovers.ddns.net/admin/

## 🔧 Настройка переменных окружения

| Переменная | Описание | Пример |
|------------|----------|---------|
| `POSTGRES_USER` | Имя пользователя PostgreSQL | `kittygram_user` |
| `POSTGRES_PASSWORD` | Пароль для PostgreSQL | `secure_password123` |
| `POSTGRES_DB` | Имя базы данных | `kittygram` |
| `SECRET_KEY` | Секретный ключ Django | `django-insecure-...` |
| `DEBUG` | Режим отладки | `False` |
| `ALLOWED_HOSTS` | Разрешённые хосты | `localhost,127.0.0.1,domain.com` |
| `DB_ENGINE` | Движок базы данных | `django.db.backends.postgresql` |
| `DB_HOST` | Хост базы данных | `db` |
| `DB_PORT` | Порт базы данных | `5432` |

## 🔄 CI/CD Процесс

Проект настроен для автоматического развертывания через GitHub Actions:

1. **Тестирование** — запуск flake8 и pytest
2. **Сборка образов** — backend, frontend, gateway
3. **Публикация** в DockerHub
4. **Развертывание** на сервере
5. **Уведомления** в Telegram

### Секреты для GitHub Actions

Добавьте следующие секреты в настройках репозитория:

```
DOCKER_USERNAME=your_dockerhub_username
DOCKER_PASSWORD=your_dockerhub_token
HOST=your_server_ip
USERNAME=your_server_username  
KEY=your_private_ssh_key
TELEGRAM_TO=your_telegram_chat_id
TELEGRAM_TOKEN=your_bot_token
```

## 📁 Структура проекта

```
kittygram_final/
├── backend/                 # Django приложение
│   ├── cats/               # Основное приложение
│   ├── kittygram_backend/  # Настройки проекта
│   ├── Dockerfile          # Образ для backend
│   └── requirements.txt    # Python зависимости
├── frontend/               # React приложение
│   ├── src/               # Исходный код
│   ├── Dockerfile         # Образ для frontend
│   └── package.json       # Node.js зависимости
├── nginx/                 # Конфигурация Nginx
│   ├── Dockerfile         # Образ для gateway
│   └── nginx.conf         # Конфигурация сервера
├── docker-compose.production.yml  # Production окружение
└── .github/workflows/main.yml     # CI/CD пайплайн
```

## 🌐 API Эндпоинты

| Метод | URL | Описание |
|-------|-----|----------|
| `GET` | `/api/cats/` | Список всех котов |
| `POST` | `/api/cats/` | Добавить кота |
| `GET` | `/api/cats/{id}/` | Получить кота по ID |
| `PUT` | `/api/cats/{id}/` | Обновить кота |
| `DELETE` | `/api/cats/{id}/` | Удалить кота |
| `GET` | `/api/achievements/` | Список достижений |
| `POST` | `/api/users/` | Регистрация |
| `POST` | `/api/auth/token/login/` | Авторизация |

## 🧪 Тестирование

```bash
# Установка зависимостей для тестирования
pip install -r backend/requirements.txt

# Запуск линтера
flake8 backend/ --ignore=E501,F401

# Запуск тестов
pytest

# Запуск тестов с покрытием
pytest --cov=backend
```

## 📝 Разработка

### Локальная разработка

```bash
# Запуск в режиме разработки
docker compose up

# Применение миграций
docker compose exec backend python manage.py migrate

# Создание миграций
docker compose exec backend python manage.py makemigrations
```

### Полезные команды

```bash
# Просмотр логов
docker compose logs -f backend

# Доступ к контейнеру
docker compose exec backend bash

# Остановка всех сервисов
docker compose down

# Пересборка образов
docker compose build --no-cache
```

## 🤝 Вклад в проект

1. Форкните репозиторий
2. Создайте ветку для фичи (`git checkout -b feature/amazing-feature`)
3. Зафиксируйте изменения (`git commit -m 'Add amazing feature'`)
4. Отправьте в ветку (`git push origin feature/amazing-feature`)
5. Откройте Pull Request

## 📄 Лицензия

Этот проект распространяется под лицензией MIT. См. файл [LICENSE](LICENSE) для подробностей.

## 👤 Автор

**eqsx000111** - [GitHub](https://github.com/eqsx000111)

## 🙏 Благодарности

- [Яндекс Практикум](https://practicum.yandex.ru/) за обучение
- Сообщество Django за отличную документацию
- Всем контрибьюторам проекта

---

⭐ Поставьте звезду, если проект был полезен!