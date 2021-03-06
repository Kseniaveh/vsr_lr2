#  Подготовка выступления и репозитория кода по сравнению характеристик Canvas и SVG.

SVG и canvas — это технологии, которые можно использовать для рисования чего-либо на веб-страницах. Поэтому их стоит сравнить и разобраться в том, когда стоит применять SVG, а когда — canvas. Даже весьма поверхностное понимание сути этих технологий позволяет сделать вполне осознанный выбор. Собственно говоря, вот — две типичных ситуации, в одной из которых стоит предпочесть SVG, а в другой — canvas:

1. Нужно нарисовать небольшую иконку? Это, безусловно, территория SVG.
1. Нужно создать интерактивную браузерную игру? Тут, определённо, нужна технология canvas.

> SVG — векторная графика

Если вы знаете о том, что вам нужно разместить на веб-странице векторное изображение, это значит, что вам подходит SVG. Векторные изображения обычно выглядят лучше аналогичных растровых, хранящихся, например, в JPG-файлах. Кроме того, файлы векторных изображений обычно меньше файлов растровых изображений.

В результате оказывается, что SVG очень часто используется для рисования логотипов. Код, описывающий такие изображения, можно встроить прямо в HTML. Он выглядит как набор декларативных инструкций:


```
<svg viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="50" />
</svg>
```
Если вам нужно, чтобы изображения были бы гибкими и отзывчивыми, значит SVG — это ваш выбор.


> Canvas — JavaScript-API для рисования

Для формирования canvas-изображений в HTML-коде страницы размещают элемент <canvas>, после чего, средствами JavaScript, «рисуют» на этом элементе. Другими словами, программист даёт браузеру команды, касающиеся того, как ему нужно что-то нарисовать (такой подход ближе к императивному, чем к декларативному). Вот как это выглядит:


```
<canvas id="myCanvas" width="578" height="200"></canvas>
<script>
  var canvas = document.getElementById('myCanvas');
  var context = canvas.getContext('2d');
  var centerX = canvas.width / 2;
  var centerY = canvas.height / 2;
  var radius = 70;

  context.beginPath();
  context.arc(centerX, centerY, radius, 0, 2 * Math.PI, false);
  context.fillStyle = 'green';
  context.fill();
</script>
```

> SVG-изображения хранятся в DOM

Если вы знакомы с событиями DOM, наподобие click и mouseDown, то знайте о том, что этими событиями можно пользоваться и при работе с SVG. В этом плане SVG-элемент <circle> не особенно сильно отличается от HTML-элемента div.

  
```
<svg viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="50" />
  <script>
    document.querySelector('circle').addEventListener('click', e => {
      e.target.style.fill = "red";
    });
  </script>
</svg>
```

> SVG лучше подходит для обеспечения доступности содержимого страниц

Элементу canvas вполне можно назначит его текстовую альтернативу:

`<canvas aria-label="Hello ARIA World" role="img"></canvas>`

То же самое можно сделать и для SVG-элемента. Но, так как SVG-изображения и их внутренние механизмы хранятся прямо в DOM, SVG обычно рассматривают как технологию, используемую в тех случаях, когда создают проекты, отличающиеся доступностью для людей с ограниченными возможностями.

Другими словами — можно создать SVG-изображение, с элементами которого смогут работать ассистивные технологии, помогающие своим пользователям ориентироваться на веб-страницах.

> На SVG-изображения можно воздействовать с помощью CSS

Выше мы уже говорили о том, что SVG-элементы хранятся в DOM, и о том, что доступ к этим элементам можно получить из JavaScript-кода. В случае с CSS эта история повторяется:


```
<svg viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="50" />
  <style>
    circle { fill: blue; }
  </style>
</svg>
```

Обратите внимание на то, что в примерах блоки <script> и <style> размещаются внутри блока <svg>. Это — совершенно нормально. Но если учесть то, что SVG-элемент находится в обычном HTML-коде, то окажется, что внутренние блоки <script> и <style> вполне можно из него убрать. Кроме того, если нужно, можно воздействовать на SVG-элемент с помощью внешних стилей и скриптов.

> Сравнение SVG и canvas от Рут Джон

|Возможность| SVG | canvas |
|--|--|--|
| Векторная графика |  + |  - |
| Растровая графика | - | + |
| Доступ в DOM | + | - |
| Доступность | + | ± |
| Вывод текста | + | + |
| Вывод градиентов и паттернов | + | + |
| Поддержка CSS-анимации | + | - |
| Поддержка CSS-фильтров | + | + |
| Поддержка SVG-фильтров | + | + |
| Поддержка вывода файлов изображений и видеофайлов | - | + |
| Экспорт содержимого элемента | - | + |
| Управление отдельными пикселями | - | + |
| Доступ из JavaScript | - | + |
| Производительность анимации | ± | + |
|Поддержка вычислений, выполняемых за пределами главного потока| | - | + |



### SVG — это стандартный выбор. Canvas — это запасной вариант

> Итоги

- Нужно нарисовать небольшую иконку? Это, безусловно, территория SVG. Дело в том, что описание SVG-изображения хранится в DOM, в результате SVG отлично подходит для того, чтобы нарисовать что-то вроде значка на кнопке. Не стоит и говорить о том, что на SVG-изображения можно влиять средствами CSS, и, с помощью JavaScript, подключать к их элементам обработчики событий.

- Нужно создать интерактивную браузерную игру? Тут, определённо, нужна технология canvas. Браузерная игра, наверняка, будет содержать множество движущихся элементов и сложных анимаций. Элементы игрового мира будут взаимодействовать друг с другом, что означает определённые требования к производительности. Для решения таких задач отлично подходит canvas.
  
  
  Источник: https://habr.com/ru/company/ruvds/blog/476292/
