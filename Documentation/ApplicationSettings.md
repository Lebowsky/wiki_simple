---
title: ApplicationSettings
description: 
published: true
date: 2024-02-07T11:18:03.633Z
tags: передача настроек через файл или qr-код, off-line, настройки
editor: markdown
dateCreated: 2024-01-24T15:01:58.484Z
---

# Настройки приложения
## Передача настроек через файл или QR-код
Настройки должны быть оформлены в виде JSON-строки или текстового файла в формате JSON. Примеры настроек:
**IntentScannerMessage** – имя сообщения сканера
**IntentScannerVariable** – имя переменной сообщения сканера
**IntentScannerLength** – имя переменной, в которой храниться длина штрихкода, если он предаётся в виде байт-массива а не строки
**IntentScanner** – режим работы сканера через интент
**CategoryDefault** – фильтр по категориям сообщений для сканера штрихкодов
**ExchangeFolder** – папка обмена. Выбирает папку обмена, при необходимости создает (создание папки работает в Android до 11 версии)
**RawConfigurationServiceON** – произвольная авторизация
**GitFormat** – формат для хранения конфигураций на github.com
**RawConfigurationURL** – URL при варианте произвольной авторизации
**RawConfigurationServiceAuth** – строка авторизации, заданная вручную для произвольной авторизации
**GitCommitsURL** – URL коммитов с GitHub
**GitStoreURL** – URL репозитория на GitHub для использования в качестве магазина
**OnlineSplitMode** – «разделенный режим» конфигурации и обработчиков
**onlineURLListener** – URL обработчиков для разделенного режима
**onlineURL** – URL конфигурации для любого режима
**onlineUser** – пользователь конфигурации для любого режима
**onlineUserListener** – пользователь обработчиков для разделенного режима
**onlineCode** – код справочника Мобильные клиенты
**onlinePass** – пароль пользователя конфигурации для любого режима
**onlinePassListener** – пароль пользователя обработчиков
**backendURL** – URL PostgREST – устарело. Для соединения с Postgre
**backendUser** – пользователь Postrgre
**oDataURL** – URL OData
**Service_URL** – URL сервиса технической информации (подписка на изменение настроек)
**offSettings** – запрет на настройки
**offChat** – отключение чата
**offToDo** – отключение списка дел
**offlineMode** – принудительный оффлайн режим
**beep** – сигнал при каждом сканировании
**torch** – подсветка при сканировании камерой
**dialogOnBackPressed** – задавать вопрос при закрытии основной программы
**gps** – получение координат GPS в Переменные перманентно
**timer** – интервал таймера
**connection_limit** – максимальное время попытки соединения для онлайн обработчиков, 0 – неограничено
**hardwarescan** – отключение кнопки сканирование камерой для экранов со штрих-кодом (для аппаратного сканера)
**conf_id** – ID конфигурации для запросов вида `/get_configuration?confid=…`
**configuration** - загрузка текста конфигурации. Можно передать в настройках конфигурацию (через файл), она будет сразу же загружена
Пример:
```JSON
{
  "onlineURL": "http://192.168.1.102:4444/TestSimple",
  "onlineUser": "usr",
  "onlineCode": "12",
  "onlinePass": "",
  "backendURL": "http://5.4.3.1:2000",
  "backendUser": "user1",
  "offSettings":false,
  "offChat":false,
  "offToDo":true,
  "connection_limit":"5",
  "offlineMode": true,
  "beep": true,
  "torch": true,
  "oDataURL": "",
  "gps": true,
  "hardwarescan": false,
  "conf_id": "1"
}
```

Передача через QR-код:
<details>
<summary>Фотогайд</summary>
<br>
<img src="/files/Pastedimage20240118095916.png" width="900">
<br>
<img src="/files/Pastedimage20240118100053.png" width="400"> 
<br>Необходимо навести камеру на QR-код.
</details>

Помимо QR-код можно передать весь файл конфигурации в виде ui файла и запустить его на устройстве.

## Передача конфигурации на устройство в режиме OFF-line через прямой запрос на сервер
При работе через веб-сервер на стороне учетной системы, каждый раз когда скачивается конфигурация, она сохраняется на мобильном устройстве. При этом в настройках можно увидеть дату последнего скачивания (last update)
Если же работа не предусматривает наличие веб-сервера на стороне бекенда, то можно передать конфигурацию на устройство прямым HTTP-запросом. Для этого надо знать адрес веб сервиса моб. клиента который можно посмотреть в настройках. Далее на этот адрес нужно послать POST-запрос **SetConf** в теле которого- текст конфигурации (содержимое UI-файла) и конфигурация будет записана в память, после чего можно обновить или перезагрузить программу чтобы она применилась.

## Централизованное управление настройками и устройствами через веб-сервис
Мобильные рабочие места могут управляться централизованно, адресно. Т.е. по AndroidID (уникальный ID устройства) можно отправить на мобильное устройство новые настройки или сменить конфигурацию. Приложение при запуске отправляет запрос 
`service_broadcast/{AndroidID}` на URL заданный в настройке Service_URL (если такая настройка не задана, то на URL конфигурации). В запросе передается AndroidID и модель устройства для организации на стороне центральной базы справочника устройств.
В ответ сервис может отправить JSON определенной структуры на смену настроек. Это может быть:
```json
{"command": "update",
 "uuid": UID,
 "value": JSON настроек}
```
где **UID** - произвольный UID, сгенерированный для идентификации конкретной команды, для ответного токена. JSON настроек - JSON строка с настройками из предыдущего раздела
После получения настроек, если все в порядке в ответ отправляется запрос 
`/service_response/{AndroidID}/{uuid}`

