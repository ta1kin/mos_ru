# Описание проекта
- Клиентское приложение с простым пользовательским интерфейсом представляет собой две страницы:
    - Страница прохождения теста. Несколько вопросов, позволяющих подобрать направление, время и формат занятий.
    - Главная страница с рекомендованными после прохождения теста фильтрами местоположения, направления, удобными часами и днями недели, онлйан/офлайн и списком отфильтрованных по предпочтениям пользователя группам активностей.
- API-сервер на express.js подключен к базе данных групп активностей обращается к модели машинного обучения при прохождении теста
- Модель машииного обучения получает результаты ответов на вопросы теста и выдает рекомендованные фильтры
# Структура
    - ./app веб-приложение (отправляет данные опроса брокеру)
    - ./broker веб-сокет брокер сообщений (принимает данные опроса и отправляет модели ML, получает результат, отправляет обратно)
    - ./ml_worker ML model (принимает результаты опроса от брокера, делает предикт)


# Запуск
```console
user@rs:~$ docker-compose up --build -d 
user@rs:~$ docker-compose up
```
Переходим на http://localhost:3000/test 

    - Пользователь может ввести свой уникальный идентификатор, если он участник MOS.ru и получает рекомендации на основе истории пользователя. 
    - Либо он проходит тест, после чего получает рекомендации.

После одного из вышеперечисленных сценариев пользователь переходит на главную страницу, где предустановлены фильтры с полученными рекомендациями. Здесь пользователь может выбрать удобные дни, район города, формат (онлайн/оффлайн). Также есть поля для поиска группы по идентификатору или названию активности

Пользователь нажимает на понравившуюся активность, переходит на ее страницу, где отображены адрес, расписание группы и местоположение на яндекс карте

Пользователь нажимает на кнопку "Записаться" и попадает на mos.ru
