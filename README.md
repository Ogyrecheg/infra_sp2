# Привет! 
 Это совместный проект трех разработчиков 17 когорты
Яндекс.Практикума: Овчарука Д., Коржова Д. и Шевченко А.

# Описание
Приложение позволяет оставлять отзывы о произведениях в различных категориях и жанрах, а также оставлять оценки произведениям и комментировать существующие отзывы.

В рамках проекта использовались следующие технологии:
##### Python 3.7
##### Django 2.2.16
##### PostgreSQl 13.0
##### DRF 3.12.4
##### GitHub
##### Nginx 1.21.3
##### Gunicorn 20.0.4
##### Docker 20.10.22

## Как развернуть проект на локальной машине:
Скопируйте проект из репозитория одного из авторов проекта:
```bash 
git clone https://github.com/Ogyrecheg/infra_sp2.git
```
Перейти в дерикторию скачанного проекта.
Создать и активировать virtual enviroment:
```bash
py -3.7 -m venv -venv
source venv/scripts/activate
```
При активированном virtual env скачать необходимые зависимости проекта:
```bash
(venv) pip install -r api_yamdb/requirements.txt
```
##### Установить докер на вашу машину ([туториал](https://docs.docker.com/engine/install/))
Запуск приложения из докер контейнера:
```bash
cd infra
docker-compose up -d --build
```
После сборки образов и создания - запуска контейнеров приложения необходимо произвести миграции в БД, создание суперюзера и сбор статики:
```bash
docker-compose exec web python manage.py makemigrations
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
Если все прошло успешно, попробуйте залогиниться в админ-панель django проекта по адресу:
http://localhost/admin/
Для того, чтобы наполнить БД записями выполните команды:
```bash
cd api_yamdb
python manage.py loaddata ../infra/fixtures.json
```