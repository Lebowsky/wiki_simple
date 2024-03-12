---
title: DynamicChange
description: 
published: true
date: 2024-03-12T11:01:11.666Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:23:11.464Z
---

## Динамическое изменение элементов экрана и конфигурации в целом
### Динамическое изменение элементов экрана
Экран представляет из себя JSON-объект, поэтому его можно динамически изменять. Экран может быть полностью пустой и генерироваться полностью «При открытии». Это не так удобно, как в конструкторе, но в некоторых случаях (например добавить кнопку в зависимости от условий) это сделать проще чем рисовать отдельную форму.

**getJSONScreen** записывает в переменную **JSONScreen** исходную структуру текущего экрана. 
```Python
hashMap.put("getJSONScreen","")
```
**setJSONScreen** применяет измененную структуру экрана

Пример кода
```Python
def screen_open(hashMap, _files=None, _data=None):
    hashMap.put("getJSONScreen", "") #Записываем в переменную JSONScreen текущий экран
    return hashMap

def screen_input(hashMap, _files=None, _data=None):
    screen = json.loads(hashMap.get('JSONScreen')) #Достаем данные из переменной JSONScreen
    el = screen['Elements'][0] 
    new_btn = {											#Создаем "образ" новой кнопки
        "type": "Button",
        "height": "wrap_content",
        "width": "wrap_content",
        "weight": "0",
        "Value": "тест",
        "Variable": "btn_change"
    }
    el['Elements'].append(new_btn) #Добавляем к экрану новую кнопку
    hashMap.put("toast", json.dumps(screen, ensure_ascii=False))
    hashMap.put("setJSONScreen", json.dumps(screen, ensure_ascii=False)) #Присваиваем к экрану новый вид
    return hashMap
```
[![лет.png](/лет.png =300x)](/лет.png)   [![лет2.png](/лет2.png =297x)](/лет2.png)



**getJSONConfiguration** - считывает в переменную _configuration текущую конфигурацию 
```Python
hashMap.put("getJSONConfiguration","")
```
**setJSONConfiguration** - применяет измененную конфигурацию немедленно.
