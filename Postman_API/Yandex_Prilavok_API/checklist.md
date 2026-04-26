# Чек-лист: тестирование API Яндекс.Прилавка

**Стенд:** API Яндекс.Прилавок 3.1.1 (учебный)

## Добавление продуктов в набор (POST /api/v1/kits/{id}/products)

| № | Описание | Ожидаемый результат | Статус | Баги |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Добавление продукта, если в наборе 0 продуктов | 200 OK, продукт добавлен | Passed | — |
| 2 | Добавление продукта, если в наборе 1 продукт | 200 OK, продукт добавлен | Passed | — |
| 3 | Добавление продукта, если в наборе 29 продуктов | 200 OK, продукт добавлен | Passed | — |
| 4 | Добавление продукта, если в наборе 30 продуктов | 400 Bad Request, «Не более 30 продуктов в наборе» | Passed | — |
| 5 | Добавление продукта, если в наборе 31 продукт | 400 Bad Request, «Не более 30 продуктов в наборе» | Passed | — |
| 6 | Ошибка при несуществующем id продукта (125) | 400 Bad Request, продукт не добавлен | Passed | — |
| 7 | Ошибка при несуществующем id набора (35) | 404 Not Found, продукт не добавлен | Passed | — |
| 8 | Добавление продукта при quantity = 1 | 200 OK, продукт добавлен | Passed | — |
| 9 | Ошибка при quantity = 9999999999 | 400 Bad Request, продукт не добавлен | Passed | [BUG10](./bug-reports.md#BUG10) |
| 10 | Заполнены id и quantity | 200 OK, продукт добавлен | Passed | — |
| 11 | Незаполнены id и quantity | 400 Bad Request, продукт не добавлен | Passed | — |
| 12 | Заполнен id, пустой quantity | 400 Bad Request, продукт не добавлен | Passed | — |
| 13 | Пустой id, заполнен quantity | 400 Bad Request, продукт не добавлен | Passed | — |
| 14 | Ошибка при id = 0 | 400 Bad Request, продукт не добавлен | Failed | [BUG14](./bug-reports.md#BUG14) |
| 15 | Ошибка при id = null | 400 Bad Request, продукт не добавлен | Failed | [BUG13](./bug-reports.md#BUG13) |
| 16 | Ошибка при id # (спецсимволы) | 404 Not Found, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 17 | Ошибка при id Ж (буквы) | 404 Not Found, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 18 | Ошибка при id -5 (отрицательные числа) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG1](./bug-reports.md#BUG1) |
| 19 | Ошибка при id 2.5 (дробные числа) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG2](./bug-reports.md#BUG2) |
| 20 | Ошибка при id + (мат. символы) | 400 Bad Request, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 21 | Ошибка при id , (пунктуация) | 400 Bad Request, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 22 | Ошибка при quantity # (спецсимволы) | 400 Bad Request, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 23 | Ошибка при quantity Ж (буквы) | 400 Bad Request, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 24 | Ошибка при quantity -5 (отрицательные) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG3](./bug-reports.md#BUG3) |
| 25 | Ошибка при quantity 2.5 (дробные) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG4](./bug-reports.md#BUG4) |
| 26 | Ошибка при quantity + (мат. символы) | 400 Bad Request, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 27 | Ошибка при quantity , (пунктуация) | 400 Bad Request, продукт не добавлен | Passed | [BUG2](./bug-reports.md#BUG2), [BUG9](./bug-reports.md#BUG9) |
| 28 | Пустой массив productsList | 400 Bad Request, продукт не добавлен | Failed | [BUG11](./bug-reports.md#BUG11) |
| 29 | productsList передан строкой | 400 Bad Request, продукт не добавлен | Passed | — |
| 30 | Параметр productsList отсутствует | 400 Bad Request, продукт не добавлен | Failed | [BUG12](./bug-reports.md#BUG12) |
| 31 | quantity = null | 400 Bad Request, продукт не добавлен | Failed | [BUG15](./bug-reports.md#BUG15) |
| 32 | Удалена строка id из запроса | 400 Bad Request, продукт не добавлен | Failed | [BUG16](./bug-reports.md#BUG16) |
| 33 | Удалена строка quantity из запроса | 400 Bad Request, продукт не добавлен | Failed | [BUG17](./bug-reports.md#BUG17) |
| 34 | Повторное добавление продукта в набор | 200 OK, продукт добавлен | Passed | — |

## Расчёт доставки (POST /fast-delivery/v3.1.1/calculate-delivery.xml)

| № | Описание | Ожидаемый результат | Статус | Баги |
| :--- | :--- | :--- | :--- | :--- |
| 35 | Доставка в рабочее время (7 ч.) | 200 OK, isItPossibleToDeliver="true" | Passed | — |
| 36 | Доставка в рабочее время (8 ч.) | 200 OK, isItPossibleToDeliver="true" | Passed | — |
| 37 | Доставка в рабочее время (20 ч.) | 200 OK, isItPossibleToDeliver="true" | Passed | — |
| 38 | Доставка в рабочее время (21 ч.) | 200 OK, isItPossibleToDeliver="true" | Passed | — |
| 39 | Доставка в нерабочее время (5 ч.) | 200 OK, isItPossibleToDeliver="false" | Failed | [BUG5](./bug-reports.md#BUG5) |
| 40 | Доставка в нерабочее время (6 ч.) | 200 OK, isItPossibleToDeliver="false" | Failed | [BUG5](./bug-reports.md#BUG5) |
| 41 | Доставка в нерабочее время (22 ч.) | 200 OK, isItPossibleToDeliver="false" | Failed | [BUG5](./bug-reports.md#BUG5) |
| 42 | Доставка в нерабочее время (23 ч.) | 200 OK, isItPossibleToDeliver="false" | Failed | [BUG5](./bug-reports.md#BUG5) |
| 43 | Доставка в некорректное время (24 ч.) | 400 Bad Request | Failed | [BUG5](./bug-reports.md#BUG5) |
| 44 | Доставка в некорректное время (25 ч.) | 400 Bad Request | Failed | [BUG5](./bug-reports.md#BUG5) |
| 45 | Доставка в некорректное время (-1 ч.) | 400 Bad Request | Failed | [BUG5](./bug-reports.md#BUG5) |
| 46 | Доставка в некорректное время (-5 ч.) | 400 Bad Request | Failed | [BUG5](./bug-reports.md#BUG5) |
| 47 | Вес 0.1 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 48 | Вес 2.4 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 49 | Вес 2.5 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 50 | Вес 2.6 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 51 | Вес 2.7 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 52 | Вес 5.9 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 53 | Вес 6 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 54 | Вес 6.1 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 55 | Вес 6.2 кг, кол-во 10 | 200 OK, доставка возможна | Passed | — |
| 56 | Количество продуктов 0 | 400 Bad Request, доставка невозможна | Failed | [BUG6](./bug-reports.md#BUG6) |
| 57 | Вес 5 кг, кол-во 1 | 200 OK, доставка возможна | Passed | — |
| 58 | Вес 5 кг, кол-во 2 | 200 OK, доставка возможна | Passed | — |
| 59 | Вес 5 кг, кол-во 6 | 200 OK, доставка возможна | Passed | — |
| 60 | Вес 5 кг, кол-во 7 | 200 OK, доставка возможна | Passed | — |
| 61 | Вес 5 кг, кол-во 8 | 200 OK, доставка возможна | Passed | — |
| 62 | Вес 5 кг, кол-во 9 | 200 OK, доставка возможна | Passed | — |
| 63 | Вес 5 кг, кол-во 13 | 200 OK, доставка возможна | Passed | — |
| 64 | Вес 5 кг, кол-во 14 | 200 OK, доставка возможна | Passed | — |
| 65 | Вес 5 кг, кол-во 15 | 200 OK, доставка возможна | Passed | — |
| 66 | Стоимость доставки: вес 2 кг, кол-во 5 | hostDeliveryCost = 23, clientDeliveryCost = 0 | Passed | — |
| 67 | Стоимость доставки: вес 2 кг, кол-во 10 | hostDeliveryCost = 43, clientDeliveryCost = 0 | Passed | — |
| 68 | Стоимость доставки: вес 4.5 кг, кол-во 5 | hostDeliveryCost = 43, clientDeliveryCost = 0 | Passed | — |
| 69 | Стоимость доставки: вес 4.5 кг, кол-во 10 | hostDeliveryCost = 43, clientDeliveryCost = 0 | Passed | — |
| 70 | Стоимость доставки: вес 2 кг, кол-во 20 | hostDeliveryCost = 43, clientDeliveryCost = 99 | Passed | — |
| 71 | Стоимость доставки: вес 7 кг, кол-во 10 | hostDeliveryCost = 43, clientDeliveryCost = 99 | Passed | — |
| 72 | Стоимость доставки: вес 7 кг, кол-во 20 | hostDeliveryCost = 43, clientDeliveryCost = 99 | Passed | — |
| 73 | productsCount = null | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 74 | productsCount # (спецсимволы) | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 75 | productsCount Ж (буквы) | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 76 | productsCount -5 (отрицательные) | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 77 | productsCount 2.5 (дробные) | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 78 | productsCount + (мат. символы) | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 79 | productsCount , (пунктуация) | 400 Bad Request | Failed | [BUG22](./bug-reports.md#BUG22) |
| 80 | productsWeight = null | 400 Bad Request | Passed | — |
| 81 | productsWeight # (спецсимволы) | 400 Bad Request | Passed | — |
| 82 | productsWeight Ж (буквы) | 400 Bad Request | Passed | — |
| 83 | productsWeight -5 (отрицательные) | 400 Bad Request | Passed | — |
| 84 | productsWeight 2.5 (дробные) | 400 Bad Request | Passed | — |
| 85 | productsWeight + (мат. символы) | 400 Bad Request | Passed | — |
| 86 | productsWeight , (пунктуация) | 400 Bad Request | Passed | — |
| 87 | deliveryTime = null | 400 Bad Request | Passed | — |
| 88 | deliveryTime # (спецсимволы) | 400 Bad Request | Passed | — |
| 89 | deliveryTime Ж (буквы) | 400 Bad Request | Passed | — |
| 90 | deliveryTime -5 (отрицательные) | 400 Bad Request | Passed | — |
| 91 | deliveryTime 2.5 (дробные) | 400 Bad Request | Passed | — |
| 92 | deliveryTime + (мат. символы) | 400 Bad Request | Passed | — |
| 93 | deliveryTime , (пунктуация) | 400 Bad Request | Passed | — |

## Корзина: получение списка (GET /api/v1/orders/{id})

| № | Описание | Ожидаемый результат | Статус | Баги |
| :--- | :--- | :--- | :--- | :--- |
| 94 | Получение списка при 1 продукте | 200 OK, список получен | Passed | — |
| 95 | Получение списка при 10 продуктах | 200 OK, список получен | Passed | — |
| 96 | Несуществующий id корзины (10) | 404 Not Found | Passed | — |

## Корзина: добавление продуктов (PUT /api/v1/orders/{id})

| № | Описание | Ожидаемый результат | Статус | Баги |
| :--- | :--- | :--- | :--- | :--- |
| 97 | Добавление с корректными данными (id=1, quantity=1) | 200 OK, продукты добавлены | Passed | — |
| 98 | Количество больше, чем на складе (id=1, quantity=100) | 409 Conflict | Passed | — |
| 99 | Повторное добавление товара | 200 OK, продукты добавлены | Passed | — |
| 100 | Пустой массив productsList | 400 Bad Request | Failed | [BUG7](./bug-reports.md#BUG7) |
| 101 | Несуществующий id продукта (125) | 404 Not Found | Passed | — |
| 102 | Удалена строка id из запроса | 400 Bad Request | Passed | — |
| 103 | Удалена строка quantity из запроса | 400 Bad Request | Passed | — |
| 104 | quantity = 1 | 200 OK, продукт добавлен | Passed | — |
| 105 | quantity = 9999999999 | 400 Bad Request | Passed | — |
| 106 | Заполнены id и quantity | 200 OK, продукт добавлен | Passed | — |
| 107 | Незаполнены id и quantity | 400 Bad Request | Passed | — |
| 108 | Заполнен id, пустой quantity | 400 Bad Request | Passed | — |
| 109 | Пустой id, заполнен quantity | 400 Bad Request | Passed | — |
| 110 | id = 0 | 400 Bad Request | Passed | — |
| 111 | id = null | 400 Bad Request | Passed | — |
| 112 | id # (спецсимволы) | 404 Not Found | Failed | [BUG21](./bug-reports.md#BUG21) |
| 113 | id Ж (буквы) | 404 Not Found | Failed | [BUG21](./bug-reports.md#BUG21) |
| 114 | id -5 (отрицательные) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG21](./bug-reports.md#BUG21) |
| 115 | id 2.5 (дробные) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG21](./bug-reports.md#BUG21) |
| 116 | id + (мат. символы) | 400 Bad Request | Failed | [BUG21](./bug-reports.md#BUG21) |
| 117 | id , (пунктуация) | 400 Bad Request | Failed | [BUG21](./bug-reports.md#BUG21) |
| 118 | quantity # (спецсимволы) | 400 Bad Request | Failed | [BUG20](./bug-reports.md#BUG20) |
| 119 | quantity Ж (буквы) | 400 Bad Request | Failed | [BUG20](./bug-reports.md#BUG20) |
| 120 | quantity -5 (отрицательные) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG20](./bug-reports.md#BUG20) |
| 121 | quantity 2.5 (дробные) | 400 Bad Request, «Unexpected number in JSON» | Failed | [BUG20](./bug-reports.md#BUG20) |
| 122 | quantity + (мат. символы) | 400 Bad Request | Failed | [BUG20](./bug-reports.md#BUG20) |
| 123 | quantity , (пунктуация) | 400 Bad Request | Failed | [BUG20](./bug-reports.md#BUG20) |
| 124 | productsList передан строкой | 400 Bad Request | Failed | [BUG18](./bug-reports.md#BUG18) |
| 125 | Параметр productsList отсутствует | 400 Bad Request | Failed | [BUG19](./bug-reports.md#BUG19) |

## Корзина: удаление (DELETE /api/v1/orders/{id})

| № | Описание | Ожидаемый результат | Статус | Баги |
| :--- | :--- | :--- | :--- | :--- |
| 126 | Успешное удаление корзины (id=5) | 200 OK, корзина удалена | Failed | [BUG8](./bug-reports.md#BUG8) |
| 127 | Удаление несуществующей корзины (id=50) | 404 Not Found | Passed | — |
