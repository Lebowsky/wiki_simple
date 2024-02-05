---
title: Debugging
description: 
published: true
date: 2024-02-05T09:44:41.864Z
tags: 
editor: markdown
dateCreated: 2024-01-25T07:43:20.903Z
---

# Отладка
## Консоль запросов
Прежде всего, если для хранения используется SQL СУБД, для просмотра содержимого таблиц, проверки работы запросов, которые используются в скриптах рекомендуется использовать "Консоль SQL запросов"(SQL Query). Устройство и вызывающая обработка должны использовать одну подсеть, так как отправка запросов идет на веб-сервис приложения. В запросах можно передать параметры. Можно использовать все возможности SQLlite – служебные таблицы и т.д.
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240122163152.png" width=1100>
<br>
<img src="/files/Pastedimage20240122163211.png" width=1100> 
</details>


## Логирование
Для получения промежуточных данных можно использовать логирование и выводить тосты особым способом (внутри кода обработчика). Таким образом можно получать как значения переменных так и например логировать датасеты запросов не в начале/конце обработчика а именно внутри кода. Записи логов отправляются http-запросами. Пример общего модуля сервисных процедур для этого:
```python
import sqlite3
from sqlite3.dbapi2 import Error
import requests
import json
import java
from requests.auth import HTTPBasicAuth
from com.chaquo.python import Python

# Процедуры для отладки python-скриптов
def query_to_json(query, args=()):
    conn = sqlite3.connect('//data/data/ru.travelfood.simple_ui/databases/SimpleWMS')
    cursor = conn.cursor()
    cursor.execute(query, args)
    result = [dict((cursor.description[i][0], value) \
               for i, value in enumerate(row)) for row in cursor.fetchall()]
    cursor.connection.close()
    return result

def send_debug_msg(hashMap,tag,message):
    username = hashMap.get("WS_USER")
    password = hashMap.get("WS_PASS")
    url = hashMap.get("WS_URL")

    py_toast( url)

    r = requests.get(url+"/python_debug?tag="+tag+"&message="+message, auth=HTTPBasicAuth(username, password),
           headers={'Content-type': 'application/json', 'Accept': 'text/plain'})

def send_debug_query(hashMap,tag,message,query, args):
    username=hashMap.get("WS_USER")
    password=hashMap.get("WS_PASS")
    url = hashMap.get("WS_URL")

    r = requests.get(url+"/python_debug?tag="+tag+"&message="+message, auth=HTTPBasicAuth(username, password),
         headers={'Content-type': 'application/json', 'Accept': 'text/plain'},data=json.dumps(query_to_json(query, args=())))

def py_toast( msg):
        from android.widget import Toast
        Toast.makeText(Python.getPlatform().getApplication(), msg,
                       Toast.LENGTH_SHORT).show()
```

- **send_debug_msg** – отсылает сообщения в лог
- **send_debug_query** – выполняет произвольный запрос с параметрами, результат упаковывает в датасет JSON
- **py_toast** – выводит тост внутри скрипта средствами Android SDK. Работает только из обработчиков Python

Пример использования:
```python
import sys
sys.path.append("/data/user/0/ru.travelfood.simple_ui/files")
import ui_global
import json
a = 2
hashMap.put("a","1")
ui_global.py_toast(hashMap.get("a"))
ui_global.send_debug_msg(hashMap,"line 3",str(a))
a += 1
ui_global.send_debug_msg(hashMap,"line 4",str(a))
ui_global.send_debug_query(hashMap,"sql","SELECT * FROM goods_bp","SELECT * FROM goods_bp",None)
```
