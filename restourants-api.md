# API Ресторанов

{% swagger method="get" path="/api/restaurants" baseUrl="https://vkusnoitochka.ru" summary="Получение всех доступных ресторанов" %}
{% swagger-description %}
Данный метод позволяет получить все существующие рестораны, а также их статусы и доступные функции.
{% endswagger-description %}

{% swagger-response status="200: OK" description="Список со всеми ресторанами, их статусами и доступными функциями. Также, передаётся описание функциям." %}
```javascript
{
    "restaurants": [
        {
            "id": 1, // порядковый ID ресторана
            "features": [ // список доступных функций ресторана (массив из ID)
                3,
                12
            ],
            "latitude": 55.764601, // широта координат ресторана
            "longitude": 37.603176, // долгота координат ресторана
            "isTempClosed": false // закрыт ли временно этот ресторан?
        }
    ],
    "features": [ // список всех доступных функций
        {
            "id": 1, // уникальный ID функций
            "name": "Авто", // название функции
            "xmlId": "mcauto" // уникальный строковый ID функции
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/restaurants/near" baseUrl="https://vkusnoitochka.ru" summary="Получение всех ресторанов рядом" %}
{% swagger-description %}
Данный метод позволяет получить все рестораны рядом с определёнными координатами.
{% endswagger-description %}

{% swagger-parameter in="query" name="lat" type="float" required="true" %}
Широта локации (например, 55.764995).
{% endswagger-parameter %}

{% swagger-parameter in="query" name="long" type="float" required="true" %}
Долгота локации (например, 37.561152).
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Список со всеми ресторанами около указанных координат." %}
```javascript
[
    {
        "id": 6, // порядковый ID ресторана
        "xmlId": "11006", // ID ресторана для использования в API
        "name": "MC Krasnaya Presnya", // наименование ресторана
        "region": "Москва", // регион местонахождения ресторана
        "city": "Москва", // город, где находится ресторан
        "street": "ул Красная Пресня", // улица
        "house": "дом 31", // номер строения (дом)
        "block": "",
        "entrance": "", // номер входа
        "latitude": 55.762308, // широта координат ресторана
        "longitude": 37.563371, // долгота координат ресторана
        "location": {
            "name": "Москва", // наименование локации (обычно, город)
            "code": "0000073738" // код локации (обычно, код города)
        }
    }
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Если один из необходимых параметров заполнен неправильно или не заполнен вообще." %}
```javascript
{
    "message": "Parameter \"long\" of value \"NULL\" violated a constraint \"Значение не должно быть null.\"\nParameter \"long\" of value \"NULL\" violated a constraint \"Значение не должно быть пустым.\"",  // текст ошибки
    "errors": [] // список ошибок (обычно - пуст)
}
```
{% endswagger-response %}
{% endswagger %}
