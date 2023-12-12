# Документация API

v1.0 2023-12-11 volcan0

Существует ряд методов для регистрации и авторизации пользователей не требующих токена авторизации.<br>
Метод регистрации требует партнерский ключ доступа к API.<br>
Все остальные методы требуют Bearer Token в заголовке запроса.

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