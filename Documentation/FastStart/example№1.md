---
title: example№1
description: 
published: true
date: 2024-02-15T12:45:53.559Z
tags: 
editor: markdown
dateCreated: 2024-02-15T10:16:05.912Z
---

## Пример 1. Создание процесса, добавление надписи, кнопки, подключение python обработчика
### Создание процесса
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

### Создание экрана
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

### Заполнение контейнера
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
### Подключение обработчика
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
### Заполнение обработчика
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
### Результат
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
