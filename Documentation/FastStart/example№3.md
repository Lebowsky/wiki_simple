---
title: example№3
description: 
published: true
date: 2024-02-15T13:47:04.640Z
tags: 
editor: markdown
dateCreated: 2024-02-15T10:16:09.639Z
---

## Пример 3. Добавление товара в SQL базу. Вывод информации о товаре с помощью сканирования его штрихкода

Реализуем 2 процесса.
1) Добавление в SQL базу данных о штрихкоде, его номер и название товара.
2) Сканирование штрихкода и получение данных отсканированного товара.

Подробнее про SQL хранение можно прочитать [тут](../DataStorage/DataStorage)

**Шаги реализации**

### Добавление общего обработчика
1) Добавляем "Общий обработчик"(Common handlers), который будет отрабатывать при старте приложения и создавать SQL таблицу
- Event - onLaunch
- Action - run
- Method - init_on_start(Имя обработчика)
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129112554.png" width="900">
<br>  
<img src="/files/Pastedimage20240129112613.png" width="700">  
</details>  

2) Напишем содержание этого обработчика
```python
def init_on_start(hashMap,_files=None,_data=None):  
    hashMap.put("SQLConnectDatabase","") 
    hashMap.put("SQLExec", json.dumps({"query": "create table IF NOT EXISTS InfoBarcode(id integer primary key autoincrement, barcode text, name text)", "params": ""}))  
    return hashMap
```
- SQLConnectDatabase - подключение к базе данных, если указать пустую строку то будет БД по умолчанию “SimpleWMS”.
- SQLExec - Запрос на изменение БД, создаем новую таблицу

### Создание процесса данных о товаре
3) Создадим процесс для добавление данных о товаре и добавим экран для него. На экране разместим контейнер LinearLayout, в контейнер добавим следующие элементы:
- TextView(Текстовая плашка), Value - "Введите название"
- EditTextText(Поле ввода), Value - @name_good, Variable - name_good
- TextView(Текстовая плашка), Value - "Введите штрихкод"
- EditTextText(Поле ввода), Value - @barcode_good, Variable - barcode_good
- Button(кнопка), Value - "Сохранить данные", Variable - btn_save
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129111614.png" width="700">
<br>  
<img src="/files/Pastedimage20240129111638.png" width="700">
<br>
<img src="/files/Pastedimage20240129111657.png" width="700">
</details>

### Добавление обработчика
4) Добавим(Add) обработчик(Handlers) для обработки события при нажатии на кнопку "Сохранить".
- Event - onInput
- Action - run
- Type - python
- Method - input_save
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129113315.png" width="700">
</details>

5) Напишем содержание этого обработчика
```python
from ru.travelfood.simple_ui import SimpleSQLProvider as sqlClass

def input_save(hashMap,_files=None,_data=None):  
    if hashMap.get("listener") == "btn_save":  
        sql = sqlClass()  
        success = sql.SQLExec("insert into InfoBarcode(barcode,name) values(?,?)",  
                              hashMap.get('barcode_good') + "," + hashMap.get("name_good"))  
        if success:  
            hashMap.put("toast", "Добавлено")  
    return hashMap
```
Считываются данных из строк для ввода и сохраняются в таблицу ранее созданную.
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129114423.png" width="400">
</details>

### Проверка SQL
6) Можно проверить создалась ли у нас таблица в БД и заполнилась ли она. В конструкторе необходимо выбрать "SQL Query" и ввести туда SQL запрос.
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129114933.png" width="700">
<br>
<img src="/files/Pastedimage20240129115057.png" width="700">
</details>

### Создание процесса для сканирования штрихкода
7) Теперь нам необходимо создать процесс для Сканирование штрихкода и добавить экран где у нас будет находиться сканер штрихкодов (barcode) и текстовое поле для вывода информации.
- barcode, Variable - barcode
- В LinearLayout, добавим TextView(Текстовое поле), Value - @info_about_good
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129115447.png" width="700">
<br>
<img src="/files/Pastedimage20240129115500.png" width="700">
<br>
<img src="/files/Pastedimage20240129115533.png" width="700">
<br>
<img src="/files/Pastedimage20240129115550.png" width="700">
</details>

### Добавление обработчика
8) Необходимо добавить обработчик(Handlers), который будет отрабатывать при сканирование товара и заполнять данные для "@info_about_good".
- Event - onInput
- Action - run
- Type - python
- Method - scan_barcode
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129115734.png" width="700">
</details>

9) Напишем код для обработчика
```python
from ru.travelfood.simple_ui import SimpleSQLProvider as sqlClass

def scan_barcode(hashMap,_files=None,_data=None):  
    if hashMap.get("listener") == "barcode":  
        sql = sqlClass()  
        query = sql.SQLQuery(f"SELECT name FROM InfoBarcode WHERE barcode = {hashMap.get('barcode')}", "") #Запрос  
        result = json.loads(query) #Преобразуем json результат, для последующей обработки  
        if query:  
            hashMap.put("info_about_good", json.dumps(result[0]["name"], ensure_ascii=False)) #Заполняем строку данных  
        else:  
            hashMap.put("toast", "Такого нет")  
    return hashMap
```
- SQLQuery - запрос выборки (SELECT) возвращает ответ в json в том же формате, в котором описываются таблицы

### Результат
10) Результат
<details>  
<summary>Результат</summary>  
<br>  
<img src="/files/Pastedimage20240129120518.png" width="400">
<br>
<img src="/files/Pastedimage20240129122638.png" width="400">
</details>
