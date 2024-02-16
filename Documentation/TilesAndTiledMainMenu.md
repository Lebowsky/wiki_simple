# Плитки и плиточное главное меню

>[!info]- ## Переопределение стартового меню
>![[RedefiningTheStartMenu]]

Плитки - это элемент контейнера который можно вывести на экран, либо использовать как главное меню программы (стартовый экран). Структура карточки может быть любая - она задается в контейнере точно также как в контейнере задаются элементы экрана. При этом можно использовать все те же визуальные элементы что и в экранах - надписи, картинки, диаграммы, индикатор а также кэшированные картинки. Поля ввода и другие элементы ввода использовать нельзя.
Плитки могут визуально заменить список карточек при не очень большом количестве элементов (построение каждой плитки по шаблону занимает некоторое время и например 1000 плиток будут несколько притормаживать)
Размер (высота) плиток зависит от количества карточек в горизонтальном ряду. Есть 3 вида размера:
> - средний размер - при количестве плиток от 2 до 3 в ряду. Высота = ширина экрана/3.14  
> - мелкий размер - количество от 4 и выше. Высота - средний размер/2
> - большой размер - при одной плитке в ряду. Высота - минимально - такая же как у среднего размера, при необходимости - увеличивается.

Плитки задаются в JSON переменной как массив рядов, а каждый ряд - тоже массив, содержащий список плиток в ряду.
При этом каждая плитка в обязательном порядке содержит:
> - поле **template** - имя экрана, содержащего контейнер с шаблоном - то есть экран в составе конфигурации в котором определена структура плитки. Он может быть один на все плитки, но хотя бы один шаблон должен быть обязательно. Т.е. из экрана берется корневой контейнер и его структура является структурой плитки
> - объект **data** - объект содержащий значения переменных плитки. Т.е. в шаблоне определяется привязка переменных через @ , а в data для каждой плитки передаются данные
> - поле **color** - цвет плитки
> - поля **start_screen** и **start_process** - запуск экрана и процесса. При нажатии на плитку будет запущен процесс, указанный в плитке в поле start_process либо экран текущего процесса в поле start_screen. Вообще плиточный экран по умолчанию воспринимается как некое меню для запуска процессов – т.е. при нажатии должен стартовать процесс, а при завершении процесса возвращаться на меню. Для этого нужно указывать start_process в плитке. Но также можно использовать его для как шаг процесса как например используется таблица или список плиток – для запуска экрана с закрытием текущего шага. Для этого используется start_screen
> - плитка может содержать поле **key** которое передается в обработчик при нажатии

Также в общем объекте определено поле **background_color** - в нем задается фон под плитками.

>[!info]- ## Фотогайд
>![[Pastedimage20240116151639.png]]
>![[Pastedimage20240116151656.png]]
>![[Pastedimage20240116151712.png]]

Пример кода:
```python
def set_tiles(hashMap,_files=None,_data=None):  
    small_tile = {  
        "type": "LinearLayout",  
        "orientation": "vertical",  
        "height": "match_parent",  
        "width": "match_parent",  
        "weight": "0",  
        "Elements": [  
            {  
                "type": "TextView",  
                "show_by_condition": "",  
                "Value": "@room",  
                "NoRefresh": False,  
                "document_type": "",  
                "mask": "",  
                "Variable": "",  
                "TextSize": "15",  
                "TextColor": "#FFFFFF",  
                "TextBold": True,  
                "TextItalic": False,  
                "BackgroundColor": "",  
                "width": "match_parent",  
                "height": "wrap_content",  
                "weight": 0,  
                "gravity_horizontal": "center"  
            },  
            {  
                "type": "LinearLayout",  
                "orientation": "horizontal",  
                "height": "wrap_content",  
                "width": "match_parent",  
                "weight": "1",  
                "Elements": [  
                    {  
                        "type": "TextView",  
                        "show_by_condition": "",  
                        "Value": "Текущая",  
                        "NoRefresh": False,  
                        "document_type": "",  
                        "mask": "",  
                        "Variable": "",  
                        "TextSize": "0",  
                        "TextColor": "#ffffff",  
                        "TextBold": False,  
                        "TextItalic": False,  
                        "BackgroundColor": "",  
                        "width": "wrap_content",  
                        "height": "wrap_content",  
                        "weight": 0  
                    },  
                    {  
                        "type": "TextView",  
                        "show_by_condition": "",  
                        "Value": "@temp",  
                        "NoRefresh": False,  
                        "document_type": "",  
                        "mask": "",  
                        "Variable": "",  
                        "TextSize": "0",  
                        "TextColor": "#ffffff",  
                        "TextBold": False,  
                        "TextItalic": False,  
                        "BackgroundColor": "",  
                        "width": "wrap_content",  
                        "height": "wrap_content",  
                        "weight": 0  
                    }  
                ]  
            },  
            {  
                "type": "LinearLayout",  
                "orientation": "horizontal",  
                "height": "wrap_content",  
                "width": "match_parent",  
                "weight": "1",  
                "Elements": [  
                    {  
                        "type": "TextView",  
                        "show_by_condition": "",  
                        "Value": "Диапазон",  
                        "NoRefresh": False,  
                        "document_type": "",  
                        "mask": "",  
                        "Variable": "",  
                        "TextSize": "0",  
                        "TextColor": "#ffffff",  
                        "TextBold": False,  
                        "TextItalic": False,  
                        "BackgroundColor": "",  
                        "width": "wrap_content",  
                        "height": "wrap_content",  
                        "weight": 0  
                    },  
                    {  
                        "type": "TextView",  
                        "show_by_condition": "",  
                        "Value": "@rate",  
                        "NoRefresh": False,  
                        "document_type": "",  
                        "mask": "",  
                        "Variable": "",  
                        "TextSize": "0",  
                        "TextColor": "#ffffff",  
                        "TextBold": False,  
                        "TextItalic": False,  
                        "BackgroundColor": "",  
                        "width": "wrap_content",  
                        "height": "wrap_content",  
                        "weight": 0  
                    }  
                ]  
            },  
            {  
                "type": "TextView",  
                "show_by_condition": "",  
                "Value": "@port",  
                "NoRefresh": False,  
                "document_type": "",  
                "mask": "",  
                "Variable": "",  
                "TextSize": "-1",  
                "TextColor": "#ffffff",  
                "TextBold": True,  
                "TextItalic": False,  
                "BackgroundColor": "",  
                "width": "match_parent",  
                "height": "wrap_content",  
                "weight": 0  
            }  
        ]  
    }  
  
    tile = {  
        "tiles": [  
            [  
                {  
                    "layout": small_tile,  
                    "data": {  
                        "room": "котельная",  
                        "temp": "23°C",  
                        "rate": "11°C...28°C",  
                        "port": "N1"  
                    },  
                    "color": "#78002e",  
                    "start_screen": "",  
                    "start_process": "Процесс 1"  
                },  
                {  
                    "layout": small_tile,  
                    "data": {  
                        "room": "водоподготовка",  
                        "temp": "24°C",  
                        "rate": "11°C...29°C",  
                        "port": "N1"  
                    },  
                    "color": "#78002e",  
                    "start_screen": "",  
                    "start_process": "Процесс 2"  
                }  
            ],  
            [  
                {  
                    "layout": small_tile,  
                    "data": {  
                        "room": "котельная #2",  
                        "temp": "23°C",  
                        "rate": "10°C...22°C",  
                        "port": "N2"  
                    },  
                    "color": "#e53935",  
                    "start_screen": "",  
                    "start_process": "Процесс 2"  
                },  
                {  
                    "layout": small_tile,  
                    "data": {  
                        "room": "станция ВЭО",  
                        "temp": "норма",  
                        "rate": "",  
                        "port": ""  
                    },  
                    "color": "#78002e",  
                    "start_screen": "",  
                    "start_process": "Процесс 1"  
                }  
            ],  
        ],  
        "background_color": "#f5f5f5"  
    }  
  
    hashMap.put("tiles",
			    json.dumps(tile, ensure_ascii=False)
			    .encode('utf8').decode())  
  
    return hashMap

```




[[GeneralFunctionsOfThePlatform]]
