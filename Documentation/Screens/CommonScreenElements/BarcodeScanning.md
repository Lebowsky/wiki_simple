# Сканирование штрих кода

Если на экране требуется распознавание штрихкода, то необходимо добавить на экран элемент «Штрих-код» и указать переменную(variable), которую будет воспринимать hashMap, в которую он будет записываться по факту сканирования.
>[!info]- Фотогайд
![[Pastedimage20240112172533.png]]
![[Pastedimage20240112172558.png]]
![[Pastedimage20240112172746.png]]

Если на устройстве есть аппаратный сканер, желательно указать галочку «Аппаратный сканер» в настройках. В противном случае на экране будет присутствовать кнопка сканирования через камеру устройства. Соответственно, при сканировании через камеру при добавлении элемента Штрих-код подразумевается что будет нажиматься парящая кнопка. Также в настройках можно включить подсветку. Также при использовании Bluetooth сканеров в режиме SSP сопряжения необходимо активировать Использовать Bluetooth и выбрать устройство и суффикс (это все обычно программируется на устройстве штрих-кодами из инструкции). Bluetooth сканеры обычно могут работать и в режиме HID но в таком случае на экране нельзя размещать другие элементы ввода – они будут перехватывать строку. Аппаратный сканер ТСД может быть запрограммирован в режиме HID (в разрыв клавиатуры) с суффиксом CR/LF на конце. Либо он может быть запрограммирован на передачу сообщения через подписку на intent. Второй вариант лучше, потому что поля ввода не перехватывают такое сообщение и можно располагать ввод штрихкода с полями ввода на одном экране. Для использования в этом режиме надо включить галку «Использовать подписку на события сканера» и заполнить поля. Заполнение полей индивидульно для разных моделей, информацию ищите в документации либо в ПО ТСД.
![[Pastedimage20240112173214.png]]
Знак сканирования через камеру