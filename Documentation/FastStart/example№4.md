---
title: example№4
description: 
published: true
date: 2024-02-19T07:20:14.151Z
tags: 
editor: markdown
dateCreated: 2024-02-15T10:16:11.469Z
---

## Пример 4. Режим дополненной реальности, вывод информации о товаре в реальном времени.

Подробнее про компьютерное зрение можно прочитать [тут](../ComputerVisionAndAugmentedRealityActiveCV/ComputerVision)
Реализуем 2 процесса
1) SimpleBase база данные, куда мы будем добавлять значения с помощью полей ввода и сохранять по нажатию кнопки. Подробнее про [SimpleBase](../DataStorage/DataStorage)
2) ActiveCV процесс, в котором при наведении на штрихкод, будет проверяться его значение в базе данных и если данные о продукте добавлены в базу данных, то будем выводить название и кол-во товара в реальном времени

**Шаги реализации**
### Создание базы данных
1) Создание базы данных мы будем производить как в "Примере 2"
На экран добавим контейнер(LinearLayout) заполним его:
- TextView(Текстовое поле), Value - Имя элемента
- EditTextText(Поле ввода), Value - @name_element, Variable - name_element
- TextView(Текстовое поле), Value - Штрихкод
- EditTextText(Поле ввода), Value - @barcode, Variable - barcode
- TextView(Текстовое поле), Value - Количество элементов
- EditTextText(Поле ввода), Value - @amount, Variable - amount
- Button(Кнопка), Value - Сохранить, Variable - btn_save
<details>  
<summary>Фото</summary>  
<br>  
<img src="/files/Pastedimage20240201173232.png" width="700">
</details>


```python
def input_bd(hashMap,_files=None,_data=None):  
    db = SimpleBase("test_db",  
                    path=suClass.get_simplebase_dir(),  
                    timeout=200)  
    if hashMap.get("listener") == "btn_save":  
        db['goods'].insert({"name": hashMap.get("name_element"), "barcode": hashMap.get("barcode"), "amount": hashMap.get("amount")})  
    return hashMap
```

### Создание процесса ActiveCV
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
<details>  
<summary>Фото</summary>  
<br>  
<img src="/files/Pastedimage20240201181332.png" width="450">
</details>