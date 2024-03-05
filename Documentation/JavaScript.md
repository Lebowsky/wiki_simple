---
title: JavaScript
description: 
published: true
date: 2024-03-05T11:27:49.548Z
tags: 
editor: markdown
dateCreated: 2024-03-05T09:02:27.291Z
---

# JavaScript
1. **Исполнение JavaScript на Android:**
	- JavaScript исполняется встроенным в Android браузером.
	- Скрипты выполняются в рамках сессии, т.е. каждый скрипт вызывается и исполняется при событии.
1. **Хранение переменных и инстансов:**
    - Переменные и инстансы не сохраняются между сессиями, аналогично Python.
3. **Доступность обработчиков JavaScript:**
    - Обработчики JavaScript доступны везде, где и обычные обработчики.
4. **Использование JavaScript для работы с JSON:**
    - JavaScript вполне подходит для парсинга JSON.
    - В Simple почти все основано на JSON: элементы интерфейса, хранение данных, команды и т. д.
5. **Преимущества JavaScript для SimpleUI:**
    - Хорошо реализована работа с JSON, что важно для Simple.
    - JavaScript удобен для написания небольших скриптов для обработки событий в SimpleUI.

JavaScript взаимодействует с Simple, используя архитектуру обработчиков событий (Архитектура 2.0), как и все остальные обработчики. Для получения и отправки данных и команд используется стек переменных. Это означает, что как и в других обработчиках, JavaScript имеет доступ ко всем командам стека переменных, который представляет собой объект типа hashMap.

Однако использование команд из стека не всегда удобно, так как они выполняются по окончании обработчика событий. Например, если требуется выполнить запрос к базе данных или отобразить прогресс выполнения операции, это хочется сделать немедленно в рамках текущего обработчика. Для этого часть таких команд вынесена в отдельный модуль, к которому можно обращаться напрямую через модуль android.

Например, команда 
```android.toast('Привет мир')```
выведет всплывающее уведомление (тост) немедленно, без ожидания завершения обработчика события.
## Интерфейсные команды
- **toast**(String) – вывести сообщение Андроид 
```JavaScript
android.toast("Hello")
```
- **speak**(String) – произнести текст (TTS engine)
```JavaScript
android.speak("Hello")
```
- **vibrate**() и **vibrate**(int duration) – вибрация и вибрация заданной длительностью в м/с
```JavaScript
android.vibrate(100)
```
- **beep**() - звуковой сигнал
```JavaScript
android.beep()
```
- **beep**(int tone) - звуковой сигнал с возможность выставить тон(от 1 до 99)
```JavaScript
android.beep(44)
```
- beep(int tone,int beep_duration,int beep_volume) – звуковой сигнал с возможностью выбрать тон (от 1 до 99) и продолжительность с громкостью (по умолчанию – 100)
```JavaScript
android.beep(44, 50, 50)
```
- **notification**(String message) - Уведомление в шторке 
```JavaScript
android.notification("Уведомление")
```
- notification (String message,String title)  - Уведомление в шторке, с названием
```JavaScript
android.notification("Уведомление", "Название уведомления")
```
- notification(String message,String title,int number) – Уведомление в шторке, с названием и с number, где number – идентификатор уведомления, по которому к нему можно потом обратиться, чтобы либо убрать, либо перезаписать(обновить)
```JavaScript
android.notification("Уведомление", "Название уведомления", 2)
```
- **notification_progress**(String message,String title,int number,int progress) – уведомление с прогресс-баром (от 0 до 100)
```JavaScript
android.notification_progress("Уведомление", "Название уведомления", 2, 54)
```
- **notification_cancel**(number) – скрыть уведомление, number - номер уведомления
```JavaScript
android.notification_cancel(2)
```
## Взаимодействие с SQL

Взаимодействие с SQLite описано в соответствующем разделе [документации](./DataStorage/SQL), приведенные ниже команды просто повторяют аналогичные команды через стек переменных, только возвращают результат сразу внутри обработчика.

Общие приемы – аналогичны, в частности перед началом работы нужно определить СУБД, с которой работаешь, создать таблицы, если их нет.

**SQLExec**(String query, String params) – выполнить команду SQL (кроме SELECT)
```JavaScript
android.SQLExec("CREATE TABLE IF NOT EXISTS students(name TEXT, age INTEGER)","");
let new_record=[hashMap.name,Number(hashMap.age)];
let res = android.SQLExec("insert into students(name, age) values (?,?)",JSON.stringify(new_record));
```
**SQLExecMany**(String query, String params) - выполнить несколько команд  SQL (кроме SELECT) в BULK- режиме

**SQLQuery**(String query, String params) – выполнить SELECT
```JavaScript
let res = android.SQLQuery("SELECT * from students","");
```
## Взаимодействие с JSON-ориентированной СУБД SimpleBase

Подробно описано в соответствующей статье и специальной [документации](./DataStorage/NoSQL), тут просто приведен интерфейс методов

**SimpleBaseInsert**(String database, String collection_name,String value) – добавить документ(JSON)
```JavaScript
let new_record={"name":hashMap.name,"age":Number(hashMap.age)}
var id = android.SimpleBaseInsert("my_db","students",JSON.stringify(new_record));
android.toast("ID записи = "+String(id))
```
**SimpleBaseUpsert**(String database, String collection_name,String value) – добавить в режиме upsert

**SimpleBaseUpdate**(String database, String collection_name,String condition,String value) – обновление документа выбранными значениями

**SimpleBaseDelete**(String database, String collection_name,String condition) – удалить документ

**SimpleBaseAll**(String database, String collection_name) – получить все документы
```JavaScript
let res = android.SimpleBaseAll("my_db","students");
```
**SimpleBaseFind**(String database, String collection_name,String condition) – найти документ по условию

## Взаимодействие с key-value NoSQL СУБД  
Иногда просто нужно хранить данные в режиме ключ-значение, для этого есть простая СУБД, доступная в т.ч. и из других обработчиков

**NoSQLPut**(String database, String key,String value) – положить в книгу значение с ключом
```JavaScript
android.NoSQLPut("base", "КЛЮЧ", "Придумали значение")
```
**NoSQLGet**(String database, String key) – достать значение по ключу
```JavaScript
let a = android.NoSQLGet("base", "КЛЮЧ")
```
**NoSQLDelete**(String database, String key) – удалить значение
```JavaScript
android.NoSQLDelete("base", "КЛЮЧ")
```
**NoSQLGetAllKeys**(String database) – получить список всех ключей в книге
```JavaScript
android.NoSQLGetAllKeys("base")
```