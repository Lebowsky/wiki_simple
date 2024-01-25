# Передача картинки

На экране может быть выведена картинка на том месте где находится элемент picture. Картинка передается через обычную переменную в виде строки Base64.
>[!info]- Фотогайд
>![[Pastedimage20240112183031.png]]
>```python
>def screen_on_start(hashMap):
>    hashMap.put("picture", base64_cod_picture)  
>    return hashMap
>```
>base64_cod_picture - картинка предварительно переведенная в base64 формат
>![[Pastedimage20240112182924.png]]