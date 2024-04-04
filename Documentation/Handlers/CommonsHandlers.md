---
title: CommonsHandlers
description: 
published: true
date: 2024-04-04T14:39:26.242Z
tags: 
editor: markdown
dateCreated: 2024-04-03T21:31:49.665Z
---

# Общие обработчики
[![Pastedimage20240122162004.png](/files/Pastedimage20240122162004.png =850x)](/files/Pastedimage20240122162004.png)
> **onLaunch** 
> При запуске перед формированием главного меню. Так как вызывается до формирования меню, то в этом обработчике например можно перерисовать меню или заполнить плитки. По сути заменяет [Таймер](../Screens/Screens) с периодом -1, который также можно использовать для этой цели. 
{.is-info}

> **onIntentBarcode**
> Получение штрихкода через подписку на Intent на уровне платформы в целом(до экрана). Например может использоваться для работы со сканером без экранов, либо для предпроверки штрихкодов. В переменные помещается: listener=”barcode”, barcode - штрихкод 
{.is-info}


>**onBluetoothBarcode**
>Получение штрихкода от подключенного Bluetooth-сканера на уровне платформы в целом. В переменные помещается: listener=”barcode”, barcode - штрихкод {.is-info}
 
> **onBackgroundCommand** 
> Получение события onBackgroundCommand в сервисе событий, отправленного из какого то обработчика (командой-переменной BackgroundCommand ) . В listener помещается аргумент команды BackgroundCommand 
{.is-info}

> **onRecognitionListenerResult** 
> События по результату распознавания речи после использования команды voice в сервисе. В переменные помещается: listener=”voice_success”, voice_result="распознанная фраза" 
{.is-info}

> **onIntent** 
> Получение сообщения от другого Андроид-приложения (подписка на Intent). Из сообщения извлекается поле “body” и помещается в переменную. Через него можно передавать данные от другого приложения. 
{.is-info}

> **onWebServiceSyncCommand**
> Получение команды через встроенный веб-сервер приложения. На адрес веб-сервиса <адрес устройства>:8095 можно послать запрос GET или POST вида 
> `http:/{ip}:8095?mode=SyncCommand&listener={NameListener}`
> Пример отправки
>```python
>query = 'http://127.0.0.1:8095/?mode=SyncCommand&listener=put_data' 
>json_data = 'json файл' 
>our_headers = {'Content-Type': 'Application/json; charset=utf-8'} 
>requests.post(query, json=json_data, headers=our_headers)
>```
> Обработчик может что то поместить в переменные и все переменные отправляются назад в виде JSON объекта. Но, можно также не отправлять все переменные а переопределить ответ(например сделать не JSON а строковый) с помощью команды WSResponse 
{.is-info}


> **onSQLDataChange** и **onError**
> Возникают при выполнении любой записи в SQL если запрос идёт через SQL-провайдера (onError в случае ошибки). Таким образом можно например перехватывать записываемые данные централизованно и помещать их в очередь на отправку. 
{.is-info}


> **onOpenFile**
> Событие, в котором можно получить файл, открытый приложением. С приложением можно поделиться текстовым файлом любым способом (через Поделиться… и через Открыть с помощью…) даже если приложение не открыто. При этом срабатывает обработчик и в переменные content и extra_text помещается содержимое файла и ссылка на файл.
{.is-info}

> **onProcessClose
> При закрытии любого экрана, будет отрабатывать наш обработчик
>```python
>            {
>              "event": "onProcessClose",
>              "listener": "",
>              "action": "run",
>              "type": "python",
>              "method": "on_process_close",
>              "postExecute": ""
>            }
>```
>
>```python
>def on_process_close(hashMap, _files=None, _data=None):
>    hashMap.put("toast", "Вышли с экрана")
>    return hashMap
>```
>Пример кода
{.is-info}

