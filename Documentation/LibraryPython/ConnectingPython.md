---
title: ConnectingPython
description: 
published: true
date: 2024-02-16T13:27:43.518Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:24:15.101Z
---

# Подключение Python библиотек
Существует возможность подключить любую python библиотеку
1) Скачать python библиотеку в формате whl
[![Pastedimage20240212164320.png](/files/Pastedimage20240212164320.png =650x)](/files/Pastedimage20240212164320.png)
2) Необходимо добавить этот файл в медиафайлы в конструкторе, сделаем key == названию библиотеки
3) Необходимо в обработчик вставить такой код:
```Python
    import zipfile
    import sys
    import os
    import base64


    whlPath =  suClass.get_stored_file("pygal")
    targetDir = suClass.get_temp_dir()
    sys.path.append(targetDir)
    with zipfile.ZipFile(whlPath, "r") as whl:
        whl.extractall(targetDir)
    sys.path.append(os.path.join(targetDir, 'pygal'))
```
4) Можем использовать библиотеку импортируя её
```Python
    import pygal  

    bar_chart = pygal.Bar()                                            # Создаем график
    bar_chart.add('Fibonacci', [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55])  # Добавляем различные значения
```
[![Pastedimage20240212165001.png](/files/Pastedimage20240212165001.png =350x)](/files/Pastedimage20240212165001.png)
