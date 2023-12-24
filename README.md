#   Дипломный проект по теме ОВ2 - Платформа для публикации платного контента

# Для запуска проетка через docker необходимо выполнить ниже указанную команду и заполнить файл .env_sample
`docker-compose up -d --build`

1. Установить виртуальное окружение
```bash
python3 -m venv env
```
2. Активировать виртуальное окружение
```bash
source venv\bin\activate.bat
```
3. Установить зависимости проекта, указанные в файле `requirements.txt`
```bash
pip install -r requirements.txt
```
6. Установить PostreSQL
```bash
pip install postgresql
```
7. Выполнить вход
```bash
psql -U postgres
```
8. Cоздать базу данных 
с помощью следующей команды:
```bash
CREATE DATABASE content;
```
9. Выйти
```bash
\q
```
10. Создать файл `.env` 
11. Записать в файл настройки, как в .env_sample

12. Создать и применить миграции

```bash
python manage.py makemigrations
```
```bash
python manage.py migrate
```
13. Загрузить данные
```bash
python manage.py loaddata data.json
```
14. Запустить сервер
```bash
python manage.py runserver
```

# Применяемый стэк
- python
- postgresql
- django
- docker

Платежи осуществляются через `Strip`

Тестовые данные из БД залиты в файл data.json
Заполнить данные можно с помощью комманды: **python -Xutf8 manage.py loadpdata data.json**



**Задача**

Реализовать платформу для публикации записей пользователями. 
Публикация может быть бесплатной, то есть доступной любому пользователю без регистрации, либо платной, 
которая доступна только авторизованным пользователям, который оплатили разовую подписку. 
Для реализации оплаты подписки использовался Stripe. Регистрация пользователя должна быть по номеру телефона.


**Итог:**
1. Использовались переменные окружения.
2. Все необходимые модели описаны или переопределены.
3. Все необходимые эндпоинты реализованы.
4. Описанны права доступа и заложены.
5. Проект покрыть тестами как минимум на 70%.
6. Код оформлен в соответствии с лучшими практиками.
7. Имеется список зависимостей.
8. Результат проверки Flake8 равен 100%, при исключении миграций.
9. Решение выложено на GitHub.


`**Модели**`

## Публикации (Content):
* name — наименование публикации.
* description — тест публикации.
* image — необходимые изображения в статье.
* paid — булевое поле, определяющее бесплатная или платная публикация.
* price — стоимость подписки на публикацию.
* date_creation — дата публикации статьи.
* date_change — дата последних изменений внесенных в публикацию.
* number_views — количество просмотров.
* is_publication — флаг, определяющий опубликована статья или нет.
* author — автор публикации.


## Подписка (Subscription):
* publication — id публикации, на которую подписался пользователь.
* user — подписчик (пользователь).
* is_active — флаг активности подписки.
* payments — платеж за подписку.


## Платежи (Payments):
* publication — id публикации, за которую оплатил пользователь.
* user — подписчик (пользователь).
* date — дата оплаты.


## Контакты(пользователь может оставить контакты для связи с ним) (Contact):
* name — имя пользователя.
* phone — телефон пользователя.
* message — сообщение.


## User:
* email — электронная почта пользователя.
* phone — телефон пользователя (необходим для входа и регистрации).
* password — пароль.
* avatar - аватар.
* first_name - имя пользователя
* last_name - фамилия пользователя
* city - город


## Права доступа
* Бесплатные публикации могут смотреть все, в т.ч. пользователи без регистрации.
* Платные подписки доступны авторизованным пользователям, которые оплатили подписку.
* Пользователь может видеть список только своих платежей и подписок, список публикаций.
* Редактировать и удалять публикации могут только автор публикации или администратор.

## Эндпоинты

* Регистрация
* Авторизация
* Список публикаций
* Список платежей
* Список подписок
* Создание публикации
* Редактирование публикации
* Удаление публикации
* Создание платежей
* Создание подписок


```Для запуска тестов и расчета покрытия исполуем следующие команды

python manage.py test --pattern="test_*.py" 

coverage run --source='.' manage.py test --pattern="test_*.py"

coverage report

```

