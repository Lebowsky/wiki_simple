---
title: StartShina
description: 
published: true
date: 2024-11-19T11:41:22.011Z
tags: 
editor: markdown
dateCreated: 2024-11-19T10:20:41.443Z
---

# Старт Шины
Пример шины - [https://github.com/dvdocumentation/simplebus](https://github.com/dvdocumentation/simplebus) 
Измените в simplebus.py строку №34 с 

```python
from persistqueue import Queue, PDict
```

на

```python
from persistqueue.queue import Queue
```

Запуск производим через simplebus.py  
переменную **URL** меняем на ваш ip адрес
переменная **HTTPPort** - порт для HTTP (указывайте который не занят)
переменная **WSPORT** - порт для WebSocket (указывайте который не занят)

## Регистрация пользователя

Переходим по пути и регистрируем пользователя 
```python
http://URL:HTTPORT
```

## Подключение через настройки
<img src="/files/Pasted image 20241106143743.png" width=400>

Где **URL** - ваш ip адрес
**WSPort** - порт WEBSocket
**HTTPPort** - порт HTTP
**Bus Password** - пароль созданного пользователя
**SimpleBus ID** - логин созданного пользователя
Далее - "Сохранить"

Если все удачно, то получим в шине подобное сообщение
<img src="/files/Pasted image 20241106144346.png" width=400>