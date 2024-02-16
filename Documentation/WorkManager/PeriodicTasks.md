---
title: PeriodicTasks
description: 
published: true
date: 2024-02-16T13:09:40.003Z
tags: 
editor: markdown
dateCreated: 2024-02-16T13:01:19.162Z
---

## Периодические задания
Выполняются с определенной периодичностью, определение задачи такое же, как у однократной, только указывается период. RETRY для периодических не работает. 
```Python
hashMap.put("StartPeriodicWork", {"work": "массив обработчиков",
                                  "period": "период",
                                  "tag": "тэг задачи",
                                  "conditions": "список условий"})  
```

- work - унифицированный массив обработчиков, `[{"action":"run","type":"python","method":"some_longtime_routine"}]`
- period - период задается в минутах, не менее 15 минут. Если указано менее 15 минут, то будет выполняться раз в 15 минут.
- tag - нужен для того, чтобы в случае чего по нему можно было обратиться и отменить выполнение.
- conditions - устанавливает условия запуска задачи, их может быть одно или несколько сразу (разделитель – “;”). Условия следующие:
    - CONNECTED – наличие связи
    - CHARGING – устройство находится на зарядке
    - BATTERY_NOT_LOW – заряд батареи достаточен
    - IDLE – устройство не используется
    
```Python
def run_periodic_worker(hashMap,_files=None,_data=None):
    if hashMap.get("listener") == "btn_run_periodic": workercode=[{"action":"run","type":"set","method":"beep"}]         
	  hashMap.put("StartPeriodicWork",json.dumps({"work":workercode,"period":15,"tag":"periodic1","conditions":"CONNECTED"},ensure_ascii=False))

    if hashMap.get("listener") == "btn_stop_periodic":
    	hashMap.put("StopWork","periodic1")
    
    return hashMap  
```

