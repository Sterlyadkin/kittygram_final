## Описание проекта

Сайт с возможностью публикации фотографий котов и их достижений.

## Запуск проекта из образов с Docker hub

Для запуска необходимо на создать папку проекта, например `kittygram` и перейти в нее:

```bash
mkdir kittygram
cd kittygram
```

В папку проекта скачиваем файл `docker-compose.production.yml` и запускаем его:

```bash
sudo docker compose -f docker-compose.production.yml up
```

Произойдет скачивание образов, создание и включение контейнеров, создание томов и сети.

## Запуск проекта из исходников GitHub

Клонируем себе репозиторий: 

```bash 
git clone git@github.com:Sterlyadkin/kittygram_final.git
```

Выполняем запуск:

```bash
sudo docker compose -f docker-compose.yml up
```

## После запуска: Миграции, сбор статистики

После запуска необходимо выполнить сбор статистики и миграции бэкенда. Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается. 

```bash
sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/
```

И далее проект доступен на: 

```
http://localhost:9000/
```
## Необходимые переменные окружения

```bash
POSTGRES_USER= <Желаемое_имя_пользователя_базы_данных>
POSTGRES_PASSWORD= <Желаемый_пароль_пользователя_базы_данных>
POSTGRES_DB= <Желаемое_имя_базы_данных>
DB_HOST=
DB_PORT= 
SECRET_KEY = 
DEBUG = 
```

## Остановка оркестра контейнеров

В окне, где был запуск **Ctrl+С** или в другом окне:

```bash
sudo docker compose -f docker-compose.yml down
```

## Автор

Стерлядкин Владимир https://github.com/Sterlyadkin/