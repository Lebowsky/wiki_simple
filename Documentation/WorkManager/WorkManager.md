---
title: WorkManager
description: 
published: true
date: 2024-02-13T09:55:30.152Z
tags: 
editor: markdown
dateCreated: 2024-02-13T08:04:15.781Z
---

# WorkManager
Преимущества использования WorkManager:
- Задачи будут выполняться даже в случае, если приложение неактивно или отключено.
- Даже после перезагрузки устройства без ограничения по времени. 
- Мы можем установить условия выполнения задачи, например, когда устройство находится на зарядке или имеется интернет-соединение.
-  Периодические задачи будут выполняться по расписанию независимо от обстоятельств.

Когда мы создаем воркер, мы передаем задачу Андроиду, а дальнейшая судьба этой задачи зависит от операционной системы. Нет необходимости в мониторинге выполнения задачи, так как это обязанность операционной системы. ОС также контролирует условия выполнения задачи, такие как доступ к Интернету. Если условие выполнения не выполнено, задача не будет запущена, но как только условие будет выполнено, система автоматически начнет выполнение задачи. В то же время, Simple продолжает свою работу независимо.

## Однократные фоновые задания
Для запуска используется команда -переменная "**StartWork**",  в качестве параметра которой передается json с обработчиками, которые надо выполнить, и тегом задачи. Тег нужен для того, чтобы в случае чего по нему можно было обратиться и отменить выполнение:

```Python
hashMap.put(StartWork, {"work": "массив обработчиков",
						"tag": "тег задачи",
						"retry": "флаг повтора",
						"conditions": "список условий"})
```
- work - унифицированный массив обработчиков, `[{"action":"run","type":"python","method":"some_longtime_routine"}]`
- tag - нужен для того, чтобы в случае чего по нему можно было обратиться и отменить выполнение.
- retry - заставляет в случае неудачи выполнения (исключение в коде или ошибка http-запроса >200), переключаться в состояние RETRY, что ставит задачу снова в очередь выполнения. 
- conditions - устанавливает условия запуска задачи, их может быть одно или несколько сразу (разделитель – “;”). Условия следующие:
    - CONNECTED – наличие связи
    - CHARGING – устройство находится на зарядке
    - BATTERY_NOT_LOW – заряд батареи достаточен
    - IDLE – устройство не используется


Выполнение Python и выполнение некоторых команд зависит от контекста приложения, т.е. например, чтобы выполнить ShowScreen, нужно, чтобы было хотя бы в свернутом виде запущено приложение Simple и открыт какой то процесс в нем. Для speak нужен просто контекст приложения, чтобы был запущен TTS – менеджер. То есть, другими словами, некоторые команды не выполнятся, если приложение вообще не запущено или находится в сне. Но есть команды, которые будут выполнены даже если девайс перезапущен и в памяти не висит SimpleUI. Например, работа с СУБД через нативный обработчик – без проблем, HTTP-запросы – тоже без проблем. Например:
```Python
def run_request_task_native(hashMap,_files=None,_data=None):  
    hashMap.put("BreakHandlersIfError","")  
    
    workercode=[{"action":"run","type":"http","method":"GET #long1c/get_goods"},
			    {"action":"run","type":"set","method":"SQLParameter=@ResultMessage"},
			    {"action":"run","type":"sql","method":"insert into goods(art,barcode,nom) values(?,?,?)"},
			    {"action":"run","type":"set","method":"speak=Данные загружены"}]		    
          
    hashMap.put("StartWork",json.dumps({"work": workercode, "tag": "my_single_task", "retry": True, "conditions":"BATTERY_NOT_LOW;CHARGING;CONNECTED"}, ensure_ascii=False))  
		      
    return hashMap
```
Обработчик отработает и после перезагрузки устройства, но команда speak не отработает, т.к приложение отсутствует в процессах.

## Периодические задания
Выполняются с определенной периодичностью, определение задачи такое же, как у однократной, только указывается период. RETRY для периодических не работает. 
```Python
hashMap.put("StartPeriodicWork", {"work": "массив обработчиков",
                                  "period": "период",
                                  "tag": "тэг задачи",
                                  "conditions": "список условий"})  
```

- work - унифицированный массив обработчиков, `[{"action":"run","type":"python","method":"some_longtime_routine"}]`
- period - период задается в минутах, не менее 15 минут. Если указано менее 15 минут, то будет выполняться раз в 15 минут.
- tag - нужен для того, чтобы в случае чего по нему можно было обратиться и отменить выполнение.
- conditions - устанавливает условия запуска задачи, их может быть одно или несколько сразу (разделитель – “;”). Условия следующие:
    - CONNECTED – наличие связи
    - CHARGING – устройство находится на зарядке
    - BATTERY_NOT_LOW – заряд батареи достаточен
    - IDLE – устройство не используется
    
```Python
def run_periodic_worker(hashMap,_files=None,_data=None):
    if hashMap.get("listener") == "btn_run_periodic": workercode=[{"action":"run","type":"set","method":"beep"}]         
	  hashMap.put("StartPeriodicWork",json.dumps({"work":workercode,"period":15,"tag":"periodic1","conditions":"CONNECTED"},ensure_ascii=False))

    if hashMap.get("listener") == "btn_stop_periodic":
    	hashMap.put("StopWork","periodic1")
    
    return hashMap  
```

## Остановка задач
```Python
hashMap.put("StopWork", "TagName")
```
Останавливает задачу с определенным тегом. Это может быть периодическая задача или однократная в состоянии RETRY
- TagName - tag указанный в фоновом задании

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
Описание запроса: {"url": "URL или псевдоним точки доступа","method": "метод HTTP","file": "имя файла, куда будет производиться запись","postExecute": "при необходимости, массив обработчиков по окончанию выполнения"}

```Python
def download_input(hashMap,_files=None,_data=None):
    if hashMap.get('listener')=='btn_run':
        filename =suClass.get_temp_file("mp4") 
        postExecute=[{"action":"run","type":"python","method":"request_download_callback"}]
        r = {"url":"#long1c/download","method":"GET","file":filename,"postExecute":postExecute}
        hashMap.put("StartDownloadWorkRequest",json.dumps({"request":r,"tag":"my_task_download","title":"Загрузка","body":"видео.mp4"},ensure_ascii=False))
    return hashMap  
```
