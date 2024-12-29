# README

## Задача хакатона: Разработка сервиса

## Описание
Создайте асинхронный RESTful API сервис, который позволяет пользователям регистрироваться, аутентифицироваться и управлять списком своих избранных фильмов. Необходимо интегрировать [Kinopoisk API Unofficial](https://kinopoiskapiunofficial.tech/) для получения информации о фильмах.

### Интеграция с внешним API
- Зарегистрируйтесь на Kinopoisk API Unofficial и получите бесплатный API ключ.
- Ознакомьтесь с условиями использования и ограничениями API.

## Эндпойнты вашего сервиса

1. **Регистрация пользователя**
   - `POST /register`
   - Регистрация нового пользователя с указанием имени пользователя и пароля.

2. **Авторизация пользователя**
   - `POST /login`
   - Аутентификация пользователя и получение JWT токена.

3. **Получение профиля пользователя**
   - `GET /profile`
   - Получение информации о текущем аутентифицированном пользователе.

4. **Поиск фильмов**
   - `GET /movies/search?query=НазваниеФильма`
   - Требует аутентификации.
   - Ищет фильмы по названию, используя эндпойнт:
     - `GET /api/v2.1/films/search-by-keyword`

5. **Получение деталей фильма**
   - `GET /movies/{kinopoisk_id}`
   - Требует аутентификации.
   - Получает подробную информацию о фильме по его Kinopoisk ID, используя эндпойнт:
     - `GET /api/v2.2/films/{kinopoisk_id}`

6. **Добавление фильма в избранное**
   - `POST /movies/favorites`
   - Требует аутентификации.
   - Добавляет фильм в список избранных пользователя по Kinopoisk ID.

7. **Удаление фильма из избранного**
   - `DELETE /movies/favorites/{kinopoisk_id}`
   - Требует аутентификации.
   - Удаляет фильм из списка избранных пользователя.

8. **Просмотр списка избранных фильмов**
   - `GET /movies/favorites`
   - Требует аутентификации.
   - Возвращает список избранных фильмов пользователя с подробной информацией.

## Требования к реализации

1. **Аутентификация и авторизация**
   - Реализуйте аутентификацию с использованием JWT.
   - Защитите эндпойнты `/profile` и все эндпойнты под `/movies/` от неавторизованного доступа.

2. **Работа с базой данных**
   - Используйте SQLAlchemy для взаимодействия с базой данных.
   - Безопасно сохраняйте информацию о пользователях (пароли должны быть захешированы).
   - Храните список избранных фильмов каждого пользователя в базе данных (Kinopoisk ID и необходимая информация о фильме).

3. **Логирование**:
   - Реализовать систему логирования, которая будет фиксировать все операции с данными.
   - Логи должны включать информацию о времени операции, типе операции и статусе выполнения.

4. **Сбор метрик**:
   - Разработать механизм для сбора и хранения метрик производительности системы.
   - Метрики должны включать время обработки запросов, количество операций в секунду и использование ресурсов.

5. **Взаимодействие с внешним API**
   - Используйте Aiohttp, Httpx или Aiosonic для выполнения асинхронных HTTP-запросов напрямую.

6. **Обработка данных**
   - При поиске фильмов отправляйте запрос к эндпойнту `/api/v2.1/films/search-by-keyword` и возвращайте результаты.
   - При получении деталей фильма используйте эндпойнт `/api/v2.2/films/{kinopoisk_id}`.
   - При добавлении фильма в избранное сохраняйте информацию о фильме в базе данных.
   - При просмотре списка избранных фильмов возвращайте детальную информацию о каждом фильме.

7. **Безопасность**
   - Хэшируйте пароли перед сохранением в базу данных.
   - Обрабатывайте исключения и избегайте утечки подробных технических деталей во внешние сообщения об ошибках.

8.  **Тестирование**
    - Покрыть функционал тестами
    - Уровень покрытия должен быть больше 80%

9.  **Инфраструктура**
    - Реализовать dockerfile
    - Реализовать docker-compose

### Технические требования

- **Язык программирования**: Python
- **Используемые технологии**: FastAPI, Pydantic, SQLAlchemy, alembic, PostgreSQL
- **Система логирования**: Loguru | Structlog: Sentry - если получится прикрутить, с учетом санкций.
- **Система мониторинга**: Prometheus | Statsd: Grafana.


## Ожидаемый результат
- Исходный код API, соответствующий вышеописанным требованиям.
- README файл с инструкциями по запуску и использованию API.
- Пример файла конфигурации (например, `settings.toml`), исключая любые конфиденциальные данные (такие как API ключи).
