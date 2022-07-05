# API Категорий

{% swagger method="get" path="/api/v1/catalog/categories" baseUrl="https://site-api.vkusnoitochka.ru" summary="Получение всех категорий ресторана" %}
{% swagger-description %}
Данный метод позволяет получить все доступные категории для определённого ресторана. ID ресторана можно получить из метода

[#poluchenie-vsekh-restoranov-ryadom](restourants-api.md#poluchenie-vsekh-restoranov-ryadom "mention")

.
{% endswagger-description %}

{% swagger-parameter in="query" name="storeId" type="number" required="true" %}
Уникальный ID ресторана
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Список со всеми категориями, доступными для данного ресторана." %}
```javascript
[
    {
        "id": "5dfcb0c0ac65eaba25f77816", // уникальный ID категории
        "title": "Популярное" // название категории
    }
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Если Вы не указали ID ресторана (или ID ресторана был указан неправильно)." %}
```javascript
{
    "error": "You should provide at least one of location id" // текст ошибки
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Если для данного ресторана не было найдено ни одной категории." %}
```javascript
{
    "error": "categories not found" // текст ошибки
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/catalog/category" baseUrl="https://site-api.vkusnoitochka.ru" summary="Получение товаров категории" %}
{% swagger-description %}
Данный метод позволяет получить все товары определённой категории. ID ресторана можно получить из метода

[#poluchenie-vsekh-restoranov-ryadom](restourants-api.md#poluchenie-vsekh-restoranov-ryadom "mention")

, а ID категории можно получить из метода 

[#poluchenie-vsekh-kategorii-restorana](categories-api.md#poluchenie-vsekh-kategorii-restorana "mention")

.
{% endswagger-description %}

{% swagger-parameter in="query" name="categoryId" type="string" required="true" %}
Уникальный ID категории
{% endswagger-parameter %}

{% swagger-parameter in="query" name="storeId" type="number" required="true" %}
Уникальный ID ресторана
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Список со всеми товарами категории." %}
```javascript
{
    "products": [
        {
            "id": "5dfcb122ac65eaba25f7788c", // уникальный ID данного товара
            "sorting": 13000, // как сортировать данный товар (больше - товар выше, меньше - товар ниже)
            "size": "", // размер товара
            "name": "Двойной Чизбургер", // название товара
            "code": "5dfcb122ac65eaba25f7788c", // код товара
            "mcId": 2011, // ID товара в McDonalds до закрытия
            "detailText": "Два рубленых бифштекса из натуральной цельной говядины с двумя кусочками сыра Чеддер на карамелизованной булочке, заправленной горчицей, кетчупом, луком и двумя кусочками маринованного огурчика", // описание товара
            "offers": [
                {
                    "previewPicture": "https://ma-prod-cdn.mcdonalds.ru/product/f04b628194604c3c9bbf667c86253d0e/android/l/main.png", // ссылка на картинку с превью товара
                    "stickers": [ // "наклейки" на превью товара (например, "популярно")
                        {
                            "code": "is_popular" // означает, что товар популярен
                        }
                    ],
                    "price": 129.0 // цена товара в данном заведении
                }
            ],
            "subcatId": null, // ID субкатегории
            "subSubcatId": null, // ID суб-субкатегории
            "categoryName": "Популярное" // название категории, в которой этот товар находится
        }
    ],
    "catId": "5dfcb0c0ac65eaba25f77816", // ID категории, в котором этот товар находится
    "subcategories": [] // субкатегории, в которых этот товар также находится
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Если Вы не указали ID ресторана (или ID ресторана был указан неправильно)." %}
```javascript
{
    "error": "You should provide at least one of location id" // текст ошибки
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Если категория не была найдена (или Вы не указали ID категории)." %}
```javascript
{
    "error": "category or prices not found" // текст ошибки
}
```
{% endswagger-response %}
{% endswagger %}
