---
title: MethodsOfSending
description: 
published: true
date: 2024-11-19T11:27:04.609Z
tags: 
editor: markdown
dateCreated: 2024-11-19T10:15:08.193Z
---

# Параметры и отправка сообщений

## Отправка сообщений

Работа с сообщениями происходит в два основных шага

1) Отправка сообщения на шину происходит через **SendBus**, происходит проверка для каких пользователей это сообщение и отправка им, в сообщение добавляется поле **sender** (отправитель)
2) При поступлении сообщения к пользователю происходит общее событие **onSimpleBusMessage**, в стеке переменных содержится переменная **SBMessage** с текстом сообщения

## Id

Добавление пользователей не обязательно можно производить через 
```python
http://URL:HTTPORT
```
Так-же существует возможность отправлять через requests.post по пути 
```python
http://URL:HTTPORT/put_users
```

Но при requsts.post необходимо использовать HTTPBasicAuth с логином и паролем, пользователя созданного до этого.

```Python
url = f'http://URL:HTTPORT/put_users'  
username = #Логин пользователя существующего до этого
password = #Пароль
  
# Сообщение для отправки  
new_user = [{"_id": "id нового пользователя", "password": "Пароль нового пользователя"}]  
  
# Отправка POST-запроса с JSON в body и базовой авторизацией  
response = requests.post(  
    url,  
    json=new_user,  # Тело запроса - JSON  
    auth=HTTPBasicAuth(username, password),  # Базовая авторизация  
    headers={"Content-Type": "application/json",  
             "Message-Type": "queue"})  # Установка заголовка
```

Пример кода:

```python
url = f'http://{self.hash_map.get("http_shina")}/put_users'  
username = self.hash_map.get("id_user")  
password = self.hash_map.get("password_user")  
  
# Сообщение для отправки  
new_user = [{"_id": self.hash_map.get("id_user"), "password": self.hash_map.get("password_user")}]  
  
# Отправка POST-запроса с JSON в body и базовой авторизацией  
response = requests.post(  
    url,  
    json=new_user,  # Тело запроса - JSON  
    auth=HTTPBasicAuth(username, password),  # Базовая авторизация  
    headers={"Content-Type": "application/json",  
             "Message-Type": "queue"})  # Установка заголовка
```


Отправка сообщения по id пользователя, перед id используем @

```python
message = {"to": ["@user1"], "message": "текст сообщения"}  
self.hash_map.put("SendBus", json.dumps(message, ensure_ascii=False))
```


## Тэги

Тэги - подписка пользователя к какой-то группе пользователей (админ, пользователь, подписчик и т.д) или по какому-то признаку (первые, главные и т.д)

Добавление тэга к пользователю так-же как и с новым пользователем, можно добавить к старому пользователю тэг или создать нового пользователя с тэгом

```Python
url = f'http://URL:HTTPORT/put_users'  
username = #Логин пользователя существующего до этого, если тэг с существующему пользователю, то можно и его
password = #Пароль
  
# Сообщение для отправки  
new_tag = [{"_id": "id нового пользователя", "password": "Пароль нового пользователя", "tags": "Новый тэг"}]  
  
# Отправка POST-запроса с JSON в body и базовой авторизацией  
response = requests.post(  
    url,  
    json=new_tag,  # Тело запроса - JSON  
    auth=HTTPBasicAuth(username, password),  # Базовая авторизация  
    headers={"Content-Type": "application/json",  
             "Message-Type": "queue"})  # Установка заголовка
```


Отправка сообщения по tags, перед tag используем #

```python
message = {"to": ["#name_tag"], "message": f"Текст: {text}\nДля тэгов: {messages_for}"}  
self.hash_map.put("SendBus", json.dumps(message, ensure_ascii=False))
```

## UID

Способ узнать текущий uid версии:

<img src="/files/Pasted image 20241112115559.png" width=400>

Обращение по uid, в отправке сообщения SendBus можно указать одним из атрибутов

```python 
# Если один uid
uid: "uid конфига"

# Если несколько uid
uid: ["uid конфа 1", "uid конфа 2"]
```

Если uid не установлен, то сообщение будет передаваться текущей конфигурации (которая в данный момент выполняется) затем всем остальным конфигурациям.

Если uid задан то в том же порядке будут отбираться конфигурации, которым нужно передать сообщение.