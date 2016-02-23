# Nurline API v 1.1
# Регистрация
URL: http://cabinet.nurline.kz/php/reg.php

#### Запрос:
```
{
	method: 'register',
	email: [email]',
	password: [пароль],
	phone: [телефон],
	name: [Имя пользователя]
}
```
#### Ответ:
```
{
	status:[0 - email уже зарегистрирован, 1 - успешно]
}
```


---------



# Логин
URL:http://cabinet.nurline.kz/php/reg.php
#### Запрос:
```
{
	method:'login',
	email:'email',
	password:'password'
}

```
#### Ответ:
```
{
	status:[0 - неверный логин/пароль, 1-email не подтвержден, 2 - успешный вход],
	token:[token]
}
```

---------

# Все запросы, кроме регистрации и логина отправляются POST запросом на:
http://cabinet.nurline.kz/php/server.php

# Получение списков камер и объектов
#### Запрос:
```
{
	command:'cams',
	method:'get',
	token:[token]
}

```
#### Ответ:
```
{
	status:[статус (0 - ошибка, 1 - успешно)],
	objects:[{
		id: [Идентификатор объекта в Nurline]
		name: [Имя объекта]
		description: [Описание объекта]
		img: [URL к изображению объекта]
		note: [Примечание объекта]
	}],
	cams:[{
		id: [Идентификатор камеры в Nurline]
		name: [Имя камеры]
		description: [Описание камеры]
		active: [1/0-активный/неактивный]
		fav: [1/0 - избранный]
		lat: [Широта]
		lon: [Долгота]
		note: [Примечание камеры]
		object: [ID объекта]
		object_title: [Имя объекта]
		preview: [URL к изображению]
		pub: [1/0 - публичный]
		uuid: [Идентификатор для просмотра]
	}]
}
```

---------
# Просмотр камеры
#### Запрос:
```
{
	command:'api',
	method:'view_cam',
	token:[token],
	uuid:[Идентификатор для просмотра]
}


```
#### Ответ:
 (Почти все как у мегакама, за исключением значения timings, это временные интервалы для архива камервы)
```
{
	archive_enabled: [true/false]
	archive_hls_template: "http://5.251.235.199/hls/9788_low.m3u8?auth=1930dc65c5557f747356e5373684a96c"
	archive_url_list: "http://megacam.kz/rest/archiveList/token/VE7heNQuzJUaRaem60BzHHtr6kB2q7tR5nAumQZmNDyiSGoQNVbcqhYHrIpF82Me/session_id/26f89ec5b546703692f201cf044f81e4"
	archive_url_template: "rtmp://5.251.235.199:1935/nvr/::9788?auth=26f89ec5b546703692f201cf044f81e4&t={start}000"
	category_id: 0
	code: 0
	coordinates: [51.16241453822, 71.420112932101]
	desc: "ЖК "Гранд Алатау" УЛ. ВХОД С ПАРКИНГА"
	name: "ГА-Камера №11"
	preview: "http://grandalatau.cdn.camflows.kz/screenshots/Y8CUxBJ2KyKW.jpg"
	session_id: "26f89ec5b546703692f201cf044f81e4"
	session_id_low: "1930dc65c5557f747356e5373684a96c"
	timing: {time: 1456051630,…}
	code: 0
	time: 1456051630
	timings: [{start: 1454928600, end: 1455344021}, {start: 1455344080, end: 1456051456}] // Тайминги
	uuid: "Y8CUxBJ2KyKW"
	url: "rtmp://5.251.235.199:1935/live/::9788?auth=26f89ec5b546703692f201cf044f81e4"
	url_hls: "http://5.251.235.199/hls/9788_low.m3u8?auth=1930dc65c5557f747356e5373684a96c"
	url_low: "rtmp://5.251.235.199:1935/live/::9788?auth=1930dc65c5557f747356e5373684a96c"
	uuid: "Y8CUxBJ2KyKW"
}
```


---------
# Добавление в избранное
#### Запрос:
```
{
	command:'cams',
	method:'fav',
	token:[token],
	id:[id камеры (не uuid)],
}
```
#### Ответ:
```
{
	status:[статус (0 - ошибка, 1 - успешно)]
}
```

---------
# Добавление заметки к камере
#### Запрос:
```
{
	command:'cams',
	method:'note',
	token:[token],
	id:[id камеры (не uuid)],
	note:[заметка, текст]
}
```
#### Ответ:
```
{
	status:[статус (0 - ошибка, 1 - успешно)]
}
```

---------
# Добавление заметки к объекту
#### Запрос:
```
{
	command:'cams',
	method:'object_note',
	token:[token],
	id:[id объекта],
	note:[заметка, текст]
}
```
#### Ответ:
```
{
	status:[статус (0 - ошибка, 1 - успешно)]
}
```

---------
# Добавление объекта по PIN коду
#### Запрос:
```
{
	command:'cams',
	method:'addByPin',
	token:[token],
	pin:[PIN код]
}
```
#### Ответ:
```
{
	status:[статус (0 - ошибка, 1 - успешно)],
	object:{
		id: [Идентификатор объекта в Nurline]
		name: [Имя объекта]
		description: [Описание объекта]
		img: [URL к изображению объекта]
		note: [Примечание объекта]
	},
	cams:[{
		id: [Идентификатор камеры в Nurline]
		name: [Имя камеры]
		description: [Описание камеры]
		active: [1/0-активный/неактивный]
		fav: [1/0 - избранный]
		lat: [Широта]
		lon: [Долгота]
		note: [Примечание камеры]
		object: [ID объекта]
		object_title: [Имя объекта]
		preview: [URL к изображению]
		pub: [1/0 - публичный]
		uuid: [Идентификатор для просмотра]
	}]
}
```



---------
# Информация акаунта
#### Запрос:
```
{
	"command": "users",
	"method": "info",
	"token": ""
}
```
#### Ответ:
```
{
	"email": "me@blackcat95.ru",
	"name": "",
	"surname": null,
	"phone": "",
	"id": 25,
	"avatar": [URL],
	"tarif": 1,
	"balance": 0,
	"email_confirmed": 1,
	"phone_confirmed": 0,
	"ban": 0
}
```

---------
# Настройки акаунта (имя/телефон)
#### Запрос:
```
{
	command:'users',
	method:'save',
	token:[token],
	name:[name],
	phone:[phone]
}
```
#### Ответ:
```
{
	status:[статус (0 - ошибка, 1 - успешно)]
}
```
---------
# Изменить пароль
#### regex для пароля 
```
/(?=^.{6,}$)(?=.*\d)(?=.*[A-Za-z]).*$/
```

#### Запрос:
```
{
	command:'password',
	method:'change',
	password:[password],
	token:[token]
}
```
#### Ответ:
```
{
	status:[статус (0 - пароль не соответвует regex, 1 - изменен)]
}
```