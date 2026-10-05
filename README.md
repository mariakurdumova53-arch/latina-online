# LATINA — профессиональная онлайн-платформа

## Возможности
- регистрация и вход студентов по email/паролю;
- роли `student` и `teacher`;
- серверное хранение результатов;
- PostgreSQL в production, SQLite для локальной разработки;
- история результатов студента;
- панель преподавателя со статистикой;
- добавление/скрытие вопросов;
- импорт вопросов из Excel;
- экспорт вопросов в CSV;
- CSRF-защита форм;
- хеширование паролей;
- HttpOnly/SameSite cookies;
- Docker + Gunicorn;
- 166 вопросов из исходной таблицы (вопросы без корректного ключа ответа не импортируются до исправления).

## Быстрый запуск
```bash
cp .env.example .env
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
python -m flask --app app:create_app run --debug
```
Откройте http://127.0.0.1:5000

## Production через Docker
1. Скопируйте `.env.example` в `.env`.
2. Обязательно задайте длинные уникальные `SECRET_KEY` и `ADMIN_PASSWORD`.
3. Измените пароль PostgreSQL в `docker-compose.yml`.
4. Настройте домен и HTTPS на reverse proxy/облачной платформе.
5. Запустите:
```bash
docker compose up -d --build
```

### Переменные
- `SECRET_KEY` — секрет Flask-сессий.
- `DATABASE_URL` — PostgreSQL URL в production.
- `ADMIN_EMAIL`, `ADMIN_PASSWORD` — первоначальный аккаунт преподавателя.
- `COOKIE_SECURE=1` — включить для HTTPS.

## Публикация
Проект можно развернуть на любой платформе, которая поддерживает Docker/Python + PostgreSQL. Нужны:
- web service с Docker;
- PostgreSQL;
- HTTPS;
- постоянное хранение базы;
- секреты через environment variables.

После запуска войдите под `ADMIN_EMAIL`/`ADMIN_PASSWORD`, затем создавайте/импортируйте вопросы через `/admin`.

## Безопасность
Перед публичным запуском замените все демонстрационные значения. Не храните `.env` в Git. Для production используйте HTTPS и PostgreSQL.
