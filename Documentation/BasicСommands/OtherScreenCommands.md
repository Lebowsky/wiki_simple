---
title: OtherScreenCommands
description: 
published: true
date: 2024-02-19T07:35:43.898Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:23:18.185Z
---

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
[Подробнее](../ComputerVisionAndAugmentedRealityActiveCV/ComputerVision)
