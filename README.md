# Документация API
v1.0 2023-12-11 volcan0

Существует ряд методов для регистрации и авторизации пользователей не требующих токена авторизации.
Все отсальные методы требуют Bearer Token в заголовке запроса.

## Авторизация
<details>

<summary>
	Авторизация по Email /api/client/v2/auth/email
</summary>

### Получение токена доступа по email пользователя.

```
/api/client/v2/auth/email
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
