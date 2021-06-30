![example workflow](https://github.com/PatimatN/yamdb_final/actions/workflows/main.yml/badge.svg)

API развернут по адресу http://130.193.54.64/api/v1/
# Докеризация API YaMDb. База отзывов о фильмах, книгах и музыке.
С Docker, Continuous Integration на GitHub Actions

### Алгоритм регистрации пользователей
* Пользователь отправляет запрос с параметром email на /auth/email/.
* YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email .
* Пользователь отправляет запрос с параметрами email и confirmation_code на /auth/token/, в ответе на запрос ему приходит token (JWT-токен).
* При желании пользователь отправляет PATCH-запрос на /users/me/ и заполняет поля в своём профайле (описание полей — в документации). Полная документация API (redoc.yaml)

## Деплой на удаленный сервер
Для запуска проекта на удаленном сервере необходимо:

* скопировать на сервер файлы docker-compose.yaml, .env и папку nginx командами:
```
scp docker-compose.yaml  <user>@<server-ip>:
scp .env <user>@<server-ip>:
scp -r nginx/ <user>@<server-ip>:
```
* создать переменные окружения в разделе secrets настроек текущего репозитория:
```
DOCKER_PASSWORD # Пароль от Docker Hub
DOCKER_USERNAME # Логин от Docker Hub
HOST # Публичный ip адрес сервера
USER # Пользователь зарегистрированный на сервере
PASSPHRASE # Если ssh-ключ защищен фразой-паролем
SSH_KEY # Приватный ssh-ключ
TELEGRAM_TO # ID телеграм-аккаунта
TELEGRAM_TOKEN # Токен бота
```

### После каждого обновления репозитория (git push) будет происходить:
1. Проверка кода на соответствие стандарту PEP8 (с помощью пакета flake8) и запуск pytest из репозитория yamdb_final
2. Сборка и доставка докер-образов на Docker Hub.
3. Автоматический деплой.
4. Отправка уведомления в Telegram.

