![Docker](https://img.shields.io/badge/Docker-2496ED?style=plastic&logo=Docker&logoColor=FFFFFF) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=plastic&logo=postgresql&logoColor=FFFFFF) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=plastic&logo=nginx&logoColor=FFFFFF) ![Python 3.7](https://img.shields.io/badge/Python-_>_3.7-3776AB?style=plastic&logo=python&logoColor=FFFFFF) ![Django-Yamdb Workflow](https://github.com/vegarus2013/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

Сайт развернут - http://yamdb.vegarus.su/api/v1/
Документация доступна по эндпойнту: http://yamdb.vegarus.su/redoc/

---

# API_YAMDB
_REST API проект для сервиса YaMDb — сбор отзывов о фильмах, книгах или музыке._

## _Описание_
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

---

## Как запустить проект:
1. Клонируем репозиторий и переходим в него
```bash
git clone https://github.com/vegarus2013/yamdb_final
```
2. Прежде чем запустить проект. Необходимо создать файл .env расположенный по пути **infra/.env** (не включен в текущий репозиторий).
**Шаблон наполнения:**
```env
DJANGO_SECRET_KEY=<Ваш секретный ключ Джанги>
DB_ENGINE=django.db.backends.postgresql
DB_HOST=db
DB_PORT=5432
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_NAME=postgres
```
3. Создаем и активируем виртуальное окружение
####  Windows
```bash
python -m venv venv
venv/Scripts/activate.bat
python -m pip install --upgrade pip
```
4. Ставим зависимости из requirements.txt
```bash
pip install -r requirements.txt
```
5. Переходим в папку с файлом docker-compose.yaml
```bash
cd infra
```
6. Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1)
```bash
docker-compose up -d --build
```
7. Выполняем по очереди
  * Выполнить миграцию
```bash
docker-compose exec web python manage.py migrate
```
  * Создать суперпользователя
```bash
docker-compose exec web python manage.py createsuperuser
```
  * Собрать статику
```bash
docker-compose exec web python manage.py collectstatic --no-input
```
 * Дамп локальной базы в проекте существет, для заполнения базы выполните команду
```bash
docker-compose exec web python manage.py loaddata fixtures.json
```
Остановка контейнера
```bash
docker-compose down -v
```

### Документация API YaMDb
Документация доступна по эндпойнту: http://localhost/redoc/