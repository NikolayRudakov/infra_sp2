# api_yamdb

#### **Об авторе:**


* Имя: Николай Рудаков	
* Род деятельности: Студент курса Яндекс.Практикум Python-разработчик
* Контакты: https://github.com/NikolayRudakov/


#### **Описание:**

Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха.
Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

---

#### **Установка/запуск**

Клонировать репозиторий и перейти в него.

```
git clone git@github.com:MNikolayRudakov/infra_sp2.git
cd infra_sp2
cd api_yamdb
```

Cоздать и активировать виртуальное окружение:

```
python -m venv env
source env/Scripts/activate 
python -m pip install --upgrade pip
```

Переходим в папку с файлом docker-compose.yaml:

```
cd infra
```

Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1):

```
docker-compose up -d --build
```

Выполняем миграции:

```
docker-compose exec web python manage.py makemigrations
docker-compose exec web python manage.py migrate
```

Создаем суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```

Собираем статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

Создаем дамп базы данных (нет в текущем репозитории):

```
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```

Останавливаем контейнеры:

```
docker-compose down -v
```

#### **Шаблон наполнения .env (не включен в текущий репозиторий) расположенный по пути infra/.env**

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

#### **Документация API YaMDb**

Документация доступна по эндпойнту: http://localhost/redoc/
