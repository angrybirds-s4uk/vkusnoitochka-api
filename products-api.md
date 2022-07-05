# API Товаров

{% swagger method="get" path="/api/v1/catalog/product" baseUrl="https://site-api.vkusnoitochka.ru" summary="Получение информации про определённый товар" %}
{% swagger-description %}
Данный метод позволяет получить информацию про определённый товар.  ID ресторана можно получить из метода

[#poluchenie-vsekh-restoranov-ryadom](restourants-api.md#poluchenie-vsekh-restoranov-ryadom "mention")

, а ID товара можно получить из метода 

[#poluchenie-tovarov-kategorii](categories-api.md#poluchenie-tovarov-kategorii "mention")

.
{% endswagger-description %}

{% swagger-parameter in="query" name="storeId" type="number" required="true" %}
Уникальный ID ресторана
{% endswagger-parameter %}

{% swagger-parameter in="query" required="true" type="string" name="productId" %}
Уникальный ID товара
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Список со всеми вариациями указанного товара." %}
```javascript
{
    "offers": [
        {
            "sorting": 13000, // как сортировать данный товар (больше - товар выше, меньше - товар ниже)
            "weight": 173.0, // вес товара
            "size": "", // размер товара
            "name": "Двойной Чизбургер", // наименование товара
            "allergens": [ // возможные аллергены
                "Глютен",
                "Молоко",
                "Горчица",
                "Может содержать сою, яйцо, следы кунжута"
            ],
            "id": "5dfcb122ac65eaba25f7788c", // уникальный ID данного товара
            "mcId": 2011, // ID товара в McDonalds до закрытия
            "energy": {
                "KCal": 441.0, // количество килокалорий
                "energyKj": 1844.0 // энергетическая ценность (кДж)
            },
            "stickers": [ // "наклейки" на превью товара (например, "популярно")
                {
                    "code": "is_popular" // означает, что товар популярен
                }
            ],
            "detailPicture": "https://ma-prod-cdn.mcdonalds.ru/product/f04b628194604c3c9bbf667c86253d0e/android/l/main.png",
            "detailText": "Два рубленых бифштекса из натуральной цельной говядины с двумя кусочками сыра Чеддер на карамелизованной булочке, заправленной горчицей, кетчупом, луком и двумя кусочками маринованного огурчика",
            "nutritionalValue": { // информация про питательные вещества товара 
                "fat": { // информация про жиры
                    "amount": 23.0, // количество
                    "rationIndex": 33.0 // количество в %
                },
                // для всех остальных применимо тоже самое, что и наверху ^
                "saturatedFat": {
                    "amount": 12.0,
                    "rationIndex": 59.0
                },
                "carbohydrate": {
                    "amount": 31.0,
                    "rationIndex": 12.0
                },
                "sugar": {
                    "amount": 7.7,
                    "rationIndex": 9.0
                },
                "dietfiber": {
                    "amount": 2.2,
                    "rationIndex": ""
                },
                "protein": {
                    "amount": 26.0,
                    "rationIndex": 53.0
                },
                "salt": {
                    "amount": 2.6,
                    "rationIndex": 39.0
                }
            },
            "composition": [ // состав товара
                "Булочка для гамбургеров из пшеничной муки",
                "Бифштексы из говядины рубленые",
                "Плавленый сыр Чеддер",
                "Кетчуп томатный",
                "Огурцы маринованные резаные",
                "Лук репчатый резаный восстановленный",
                "Горчичный соус",
                "Приправа для гриля"
            ],
            "mealChoices": [],
            "isChoices": false,
            "price": 129.0 // цена товара в данном заведении
        }
    ],
    "id": "5dfcb122ac65eaba25f7788c" // уникальный ID товара
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Если Вы не указали ID ресторана или товара (или ID ресторана был указан неправильно)." %}
```javascript
{
    "error": "You should provide at least one of location id" // текст ошибки
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Если товар не был найден (или Вы не указали ID товара)." %}
```javascript
{
    "error": "product/category/prices not found" // текст ошибки
}
```
{% endswagger-response %}
{% endswagger %}
