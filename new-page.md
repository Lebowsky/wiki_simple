---
title: Работа с ячейками
description: 
published: true
date: 2024-02-05T14:05:11.963Z
tags: 
editor: markdown
dateCreated: 2024-01-24T12:08:38.586Z
---


fas
<style>
  img.big {cursor: pointer; max-width: 150px; transition: max-width 0.5s ease;}
  img.big:hover {max-width: 75px;}
</style>


<img class="big" src="/files/Pastedimage20240126134630.png">
sss




[![Alt текст](/files/Pastedimage20240126134630.png)](#)

<style>
/* Скрыть стандартный стиль для ссылок */
a {
    text-decoration: none;
}

/* Создать модальное окно для отображения изображения */
.modal {
    display: none; /* По умолчанию скрыто */
    position: fixed; /* Фиксированное положение */
    z-index: 1; /* Поверх остальных элементов */
    padding-top: 100px; /* Отступ сверху */
    left: 0;
    top: 0;
    width: 100%; /* Ширина на всю ширину экрана */
    height: 100%; /* Высота на всю высоту экрана */
    overflow: auto; /* Добавить прокрутку, если содержимое выходит за пределы */
    background-color: rgba(0,0,0,0.9); /* Цвет фона с небольшим прозрачным эффектом */
}

/* Отображение изображения внутри модального окна */
.modal-content {
    margin: auto;
    display: block;
    width: 80%; /* Ширина изображения */
    max-width: 700px; /* Максимальная ширина изображения */
}

/* Кнопка для закрытия модального окна */
.close {
    position: absolute;
    top: 15px;
    right: 35px;
    color: #fff;
    font-size: 40px;
    font-weight: bold;
    transition: 0.3s;
}

.close:hover,
.close:focus {
    color: #bbb;
    text-decoration: none;
    cursor: pointer;
}
</style>

<!-- Модальное окно -->
<div id="myModal" class="modal">
  <span class="close">&times;</span>
  <img class="modal-content" id="img01">
</div>

<!-- Ссылка для открытия модального окна при клике -->
[![Alt текст](/files/Pastedimage20240126134630.png)](#myModal)

<script>
// Получить ссылку на модальное окно и изображение
var modal = document.getElementById('myModal');
var img = document.getElementById('img01');

// Получить ссылки на изображения и установить обработчик событий для открытия модального окна
var images = document.getElementsByTagName('img');
for (var i = 0; i < images.length; i++) {
    images[i].addEventListener('click', function(){
        modal.style.display = "block";
        img.src = this.src;
    });
}

// Получить ссылку на кнопку закрытия модального окна и установить обработчик события для закрытия окна
var span = document.getElementsByClassName("close")[0];
span.onclick = function() {
  modal.style.display = "none";
}
</script>