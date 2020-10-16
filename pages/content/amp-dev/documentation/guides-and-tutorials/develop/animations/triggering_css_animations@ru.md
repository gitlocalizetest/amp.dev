---
"$title": Запуск CSS-анимации и переходов
"$order": '1'
description: Запуск анимации CSS на страницах основан на добавлении и удалении классов с помощью JavaScript. Вы можете добиться того же поведения на страницах AMP, используя действие toggleClass ...
formats:
- websites
- ads
---

CSS-анимация позволяет веб-элементам переходить от одной конфигурации стиля CSS к другой. Браузер может запускать определенные анимации при загрузке, но анимация CSS, запускаемая событием, [зависит от добавления и удаления классов](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) . AMP поддерживает оба типа анимации.

Используйте CSS, когда у вас есть небольшая, содержащаяся анимация, для которой не нужно точно рассчитывать время.

## Определение CSS и ключевых кадров

Вы можете определить CSS в AMP следующими способами:

[filter formats="websites, stories"]

- В `<style amp-custom>` заголовке документа. Предел 75000 байт.
- Встроенные стили. Каждый экземпляр встроенного стиля имеет ограничение в 1000 байт. Встроенные стили учитываются при учете ограничения `<style amp-custom>` в 75 000 байт.
- В `<style amp-keyframes>` заголовке документа. Предел 500000 байт. Ограничено свойствами ключевого кадра.

[/filter]

[filter formats="ads"]

- В `<style amp-custom>` заголовке документа. Ограничение 20 000 байт.
- Встроенные стили. Каждый экземпляр встроенного стиля имеет ограничение в 1000 байт. Встроенные стили учитываются при учете ограничения `<style amp-custom>` в 20 000 байт.
- В `<style amp-keyframes>` заголовке документа. Предел 500000 байт. Ограничено свойствами ключевого кадра.

[/filter]

[tip type="read-on"] Read more in [Style & layout](../style_and_layout/index.md) about using CSS in AMP. [/tip]

[filter formats="websites, stories"] To keep your pages lean and speedy, AMP has enforced a 75,000 byte CSS limit in the `<amp style-custom>` tag. While you can use this to define animation styles, the 500,000 bye limit inside of `<amp style-keyframes>` tag allows for more verbose animations that won't take away precious site style resources. [/filter]

[filter formats="ads"] To keep your ads lean and speedy, AMP has enforced a 20,000 byte CSS limit in the `<amp style-custom>` tag. While you can use this to define animation styles,the 500,000 bye limit inside of `<amp style-keyframes>` tag allows for more verbose animations that won't take away precious site style resources. [/filter]

```html
  <style amp-custom>
    div {
      width: 100px;
      height: 100px;
      background: red;
      position: relative;
      animation: mymove 5s infinite;
    }
  </style>
</head>
<body>

<div></div>
  <style amp-keyframes>
   @keyframes mymove {
      0%   {transform: translatey(0px);}
      25%  {transform: translatey(200px);}
      75%  {transform: translatey(50px);}
      100% {transform: translatey(100px);}
    }
  </style>
</body>
```

## Добавление, удаление и переключение классов

Действие AMP, `toggleClass` позволяет добавлять и удалять классы для определенных элементов.

```js
elementName.toggleClass(class="className")
```

Вы можете переключить класс на тот же элемент, с которым вы хотите, чтобы пользователи взаимодействовали, например, на анимированном гамбургер-меню.

```html
 <div id="hamburger" tabindex=1 role=button on="tap:hamburger.toggleClass(class='close')">
```

Действие `toggleClass` может применяться к другим элементам и переключаться между двумя классами, добавляя атрибут `force` .

```html
<button on="tap:magicBox.toggleClass(class='invisible', force=true),magicBox.toggleClass(class='visible', force=false)">
  Disappear
</button>
<button on="tap:magicBox.toggleClass(class='visible', force=true),magicBox.toggleClass(class='invisible', force=false)">
  Reappear
</button>
```

Если вам нужно удалить класс и запретить повторное применение, добавьте атрибут `force` со значением `false` . Если вам нужно добавить класс и запретить удаление, добавьте `force` со значением `true` .

## Анимируйте с помощью CSS и состояния

Вы можете добавлять и удалять любое количество классов CSS с состояниями с помощью [`amp-bind`](../../../../documentation/components/reference/amp-bind.md) .

[example preview="top-frame" playground="true"]

```html
<head>
  <script async custom-element="amp-bind" src="https://cdn.ampproject.org/v0/amp-bind-0.1.js"></script>
  <style amp-custom>
    div {
      height: 100px;
      width: 100px;
      margin: 1em;
      background-color: green;
      margin-left: 100px;
      transition: 2s;
    }
    .visible {
      opacity: 1;
    }
    .invisible {
      opacity: 0;
    }
    .left {
      transform: translatex(-50px)
    }
    .right {
      transform: translatex(50px)
    }
    button {
      margin-top:  1rem;
      margin-left: 1rem;
    }
  </style>
</head>
<body>
  <amp-state id="magicBox">
    <script type="application/json">
      {
        "visibleBox": {
          "className": "visible"
        },
        "invisibleBox": {
          "className": "invisible"
        },
        "moveLeft": {
          "className": "left"
        },
        "moveRight": {
          "className": "right"
        }
      }
    </script>
  </amp-state>
  <div [class]="magicBox[animateBox].className"> </div>
  <button on="tap:AMP.setState({animateBox: 'invisibleBox'})">
    Disappear
  </button>
  <button on="tap:AMP.setState({animateBox: 'visibleBox'})">
    Reappear
  </button>
  <button on="tap:AMP.setState({animateBox: 'moveLeft'})">
    Move Left
  </button>
  <button on="tap:AMP.setState({animateBox: 'moveRight'})">
    Move Right
  </button>
</body>
```

[/example]

Определение несколько анимации класса сначала добавить список классов CSS в `<style amp-custom>` тег в `head` документа:

```css
    .visible {
      opacity: 1;
    }
    .invisible {
      opacity: 0;
    }
    .left {
      transform: translatex(-50px)
    }
    .right {
      transform: translatex(50px)
    }
```

Затем соедините каждый класс с состоянием:

```html
<amp-state id="magicBox">
  <script type="application/json">
    {
      "visibleBox": {
        "className": "visible"
      },
      "invisibleBox": {
        "className": "invisible"
      },
      "moveLeft": {
        "className": "left"
      },
      "moveRight": {
        "className": "right"
      }
    }
  </script>
</amp-state>
```

И свяжем элемент с классами:

```html
  <div [class]="magicBox[animateBox].className"> </div>
```

Состояния изменяются от связанного действия или события AMP. В следующем примере изменяется состояние от взаимодействия с пользователем:

```html
<button on="tap:AMP.setState({animateBox: 'invisibleBox'})">
    Disappear
</button>
<button on="tap:AMP.setState({animateBox: 'visibleBox'})">
    Reappear
</button>
<button on="tap:AMP.setState({animateBox: 'moveLeft'})">
    Move Left
</button>
<button on="tap:AMP.setState({animateBox: 'moveRight'})">
  Move Right
</button>
```

Использование [`amp-bind`](../../../../documentation/components/reference/amp-bind.md) таким образом явно устанавливает класс для определенного класса. Вам не нужно сообщать ему об удалении других классов.
