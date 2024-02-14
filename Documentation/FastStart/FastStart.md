---
title: FastStart
description: 
published: true
date: 2024-02-14T06:47:50.508Z
tags: sql, nosql, хранение данных, быстрый старт, simplebase, sqlexec, sqlclass, sqlquery, activecv, надпись, обработчик
editor: markdown
dateCreated: 2024-01-26T10:34:57.952Z
---

## Запуск конструктора и вот это вот все
Сюда надо будет добавить ссылки туда сюда

## Пример 1. Создание процесса, добавление надписи, кнопки, подключение python обработчика


Ссылка на конструктор
1) Создаем новый проект
2) Необходимо создать новый процесс, в конструкторе выбрать вкладку "Proccesses", для добавление нажать кнопку "Add".

<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126134630.png" width=700>
<br>
<img src="/files/Pastedimage20240126134752.png" width=700>
<br>
</details>


3) Необходимо добавить к нашему процессу экран, который у нас будет отображаться и придумаем ему имя. В конструкторе на вкладке "Proccesses", необходимо нажать "Add" под надписью "Screens"
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126135020.png" width=700>
<br>
<img src="/files/Pastedimage20240126135127.png" width=700> 
</details>

4) Добавим контейнер и начнем его наполнять. Зайдите в созданный "экран", в нем перейдите на вкладку "Elements", нажмите "Add" и далее выберите "LinearLayout" 
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126135332.png" width=700>
<br>
<img src="/files/Pastedimage20240126135423.png" width=700> 
</details>

5) Добавим(Add) в контейнер(LinearLayout) надпись(TextView), и сделаем ее значение "Value" (текст который будет отображаться) в виде переменной "@text_example", знак @ обязательно использовать перед названием переменной.

<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126135530.png" width=700>
<br>
<img src="/files/Pastedimage20240126135938.png" width=700> 
<br>  
<img сlass="big" src="/files/Pastedimage20240126140057.png"> 
</details>


6) Добавим(Add) в контейнер(LinearLayout) кнопку(button) при нажатии на которую будет выводиться текст. Укажем "Value" (Текст, который будет отображаться на кнопке) и Variable - переменная, которая будет отправляться в "listener" (переменная, которая имеет значение последнего элемента действия/нажатия. Далее в коде познакомимся с ней поближе)
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126140200.png" width=700>
<br>
<img src="/files/Pastedimage20240126140653.png" width=700> 
</details>

7) Необходимо добавить **"Handlers"** к нашему экрану, "Handlers" - обработчики, которые срабатывают в зависимости от каких-либо действий. Мы добавим 2 обработчика
	- onStart - обработчик, который будет срабатывать при открытии экрана. Дадим ему имя(Method) - start_example
	- onInput - обработчик, который будет срабатывать при нажатии на кнопки. Дадим ему имя(Method) - input_example
  
В обработчиках обязательно необходимо указать **"Method"**, это название функции в Python, которая будет отрабатывать
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126141145.png" width=700>
<br>
<img src="/files/Pastedimage20240126141211.png" width=700> 
<br>
<img src="/files/Pastedimage20240126141239.png" width=700> 
</details>

8) После добавления всех основных элементов в экран, необходимо обязательно **сохранить**(save project)
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240206172225.png" width=700>
</details>


9) Необходимо создать файл **.py** где будут храниться наши обработчики(start_example и input_example), которые мы добавили до этого в Handlers. Добавим этот файл во вкладку Python files в конструкторе
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126144410.png">
</details>

10) Добавляем в наш Python файл 2 функции для обработчиков, которые добавили в пункте 7
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

11) Теперь нам необходимо в приложении на телефоне отсканировать QR-код из конструктора и после этого перезагрузить приложение. В настройках приложения на телефоне выбрать "QR-настройки", а в конструкторе выбрать вкладку "QR settings"
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240126151049.png" width=1100>
</details>

12) Теперь у нас в приложении появился процесс "Пример 1" при клике на него мы увидим, что переменная "@text_example" заполнилась, значение, которое мы передали с помощью `hashMap.put("text_example", "Этим текстом мы наполняем переменную в TextView")`. При клике на кнопку, будет выводиться текст, который мы задали с помощью 
```python
    if hashMap.get("listener") == "btn_click":  
        hashMap.put("toast", "Вы нажали на кнопку!!!")  
```
Подробнее про "toast" можно почитать [тут](../GeneralFunctionsOfThePlatform/GeneralFunctionsOfThePlatform) во вкладке "Уведомление и тосты"
<details>
<summary>Результаты</summary>
<br>
<img src="/files/Pastedimage20240126151642.png" width="400">
<br>
<img src="/files/Pastedimage20240126151707.png" width="400"> 
<br>
<img src="/files/Pastedimage20240126151819.png" width="400"> 
</details>

## Пример 2. Работа с NoSQL(SimpleBase)

Реализовать будем с помощью SimpleBase, подробнее прочитать можно [тут](../DataStorage/DataStorage).
1) Создадим процесс и добавим в него новый экран. Экран у нас будет содержать контейнер(LinearLayout), контейнер мы наполним следующими элементами: 
- Поле для ввода новой информации. EditTextText, Value - @name_object, Variable - name_object
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129152240.png" width=700>
</details>
- Поле для вывода данных из БД. TextView, Value - @names_elements
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129152310.png" width=700>
</details>
- Кнопку сохранения новой информации. Button, Value - Добавить, Variable - btn_add
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129152350.png" width=700>
</details>
- Кнопку полной очистки БД. Button, Value - Очистить БД, Variable - btn_delete
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129152420.png" width=700>
</details>

2) Так же к нашему экрану, необходимо добавить обработчик(Handlers), который будет обрабатывать при открытии экрана (OnStart). К нему мы привяжем вывод информации из БД в переменную "names_elements"
  ! **ВАЖНО**
  OnStart отрабатывает не только в тот момент, когда мы открыли экран, но и после каждого события OnInput. На OnInput мы сделаем привязку нажатия на клавиши "Добавить" и "Очистить БД". При нажатии на клавишу у нас будет отрабатывать логика, которую мы пропишем в OnInput и после этого автоматически отработает логика, которая прописана в OnStart.
  Эту логику можно отключить с помощью 
  ```Python 
  hashMap.put("noRefresh", "")
  ```
  подробнее [тут](../Screens/Screens)
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129155736.png" width=700>
</details>
```python
from pysimplebase import SimpleBase  
from ru.travelfood.simple_ui import SimpleUtilites as suClass    
  
  
def start_simplebase(hashMap,_files=None,_data=None):  
    db = SimpleBase("test_db",  
                    path=suClass.get_simplebase_dir(),  
                    timeout=200)  
    result = db['goods'].all()  
    list_result = [x["name"] for x in result]  
    hashMap.put("names_elements", str(list_result))  
    return hashMap
```

3) Обработчик OnInput
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129155918.png" width=700>
</details>
```python
def input_simplebase(hashMap,_files=None,_data=None):  
    if hashMap.get("listener") == "btn_add":  
        db['goods'].insert({"name": hashMap.get("name_object")}) #Добавление из поля name_object данных в БД
        hashMap.put("toast", "Сохранено")  
    elif hashMap.get("listener") == "btn_delete":  
        db['goods'].clear()  # Очистка БД
        hashMap.put("toast", "База очищена")  
    return hashMap
```

4) Результат
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129160228.png" width=450>
</details>


## Пример 3. Добавление товара в SQL базу. Вывод информации о товаре с помощью сканирования его штрихкода

Реализуем 2 процесса.
1) Добавление в SQL базу данных о штрихкоде, его номер и название товара.
2) Сканирование штрихкода и получение данных отсканированного товара.

Подробнее про SQL хранение можно прочитать [тут](../DataStorage/DataStorage)

**Шаги реализации**

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

6) Можно проверить создалась ли у нас таблица в БД и заполнилась ли она. В конструкторе необходимо выбрать "SQL Query" и ввести туда SQL запрос.
<details>  
<summary>Фотогайд</summary>  
<br>  
<img src="/files/Pastedimage20240129114933.png" width="700">
<br>
<img src="/files/Pastedimage20240129115057.png" width="700">
</details>

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

10) Результат
<details>  
<summary>Результат</summary>  
<br>  
<img src="/files/Pastedimage20240129120518.png" width="400">
<br>
<img src="/files/Pastedimage20240129122638.png" width="400">
</details>

## Пример 4. Режим дополненной реальности, вывод информации о товаре в реальном времени.

Подробнее про компьютерное зрение можно прочитать [тут](../ComputerVisionAndAugmentedRealityActiveCV/ComputerVisionAndAugmentedRealityActiveCV)
Реализуем 2 процесса
1) SimpleBase база данные, куда мы будем добавлять значения с помощью полей ввода и сохранять по нажатию кнопки. Подробнее про [SimpleBase](../DataStorage/DataStorage)
2) ActiveCV процесс, в котором при наведении на штрихкод, будет проверяться его значение в базе данных и если данные о продукте добавлены в базу данных, то будем выводить название и кол-во товара в реальном времени

**Шаги реализации**

1) Создание базы данных мы будем производить как в "Примере 2"
На экран добавим контейнер(LinearLayout) заполним его:
- TextView(Текстовое поле), Value - Имя элемента
- EditTextText(Поле ввода), Value - @name_element, Variable - name_element
- TextView(Текстовое поле), Value - Штрихкод
- EditTextText(Поле ввода), Value - @barcode, Variable - barcode
- TextView(Текстовое поле), Value - Количество элементов
- EditTextText(Поле ввода), Value - @amount, Variable - amount
- Button(Кнопка), Value - Сохранить, Variable - btn_save
[![Pastedimage20240201173232.png](/files/Pastedimage20240201173232.png =850x)](/files/Pastedimage20240201173232.png)


```python
def input_bd(hashMap,_files=None,_data=None):  
    db = SimpleBase("test_db",  
                    path=suClass.get_simplebase_dir(),  
                    timeout=200)  
    if hashMap.get("listener") == "btn_save":  
        db['goods'].insert({"name": hashMap.get("name_element"), "barcode": hashMap.get("barcode"), "amount": hashMap.get("amount")})  
    return hashMap
```

2) Для работы с компьютерным зрением нам необходимо создать процесс ActiveCV, и добавить обработчик на событие "OnObjectDetected"
### **Надо будет добавить фотографий из нового обработчика!!!!**
```python
def object_detect(hashMap,_files=None,_data=None):  
    db = SimpleBase("test_db",  
                    path=suClass.get_simplebase_dir(),  
                    timeout=200)  
    result = db['goods'].all() # Получаем все данные из БД
    list_result = [[x["name"], x["amount"]] for x in result if x["barcode"] == str(hashMap.get("current_object"))] #Получаем имя и кол-во товара по штрихкоду(barcode)
    json_list = [{"object": str(hashMap.get("current_object")),  
                 "caption": str(": ".join(list_result[0]))}]  
    hashMap.put("object_caption_list", json.dumps(json_list, ensure_ascii=False))  
    return hashMap
```

В случае первого обнаружения штрихкода, отрабатывает событие "OnObjectDetected", при первом данные о штрихкоде направляются в переменную "current_object". С помощью команды **object_caption_list** можно передать json-объект, где 
- object - штрихкод 
- caption - данные, которые мы хотим отображать
, при наведении на штрихкод у нас будет выводиться информация, которую мы передали.
Подробнее информация [тут](../ComputerVisionAndAugmentedRealityActiveCV/ComputerVisionAndAugmentedRealityActiveCV)

Результат
[![Pastedimage20240201181332.png](/files/Pastedimage20240201181332.png =350x)](/files/Pastedimage20240201181332.png)