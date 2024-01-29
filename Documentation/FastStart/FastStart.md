---
title: FastStart
description: 
published: true
date: 2024-01-29T10:30:15.632Z
tags: 
editor: markdown
dateCreated: 2024-01-26T10:34:57.952Z
---

## Пример 1. Создание процесса, добавление надписи, кнопки, подключение python обработчика

Ссылка на конструктор
1) Создаем новый проект
2) Необходимо создать новый процесс
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126134630.png">
<img src="/files/Pastedimage20240126134752.png"> 
</details>

3) Необходимо добавить к нашему процессу экран, который у нас будет отображаться и придумаем ему имя
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126135020.png">
<img src="/files/Pastedimage20240126135127.png"> 
</details>

4) Добавим контейнер и начнем его наполнять
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126135332.png">
<img src="/files/Pastedimage20240126135423.png"> 
</details>

5) Добавим надпись, и сделаем ее значение "Value" (текст который будет отображаться) в виде переменной "@text_example", знак @ обязательно использовать перед названием переменной.
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126135530.png">
<img src="/files/Pastedimage20240126135938.png"> 
<img src="/files/Pastedimage20240126140057.png"> 
</details>

6) Добавим кнопку при нажатии на которую будет выводиться текст. Укажем "Value" (Текст, который будет отображаться на кнопке) и Variable - переменная, которая будет отправляться в "listener" (переменная, которая имеет значение последнего элемента действия/нажатия. Далее в коде познакомимся с ней поближе)
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126140200.png">
<img src="/files/Pastedimage20240126140653.png"> 
</details>

7) Необходимо добавить **"Handlers"** к нашему экрану, "Handlers" - обработчики, которые срабатывают в зависимости от каких-либо действий. Мы добавим 2 обработчика
	- onStart - обработчик, который будет срабатывать при открытии экрана
	- onInput - обработчик, который будет срабатывать при нажатии на кнопки
	В обработчиках обязательно необходимо указать **"Method"**, это название функции в Python, которая будет отрабатывать
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126141145.png">
<img src="/files/Pastedimage20240126141211.png"> 
<img src="/files/Pastedimage20240126141239.png"> 
</details>

8) Необходимо создать файл **.py** где будут храниться наши обработчики и добавить этого файл во вкладку Python files
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126144410.png">
</details>

9) Добавляем в наш Python файл 2 функции для обработчиков, которые добавили в пункте 7
Все переменные, события, команды передаются через стек hashMap и возвращаются через него же. 
Функции hashMap
- put("key", "value") - помещает в hashMap 
- get("key") - получить из hashMap
- containsKey("key") - проверяет существование функцией
- remove("key") - удаляет из hashMap

**Имейте ввиду что это не словарь Python а Java-объект, вызываемый из Python.**

```python
def start_example(hashMap,_files=None,_data=None):  
    hashMap.put("text_example", "Этим текстом мы наполняем переменную в TextView")  
    return hashMap  
  
  
def input_example(hashMap, _files=None, _data=None):  
    if hashMap.get("listener") == "btn_click":  
        hashMap.put("toast", "Вы нажали на кнопку!!!")  
    return hashMap
```

10) Теперь нам необходимо в приложении на телефоне отсканировать QR-код из конструктора и после этого перезагрузить приложение
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126151049.png">
</details>

11) Теперь у нас в приложении появился процесс "Пример 1" при клике на него мы увидим, что переменная "@text_example" заполнилась, значение, которое мы передали с помощью `hashMap.put("text_example", "Этим текстом мы наполняем переменную в TextView")`. При клике на кнопку, будет выводиться текст, который мы задали с помощью 
```python
    if hashMap.get("listener") == "btn_click":  
        hashMap.put("toast", "Вы нажали на кнопку!!!")  
```
Подробнее про "toast" можно почитать [тут](../GeneralFunctionsOfThePlatform/GeneralFunctionsOfThePlatform) во вкладке "Уведомление и тосты"
<details>
<summary>Результаты</summary>
<br>
<img src="/files/Pastedimage20240126151642.png">
<img src="/files/Pastedimage20240126151707.png"> 
<img src="/files/Pastedimage20240126151819.png"> 
</details>

## Пример 2. Работа с NoSQL(SimpleBase)

## Пример 3. Добавление товара в SQL базу. Вывод информации о товаре с помощью сканирования его штрихкода

Реализуем 2 процесса.
1) Добавление в SQL базу данных о штрихкоде, его номер и название товара.
2) Сканирование штрихкода и получение данных отсканированного товара.

Подробнее про SQL можно прочитать [тут](../DataStorage/DataStorage)

**Шаги реализации**

1) Добавляем "Общий обработчик", который будет отрабатывать при старте приложения и создавать SQL таблицу
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129112554.png">  
<img src="/files/Pastedimage20240129112613.png">  
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

3) Создадим процесс для добавление данных о товаре и добавим экран для него. На экране разместим, строки для ввода данных и кнопку для сохранения данных.
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129111614.png">  
<img src="/files/Pastedimage20240129111638.png">
<img src="/files/Pastedimage20240129111657.png">
</details>

4) Добавим обработчик для обработки события при нажатии на кнопку "Сохранить"
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129113315.png">
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
<img src="/files/Pastedimage20240129114423.png">
</details>

6) Можно проверить создалась ли у нас таблица в БД и заполнилась ли она. В конструкторе необходимо выбрать "SQL Query" и ввести туда запрос.
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129114933.png">
<img src="/files/Pastedimage20240129115057.png">
</details>

7) Теперь нам необходимо создать процесс для Сканирование штрихкода и добавить экран где у нас будет находиться сканер штрихкодов (barcode) и текстовое поле для вывода информации.
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129115447.png">
<img src="/files/Pastedimage20240129115500.png">
<img src="/files/Pastedimage20240129115533.png">
<img src="/files/Pastedimage20240129115550.png">
</details>

8) Необходимо добавить обработчик, который будет отрабатывать при сканирование товара и заполнять данные для "@info_about_good".
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129115734.png">
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

10) Результат
<details>  
<summary>Результат</summary>  
<br>  
<img src="/files/Pastedimage20240129120518.png">
<img src="/files/Pastedimage20240129122638.png">
</details>
