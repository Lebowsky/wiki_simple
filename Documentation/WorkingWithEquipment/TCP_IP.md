---
title: TCP_IP
description: 
published: true
date: 2024-02-19T08:06:27.134Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:24:56.915Z
---

## Подключение к устройству через TCP_IP (только отправка)
Возможно только из python-обработчика. Работа заключается в вызове Java-функции `write_socket(String host,int port, String message,String charset)` из модуля SimpleUtilites:
```python
from ru.travelfood.simple_ui import SimpleUtilites as su
su.write_socket(IP, port, data, handlers)
```
- IP, port – IP-адрес и порт (9100 по умолчанию) принтера
- data – либо байт-массив либо строка(UTF-8) данных
- handlers – строка-массив обработчиков в случае неудачи

Функция возвращает `True` в случае успешной отправки и `False` – во всех остальных случаях
