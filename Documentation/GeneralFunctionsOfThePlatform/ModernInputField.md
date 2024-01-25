# Современное поле ввода

"ModernEditText"
Поле ввода, в котором размещается заголовок/подсказка в зависимости от того, заполнено оно или нет. Если в поле присутствует информация, подсказка смещается в область заголовка. Таким образом достаточно размещать только один элемент, что экономит место и упрощает разработку.
Значение задается в виде JSON. Обязательными является hint – подсказка. Например
```json
{
"hint":"Логин",
"default_text":"default_login"
}
```
– задает подсказку, и если поле уже должно содержать данные то они задаются в default_text
По умолчанию – это текстовое поле, но можно задать любой тип имеющийся на Андроиде через input_type. [Варианты](https://developer.android.com/reference/android/text/InputType) 
Также, можно задать counter – счетчик введенных символов внизу и counter_max – максимальное количество символов.
Ключом events можно подключить генерацию событий с каждым введенным символом в поле, чтобы например записывать в БД сразу же введенный текст. Значение должно быть «true»
Например:
![[Pastedimage20240116164103.png]]
```python
def modern_start(hashMap,_files=None,_data=None):  
    modern_json = {  
        "hint": "Пароль",  
        "default_text": "default_password",  
        "counter": "true",  
        "counter_max": 15,  
        "input_type": 145,  
        "password": "true"  
        }  
    hashMap.put("Modern",
				json.dumps(modern_json,
				ensure_ascii=False)
			    .encode('utf8').decode())  
    return hashMap
```
![[Pastedimage20240116164313.png]]