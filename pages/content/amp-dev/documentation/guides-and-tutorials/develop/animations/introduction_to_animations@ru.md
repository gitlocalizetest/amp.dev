---
"$title": Введение в сложные анимации
"$order": '2'
description: Для анимации, которой нельзя управлять путем добавления и удаления классов, AMP предлагает несколько компонентов, специфичных для анимации. Эти компоненты применяют принципы AMP к анимации ...
formats:
- websites
- ads
author: CrystalOnScript
---

Для анимаций, которые нельзя управлять путем [добавления и удаления классов](triggering_css_animations.md) , AMP предлагает несколько компонентов, специфичных для анимации. Эти компоненты применяют принципы AMP к анимации: они быстрые, эффективные и ориентированные на пользователя. AMP ограничивает допустимые свойства CSS внутри ключевых кадров, но предоставляет такие преимущества, как детальное управление, бесшовную анимацию и кроссбраузерную совместимость без дополнительной работы.

Используйте amp-animation, если вам нужно жестко контролировать воспроизведение, а также иметь точную синхронизацию с одновременной анимацией нескольких элементов.

## Создание базовой анимации AMP

Компонент [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) позволяет использовать [API веб-анимации](https://www.w3.org/TR/web-animations/) в AMP.

Базовая [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) - это объект JSON, состоящий из следующих основных частей:

- Элемент, который компонент анимирует, или `selector` .
- [Временные свойства](../../../../documentation/components/reference/amp-animation.md#timing-properties)
- [Ключевые кадры](../../../../documentation/components/reference/amp-animation.md#keyframes)
- [Вызывать](../../../../documentation/components/reference/amp-animation.md#triggering-animation)

```
<amp-animation layout="nodisplay" id="exampleAnimation">
<script type="application/json">
{
 "selector": "#elementID", //select the element to animate
 "duration": "1s", //timing property
 "iterations": 2, //timing property
 "fill": "both", //timing property
 "keyframes": {"opacity": 0, "transform": "scale(2)"} //keyframes
}
</script>
</amp-animation>
<!-- trigger -->
<button on="tap:exampleAnimation.start">
```

### Селектор

Как и CSS, компонент [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) связывает свойства анимации с элементом, объявляя имя тега, класс или идентификатор элемента в поле `"selector"` . Компонент анимирует каждый элемент с объявленным типом тега или именем класса. Используйте идентификатор, чтобы гарантировать анимацию одного элемента.

### Свойства времени

[Свойства синхронизации](../../../../documentation/components/reference/amp-animation.md#timing-properties) определяют, сколько времени занимает анимация, сколько раз она воспроизводится и какие ключевые кадры направления выполняются.

Свойства времени не требуются, но анимация может не запускаться, если отсутствуют свойства, связанные со временем и отображением, например `duration` и `fill` .

### Ключевые кадры

Хотя CSS позволяет вам переходить из одного состояния в другое с помощью переходов, вы должны объявить свойства анимации как ключевые кадры для реализации [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) (аналогично [CSS-анимации](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) ). Чтобы обеспечить плавное воспроизведение и кроссбраузерную совместимость, [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) [ограничивает то, какие свойства ключевых кадров](../../../../documentation/components/reference/amp-animation.md#allow-listed-properties-for-keyframes) можно использовать для свойств с ускорением графического процессора, которые не вызывают перепланировку и могут анимироваться в [потоке композитора](https://dev.chromium.org/developers/design-documents/compositor-thread-architecture) . Это предотвращает вмешательство анимации в AMP и [процесс рендеринга](https://developers.google.com/web/updates/2018/09/inside-browser-part3#javascript_can_block_the_parsing) браузера.

[tip type="note"] Ключевые кадры либо определены непосредственно в [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) либо на них имеются ссылки из [`<amp style-keyframe>`](../../../../documentation/guides-and-tutorials/learn/spec/amphtml.md#keyframes-stylesheet) если они соответствуют ограничениям свойств. Подробнее [о ключевых кадрах в `amp-animation`](../../../../documentation/components/reference/amp-animation.md#keyframes) . [/tip]

### Вызывать

Триггер запускает последовательность анимации. Расширение [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) запускается либо тогда, когда `<body>` становится видимым на странице, либо при подключении его к [действию или событию AMP.](../../../../documentation/guides-and-tutorials/learn/amp-actions-and-events.md)

Запуск по видимости `<body>` полезен, когда анимация должна запускаться сразу после загрузки страницы, потому что она отображается «над сгибом» или в первом окне просмотра страницы. Анимация запускается через видимость при добавлении `trigger="visibility"` в качестве атрибута к компоненту.

```
<amp-animation layout="nodisplay"
    trigger="visibility">
  ...
</amp-animation>
```

Анимации подключаются к действию или событию, присваивая компоненту [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) `id` и связывая этот `id` с желаемым триггером события, например, нажав кнопку.

```
<amp-animation layout="nodisplay" id="exampleAnimation">
  ...
</amp-animation>

<button on="tap:exampleAnimation.start">
```

## Создание сложных анимаций

Создание анимации в [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) позволяет осуществлять точный контроль, который выходит за рамки запуска и остановки анимации: он также может приостанавливать, реверсировать и направлять к определенной точке. Вы даже можете связать несколько анимаций вместе и анимировать элементы в последовательности.

### Подцели

Элементы одного и того же тега или класса могут иметь указанные временные свойства и переопределять значения переменных, определенных в анимации верхнего уровня.

[example preview="top-frame" playground="true" imports="amp-animation"]

```html
<body>
  <h1>Hello World!</h1>
  <h1>Hello World!</h1>
  <h1 id="helloMe">Hello World!</h1>
  <h1>Hello World!</h1>
  <amp-animation layout="nodisplay" id="animateThis">
    <script type="application/json">
      {
        "selector": "h1",
        "duration": "3s",
        "fill": "both",
        "keyframes": [{"transform": "translateX(0px)"}, {"transform": "translateX(50%)"}],
        "subtargets": [
          {
            "index": 1,
            "duration": "1s"
          },
          {
            "selector": "#helloMe",
            "direction": "reverse",
            "duration": "5s"
          }
        ]
      }
    </script>
  </amp-animation>
  <button on="tap:animateThis.start">
   start
  </button>
</body>
```

[/example]

### Цепные анимации

Несколько анимаций могут соединяться вместе, образуя большую последовательность. Вы можете создавать синхронизированные эффекты, такие как накладки на видео, написав анимацию в `animations` массиве внутри [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) компоненты.

```
<amp-animation id="overlaysAnim" layout="nodisplay">
  <script type="application/json">
    {
      "duration": "3s",
      "fill": "both",
      "animations": [{
          "selector": ".one",
          "keyframes": [{
              "opacity": "1",
              "offset": 0
            },
            {
              "opacity": "1",
              "offset": 0.04
            },
            {
              "opacity": "0",
              "offset": 0.0401
            },
            {
              "opacity": "0",
              "offset": 1
            }
          ]
        },
      ]
    }
  </script>
</amp-animation>
```

Эта установка воспроизводит каждую анимацию в течение 3 секунд в последовательности.

Для более крупных анимаций анимации внутри массива `animations` могут ссылаться на другие компоненты [`amp-animation`](../../../../documentation/components/reference/amp-animation.md) .

```
<amp-animation id="addEnergy" layout="nodisplay">
  <script type="application/json">
  {
    "duration": "0.3s",
    "fill": "both",
    "direction": "alternate",
    "animations": [
      {
        "selector": "#energy",
        "keyframes": [
          {"transform": "scaleX(calc(num(width('#energy'))/10))"},
          {"transform": "scaleX(calc(num(width('#energy'))/10 + 3))"}
        ]
      },
      {
        "animation": "atomExcite"
      }
    ]
  }
  </script>
</amp-animation>


<amp-animation id="atomExcite" layout="nodisplay" trigger="visibility">
<script type="application/json">
  {
    "duration": "0.3s",
    "iterations": "2",
    "fill": "both",
    "direction": "alternate",
    "animations": [
      {
        "selector": ".atom",
        "keyframes": {
          "transform": "translate(20vw)"
        }
      }
    ]
  }
  </script>
</amp-animation>
```

### Анимация неизвестного количества элементов

Используя [выражения `var()` и `calc()`](../../../../documentation/components/reference/amp-animation.md) вместе с [расширениями CSS](../../../../documentation/components/reference/amp-animation.md#css-extensions) , вы можете писать сложные и синхронизированные анимации, которые работают с любым количеством элементов. Это позволяет легко и плавно анимировать динамические и пользовательские данные.

[example preview="top-frame" playground="true"]

```html
<head>
  <script async custom-element="amp-animation" src="https://cdn.ampproject.org/v0/amp-animation-0.1.js"></script>
  <style amp-custom>
    .parent {
      perspective: 1000px;
      transform-style: preserve-3d;
      position: relative;
      margin: 10px;
      width: 239px;
      height: 335px;
    }
    .card {
      transform-origin: left;
      height: 50%;
      width: 50%;
    }
  </style>
</head>
<body>
  <amp-animation layout="nodisplay" id="cardAdmin">
    <script type="application/json">
      {
        "selector": ".card",
        "--duration": "2s",
        "duration": "var(--duration)",
        "delay": "calc((length() - index() - 1) * var(--duration))",
        "easing": "ease-in",
        "iterations": "1",
        "fill": "both",
        "keyframes": [
            {"transform": "translate3d(0px, 0px, 0px)"},
            {"transform": "translate3d(50%, 0px, 100px)"},
            {"transform": "translate3d(110%, 0px, 0px) rotateY(-20deg)"},
            {"transform": "translate3d(50%, 0px, -100px)"},
            {"transform": "translate3d(0px, 0px, -1px)"}
        ]
      }
    </script>
  </amp-animation>
  <div class="parent" on="tap:cardAdmin.start" tabindex=none role="animation">
    <amp-img class="card" src="https://upload.wikimedia.org/wikipedia/commons/7/70/3C.svg" layout="fill"></amp-img>
    <amp-img class="card" src="https://upload.wikimedia.org/wikipedia/commons/3/3a/3H.svg" layout="fill"></amp-img>
    <amp-img class="card" src="https://upload.wikimedia.org/wikipedia/commons/e/e1/KC.svg" layout="fill"></amp-img>
  </div>
</body>
```

[/example] This example works by:

- Объявление переменной `--duration` и присвоение ей значения двух секунд.
- Sets the `duration` to the var `--duration`'s value.
- Вычисляет задержку, применяемую к каждому элементу, который соответствует `.card` селектора.
    1. Расширение [`length()`](../../../../documentation/components/reference/amp-animation.md#css-length()-extension) вычисляет, сколько элементов `.card` было выбрано.
    2. The length then subtracts each `.card`'s [index()](../../../../documentation/components/reference/amp-animation.md#css-index()-extension)
    3. Полученное значение умножается на `--duration`
    4. Окончательная сумма применяется в секундах к задержке этого элемента.
- Анимация применяется к каждому элементу индивидуально, так что карты перемешиваются одна за другой, а не все одновременно.

Откройте анимацию на игровой площадке AMP и добавьте дополнительные элементы [`amp-img`](../../../../documentation/components/reference/amp-img) чтобы проверить это поведение.

### Отлично выглядеть везде

Анимация может включать [`conditions`](../../../../documentation/components/reference/amp-animation.md#conditions) , позволяющие настраивать эффекты. Адаптируйте анимацию к любому размеру экрана с помощью [условия `media`](../../../../documentation/components/reference/amp-animation.md#media-query) и поддерживает обратную совместимость с браузером, включив [условия `supports`](../../../../documentation/components/reference/amp-animation.md#supports-condition) в операторе [`switch`](../../../../documentation/components/reference/amp-animation.md#animation-switch-statement) .

[example preview="top-frame" playground="true"]

```html
<head>
 <style amp-custom>
    .drop {
      width: 20px;
      height: 20px;
      background: blue;
      margin-top: 1em;
      border-radius: 50%;
    }
    .right {
      position: absolute;
      right: 0;
      background: red;
    }
  </style>
  <script async custom-element="amp-animation" src="https://cdn.ampproject.org/v0/amp-animation-0.1.js"></script>
</head>
<body>
<amp-animation id="mediaAnimation" layout="nodisplay">
  <script type="application/json">
    {
      "duration": "1s",
      "iterations": "4",
      "fill": "both",
      "direction": "alternate",
      "animations": [
        {
          "media": "(min-width: 300px)",
          "selector": ".drop",
          "keyframes": {
            "transform": "translate(100vw)"
          }
        },
        {
          "media": "(max-width: 300px)",
          "selector": ".drop",
          "keyframes": {
            "transform": "translate(50vw)"
          }
        },
        {
          "media": "(min-width: 300px)",
          "selector": ".right",
          "keyframes": {
            "transform": "translate(-100vw)"
          }
        },
        {
          "media": "(max-width: 300px)",
          "selector": ".right",
          "keyframes": {
            "transform": "translate(-50vw)"
          }
        }
      ]
    }
  </script>
</amp-animation>

  <div class="rain">
    <div class="drop"></div>
    <div class="drop right"></div>
    <div class="drop"></div>
    <div class="drop right"></div>
    <div class="drop"></div>
    <div class="drop right"></div>
    <div class="drop"></div>
    <div class="drop right"></div>
  </div>
  <button on="tap:mediaAnimation.start">Start</button>
</body>
```

[/example]
