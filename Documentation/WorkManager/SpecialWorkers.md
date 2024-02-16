---
title: SpecialWorkers
description: 
published: true
date: 2024-02-16T12:58:31.263Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:24:48.239Z
---

## Особые воркеры для скачивания и отправки файлов
Несмотря на то, что описанные выше воркеры могут решать любые задачи, включая отправку файлов, предусмотрено еще 2 команды, которые заточены именно на отправку и получение файлов – StartUploadWorkRequest и StartDownloadWorkRequest, тому есть причины:

1.     Самое главное – эти задачи передают и скачивают файлы в бинарном виде в режиме multipart, т.е. поддерживают докачку и постоянное соединение, что критично для больших файлов и слабых каналов. Даже для небольших файлов (фотографий), при наличии слабого канала есть смысл использовать данный тип фонового задания, тем более это очень просто. 
2.     Соответственно раз есть Boundary и цикл побайтового чтения, то в этот цикл вписывается прогрессбар в шторке уведомлений, что позволяет контролировать прогресс выполнения
3.     Упрощенный вызов для таких задач: если вам надо что-то оправить или скачать, достаточно указать настройки подключения и имя файла, остальное сделается автоматически, сразу можно определить postExecute на событие после загрузки

Для скачивания:
```Python
hashMap.put(StartDownloadWorkRequest, {"request": "описание запроса", "tag": "тег задачи", "title": "необязательный, заголовок в шторке уведомлений","body": "необязательный, текст в уведомлении"})
```
- Описание запроса: {"url": "URL или псевдоним точки доступа","method": "метод HTTP","file": "имя файла, куда будет производиться запись","postExecute": "при необходимости, массив обработчиков по окончанию выполнения"}. Если используется альяс, предварительно записанный в HTTPAddAlias, то как правило, в нем есть все необходимое для подключения – авторизация, заголовки. Если не используется то можно определить сразу в описании запроса.

```Python
def upload_input(hashMap,_files=None,_data=None):
    if hashMap.get('listener')=='photo':
        filename =hashMap.get("photo_path") 
        postExecute=[{"action":"run","type":"python","method":"request_upload_callback"}]
        username=""
        password=""
        userpass = username + ':' + password
        encoded_u = base64.b64encode(userpass.encode()).decode()
        r = {"url":"http://192.168.1.41:3000/upload", "auth":"Basic %s" % encoded_u,"method":"POST", "headers":{"Accept":"*/*"},"file":filename,"postExecute":postExecute}
        hashMap.put("StartUploadWorkRequest",json.dumps({"request":r,"tag":"my_task_upload"},ensure_ascii=False))
    if hashMap.get('listener')=='btn_stop':    
        hashMap.put("StopWork","my_task_upload")
    
    return hashMap  
```

Для отправки:
```Python
hashMap.put(StartUploadWorkRequest, {"request": "описание запроса","tag": "тег задачи","title": "необязательный, заголовок в шторке уведомлений","body": "необязательный, текст в уведомлении"})
``` 
Описание запроса(request): {"url": "URL или псевдоним точки доступа","method": "метод HTTP","file": "имя файла, куда будет производиться запись","postExecute": "при необходимости, массив обработчиков по окончанию выполнения"}.
```Python
def download_input(hashMap,_files=None,_data=None):
    if hashMap.get('listener')=='btn_run':
        filename =suClass.get_temp_file("mp4") 
        postExecute=[{"action":"run","type":"python","method":"request_download_callback"}]
        r = {"url":"#long1c/download","method":"GET","file":filename,"postExecute":postExecute}
        hashMap.put("StartDownloadWorkRequest",json.dumps({"request":r,"tag":"my_task_download","title":"Загрузка","body":"видео.mp4"},ensure_ascii=False))
    return hashMap  
```
