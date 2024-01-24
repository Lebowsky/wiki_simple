# Подключение к устройству через USB (только отправка)

Подключение осуществляется из модуля SimpleUSB. Сканируются подключенные в текущий момент устройства и возвращается первое из списка либо первый принтер из списка подключенных.

Подключение и отправка данных на любое устройство осуществляется командой **write_usb(data, handlers)** (data – строка или массив байтов, handlers – обработчики в случае неудачи):
```python
from ru.travelfood.simple_ui import SimpleUSB as usbClass

usb = usbClass()
usb.write_usb(data, handlers)
```

Подключение к принтеру через USB осуществляется аналогичной командой **print_usb(data, handlers)**
```Python
from ru.travelfood.simple_ui import SimpleUSB as usbClass

usb = usbClass()
usb.print_usb(data, handlers)
```