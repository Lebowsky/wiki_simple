Для удобства есть возможность генерировать временные файлы нужного расширения методом **get_temp_file**
```python
from ru.travelfood.simple_ui import SimpleUtilites as subclass
output_file = suClass.get_temp_file("txt")
```
Получить абсолютный путь к папке, в которой можно хранить свои файлы можно с помощью **get_temp_dir()**
`targetDir = suClass.get_temp_dir()`