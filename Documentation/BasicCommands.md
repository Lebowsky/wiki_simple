---
title: BasicCommands
description: 
published: true
date: 2024-02-16T12:12:15.149Z
tags: обработчик, экран, диалог, процесс, уведомления, toast, screen, handler, beep, speak, звук, речь, notification, show, event, runpy, функции, getjson
editor: markdown
dateCreated: 2024-01-25T07:43:02.141Z
---

> **[Экраны, диалоги и процессы](/Documentation/BasicСommands/ScreensDialogsProcesses)**
{.is-info}

> **[Запуск процессов из процессов](/Documentation/BasicСommands/ProcessFromProcess)**
{.is-info}

> **[Команды управления обработчиками](/Documentation/BasicСommands/ManagingHandlers)**
{.is-info}

> **[Уведомления, звуки и речь](/Documentation/BasicСommands/NotificationsSoundsSpeech)**
{.is-info}

> **[Динамическое изменение элементов экрана и конфигурации в целом](/Documentation/BasicСommands/DynamicChange)**
{.is-info}




# Основные команды






## Динамическое изменение элементов экрана и конфигурации в целом
**getJSONScreen** записывает в переменную **JSONScreen** исходную структуру текущего экрана. 
```Python
hashMap.put("getJSONScreen","")
```
**setJSONScreen** применяет измененную структуру экрана	
**getJSONConfiguration** - считывает в переменную _configuration текущую конфигурацию 
```Python
hashMap.put("getJSONConfiguration","")
```
**setJSONConfiguration** - применяет измененную конфигурацию немедленно.

## Прочие команды Экранов
**RunCV** - запуск режима AciveCV из экрана. После завершения ActiveCV в таком варианте запуска, возникает событие ввода с listener=ActiveCV 
```Python
hashMap.put("RunCV","NameCV")
```
**StartMediaGallery** - запуск выбора файла из галереи мультимедиа, котрый можно инициировать из кода (т.е. определить на свою кнопку например) 
```Python
hashMap.put("StartMediaGallery", "photo_from_camera")
```
**StartCaptureCamera** - запуск камеры 
```Python
hashMap.put("StartCaptureCamera","photo_from_camera")  
```
**SetTitle**, параметра: заголовок экрана - переопределение заголовка экрана 
```Python
hashMap.put("SetTitle","Новый заголовок")
```
**PrintPreview** ,параметр:html-строка - запуск окна с предпросмотром html. Для например, печатных форм, которые из этого окна можно отправить на принтер 
```Python
def test_html_input(hashMap, _files=None, _data=None):
    test_template = Template("""{% for user in users -%}
    <p>Привет, {{ user }}!</p>
    {% endfor %}""")
    res = test_template.render(users=["admin", "Alex", "prog1C"])

    hashMap.put("PrintPreview", res)

    return hashMap
```
[![Pastedimage20240213144851.png](/files/Pastedimage20240213144851.png =350x)](/files/Pastedimage20240213144851.png)
**PrintService** команда запуска PDF-документа на печать встроенной службой печати. В качестве значения нужно передать строку параметров запроса который пойдет на сервер.
```Python
hashMap.put("PrintService","operation=print, barcode=123")
```
Если print не работает - попробуйте view. Это зависит от устройства и софта.
[Подробнее](../ComputerVisionAndAugmentedRealityActiveCV/ComputerVisionAndAugmentedRealityActiveCV)

## Прочие функции, запускаемые из фонового сервиса или общих обработчиков
**ShowProcessScreen**, параметр: {"process": "process", "screen": "screen"} - запуск любого экрана любого процесса из любого состояния приложения (в случае если основной контекст приложения запущен) 
```Python
hashMap.put("ShowProcessScreen", "{'process': 'Некий процесс','screen': 'Экран 1'}")
```
**SpeechRecognitionListener**, в качестве значения можно указать количество миллисекунд отсрочки. Дело в том, что обычно запуск ввода осуществляется после озвучки голосом какого то вопроса, а эта звучка может длится какое то время, причем асинхронно. Поэтому надо примерно поставить время отсрочки пока ваш вопрос звучит, чтобы прослушивание не запустилось раньше
В случае успешного распознавания генерируется событие ввода **voice_success** и в переменную **voice_result** возвращается результат
**SendIntent** - отправка из фона некоего события ввода, на которое подписаны экраны и ActiveCV (там возникает событие ввода) 
**BackgroundCommand** - команда, которой можно передать управление в фоновый Сервис событий и запустить там какой то обработчик

## Команды Python
**RunPy** - запускает синхронное выполнение скрипта Python в UI-потоке приложения. В качестве параметра передается скрипт в виде Base64-строки. Устаревшее, рекомендуется использовать запуск массива обработчиков. 
**RunPyThreadDef** - запускает асинхронное фоновое выполнение скрипта Python. В качестве параметра передается имя функции 
**RunPyThreadProgressDef** - аналогично команде **RunPyThread** , но запускает прогресс-бар, который блокирует UI-поток. В качестве аргумента - имя функции.

