---
title: example№2
description: 
published: true
date: 2024-02-19T07:19:23.747Z
tags: 
editor: markdown
dateCreated: 2024-02-15T10:16:07.819Z
---

## Пример 2. Работа с NoSQL(SimpleBase)

Реализовать будем с помощью SimpleBase, подробнее прочитать можно [тут](../DataStorage/NoSQL).
### Создание процесса и экрана
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

### Добавление обработчиков
2) Так же к нашему экрану, необходимо добавить обработчик(Handlers), который будет обрабатывать при открытии экрана (OnStart). К нему мы привяжем вывод информации из БД в переменную "names_elements"
  ! **ВАЖНО**
  OnStart отрабатывает не только в тот момент, когда мы открыли экран, но и после каждого события OnInput. На OnInput мы сделаем привязку нажатия на клавиши "Добавить" и "Очистить БД". При нажатии на клавишу у нас будет отрабатывать логика, которую мы пропишем в OnInput и после этого автоматически отработает логика, которая прописана в OnStart.
  Эту логику можно отключить с помощью 
  ```Python 
  hashMap.put("noRefresh", "")
  ```
  подробнее [тут](../Screens/ScreenSettings)
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
### Результат
4) Результат
<details>
<summary>Фото</summary>
<br>
<img src="/files/Pastedimage20240129160228.png" width=450>
</details>

