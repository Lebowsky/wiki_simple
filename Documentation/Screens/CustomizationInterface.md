---
title: CustomizationInterface
description: 
published: true
date: 2024-02-16T10:10:28.736Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:24:25.977Z
---

# Кастомизация интерфейса
Имеется возможность кастомизировать элементы так как вам хочется, для получения любого элемента интерфейса, выведенного на экране, включая контейнеры используется симпловский метод getView("ИД"), где ИД - переменная элемента. Для изменения элемента используется библиотека [GradientDrawable](https://developer.android.com/reference/android/graphics/drawable/GradientDrawable)
```Python
def tst_input(hashMap,_files=None,_data=None):
    from ru.travelfood.simple_ui import ImportUtils as iuClass
    from android.graphics.drawable import GradientDrawable
    from android.graphics import Color
    

    v = iuClass.getView("btn_tst")
    v.setTextColor(-65536)

    shape =  GradientDrawable()
    shape.setShape(GradientDrawable.OVAL)
    shape.setColor(Color.WHITE)
    shape.setStroke(40, Color.WHITE)


    v.setBackground(shape)

    hashMap.put("noRefresh","")
    
    return hashMap 
```
[![Pastedimage20240212152034.png](/files/Pastedimage20240212152034.png =300x)](/files/Pastedimage20240212152034.png)