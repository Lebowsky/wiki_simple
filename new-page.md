---
title: Работа с ячейками
description: 
published: true
date: 2024-02-05T12:22:39.238Z
tags: 
editor: markdown
dateCreated: 2024-01-24T12:08:38.586Z
---

# Песочница

Your content here

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hover Image Resize</title>
<style>
.image-container {
  width: 200px; /* Ширина контейнера изображения */
  height: 200px; /* Высота контейнера изображения */
  overflow: hidden; /* Скрытие изображения, которое выходит за границы контейнера */
}

.image-container img {
  width: 100%; /* Подгоняет ширину изображения под ширину контейнера */
  height: auto; /* Подгоняет высоту изображения под высоту контейнера, сохраняя пропорции */
  transition: transform 0.3s ease; /* Анимация для плавного изменения размера */
}

.image-container:hover img {
  transform: scale(1.1); /* Увеличивает размер изображения при наведении */
}
</style>
</head>
<body>

<div class="image-container">
  <img src="/files/Pastedimage20240126134630.png" alt="Your Image" style="width: 100%;">
</div>

</body>
</html>

