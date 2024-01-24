Возможно только из python-обработчика. Работа заключается в вызове Java-функции `write_socket(String host,int port, String message,String charset)` из модуля SimpleUtilites:
```python
from ru.travelfood.simple_ui import SimpleUtilites as su
su.write_socket(IP, port, data, handlers)
```
- IP, port – IP-адрес и порт (9100 по умолчанию) принтера
- data – либо байт-массив либо строка(UTF-8) данных
- handlers – строка-массив обработчиков в случае неудачи

Функция возвращает `True` в случае успешной отправки и `False` – во всех остальных случаях