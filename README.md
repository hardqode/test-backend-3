
# Тестовое задание Django/Backend

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray) ![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)

Проект представляет собой площадку для размещения онлайн-курсов с набором уроков. Доступ к урокам предоставляется после покупки курса (подписки). Внутри курса студенты автоматически распределяются по группам.

Перед тем, как приступить к выполнению задания, советуем изучить документацию, которая поможет в выполнении заданий:

1. https://docs.djangoproject.com/en/4.2/intro/tutorial01/
2. https://docs.djangoproject.com/en/4.2/topics/db/models/
3. https://docs.djangoproject.com/en/4.2/topics/db/queries/
4. https://docs.djangoproject.com/en/4.2/ref/models/querysets/
5. https://docs.djangoproject.com/en/4.2/topics/signals/
6. https://www.django-rest-framework.org/tutorial/quickstart/
7. https://www.django-rest-framework.org/api-guide/viewsets/
8. https://www.django-rest-framework.org/api-guide/serializers/

# Построение системы для обучения

Суть задания заключается в проверке знаний построения связей в БД и умении правильно строить запросы без ошибок N+1.

### Построение архитектуры(5 баллов)

В этом задании у нас есть 4 бизнес-задачи на хранение:

1. Создать сущность продукта. У продукта должен быть создатель этого продукта(автор/преподаватель). Название продукта, дата и время старта, стоимость. **(0,5 балла)**
2. Определить, каким образом мы будем понимать, что у пользователя(клиент/студент) есть доступ к продукту. **(2 балла)**
3. Создать сущность урока. Урок может принадлежать только одному продукту. В уроке должна быть базовая информация: название, ссылка на видео. **(0,5 балла)**
4. Создать сущность баланса пользователя. Баланс пользователя не может быть ниже 0, баланс пользователя при создании пользователя равен 1000 бонусов. Бонусы могут начислять только через админку или посредством REST-апи с правами is_staff=True. **(2 балла)**

### Реализация базового сценария оплат (11 баллов)

В этом пункте потребуется использовать выполненную вами в прошлом задании архитектуру:

1. Реализовать API на список продуктов, доступных для покупки(доступных к покупке = они еще не куплены пользователем и у них есть флаг доступности), которое бы включало в себя основную информацию о продукте и количество уроков, которые принадлежат продукту. **(2 балла)**
2. Реализовать API оплаты продукты за бонусы. Назовем его …/pay/ **(3 балла)**
3. По факту оплаты и списания бонусов с баланса пользователя должен быть открыт доступ к курсу. **(2 балла)**
4. После того, как доступ к курсу открыт, пользователя необходимо **равномерно** распределить в одну из 10 групп студентов. **(4 балла)**

### Результат выполнения:

1. Выполненная архитектура на базе данных SQLite с использованием Django.
2. Реализованные API на базе готовой архитектуры.

### Мы ожидаем:

Ссылка на публичный репозиторий в GitHub с выполненным проектом.

** Нельзя форкать репозиторий. Используйте git clone. **



## Если вы все сделали, но хотите еще, то можете реализовать API для отображения статистики по продуктам. 
Необходимо отобразить список всех продуктов на платформе, к каждому продукту приложить информацию:

1. Количество учеников занимающихся на продукте.
2. На сколько % заполнены группы? (среднее значение по количеству участников в группах от максимального значения участников в группе, где максимальное = 30).
3. Процент приобретения продукта (рассчитывается исходя из количества полученных доступов к продукту деленное на общее количество пользователей на платформе).

За это задание не ставится баллов, но при выборе между 2 кандидатами - оно нам поможет.


## __Установка на локальном компьютере__
1. Клонируйте репозиторий:
    ```
    git clone git@github.com:hqcamp/test-backend-3.git
    ```
2. Установите и активируйте виртуальное окружение:
    ```
    python -m venv venv
    source venv/Scripts/activate  - для Windows
    source venv/bin/activate - для Linux
    ```
3. Установите зависимости:
    ```
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```
4. Перейдите в папку product и выполните миграции:
    ```
    cd product
    python manage.py migrate
    ```
5. Создайте суперпользователя:
    ```
    python manage.py createsuperuser
    ```
6. Запустите проект:
    ```
    python manage.py runserver
    ```

### __OpenAPI документация__
* Swagger: http://127.0.0.1:8000/api/v1/swagger/
* ReDoc: http://127.0.0.1:8000/api/v1/redoc/


## Доп. задание
### __Реализуйте следующее API__

<details><summary> GET: http://127.0.0.1:8000/api/v1/courses/  - показать список всех курсов.</summary>

    200 OK:
    ```
    [
        {
            "id": 3,
            "author": "Михаил Потапов",
            "title": "Backend developer",
            "start_date": "2024-03-03T12:00:00Z",
            "price": "150000",
            "lessons_count": 0,
            "lessons": [],
            "demand_course_percent": 0,
            "students_count": 0,
            "groups_filled_percent": 0
        },
        {
            "id": 2,
            "author": "Михаил Потапов",
            "title": "Python developer",
            "start_date": "2024-03-03T12:00:00Z",
            "price": "120000",
            "lessons_count": 3,
            "lessons": [
                {
                    "title": "Урок №1"
                },
                {
                    "title": "Урок №2"
                },
                {
                    "title": "Урок №3"
                }
            ],
            "demand_course_percent": 84,
            "students_count": 10,
            "groups_filled_percent": 83
        },
        {
            "id": 1,
            "author": "Иван Петров",
            "title": "Онлайн курс",
            "start_date": "2024-03-03T12:00:00Z",
            "price": "56000",
            "lessons_count": 3,
            "lessons": [
                {
                    "title": "Урок №1"
                },
                {
                    "title": "Урок №2"
                },
                {
                    "title": "Урок №3"
                }
            ],
            "demand_course_percent": 7,
            "students_count": 1,
            "groups_filled_percent": 10
        }
    ]
    ```
</details>


<details><summary> GET: http://127.0.0.1:8000/api/v1/courses/2/groups/  - показать список групп определенного курса.</summary> 

    200 OK:
    ```
    [
        {
            "title": "Группа №3",
            "course": "Python developer",
            "students": [
                {
                    "first_name": "Иван",
                    "last_name": "Грозный",
                    "email": "user9@user.com"
                },
                {
                    "first_name": "Корней",
                    "last_name": "Чуковский",
                    "email": "user8@user.com"
                },
                {
                    "first_name": "Максим",
                    "last_name": "Горький",
                    "email": "user7@user.com"
                }
            ]
        },
        {
            "title": "Группа №2",
            "course": "Python developer",
            "students": [
                {
                    "first_name": "Ольга",
                    "last_name": "Иванова",
                    "email": "user6@user.com"
                },
                {
                    "first_name": "Саша",
                    "last_name": "Иванов",
                    "email": "user5@user.com"
                },
                {
                    "first_name": "Дмитрий",
                    "last_name": "Иванов",
                    "email": "user4@user.com"
                }
            ]
        },
        {
            "title": "Группа №1",
            "course": "Python developer",
            "students": [
                {
                    "first_name": "Андрей",
                    "last_name": "Петров",
                    "email": "user10@user.com"
                },
                {
                    "first_name": "Олег",
                    "last_name": "Петров",
                    "email": "user3@user.com"
                },
                {
                    "first_name": "Сергей",
                    "last_name": "Петров",
                    "email": "user2@user.com"
                },
                {
                    "first_name": "Иван",
                    "last_name": "Петров",
                    "email": "user@user.com"
                }
            ]
        }
    ]
    ```
</details>

### __Технологии__
* [Python 3.10.12](https://www.python.org/doc/)
* [Django 4.2.10](https://docs.djangoproject.com/en/4.2/)
* [Django REST Framework  3.14.0](https://www.django-rest-framework.org/)
* [Djoser  2.2.0](https://djoser.readthedocs.io/en/latest/getting_started.html)
