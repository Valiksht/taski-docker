# taski
#  Описание

## О проекте
taski - сервис помогающий отслеживать задачи и отмечать их выполнение.

## Клонирование репозитория
Клонирование репозитория командой в терминале:
git clone https://github.com/Valiksht/taski-docker.git
или
git clone git@github.com:Valiksht/taski-docker.git

## CD/CI
### код CD/CI для развертывания находится в папке .github/workflows в файле main.yml
для работы CD/CI необходимо установить следующие секреты в hithub:
DOCKER_PASSWORD - пароль от аккаунта Docker
DOCKER_USERNAME - логин от аккаунта Docker
HOST - id адрес сервера
USER - имя пользователя для доступа к серверу
SSH_KEY - ssh ключ для доступа к серверу
SSH_PASSPHRASE - пароль от ssh ключа
TELEGRAM_TO - id аккаунта телеграм для отправки уведомлений
TELEGRAM_TOKEN - токен телеграм бота

### После развертывания проекта для доступа в admin зону необходимо создать суперпользователя:
Находясь в папке с проектом taski/ (корневой папки проекта, в которой находится файл docker-compose) необходимо выполнить команду:
sudo docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser


## Создание файла .env
### в папке с проектом taski/ (корневой папки проекта, в которой находится файл docker-compose) необходимо создать файл .env с переменными окружения:
POSTGRES_DB = логин для базы данных
POSTGRES_USER = логин пользователя базы данных
POSTGRES_PASSWORD = пароль пользователя базы данных
DB_NAME = название бызы данных
DB_HOST = db
DB_PORT = порт для базы данных, по умолчанию - 5432
ALLOWED_HOSTS_ID='id сервера'


## Запуск проекта локально через docker conteiner
### для запуска проекта локально через docker conteiner необходимо находясь в корневой папке выполнить команды:
docker-compose build
docker-compose up
### копирование и перенос статики:
docker compose exec backend python manage.py collectstatic
docker composeexec backend cp -r /app/collected_static/. /backend_static/static/
### создание суперпользователя:
docker-compose exec backend python manage.py createsuperuser

## Запуск проекта локально без docker conteiner
### создание виртуального окружения:
python3 -m venv venv
### активация виртуального окружения:
source venv/bin/activate
### перейти в папку с backend проектом:
cd backend
### установка зависимостей:
pip install -r requirements.txt
### создание суперпользователя:
python manage.py createsuperuser
### создание миграций:
python manage.py makemigrations
### Применение миграций:
python manage.py migrate
### запуск проекта:
python manage.py runserver
