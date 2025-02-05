Лабораторная работа №4
---
___Тема:___ Проектирование REST API
___Цель работы:___ Получить опыт проектирования программного интерфейса.

Документация по API
---

1. ___Регистрация нового пользователя___
   
    Эндпоинт: /api/register/
    Метод: POST
    Описание: Регистрация нового пользователя.
    Тип данных (Headers): application/json
    Запрос:
    ```json
    {
    "email": "test@example.com",
    "name": "Иван",
    "surname": "Иванов",
    "username": "ivan123",
    "password": "secure_password",
    "gender": "Мужской",
    "birthdate": "2000-01-01"
    }
    ```
    Ответы:
    - Код ответа 201 Created: Пользователь успешно зарегистрирован.
    ```json
    {
    "id": null,
    "identifier": "60b858aa-3b5d-4d2f-a234-ffb6aa82a068",
    "name": "Иван",
    "surname": "Иванов",
    "username": "ivan123",
    "password": "pbkdf2_sha256$720000$h8RZCYePmnCihLVvAZRg5D$ZrmJj/eAedWUQ1NnY1l3aPxRSLh+JZW5YAio3VFnnAQ=",
    "email": "test@example.com",
    "gender": "Мужской",
    "age": 25,
    "birthdate": "2000-01-01",
    "photo": null
    }
    ```
    - Код ответа 400 Bad Request: Некорректные данные в запросе/Ошибка валидации данных.
    ```json
    {
    "email": [
        "This field may not be blank."
    ]
    }
    ```
    - Код ответа 401 Unauthorized: Имя пользователя или почта уже используются.
    ```json
    {
    "error": "Username already exists"
    }
    ```
    или
    ```json
    {
    "error": "Email already exists"
    }
    ```
2. ___Авторизация пользователя___
   Эндпоинт: /api/login/
   Методы: POST, GET
   Описание: Авторизация пользователя.
   Тип данных (Headers): application/json
   Запрос:
   Отладочный запрос
   Ответ:
   ```json
    [
    {
        "id": 1,
        "identifier": "7a0495a0-2daf-4042-ad18-00fe8d1dcbb4",
        "name": "Артем",
        "surname": "Полозников",
        "username": "Clonn123",
        "password": "pbkdf2_sha256$720000$ecCWLqiYAAJ3kR4D6VIloz$KaZ+N6zTjw95XFfNtxLAAR3Yy9TLSpOFj3MwaMVNEzY=",
        "email": "art-clon@mail.ru",
        "gender": "Мужской",
        "age": 21,
        "birthdate": "2002-11-29",
        "photo": null
    },
    {
        "id": 2,
        "identifier": "42f2928a-c35e-4693-913b-7ab3b4c183b0",
        "name": "Андрей",
        "surname": "Смирнов",
        "username": "Gifon",
        "password": "pbkdf2_sha256$720000$yDwmbCcEIuK4GlH1a0sEL1$i/j5FpYQK+5NoGmCEMdQ5nhzLYno1ecxws8tZenhlDI=",
        "email": "andryushka-smirnov-72@mail.ru",
        "gender": "Мужской",
        "age": 21,
        "birthdate": "2002-10-29",
        "photo": null
    },
    {
        "id": 13,
        "identifier": "05140036-842b-4172-a407-47fc8dfa04e6",
        "name": "Fake",
        "surname": "Fake",
        "username": "Clonnolc",
        "password": "pbkdf2_sha256$720000$ixBvF6bne29D0G1auZrntg$GKA/+0DiZn73hgjlEs0pmbOeSXU46Y8bjTMkl2DdTNA=",
        "email": "Clonnolc",
        "gender": "Мужской",
        "age": 7,
        "birthdate": "2016-05-11",
        "photo": null
    },
    ]
    ```
    Запрос:
    ```json
    {
    "username": "Clonn123",
    "password": "Clonn123"
    }
    ```
    Ответы:
    - Код ответа 200 OK: Авторизация успешна.
    ```json
    {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzM4MDgyNTA0LCJpYXQiOjE3MzgwODE2MDQsImp0aSI6IjI5NDJjNGZmYTM2MjQ1Y2ViODE3ZWNkM2ZjZWEwMjhkIiwidXNlcl9pZCI6MX0.FzXmn41V3hLh76UW55fNl6tzWlMdLgMmXMtXsT6ebX4"
    }
    ```
    - Код ответа 401 Unauthorized: Неверные данные для входа.
    ```json
    {
    "error": "Invalid credentials"
    }
    ```
3. ___Получение информации о пользователе___
   Эндпоинт: /api/user/<int:user_id>/
   Метод: GET
   Описание: Получить информацию о пользователе по его ID.
   Тип данных (Headers): application/json
   Запрос:
   Параметры URL:
   - user_id — ID пользователя.
   Ответы:
   - Код ответа 200 OK: Информация о пользователе.
   ```json
    {
    "id": 1,
    "identifier": "7a0495a0-2daf-4042-ad18-00fe8d1dcbb4",
    "name": "Артем",
    "surname": "Полозников",
    "username": "Clonn123",
    "password": "pbkdf2_sha256$720000$ecCWLqiYAAJ3kR4D6VIloz$KaZ+N6zTjw95XFfNtxLAAR3Yy9TLSpOFj3MwaMVNEzY=",
    "email": "art-clon@mail.ru",
    "gender": "Мужской",
    "age": 21,
    "birthdate": "2002-11-29",
    "photo": null
    }
    ```
   - Код ответа 404 Not Found: Пользователь не найден.
   ```json
    {
    "error": "Users matching query does not exist."
    }
    ```
4. ___Рекомендации для манги___
   Эндпоинт: /api/rec/manga/
   Метод: GET
   Описание: Получить рекомендации для аниме на основе выбранного алгоритма (например, CBF).
   Тип данных (Headers): application/json
   Запрос:
   Параметры URL:
   - id_user — ID пользователя.
   - pageNumber — номер страницы (опционально).
   - method — метод фильтрации (например, "CBF").
   ```json
    {
    "GET /api/rec/manga/?id_user=1&pageNumber=1&method=CBF"
    }
    ```
   Ответы:
   - Код ответа 200 OK: Список рекомендаций.
   ```json
    [
    {
        "manga_id": 125036,
        "type": "Манхва",
        "title_ru": "Горизонт ",
        "url_img": "https://desu.shikimori.one/uploads/poster/mangas/125036/main_2x-1135c3a65315cdf4eb4010141ee619ac.webp",
        "data": "2016",
        "score_real": 8.67,
        "episodes": 21,
        "Genres": "Приключения, Драма",
        "Themes": "Психологическое"
    },
    {
        "manga_id": 30,
        "type": "Манга",
        "title_ru": "Клуб свиданий старшей школы Оран ",
        "url_img": "https://desu.shikimori.one/uploads/poster/mangas/30/main_2x-cc23eea1495af99fb7d92124dfed7740.webp",
        "data": "2002",
        "score_real": 8.5,
        "episodes": 87,
        "Genres": "Сёдзё, Комедия, Драма, Романтика",
        "Themes": "Кроссдрессинг, Реверс-гарем, Школа"
    },
    {
        "manga_id": 21525,
        "type": "Манга",
        "title_ru": "Йона на заре ",
        "url_img": "https://desu.shikimori.one/uploads/poster/mangas/21525/main_2x-17dd67641200d5addd689a3ebd62a02c.webp",
        "data": "2009",
        "score_real": 8.82,
        "episodes": 1,
        "Genres": "Сёдзё, Экшен, Приключения, Фэнтези, Романтика",
        "Themes": null
    },
    ]
    ```
   - Код ответа 400 Bad Request: Ошибка запроса.
   ```json
    {
        "error": "Invalid parameters"
    }
    ```
5. ___Список манги___
   Эндпоинт: /api/manga-list/
   Метод: POST
   Описание: Получение списка манги.
   Тип данных (Headers): application/json
   Запрос:
   ```json
    {
    "codeInUrl": "authorization_code",
    "userId": 123
    }
    ```
    - codeInUrl – авторизационный код, полученный после OAuth-авторизации.
    - userId – идентификатор пользователя в базе.
    Ответы:
    - Код ответа 200 OK: Список манги успешно получен.
    ```json
    {
    "manga_titles": [
        {
            "title": "One Piece",
            "score": 9,
            "status": "watching"
        },
        {
            "title": "Berserk",
            "score": 10,
            "status": "completed"
        }
    ]
    }
    ```
    - Код ответа 400 Bad Request: Не передан авторизационный код.
    ```json
    {
    "message": "Authorization code is missing"
    }
    ```
    - Код ответа 500 Internal Server Error: Ошибка получения токена доступа или списка манги.
    ```json
    {
    "message": "Failed to get access token"
    }
    ```
6. ___Мой список манги___
   Эндпоинт: /api/data/mylist-manga/<int:id>/<str:sort>/
   Методы: GET
   Описание: Получение списка манги, добавленной пользователем, с возможностью сортировки.
   Тип данных (Headers): application/json
   Запрос:
   ```json
    {
    "id": 123,
    "sort": "score"
    }
    ```
    - id – идентификатор пользователя в базе.
    - sort – поле, по которому выполняется сортировка (score, title_ru, descriptionData).
    Ответы:
    - Код 200 OK: Успешное получение списка манги.
    ```json
    [
    {
        "manga_list_id": 1,
        "url_img": "https://example.com/image1.jpg",
        "descriptionData": "2024-01-01",
        "descriptionEpisod": "Глава 100",
        "title_ru": "One Piece",
        "score": 9
    },
    {
        "manga_list_id": 2,
        "url_img": "https://example.com/image2.jpg",
        "descriptionData": "2023-05-15",
        "descriptionEpisod": "Глава 50",
        "title_ru": "Berserk",
        "score": 10
    }
    ]
    ```
        - manga_list_id – уникальный идентификатор манги в списке.
        - url_img – ссылка на изображение манги.
        - descriptionData – дата последнего обновления манги.
        - descriptionEpisod – описание текущего эпизода.
        - title_ru – название манги на русском.
        - score – оценка пользователя.

    - Код 400 Bad Request: Ошибка в параметрах запроса.
   ```json
    {
    "message": "Invalid sort parameter"
    }
    ```
    - Код 404 Not Found: Данные не найдены.
    ```json
    {
    "message": "User not found or no manga in list"
    }
    ```
    - Код 500 Internal Server Error: Ошибка на сервере.
    ```json
    {
    "message": "Internal server error"
    }
    ```
7. ___Проставление оценки манги___
   Эндпоинт: /api/score-manga/
   Методы: PUT
   Описание: Установка или обновление оценки манги пользователем.
   Тип данных (Headers): application/json
   Запрос:
   ```json
    {
    "manga_id": 456,
    "user_id": 123,
    "score": 9,
    "status": "completed"
    }
    ```
    - manga_id – идентификатор манги.
    - user_id – идентификатор пользователя.
    - score – оценка (от 1 до 10).
    - status – статус манги (completed, watching, planned и др.).

    Ответы:
    - Код 200 OK: Оценка успешно установлена или обновлена.
   ```json
    {
    "manga_id": 456,
    "user_id": 123,
    "score": 9,
    "status": "completed"
    }
    ```
    - Код 400 Bad Request: Ошибка валидации данных.
   ```json
    {
    "message": "Invalid score value"
    }
    ```
    - Код 500 Internal Server Error: Внутренняя ошибка сервера.
    ```json
    {
    "message": "Internal server error"
    }
    ```

8. Удаление манги из списка
    Эндпоинт: /api/manga/del
    Метод: DELETE
    Описание: Удаление манги из списка пользователя.
    Тип данных (Headers): application/json
    Запрос:
    ```json
    {
    "manga_id": 456,
    "user_id": 123
    }
    ```
    - manga_id – идентификатор манги.
    - user_id – идентификатор пользователя.
    Ответы:
    - Код 204 OK: Манга успешно удалена из списка.
    ```json
    {
    "message": "Объект успешно удален из списка"
    }
    ```
    - Код 404 Not Found: Манга с указанными параметрами не найдена в списке.
    ```json
    {
    "message": "Объект не найден"
    }
    ```
    - Код 500 Internal Server Error: Ошибка на сервере.
    ```json
    {
    "message": "Internal server error"
    }
    ```

Тестирование API
---
1. Регистрация нового пользователя
   Эндпоинт: /api/register/
    Метод: POST
    URL: http://127.0.0.1:8000/api/register/
    Тип данных: application/json
    ![alt text](image.png)
    ![alt text](image-1.png)
    ![alt text](image-2.png)
    ![alt text](image-3.png)
    ![alt text](image-4.png)
    ![alt text](image-5.png)
    
2. Авторизация пользователя
    Эндпоинт: /api/login/
    Методы: POST, GET
    URL: http://127.0.0.1:8000/api/login/
    Тип данных: application/json
    ![alt text](image-6.png)
    ![alt text](image-7.png)
    ![alt text](image-9.png)
    ![alt text](image-8.png)
    ![alt text](image-10.png)
    ![alt text](image-11.png)

3. Получение информации о пользователе
    Эндпоинт: /api/user/<int:user_id>/
    Метод: GET
    URL: http://127.0.0.1:8000/api/user/1/ (где 1 — ID пользователя)
    Тип данных: application/json
    ![alt text](image-12.png)
    ![alt text](image-13.png)
    ![alt text](image-14.png)

4. Рекомендации для манги
    Эндпоинт: /api/rec/manga/
    Метод: GET
    URL: http://127.0.0.1:8000/api/rec/manga/?id_user=1&pageNumber=1&method=CBF
    Тип данных: application/json
    ![alt text](image-15.png)
    ![alt text](image-16.png)
    ![alt text](image-17.png)

5. Список манги
    Эндпоинт: /api/manga-list/
    Метод: POST
    URL: http://127.0.0.1:8000/api/manga-list/
    Тип данных: application/json
    ![alt text](image-18.png)
    ![alt text](image-19.png)
    ![alt text](image-20.png)
    ![alt text](image-24.png)

6. Мой список манги
    Эндпоинт: /api/data/mylist-manga/<int:id>/<str:sort>/
    Метод: GET
    Тип данных: application/json
    URL: api/data/mylist-manga/123/-score/
    Параметры в URL:
    - id – идентификатор пользователя (например, 123).
    - sort – метод сортировки (например, -score для убывания, score для возрастания).
    ![alt text](image-21.png)
    ![alt text](image-22.png)
    ![alt text](image-23.png)

7. Проставление оценки манги
    Эндпоинт: /api/score-manga/
    Метод: PUT
    Тип данных: application/json
    ![alt text](image-25.png)
    ![alt text](image-26.png)
    ![alt text](image-27.png)

8. Удаление манги из списка
    Эндпоинт: /api/manga/del
    Метод: DELETE
    Тип данных: application/json
    URL: http://127.0.0.1:8000/api/manga/del
    Тело запроса:
    ```json
    {
        "manga_id": 456,
        "user_id": 123
    }
    ```
    ![alt text](image-28.png)
    ![alt text](image-29.png)
    ![alt text](image-30.png)