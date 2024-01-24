Базы SimpleBase хранятся в специальном каталоге SimpleBase в папке приложения. Базу можно располагать где угодно, но желательно прописывать путь к этой папке, для того, чтобы нативные функции могли работать с этой базой тоже. Для этого есть функция get_simplebase_files в классе SimpleUtilities
Инициализация будет выглядеть так
```python
from pysimplebase import SimpleBase
db = SimpleBase("test_db", 
				path=suClass.get_simplebase_dir(),
				timeout=200)
```
Вся остальная работа с СУБД согласно документации к SimpleBase