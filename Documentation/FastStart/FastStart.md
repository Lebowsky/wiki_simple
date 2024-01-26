---
title: FastStart
description: 
published: true
date: 2024-01-26T12:42:15.837Z
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
