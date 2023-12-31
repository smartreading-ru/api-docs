# Документация API

v1.0 2023-12-11 volcan0

Существует ряд методов для регистрации и авторизации пользователей не требующих токена авторизации.<br>
Метод регистрации требует партнерский ключ доступа к API.<br>
Все остальные методы требуют Bearer Token в заголовке запроса.

В запросах часто используются:

````json
"extend_data": {
"os": "12.1.4", // Версия операционной системы
"channel": "ios", // устройство пользователя. Может быть web,ios,android
"hardware": "iPhone9,3", // Версия устройства или браузера
"api_version": "2.1", // API устройства
"app_version": "v3.2.4" // Версия приложения
}
````

## Авторизация

<details>

<summary>
	Авторизация по Email /api/client/v2/auth/email
</summary>

### Получение токена доступа по email пользователя.

```
POST /api/client/v2/auth/email
```

Request body json:

```json
{
  "data": {
    "email": "my@email.com",
    "password": "mypassword",
    "apps_flyer": {
      "idfa": "EE4D67BC-AA45-4B52-A7F5-F49EC455E41B",
      "advertising_id": "",
      "uid": "1579866034725-3229704"
    }
  },
  "extend_data": {
    "os": "12.1.4",
    "channel": "ios",
    "hardware": "iPhone9,3",
    "api_version": "2.1",
    "app_version": "v3.2.4"
  }
}
```

200 OK Response json:

```json
{
  "data": {
    "id": 476130,
    "name": "user name",
    "email": "my@email.com",
    "social_id": null,
    "type": "b2c",
    "token": "long string token here",
    "user_data_update_channel": "my_email.com",
    "summaries_update_channels": [
      "summary_update"
    ],
    "subscription": {
      "tariff_alias": "6month",
      "tariff_name": "Максимальный доступ",
      "end_date": "2024-10-24T14:56:09+03:00",
      "is_trial": false,
      "had_trial": true,
      "is_recurrent": true,
      "is_purchasing_allowed": false,
      "current_time": "2023-12-11T23:28:44+03:00"
    },
    "interface_data": {
      "blog": {
        "web_site_url": "https://smartreading.ru/blog"
      }
    }
  },
  "errors": null,
  "warnings": null
}
```

200 Error Response json:

```json
{
  "data": null,
  "errors": [
    {
      "code": 2003,
      "message": "Неправильный пароль.",
      "details": "wron password here"
    }
  ],
  "warnings": null
}
```

</details>

<details>
<summary>
	Авторизация через VK /api/client/v2/social/login/vk
</summary>

### Получение токена доступа по VK аккаунту пользователя.

```
POST /api/client/v2/social/login/vk
```

Request body json:

```json
{
  "data": {
    "email": "test-1@vk.com",
    "access_token": "Test User VK-1"
  }
}
```

200 OK Response json:

```json
{
  "data": {
    "id": 476130,
    "name": "user name",
    "email": "my@email.com",
    "social_id": null,
    "type": "b2c",
    "token": "long string token here",
    "user_data_update_channel": "my_email.com",
    "summaries_update_channels": [
      "summary_update"
    ],
    "subscription": {
      "tariff_alias": "6month",
      "tariff_name": "Максимальный доступ",
      "end_date": "2024-10-24T14:56:09+03:00",
      "is_trial": false,
      "had_trial": true,
      "is_recurrent": true,
      "is_purchasing_allowed": false,
      "current_time": "2023-12-11T23:28:44+03:00"
    },
    "interface_data": {
      "blog": {
        "web_site_url": "https://smartreading.ru/blog"
      }
    }
  },
  "errors": null,
  "warnings": null
}
``` 

200 Error response json:

```json
{
  "errors": [
    {
      "code": 2005,
      "message": "Ошибка при авторизации ВКонтакте",
      "details": null
    },
    {
      "code": 2017,
      "message": "Некорректный авторизационный токен",
      "details": "Test User VK-1"
    }
  ],
  "data": null,
  "warnings": null
}
```

</details>

<details>
<summary>
	Авторизация через Google /api/client/v2/social/login/google
</summary>

### Получение токена доступа через Google аккаунт пользователя.

```
POST /api/client/v2/social/login/google
```

Request body json:

```json
{
  "data": {
    "id_token": "токен"
  }
}
```

200 OK Response json:

```json
{
  "data": {
    "id": 476130,
    "name": "user name",
    "email": "my@email.com",
    "social_id": null,
    "type": "b2c",
    "token": "long string token here",
    "user_data_update_channel": "my_email.com",
    "summaries_update_channels": [
      "summary_update"
    ],
    "subscription": {
      "tariff_alias": "6month",
      "tariff_name": "Максимальный доступ",
      "end_date": "2024-10-24T14:56:09+03:00",
      "is_trial": false,
      "had_trial": true,
      "is_recurrent": true,
      "is_purchasing_allowed": false,
      "current_time": "2023-12-11T23:28:44+03:00"
    },
    "interface_data": {
      "blog": {
        "web_site_url": "https://smartreading.ru/blog"
      }
    }
  },
  "errors": null,
  "warnings": null
}
``` 

200 Error response json:

```json
{
  "errors": [
    {
      "code": 2007,
      "message": "Ошибка при авторизации в Google",
      "details": null
    },
    {
      "code": 2017,
      "message": "Некорректный авторизационный токен",
      "details": null
    }
  ],
  "data": null,
  "warnings": null
}
```

</details>


<details>
<summary>
	Авторизация по AppleID /api/client/v2/social/login/apple-id
</summary>

### Получение токена доступа по Apple ID пользователя.

```
POST /api/client/v2/social/login/apple-id
```

Request body json:

```json
{
  "data": {
    "access_token": "XXX-1",
    "email": "test-a-1@apple.com",
    "name": "Test User Apple-1"
  },
  "extend_data": {
    "os": "12.1.4",
    "channel": "ios",
    "hardware": "iPhone9,3",
    "app_version": "v3.2.4"
  }
}
```

200 OK Response json:

```json
{
  "data": {
    "id": 476130,
    "name": "user name",
    "email": "my@email.com",
    "social_id": null,
    "type": "b2c",
    "token": "long string token here",
    "user_data_update_channel": "my_email.com",
    "summaries_update_channels": [
      "summary_update"
    ],
    "subscription": {
      "tariff_alias": "6month",
      "tariff_name": "Максимальный доступ",
      "end_date": "2024-10-24T14:56:09+03:00",
      "is_trial": false,
      "had_trial": true,
      "is_recurrent": true,
      "is_purchasing_allowed": false,
      "current_time": "2023-12-11T23:28:44+03:00"
    },
    "interface_data": {
      "blog": {
        "web_site_url": "https://smartreading.ru/blog"
      }
    }
  },
  "errors": null,
  "warnings": null
}
``` 

200 Error response json:

```json
{
  "errors": [
    {
      "code": 2028,
      "message": "Ошибка при авторизации по AppleID",
      "details": "Wrong number of segments"
    },
    {
      "code": 2017,
      "message": "Некорректный авторизационный токен",
      "details": null
    }
  ],
  "data": null,
  "warnings": null
}
```

</details>

## Регистрация

<details>
<summary>
    (Устаревший метод) Регистрация по email /api/client/v2/registration/email
</summary>

```
POST /api/client/v2/registration/email
```

Request body json:

````json
{
  "data": {
    "email": "my email",
    "name": "my name",
    "password": "my password",
    "apps_flyer": {
      "idfa": "EE4D67BC-AA45-4B52-A7F5-F49EC455E41B",
      "advertising_id": "1579866034725",
      "uid": "1579866034725-3229704"
    }
  },
  "extend_data": {
    "channel": "ios",
    "os": "12.1.4",
    "hardware": "iPhone9,3",
    "api_version": "2.1",
    "app_version": "v3.2.4"
  }
}
````

200 Response json:

````json
{
  "data": {
    "id": 644228,
    "name": "my name",
    "email": "my email",
    "social_id": null,
    "type": "b2c",
    "token": "my access token",
    "user_data_update_channel": "my_email.com",
    "summaries_update_channels": [
      "summary_update"
    ],
    "subscription": {
      "tariff_alias": "trial",
      "tariff_name": "Триал (Пробный)",
      "end_date": "2023-12-19T17:30:49+03:00",
      "is_trial": true,
      "had_trial": true,
      "is_recurrent": false,
      "is_purchasing_allowed": true,
      "current_time": "2023-12-12T17:30:49+03:00"
    },
    "interface_data": {
      "blog": {
        "web_site_url": "https://smartreading.ru/blog"
      }
    }
  },
  "errors": null,
  "warnings": null
}
````

200 Error response:

````json
{
  "data": null,
  "errors": [
    {
      "code": 2001,
      "message": "Пользователь с таким email уже существует",
      "details": "my email"
    }
  ],
  "warnings": null
}
````

</details>

## Восстановление доступа

<details>
<summary>
Восстановление пароля по Email /api/client/v2/password/reset/email
</summary>

### Запрос ссылки на сброс пароля для определенного Email

Ответ со ссылкой на сброс приходит на запрошенный Email.

````
POST /api/client/v2/password/reset/email
````

Request body json:

````json
{
  "data": {
    "email": ""
  }
}
````

200 OK Response json:

````json
{
  "data": null,
  "errors": null,
  "warnings": null
}
````

200 Error Response json:

````json
{
  "data": null,
  "errors": [
    {
      "code": 2004,
      "message": "Пользователь не найден."
    }
  ],
  "warnings": null
}
````

</details>

## Библиотека саммари

<details>
<summary>
Получение списка категорий /api/client/v2/themes/get-list/v2
</summary>

### Возвращает полный список тем саммари

````
POST /api/client/v2/themes/get-list/v2
````

Request Headers:

````
Authorization: Bearer access_token
````

Request body json:

````json
{
  "data": {
    "channel": "android"
  }
}
````

200 Response json:

````json
 {
  "data": {
    "themes": [
      {
        "id": 1,
        "title": "Бизнес",
        "sub_title": "Все про бизнес",
        "children": [
          {
            "id": 2,
            "title": "Области бизнеса",
            "sub_title": "Все о функциях бизнеса",
            "children": [
              {
                "id": 3,
                "title": "Маркетинг",
                "children": null
              },
              {
                "id": 4,
                "title": "Продажи",
                "children": null
              },
              {
                "id": 5,
                "title": "Инновации",
                "children": null
              }
            ]
          }
        ]
      }
    ]
  },
  "errors": null,
  "warnings": null
}
````

</details>
<details>
<summary>Получение списка рекомендаций /api/client/v2/recommendations/get-list</summary>

### Возвращает полный набор рекомендаций для текущего пользователя

Запрос возвращает большое кол-во данных, включая подробные данные для каждого саммари для каждой строки
рекомендаций.<br>
Устарело и будет замененно в будущем.

````
POST /api/client/v2/recommendations/get-list
````

Request Headers:

````
Authorization: Bearer access_token
````

Request body json:

````json
{
  "data": {},
  "extend_data": {
    "channel": "ios",
    "app_version": "4.8.0"
  }
}
````

200 OK Response json:

````json
{
  "data": {
    "themes": [
      {
        "theme": {
          "id": null,
          "title": "Новинки"
        },
        "recommendations": [
          {
            "summary_id": 1068,
            "title": "Психология денег. Вечные уроки богатства, жадности и счастья",
            "title_en": "The Psychology of Money: Timeless lessons on wealth, greed, and happiness",
            "authors": "Морган Хаузел",
            "authors_en": "Morgan Housel",
            "audio": {
              "duration_ms": 1818000
            },
            "themes": [
              1,
              2,
              3
            ],
            "themes_v2": [
              {
                "id": 48,
                "depth_level": 1,
                "weight": 9
              },
              {
                "id": 49,
                "depth_level": 2,
                "weight": 9
              }
            ],
            "similar_summaries": [
              668,
              451,
              449,
              304
            ],
            "sponsor": null,
            "attributes": [
              1,
              3
            ],
            "current_time": "2023-12-12T20:36:11+03:00",
            "is_has_infographics": false
          }
        ]
      }
    ],
    "banners": [
      {
        "alias": "calendar_2024",
        "image_url": "https://cdn.smartreading.ru/images/mobile/adv_banners/24_135654_banner.png",
        "link_url": "https://www.ozon.ru/highlight/umnyy-kalendar-1226335/",
        "place": "top",
        "width": 320,
        "height": 140,
        "link_type": "url",
        "screen_alias": null
      }
    ],
    "meta": {
      "attributes": [
        {
          "id": 1,
          "title": "new"
        },
        {
          "id": 2,
          "title": "free"
        },
        {
          "id": 3,
          "title": "audio"
        },
        {
          "id": 4,
          "title": "recommend"
        },
        {
          "id": 5,
          "title": "first_time_ru"
        },
        {
          "id": 6,
          "title": "popular"
        },
        {
          "id": 7,
          "title": "coming_soon"
        }
      ],
      "themes": [
        {
          "id": 1,
          "title": "Саморазвитие"
        },
        {
          "id": 2,
          "title": "Бизнес"
        },
        {
          "id": 3,
          "title": "Деньги"
        },
        {
          "id": 4,
          "title": "Технологии"
        },
        {
          "id": 5,
          "title": "Общество"
        },
        {
          "id": 6,
          "title": "Семья"
        },
        {
          "id": 7,
          "title": "ЗОЖ"
        }
      ]
    }
  }
}
````

</details>

<details>
<summary>Получение библиотеки /api/client/v2/summaries/get-list</summary>

### Постраничное получение библиотеки саммари с фильтрами по темам

````
POST /api/client/v2/summaries/get-list
````

Request Headers:

````
Authorization: Bearer access_token
````

Request body json:

````json
{
  "data": {
    "is_load_full_lib": 0,
    "language": "ru",
    "page": 1,
    "on_page": 1,
    "themes": [
      7,
      3,
      1,
      4
    ],
    "full_themes": 1,
    "channel": "android"
  }
}
````

Если указан **is_load_full_lib=1** , то **page,
on_page, themes** игнорируются и передается полная библиотека.

**page** - страница ответа<br>
**on_page** - кол-во саммари на странице<br>
**themes** - массив тем саммари, может быть пустым или отсутствовать<br>
**full_themes** - к ответу прибавляется детализированный список тем саммари (аналог
*[/api/client/v2/themes/get-list/v2](#возвращает-полный-список-тем-саммари)*)<br>

200 Response json:

````json
{
  "data": {
    "summaries": [
      {
        "summary_id": 1,
        "title": "Никогда не ешьте в одиночку и другие правила нетворкинга",
        "title_en": "Never Eat Alone and Other Secrets to Success, One Relationships at a Time",
        "authors": "Кейт Феррацци, Тал Рэз",
        "authors_en": "Keith Ferrazzi, Tahl Raz",
        "audio": {
          "duration_ms": 942000
        },
        "themes": [
          1,
          2
        ],
        "similar_summaries": [
          383,
          97,
          91,
          39,
          20
        ],
        "sponsor": null,
        "slug": "nikogda-ne-eshte-v-odinochku-i-drugie-pravila-netvorkinga",
        "attributes": [
          3
        ],
        "is_has_infographics": true
      }
    ],
    "meta": {
      "attributes": [
        {
          "id": 1,
          "title": "new"
        },
        {
          "id": 2,
          "title": "free"
        },
        {
          "id": 3,
          "title": "audio"
        },
        {
          "id": 4,
          "title": "recommend"
        },
        {
          "id": 5,
          "title": "first_time_ru"
        },
        {
          "id": 6,
          "title": "popular"
        },
        {
          "id": 7,
          "title": "coming_soon"
        }
      ],
      "themes": [
        {
          "id": 1,
          "title": "Саморазвитие"
        },
        {
          "id": 2,
          "title": "Бизнес"
        },
        {
          "id": 3,
          "title": "Деньги"
        },
        {
          "id": 4,
          "title": "Технологии"
        },
        {
          "id": 5,
          "title": "Общество"
        },
        {
          "id": 6,
          "title": "Семья"
        },
        {
          "id": 7,
          "title": "ЗОЖ"
        }
      ]
    }
  }
}
````

</details>



<details>
<summary>Получение детализации саммари /api/client/v2/summary/get-full-data/v2</summary>

### Возвращает всю информацию о запрошенном саммари по ID

````
POST /api/client/v2/summary/get-full-data/v2
````

Request Headers:

````
Authorization: Bearer access_token
````

Request body json:

````json
{
  "data": {
    "summary_id": 41
  }
}
````

200 Response json:

````json
{
  "data": {
    "summary_id": 41,
    "title": "Отдел продаж под ключ",
    "title_en": null,
    "authors": "Сергей Капустин, Дмитрий Крутов",
    "authors_en": null,
    "audio": {
      "duration_ms": 1764467
    },
    "themes": [
      2
    ],
    "themes_v2": [
      {
        "id": 1,
        "depth_level": 1,
        "weight": 9
      },
      {
        "id": 2,
        "depth_level": 2,
        "weight": 9
      },
    ],
    "similar_summaries": [
      447,
      370,
      43,
      32,
      5
    ],
    "sponsor": null,
    "attributes": [
      3,
      4,
      4
    ],
    "testing": {
      "id": 334,
      "title": null,
      "max_score": 0,
      "score_to_pass": 0,
      "questions": [
        {
          "id": 56193,
          "title": "Отметьте правильную последовательность «воронки продаж» по мере сужения…",
          "answers": [
            {
              "id": 223771,
              "title": "встречи, сделки, звонки",
              "is_correct": false
            },
            {
              "id": 223772,
              "title": "звонки, встречи, сделки",
              "is_correct": true
            }
          ]
        },
        {
          "id": 56204,
          "title": "По каким параметрам правильнее всего сегментировать клиентов?",
          "answers": [
            {
              "id": 223815,
              "title": "Прибыльные и неприбыльные",
              "is_correct": false
            },
            {
              "id": 223816,
              "title": "Допустим каждый из вариантов, в зависимости от изучаемого при анализе вопроса",
              "is_correct": true
            }
          ]
        }
      ]
    },
    "current_time": "2023-12-15T11:36:02+03:00",
    "slug": "otdel-prodazh-pod-klyuch",
    "is_has_infographics": false
  }
}
````

200 Error response:
````json
{
    "errors": [
        {
            "code": 3004,
            "message": "Саммари отсутсвует",
            "details": 9141
        }
    ],
    "data": null,
    "warnings": null
}
````

</details>

<details>
<summary>Получение обложки саммари /api/client/v2/summary/{{ book_id }}/file/get/cover</summary>

### Возвращает JPEG изображение обложки запрошенного саммари

````
GET /api/client/v2/summary/{{ book_id }}/file/get/cover
````

Request Headers:

````
Authorization: Bearer access_token
````

200 Response raw image.

</details>




<details>
<summary>Получение MP3 файла саммари /api/client/v2/summary/{{ book_id }}/file/get/audio</summary>

### Возвращает MP3 файл запрошенного саммари

````
GET /api/client/v2/summary/{{ book_id }}/file/get/audio
````

Request Headers:

````
Authorization: Bearer access_token
````

200 Response MP3 file.

</details>

<details>
<summary>Получение EPUB файла саммари /api/client/v2/summary/{{ book_id }}/file/get/epub</summary>

### Возвращает EPUB файл запрошенного саммари

````
GET /api/client/v2/summary/{{ book_id }}/file/get/epub
````

Request Headers:

````
Authorization: Bearer access_token
````

200 Response EPUB file.

</details>



<details>
<summary>Получение описания саммари /api/client/v2/summary/{{ book_id }}/file/get/intro</summary>

### Возвращает HTML блок с текстом запрошенного саммари

````
GET /api/client/v2/summary/{{ book_id }}/file/get/intro
````

Request Headers:

````
Authorization: Bearer access_token
````

200 Response raw:

````html
<p>Согласно Денису Каплунову, коммерческое предложение — это война за первое впечатление. За одного клиента на рынке сражаются сотни компаний. Текст в этой войне — орудие массового поражения. Идеальная оферта формирует имидж компании и начинается с уважения к партнеру. Как минимум, ее следует посылать заинтересованному человеку. Вот почему холодная рассылка в последние годы приносит слабые результаты. Удачное предложение должно быть корректным, логичным, выделять конкретные преимущества товара или услуги и быть взаимовыгодным. Денис Каплунов предлагает подробное руководство по написанию взвешенного продающего текста. Владелец крупнейшей в России студии копирайтинга учит, как предложить сотрудничество и получить согласие.</p><h3 dir="ltr">АВТОРЫ</h3><p>Денис Каплунов начал заниматься копирайтингом, заинтересовавшись рассылкой о заработке в интернете. Он не любит термин «продающий текст». Однако самое эффективное коммерческое предложение от Дениса Каплунова привело к сделке стоимостью 4,5 миллиона долларов. Продающим он называет любой текст, который приносит результат. Будучи основателем крупнейшей в России студии копирайтинга, он говорит о себе: «Мой лучший текст еще не написан».</p><h3 dir="ltr">ПОЧЕМУ НУЖНО ЧИТАТЬ ЭТУ КНИГУ</h3><p><br />— Понять, почему некоторые коммерческие предложения не работают.<br />— Научиться писать эффективные коммерческие предложения.<br />— Расставлять в продающих текстах правильные акценты.</p>
````

</details>

<details>
<summary>Единый метод получения данных о саммари /api/client/v2/file/get</summary>

###

````
POST /api/client/v2/file/get
````

Request Headers:

````
Authorization: Bearer access_token
````

Request body form-data:

````form-data
data[summary_id]: {{ book_id }}
data[type]: [audio|cover|epub|intro]
````

200 Response raw body:


</details>


<details>
<summary></summary>

###

````
````

Request Headers:

````
Authorization: Bearer access_token
````

Request body json:

````json
````

200 Response json:

````json
````

</details>


2023 Smartreading.ru 