---
title: SendSettings
description: 
published: true
date: 2024-11-19T11:33:27.932Z
tags: 
editor: markdown
dateCreated: 2024-11-19T11:33:27.932Z
---

# Отправка настроек

## В шине
В момент подключения пользователя у нас срабатывает функция отправки настроек
```python

def handleConnected(self):  
    global clients  
  
    print(self.address, 'connected')  
    try:  
        self.send_settings_via_websocket(self.address)  
    except:  
        pass  
    clients.append(self)

def send_settings_via_websocket(self, client):  
    settings = {  
	    "message": "Настройки",
	    "sender": "1"
      "settings": {  
                     "IntentScannerMessage": "112"  #Можем перечислять через запятую настройки и их значения
            		  }  
        			  }  
  
    # Отправка через WebSocket  
    message = json.dumps(settings, ensure_ascii=False)  # Конвертация в JSON-формат  
    self.sendMessage(message)  # Вызываем sendMessage напрямую у объекта SimpleChat  
    print("Settings sent via WebSocket:", message)
```

## В общем обработчике OnSimpleBusMessage 

```python
from general import *
sbmessage = json.loads(hashMap.get("SBMessage"))
message = sbmessage['message']
sender = sbmessage['sender']

if "settings" in message:
	settings = sbmessage.get('settings', None)
	#Присвоим настройки устройству
  hashMap.put("SetSettingsJSON", json.dumps(settings))
```
