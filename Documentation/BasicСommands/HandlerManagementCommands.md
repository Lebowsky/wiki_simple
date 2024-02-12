---
title: HandlerManagementCommands
description: 
published: true
date: 2024-02-12T08:40:08.670Z
tags: 
editor: markdown
dateCreated: 2024-01-25T07:43:05.534Z
---

# Команды управления обработчиками

**RunEvent**, параметр: строка в формате [обработчиков](/Documentation/Handlers/StringHandlers) - запуск массива любых обработчиков. Т.е. это генерация произвольного события из кода. 


`hashMap.put('RunEvent', json.dumps([{"action": "run", "type": "python", "method": "post_online"}])`

``` python
hashMap.put('RunEvent', json.dumps([{"action": "run", "type": "python", "method": "post_online"}])
```

**BreakHandlers** - прерывание выполнения массива обработчиков. Может быть вызвана в каком то обработчике массива (например, проверка ввода) чтобы прервать весь остальной массив 

``` python
hashMap.put('RunEvent', json.dumps([{"action": "run", "type": "python", "method": "post_online"}])
```

**BreakHandlersIfError**, без параметра – прерывает дальнейшее выполнение массива обработчиков если в текущем обработчике ошибка