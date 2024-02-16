---
title: ImagesCache
description: 
published: true
date: 2024-02-16T12:25:07.636Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:23:55.143Z
---

# Картинки из кэша
Для повышения быстродействия интерфейса, особенно для повторяющихся элементов, например в карточках, рекомендуется передавать картинки не через base64 а указывать их в конфигурации на странице «Медиаресурсы». Так, картинки передаются вместе с конфигурацией и загружаются на устройство в виде файлов (в папке приложения).
Дальнейшая работа с ними происходит в формате **^имя ресурса** , где имя ресурса вы определяете на странице «Медиаресурсы». Такое обращение доступно везде где есть объект «Картинка» - экраны, карточки и т.д. Также для плиток можно указывать не явную ссылку а ссылку на переменную, а явная ссылка указывается в объекте **data** плитки.
Также использование таких картинок более удобно для структурирования проекта.
Пример структуры:
```json
tiny_tile = {  
    "type": "LinearLayout",  
    "orientation": "vertical",  
    "height": "match_parent",  
    "width": "match_parent",  
    "weight": "0",  
    "Elements": [  
        {  
            "type": "Picture",  
            "show_by_condition": "",  
            "Value": "^kitty",  
            "NoRefresh": False,  
            "document_type": "",  
            "mask": "",  
            "Variable": "",  
            "TextSize": "11",  
            "TextColor": "",  
            "TextBold": False,  
            "TextItalic": False,  
            "BackgroundColor": "",  
            "width": "match_parent",  
            "height": "match_parent",  
            "weight": 1  
        }  
    ]  
}
```
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240116182533.png">
<img src="/files/Pastedimage20240116182851.png"> 
<img src="/files/Pastedimage20240116182743.png"> 
</details>
