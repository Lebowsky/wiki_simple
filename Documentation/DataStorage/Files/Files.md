# Файлы

Все файлы хранятся во внутренней папки приложения SimpleUI, которая полностью доступна из самого приложения, но недоступна для других приложений (кроме как через root). С файлами можно выполнять любые операции из обработчиков python - читать содержимое папки, чистать файлы, записывать и т.д. Т.е. например, можно перехватить картинку, сделанную с камеры и выполнить кроп, сжатие в обработчике python а потом отправить на ресурс. Например, зная путь к файлу можно его открыть:

```python
with open(filename, "rb") as image_file:
      encoded_string = base64.b64encode(image_file.read()).decode('utf-8')
```
>[!info]- ## Диалоги открытия и сохранения файла из экрана
>![[DialogsForOpeningAndSavingAFileFromTheScreen]]

>[!info]- ## Сохранение в Downloads
>![[SavingToDownloads]]

>[!info]- ## Статические ресурсы
>![[StaticResources]]

>[!info]- ## Изображения
>![[Images]]

>[!info]- ## Полезные утилиты для работы с файлами в SimpleUtilites
>![[UsefulUtilitiesForWorkingWithFilesInSimpleUtilites]]