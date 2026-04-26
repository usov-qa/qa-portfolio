# Баг-репорты

**Стенд:** API Яндекс.Прилавок 3.1.1 (учебный)
**Сервер:** {{server_url}}

### BUG1
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG1 | Добавление продукта в набор с отрицательным id (200 OK вместо 400) | Критический | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":-1,"quantity":2}]}` | 400 Bad Request | 200 OK, продукт добавлен |

### BUG2
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG2 | Набор выдаёт 500 после добавления продукта с дробным id | Блокирующий | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":1.5,"quantity":2}]}` | 400 Bad Request | 500 Internal Server Error |

### BUG3
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG3 | Добавление отрицательного количества товара в набор (200 OK вместо 400) | Критический | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":1,"quantity":-2}]}` | 400 Bad Request | 200 OK, продукт добавлен с quantity=-2 |

### BUG4
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG4 | Ошибка 500 при добавлении продукта с дробным quantity | Блокирующий | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":1,"quantity":2.5}]}` | 400 Bad Request | 500 Internal Server Error |

### BUG5
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG5 | Пустое тело ответа XML при deliveryTime вне рабочего времени | Блокирующий | Открыть Postman | POST {{server_url}}/fast-delivery/v3.1.1/calculate-delivery.xml, тело: `<InputModel><productsCount>2</productsCount><productsWeight>5.1</productsWeight><deliveryTime>5</deliveryTime></InputModel>` | 200 OK, isItPossibleToDeliver="false" | 200 OK, пустое тело |

### BUG6
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG6 | Доставка возможна при productsCount=0 | Стандартный | Открыть Postman | POST {{server_url}}/fast-delivery/v3.1.1/calculate-delivery.xml, тело: `<InputModel><productsCount>0</productsCount><productsWeight>5.1</productsWeight><deliveryTime>10</deliveryTime></InputModel>` | 400 Bad Request, isItPossibleToDeliver="false" | 200 OK, isItPossibleToDeliver="true" |

### BUG7
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG7 | 200 OK при добавлении в корзину пустого массива productsList | Стандартный | Открыть Postman | PUT {{server_url}}/api/v1/orders/4, тело: `{"productsList":[]}` | 400 Bad Request | 200 OK |

### BUG8
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG8 | Корзина не удаляется (404 вместо 200) | Блокирующий | Открыть Postman | DELETE {{server_url}}/api/v1/orders/4 | 200 OK, корзина удалена | 404, «Корзина с id=4 не найдена» |

### BUG9
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG9 | Ошибка 500 при нечисловом параметре id | Блокирующий | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":"Ж","quantity":1}]}` | 400 Bad Request | 500 Internal Server Error |

### BUG10
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG10 | Ошибка 500 при quantity=9999999999 | Блокирующий | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":1,"quantity":9999999999}]}` | 400 Bad Request | 500 Internal Server Error |

### BUG11
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG11 | Ошибка 500 при productsList передан строкой | Блокирующий | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":"Привет"}` | 400 Bad Request | 500 Internal Server Error |

### BUG12
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG12 | 200 OK при отсутствии параметра productsList | Стандартный | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{}` | 400 Bad Request | 200 OK |

### BUG13
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG13 | 200 OK при id=null | Стандартный | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":null,"quantity":1}]}` | 400 Bad Request | 200 OK |

### BUG14
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG14 | 200 OK при id=0 | Стандартный | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":0,"quantity":1}]}` | 400 Bad Request | 200 OK |

### BUG15
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG15 | 200 OK при quantity=null | Стандартный | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":1,"quantity":null}]}` | 400 Bad Request | 200 OK |

### BUG16
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG16 | 200 OK при удалённой строке id из запроса | Стандартный | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"quantity":1}]}` | 400 Bad Request | 200 OK |

### BUG17
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG17 | 200 OK при удалённой строке quantity из запроса | Стандартный | Открыть Postman | POST {{server_url}}/api/v1/kits/3/products, тело: `{"productsList":[{"id":1}]}` | 400 Bad Request | 200 OK |

### BUG18
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG18 | PUT: 404 при передаче строки в productsList вместо 400 | Стандартный | Открыть Postman | PUT {{server_url}}/api/v1/orders/3/products, тело: `{"productsList":"Привет"}` | 400 Bad Request | 404 |

### BUG19
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG19 | PUT: 404 при отсутствии productsList вместо 400 | Стандартный | Открыть Postman | PUT {{server_url}}/api/v1/orders/3/products, тело: `{"productsList":[]}` | 400 Bad Request | 404 |

### BUG20
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG20 | PUT: 200 OK при невалидном quantity | Стандартный | Открыть Postman | PUT {{server_url}}/api/v1/orders/3/products, тело: `{"productsList":[{"id":1,"quantity":"ж"}]}` | 400 Bad Request | 200 OK |

### BUG21
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG21 | PUT: 200 OK при невалидном id | Стандартный | Открыть Postman | PUT {{server_url}}/api/v1/orders/3/products, тело: `{"productsList":[{"id":"ж","quantity":1}]}` | 400 Bad Request | 200 OK |

### BUG22
| ID | Название | Приоритет | Предусловия | Шаги | Ожидаемый результат | Фактический результат |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BUG22 | 200 OK при невалидном productsCount в XML | Стандартный | Открыть Postman | POST {{server_url}}/fast-delivery/v3.1.1/calculate-delivery.xml, тело: `<InputModel><productsCount>null</productsCount><productsWeight>5.1</productsWeight><deliveryTime>20</deliveryTime></InputModel>` | 400 Bad Request | 200 OK |
