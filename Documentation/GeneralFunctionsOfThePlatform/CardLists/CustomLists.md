# Кастомные списки

Можно определить любую разметку для элемента списка на основе структуры контейнера. Для этого используется либо элемент «Список карточек» с структурой списка
```json
{"customcards": 
	{
	"layout": {..контейнер..},
	"cardsdata": [{данные},{},{}]
	} 
}
```
Для отображения в виде «карточек», либо элемент «Таблица» с переменной типа
```json
{"customcards": 
	{
	"layout": {..контейнер..},
	"tabledata": [{данные},{},{}]
	} 
}
```
Для отображения в виде сплошного списка без выделения карточек.
Контейнер можно разработать в «редакторе» и перенести через буфер обмена в код переменной

Данные в обоих случаях – массив JSON -объектов по одному на каждый элемент списка. В которых перечисляются переменные, отображаемые в контейнере. Также могут быть добавлены любые другие.

Также отдельно нужно выделить key – ключ, возвращаемый при нажатии

Пример определения такой переменной в python:
```python
form_custom = { "customcards":         {
        "options":{
          "search_enabled":True,
          "save_position":True
        },

        "layout": {
        "type": "LinearLayout",
        "orientation": "vertical",
        "height": "match_parent",
        "width": "match_parent",
        "weight": "0",
        "Elements": [
        {
            "type": "LinearLayout",
            "orientation": "horizontal",
            "height": "wrap_content",
            "width": "match_parent",
            "weight": "0",
            "Elements": [
            {
            "type": "Picture",
            "show_by_condition": "",
            "Value": "@pic1",
            "NoRefresh": False,
            "document_type": "",
            "mask": "",
            "Variable": "",
            "TextSize": "16",
            "TextColor": "#DB7093",
            "TextBold": True,
            "TextItalic": False,
            "BackgroundColor": "",
            "width": "match_parent",
            "height": "wrap_content",
            "weight": 2
            },
            {
            "type": "LinearLayout",
            "orientation": "vertical",
            "height": "wrap_content",
            "width": "match_parent",
            "weight": "1",
            "Elements": [
            {
                "type": "TextView",
                "show_by_condition": "",
                "Value": "@string1",
                "NoRefresh": False,
                "document_type": "",
                "mask": "",
                "Variable": ""
            },
            {
                "type": "TextView",
                "show_by_condition": "",
                "Value": "@string2",
                "NoRefresh": False,
                "document_type": "",
                "mask": "",
                "Variable": ""
            },
            {
                "type": "TextView",
                "show_by_condition": "",
                "Value": "@string3",
                "NoRefresh": False,
                "document_type": "",
                "mask": "",
                "Variable": ""
            }
            ]
            },
            {
            "type": "TextView",
            "show_by_condition": "",
            "Value": "@val",
            "NoRefresh": False,
            "document_type": "",
            "mask": "",
            "Variable": "",
            "TextSize": "16",
            "TextColor": "#DB7093",
            "TextBold": True,
            "TextItalic": False,
            "BackgroundColor": "",
            "width": "match_parent",
            "height": "wrap_content",
            "weight": 2
            }
            ]
        },
        {
            "type": "TextView",
            "show_by_condition": "",
            "Value": "@descr",
            "NoRefresh": False,
            "document_type": "",
            "mask": "",
            "Variable": "",
            "TextSize": "-1",
            "TextColor": "#6F9393",
            "TextBold": False,
            "TextItalic": True,
            "BackgroundColor": "",
            "width": "wrap_content",
            "height": "wrap_content",
            "weight": 0
        }
        ]
    }

}
}

form_custom["customcards"]["cardsdata"]=[]
for element in range(0,2):
    filling = {
    "key": str(element),
    "descr": "Pos. " + str(element),
	"string1": "Котята",  
	"string2": "2 штуки",  
	"string3": "сидят"
  }
    form_custom["customcards"]["cardsdata"].append(filling)

hashMap.put("cards",json.dumps(form_custom,ensure_ascii=False).encode('utf8').decode())
```
![[Pastedimage20240115172510.png]]