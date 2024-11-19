---
title: OnSimpleBusMessage
description: 
published: true
date: 2024-11-19T10:00:36.725Z
tags: 
editor: markdown
dateCreated: 2024-11-19T09:54:50.650Z
---

# OnSimpleBusMessage
Общее событие, происходящие в момент приема сообщения, у пользователя, для которого предполагалось сообщение

<img src="/files/Pastedimage20241112120701.png" width=400>

Пример работы:
```python
from general import *

sbmessage = json.loads(hashMap.get("SBMessage")) # Получаем информацию о сообщении
message = sbmessage['message'] # Текст сообщения
sender = sbmessage['sender'] # Отправитель
android.toast(str(message)) # Тост с сообщением 
hashMap.put("basic_notification",
			json.dumps([{"title":f"От{sender}","message":message}],ensure_ascii=False))
			# Создание уведомления с информацией от кого сообщение и с его содержанием
```

## SBMessage

Содержит основную информацию о сообщении и о том кто ее отправил.

message - текст сообщения
sender - отправитель
tags - тэги по которым было отправлено
uid - версии uid для кого сообщение

Можно отправлять данные по своим ключам при желании. Предварительно добавив его в само сообщение