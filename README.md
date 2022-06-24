## YaMDb - сервис отзывов на произведения

[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org/)
[![SQLite](https://img.shields.io/badge/-SQLite-464646?style=flat-square&logo=SQLite)](https://www.sqlite.org/index.html)


Сервис собирает отзывы пользователей на различные произведения в категориях: «Книги», «Фильмы», «Музыка». Список категорий может быть расширен администратором. Также произведению может быть присвоен жанр из списка предустановленных, либо добавленный администратором. Пользователи оставляют к произведениям отзывы и ставят  оценку; из пользовательских оценок формируется рейтинг произведения. На одно произведение пользователь может оставить только один отзыв. Взаимодействие с сервисом реализовано с помщью API.

### Запуск проекта на локальной машине

Склонировать файлы проекта:
```
git clone https://github.com/elvir906/yamdb
```
Перейти в директорию с проектом:
```
cd api_yamdb
```

Cоздать и активировать виртуальное окружение:
```
python -m venv venv
```
```
source venv/Scripts/activate
```

Установить зависимости из файла requirements.txt:
```
pip install -r requirements.txt
```

Выполнить миграции:
```
python manage.py migrate
```

Запустить проект:
```
python manage.py runserver
```

### Описание API

Для ознакомления с API следует открыть ReDoc.

Для этого запустите сервер командой:
```
python manage.py runserver
```

В окне браузера откройте страницу по адресу:
```
http://127.0.0.1:8000/redoc/
```

### Наполнение базы данных из файлов *.csv

Проект имеет возможность с помощью специальной команды наполнить БД данными из файлов *.csv
Данный способ хорош тем, что данные для заполнения можно подготовить даже в приложении "Блокнот",
а наполнение осуществляется одной командой в консоли терминала.

Для начала необходимо проверить, чтобы имена csv-файлов с данными были следующими:
```
category.csv
comments.csv
genre_title.csv
genre.csv
reviews.csv
titles.csv
users.csv
```

Скрипт чувствителен к данным именам, но при необходимости можно поменять их
в самом скрипте, в значениях словаря 'paths'.
Располагаться файлы должны в директории static/data/.
Для корректной работы БД необходимо убедиться, что все поля таблиц заполнены.

Для заполнения БД выполните команду:
```
python manage.py csv_to_base
```

Сообщение 'Успешно! Данные из *.csv теперь в базе.' означает, что данные перенесены успешно.

Файл со скриптом находится в директории reviews/management/commands/

### Запуск приложения в контейнерах

Склонируйте репозиторий на свой диск. В директории infra/ создайте файл .env, в котором опишите переменные:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME= #название БД
POSTGRES_USER= #ваше имя пользователя
POSTGRES_PASSWORD= #пароль для доступа к БД
DB_HOST=db
DB_PORT=5432
```

Из директории infra/ соберите образ командой:
```
docker-compose up -d --build
```

Выполните миграции:
```
docker-compose exec web python manage.py migrate
```

Соберите статику:
```
docker-compose exec web python manage.py collectstatic --no-input
```

Зарегистрируйте суперюзера:
```
docker-compose exec web python manage.py createsuperuser
```

### Авторы проекта:

Эльвир Давлетгареев [elvir906](https://github.com/elvir906), Абрамсон Арсений [ArS181](https://github.com/ArS181), Антон Лукин [AntonLukin1986](https://github.com/AntonLukin1986)
