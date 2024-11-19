---
title: GroupWork
description: 
published: true
date: 2024-11-19T13:06:21.138Z
tags: 
editor: markdown
dateCreated: 2024-11-19T11:44:04.416Z
---

# Пример групповой работы

Существует возможность групповой работы. Основывается она на работе с базой данных на устройстве.
В примере представлена одновременная работа с со списком штрихкодов. Сканирует один, появляется у всех. Сам принцип работы состоит из пяти основных моментов.
1) Сканирование штрихкода
2) Внос штрихкода в базу данных на своем устройстве
3) Вывод с новыми значениями штрихкодов на своем устройстве
4) Отправка штрихкода на шину
5) Доставка через шину штрихкода для остальных пользователей
6) Внос остальными пользователями штрихкода в базу данных на своих устройствах

## Сканирование штрихкода

Сканирование штрихкода происходит через специальный элемент в конструкторе (Штрихкод).
<img src="/files/Pasted image 20241119110512.png" width=1000>


<img src="/files/Pasted image 20241119111346.png" width=800>

## Внос штрихкода в базу данных на своем устройстве и Отправка на шину

Предварительно необходимо инициализировать базу данных на своем устройстве. Подробнее [тут](..//DataStorage).

**self.hash_map.get("barcode")** - Данные в результате сканирования, где barcode - переменная сканера.

<img src="/files/Pasted image 20241119111725.png" width=1000>


```python
def on_input(self):  
    if self.listener == "barcode":  
        message_info = {"_id": self.hash_map.get("barcode"), "barcode": self.hash_map.get("barcode"), "qty": "",  
             "user": str(self.hash_map.get("BUS_ID"))}  
        #Заполняем данные в своей таблице  
        pelicans['samples_bus']['barcodes'].insert(message_info, upsert=True)  
        #operation = insert. Для будущего определния для чего были отправлены данные
        message = {"to": ["$all"], "message": {"operation": "insert", "data": message_info}}  
        #Отправляем сообщение с данными нового штрихкода  
        self.hash_map.put("SendBus", json.dumps(message, ensure_ascii=False))
```

## Отрисовка данных на своем устройстве

Используем таблицу, где каждый новый штрихкод является карточкой.

<img src="/files/Pasted image 20241119111708.png" width=1000>


```python
def on_start(self):  
    card_barcodes = {"customtable": {  
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
                    "StrokeWidth": 1,  
                    "Padding": 2,  
                    "BackgroundColor": "#EEF0F2",  
                    "height": "wrap_content",  
                    "width": "match_parent",  
                    "weight": "1",  
                    "Elements": [  
                        {  
                            "type": "TextView",  
                            "width": "match_parent",  
                            "Value": "@user",  
                            "Variable": "",  
                            "weight": "1"  
                        },  
                        {  
                            "type": "TextView",  
                            "width": "match_parent",  
                            "Value": "@barcode",  
                            "Variable": "",  
                            "weight": "1"  
                        }  
                    ]  
                }  
  
            ]  
        }  
  
    }  
    }  
  
    card_barcodes["customtable"]["tabledata"] = []  
    #Получаем все данные по штрихкодам  
    barcodes_info = pelicans['samples_bus']['barcodes'].all()  
    #Проходимся по списку, заполняя основную информацию  
    for barcode_info in barcodes_info:  
        element_info = {  
            "key": barcode_info["_id"],  
            "barcode": barcode_info["barcode"],  
            "user": barcode_info["user"]  
  
        }  
		# Добавляем данные по каждой карточке
        card_barcodes["customtable"]["tabledata"].append(element_info)  
    #Заполняем таблицу  
    self.hash_map.put("barcode_table", json.dumps(card_barcodes, ensure_ascii=False))
```

## Получение и внос новых данных происходит через общий обработчик onSimpleBusMessage

```python
import android
from pelican import pelicans
import json


sbmessage = json.loads(hashMap.get("SBMessage"))
message = sbmessage['message']
sender = sbmessage['sender']

if "operation" in message:
	operation_info = message.get("operation")
	if operation_info == "insert":
		#Дополнение данных таблицы
		pelicans['samples_bus']['barcodes'].insert(message['data'],upsert=True)
	if android.process_started():
		#Перерисовка экрана
		hashMap.put("RestartScreen","")
	elif android.cv_started():
		#Перезапуск CV
		hashMap.put("RestartCV","")	
	android.toast('Сообщение operation')
```
