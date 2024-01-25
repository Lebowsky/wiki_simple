# Работа с картой

**map_edit_mode** – включение режима пользовательского редактирования 
`hashMap.put("map_edit_mode", "")`
**map_background_picture** – установка фона – картинки. Принципы работы такие же как с картинками в [[ImagesFromTheCache|Simple UI]] 
**map_background_html** – установка в качестве картинки html на экране, по сути скриншот содержимого html. Важно! Данный метод можно вызывать только на экране, где есть html поле, т.е. до экрана в котором присутствует поле карты. Таким образом если нужно передать на редактирование печатную форму/отчет html, то должно быть 2 экрана – сначала html, потом экран редактирования 
**map_save** – сохранение того, что нарисовал пользователь вместе с фоном. В случае с включенным режимом mm_local возвращается переменная **map_saved_file** с именем файла, куда это записалось, если не включен этот режим то возвращается в **map_saved_base64** 
**map_zoom** – увеличение карты. Пример «1.5» - увеличение в 1,5 раза 
**map_move_x** и **map_move_y** – сдвиги по осям. Имеет смысл использовать совместно с **map_zoom**. Можно указывать положительные (вправо, вниз) и отрицательные (влево, вверх)