# Распознавание материальных объектов, предметов

В этом виде детектора происходит выделение границ материальных объектов в кадре и захват объекта в целом. При этом выделяются только те объекты в которых есть учетная информация - штрихкод или объект OCR. Система связывает физический объект с его идентификатором и воспринимает как целостный объект. Т.е. например система захватит и покажет границы коробки, если на этой коробке есть серийный номер или штрихкод. При этом даже если штрихкод или текст уже не распознаются, но объект остается захвачен в кадре для системы это остается прежним объектом - она его ведет и знает что это искомый идентифицированный объект. Работает более плавно чем OCR/чтение штрихкодов так как не ищет новые гипотезы при разных условиях видимости текста/штрихкода. Существует 3 настройки: Объекты с OCR и штрихкодом/Объекты только с OCR и Объекты только с штрихкодом.
