---
title: DynamicChange
description: 
published: true
date: 2024-02-16T12:12:29.384Z
tags: 
editor: markdown
dateCreated: 2024-02-16T08:23:11.464Z
---

## Динамическое изменение элементов экрана и конфигурации в целом
**getJSONScreen** записывает в переменную **JSONScreen** исходную структуру текущего экрана. 
```Python
hashMap.put("getJSONScreen","")
```
**setJSONScreen** применяет измененную структуру экрана	
**getJSONConfiguration** - считывает в переменную _configuration текущую конфигурацию 
```Python
hashMap.put("getJSONConfiguration","")
```
**setJSONConfiguration** - применяет измененную конфигурацию немедленно.
