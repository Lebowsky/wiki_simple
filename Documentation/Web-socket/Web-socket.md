---
title: Web-socket
description: 
published: true
date: 2024-01-25T14:56:54.413Z
tags: 
editor: markdown
dateCreated: 2024-01-25T07:44:11.346Z
---

# Web-socket

**ConnectWebSocket** – соединиться с веб сокетом. Пример: `hashMap.put("ConnectWebSocket","ws://192.168.1.41:8765")`

**WSOnConnectHandlers** – подключить обработчики события успешного соединения с сокетом.
Пример: 
```python
json_web = [{"action": "run",
			 "type": "python",
			 "method": "ws_connect"}]
hashMap.put("WSOnConnectHandlers",json.dumps(json_web))
```

**WSOnMessageHandlers** - подключить обработчики события получения сообщения. Само сообщение приходит в переменной _WebSocketMessage_

**WSOnCloseHandlers** - подключить обработчики события нормального завершения соединения.

**WSOnFailureHandlers** - подключить обработчики события потери соединения.

**WebSocketSend** – команда отправки сообщения в сокет.

**CloseWebSocket** – команда завершения соединения. Также можно закрывать соединения со стороны сервера например.

## Особенности работы

> 1. При разрыве соединения автоматически происходит переподключение каждую секунду. Чтобы остановить попытки надо удалить переменную _ConnectWebSocket_
>     
> 2. При начальном соединении автоматически посылается сообщение в формате `id:<AndroidID>` . Это можно использовать для идентификации пользователей.