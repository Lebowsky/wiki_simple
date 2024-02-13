---
title: Web-socket
description: 
published: true
date: 2024-02-13T14:44:58.949Z
tags: веб-сокет, web-socket
editor: markdown
dateCreated: 2024-01-25T07:44:11.346Z
---

# Web-socket

**ConnectWebSocket** – соединиться с веб сокетом.
```Python
hashMap.put("ConnectWebSocket","ws://192.168.1.41:8765")
```

**WSOnConnectHandlers** – подключить обработчики события успешного соединения с сокетом.
Пример: 
```python
json_web = [{"action": "run",
			 "type": "python",
			 "method": "ws_connect"}]
hashMap.put("WSOnConnectHandlers",json.dumps(json_web))
```

**WSOnMessageHandlers** - подключить обработчики события получения сообщения. Само сообщение приходит в переменной _WebSocketMessage_
```Python
hashMap.put("WSOnMessageHandlers",json.dumps([{"action":"run","type":"python","method":"ws_message"}] ))

def ws_message(hashMap,_files=None,_data=None):
    
    message = hashMap.get("WebSocketMessage")

    jmessage = json.loads(message)

    hashMap.put("speak",jmessage.get("message",""))
    hashMap.put("basic_notification",json.dumps([{"number":1,"title":"Чат","message":jmessage.get("message","")}]))
    hashMap.put("_messages",add_message_to_table(hashMap,jmessage.get("message",""),jmessage.get("user","")))
    #hashMap.put("basic_notification",hashMap.get("messages"))
    hashMap.put("RefreshScreen","")
        conn = sqlite3.connect('//data/data/ru.travelfood.simple_ui/databases/SimpleWMS')

    try:
        сursor1 = conn.cursor()
        сursor1.execute("insert into chat(body,title,sender,sent) values (?,?,?,?)", (message,jmessage.get("message",""),jmessage.get("user",""),0))
        conn.commit()
    except sqlite3.Error as err:
        hashMap.put("toast","Ошибка SQL"+str(err))
        raise ValueError(err) 

        
    conn.close()

    hashMap.put("UpdateChat","")

    return hashMap    
```
**WSOnCloseHandlers** - подключить обработчики события нормального завершения соединения.
```Python
hashMap.put("WSOnCloseHandlers",json.dumps([{"action":"run","type":"python","method":"ws_close"}] ))

def ws_close(hashMap,_files=None,_data=None):
    
    hashMap.put("speak","Соединение с чатом закрыто")
    hashMap.put("_wsConnected","false")

    return hashMap 
```
**WSOnFailureHandlers** - подключить обработчики события потери соединения.
```Python
hashMap.put("WSOnFailureHandlers",json.dumps([{"action":"run","type":"python","method":"ws_failure"}] ))

def ws_failure(hashMap,_files=None,_data=None):
    import time
    hashMap.put("speak","Ошибка соединения")
    hashMap.put("_wsConnected","false")
    return hashMap  
```

**WebSocketSend** – команда отправки сообщения в сокет.
```Python
hashMap.put("WebSocketSend",hashMap.get("message"))
```

**CloseWebSocket** – команда завершения соединения. Также можно закрывать соединения со стороны сервера например.

## Особенности работы

> 1. При разрыве соединения автоматически происходит переподключение каждую секунду. Чтобы остановить попытки надо удалить переменную _ConnectWebSocket_
>     
> 2. При начальном соединении автоматически посылается сообщение в формате `id:<AndroidID>` . Это можно использовать для идентификации пользователей.