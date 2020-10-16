---
"$title": Включить фреймы
"$order": '10'
description: Узнайте, как отображать мультимедийный контент на ваших страницах и как использовать фреймы для отображения расширенного контента за пределами ограничений AMP.
formats:
- websites
components:
- iframe
author: pbakaus
contributors:
- Meggin
- bpaduch
---

Узнайте, как отображать мультимедийный контент на ваших страницах и как использовать фреймы для отображения расширенного контента за пределами ограничений AMP.

## Основы

Вы можете отобразить iframe на своей странице с помощью элемента [`amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) .

Фреймы iframe особенно полезны в AMP для отображения содержимого, не поддерживаемого в контексте главной страницы, например содержимого, требующего написанного пользователем JavaScript.

### Требования для `amp-iframe`

- Must be at least **600px** or **75%** of the first viewport away from the top (except for iframes that use a [`placeholder`](#using-placeholders)).
- Могут запрашивать ресурсы только через HTTPS, и они не должны находиться в том же источнике, что и контейнер, если только они не указывают allow-same-origin.

[tip type="read-on"] ПРОЧИТАЙТЕ **-** Узнайте больше в [полной спецификации `amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) . [/tip]

### Включите сценарий

Чтобы включить [`amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) на свою страницу, сначала включите следующий скрипт в `<head>` , который загружает дополнительный код для расширенного компонента:

[sourcecode:html]
<script async custom-element="amp-iframe"
  src="https://cdn.ampproject.org/v0/amp-iframe-0.1.js"></script>
[/sourcecode]

### Напишите разметку

In the following example, we created a responsive [`amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) to embed a Google Map via the [Google Maps Embed API](https://developers.google.com/maps/documentation/embed/guide):

```html
<amp-iframe width="200" height="100"
    sandbox="allow-scripts allow-same-origin"
    layout="responsive"
    src="https://www.google.com/maps/embed/v1/place?key={YOUR API KEY}&q=europe">
</amp-iframe>
```

## Использование заполнителей<a name="using-placeholders"></a>

Вы можете отобразить [`amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) в верхней части документа, если [`amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) содержит элемент с атрибутом `placeholder` (например, элемент [`amp-img`](../../../../documentation/components/reference/amp-img.md) ), который будет отображаться как заполнитель, пока iframe не будет готов к отображаться.

[tip type="read-on"] **READ ON –**: Learn more about placeholders in [Iframe with placeholder](../../../../documentation/components/reference/amp-iframe.md#iframe-with-placeholder). [/tip]

Пример с заполнителем:

```html
<amp-iframe width="400" height="225"
    sandbox="allow-scripts allow-same-origin"
    layout="responsive"
    src="https://giphy.com/embed/OWabwoEn7ezug">
  <amp-img placeholder layout="fill"
      src="https://ampproject-b5f4c.firebaseapp.com/examples/images/kittens-biting.jpg"></amp-img>
</amp-iframe>
```

Отображается как:

<amp-iframe width="400" height="225" sandbox="allow-scripts allow-same-origin" layout="responsive" src="https://giphy.com/embed/OWabwoEn7ezug">
<amp-img placeholder layout="fill" src="https://ampproject-b5f4c.firebaseapp.com/examples/images/kittens-biting.jpg"></amp-img>
</amp-iframe>

## Примеры

Вы можете найти более сложные примеры [`amp-iframe`](../../../../documentation/components/reference/amp-iframe.md) в [AMP By Example](../../../../documentation/examples/documentation/amp-iframe.html) .
