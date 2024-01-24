Стандартным для Android является встроенный SQLite. Его преимущества в том, что это классическая реляционная СУБД – быстрая работа, SQL запросы, агрегирующие функции. Например найти товар по штрихкоду из 1 миллиона записей, да еще по сложному условию -это не сделать быстрее чем на SQL с индексами. Или например посчитать агрегаты – сумму по строкам таблицы. Опять же быстрее SQL с этим никто не справиться.
Можно завести несколько СУБД в рамках приложения.
К SQL можно обращаться из Python напрямую, в т.ч использую ORM но рекомендуется использовать единую точку входа(SQLProvider) либо через команды переменные либо через класс **SimpleSQLProvider** в Python либо через нативные обработчики (они также используют SimpleSQLProvider).Т.е. при обращении к SQL используется Java-класс реализующий монопольное подключение к СУБД и общий поток событий.
Можно работать с SQL через команды-переменные либо(если из питон-обработчиков) использовать вызовы специального класса в явном виде.
Справочник команд-переменных:
>[!info]- ## **SQLConnectDatabase**
>`hashMap.put("SQLConnectDatabase", "test1.DB")`
>Так как указывается имя базы предполагается что можно использовать несколько баз, помимо дефолтной.

>[!info]- ## **SQLExec**
>`{"query": "SQL statement", "params": "parameters with delimiter"}`
>Например:
>```sql
>sql_query = "CREATE TABLE IF NOT EXISTS Record
>		(id integer primary key autoincrement,
>		 art text,
>		 barcode text, 
>		 name text, 
>		 qty real)"
>```
>```python
>hashMap.put("SQLExec",
>		     json.dumps({"query": sql_query,
>		     "params":""}))
>```
>Выполняет запрос на изменение БД (все кроме SELECT), параметры в запросе указываются в неименованном виде, а в params, перечисляются через запятую

>[!info]- ## **SQLExecMany**
>`{"query": "SQL statement", "params": "parameters with delimiter"}`
> Выполняет запрос в BULK-режиме с массивом из множества записей. Параметры запроса передаются в виде массива записей в неименованном виде (через ?)
> Пример:
> ```SQL
> sql_query = "INSERT INTO goods(art,barcode,nom) 
> 		   VALUES(?,?,?)"
> ```
> ```python
> values=[]
> for i in range(1,3):
> 	record =[]
> 	record.append("AA"+str(i))
> 	record.append("22"+str(i))
> 	record.append(f"Товар переменной {str(i))}"
> 	values.append(record)
> 
> hashMap.put("SQLExecMany",
>			json.dumps({"query": sql_query,
>			"params": json.dumps(values, ensure_ascii=False)}))
> ```

>[!info]- ## **SQLParameter**
>Имеет смысл для SQLExecMany для передачи массива записей в качестве параметра из других обработчиков

>[!info]- ## **SQLQuery**
>`{"query": "SQL statement","params": "parameters with delimiter"}`
> Запрос типа SELECT, который пишет выборку в виде JSON-массива в стек переменных в SQLResult
> Пример query:
>```SQL
>sql_query = "SELECT name FROM sqlite_master WHERE type='table'" 
>```
>Пример запроса:
>```python
>info = requests.post(f"url={our_url}&query={sql_query}&params=",
>			headers={'Content-Type': 'Application/json;charset=utf-8'})
>```

>[!info]- ## **SQLQueryMany**
>`{"query": "SQL statement","params": "parameters with delimiter"}`
> Запрос типа SELECT, который пишет выборку в виде JSON-массива во временный файл и в параметре SQLResultFile возвращает имя этого файла. Для очень больших выборок (>0.5 млн строк)

Те же функции можно вызывать из импортируемого класса напрямую. Этот вариант хорош тем что результат получаешь сразу а не на конец шага и его лучше использовать в python-обработчиках.

```python
from ru.travelfood.simple_ui import SimpleSQLProvider as sqlClass
sql = sqlClass()
  success=sql.SQLExec("insert into goods(art,barcode,nom) values(?,?,?)","111222,22000332323,Некий товар")
  res = sql.SQLQuery("select * from goods where id=1","")
  if success:
      hashMap.put("toast",res)
```
