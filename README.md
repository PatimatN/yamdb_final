![example workflow](https://github.com/PatimatN/yamdb_final/actions/workflows/main.yml/badge.svg)

# Докеризация API YaMDb. База отзывов о фильмах, книгах и музыке.

## Развертывание

### Шаг первый. Сборка контейнера
```
docker-compose build
```

### Шаг третий. Запуск контейнера
```
docker-compose up
```

### Шаг четвертый. База данных
```
docker-compose run web python manage.py migrate --no-input
```


## Использование

### Создание суперпользователя Django
```
docker-compose run web python manage.py createsuperuser
```

### Импорт данных в формате .json
```
docker-compose run web python manage.py loaddata path/to/your/json
```
#### Пример инициализации стартовых данных:
```
docker-compose run web python manage.py loaddata fixtures/fixture.json
```


## Выключение контейнера
```
docker-compose down
```


## Удаление всех Docker контейнеров
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```
