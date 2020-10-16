---
$title: Руководства и руководства по форматированию
$order: 3
description: Требования к форматированию файлов для amp.dev
formats:
- веб-сайты
- истории
- Объявления
- Эл. адрес
author: CrystalOnScript
---

Руководства и учебные пособия представлены в [Markdown](https://www.markdownguide.org/) с дополнительным форматированием внешнего вида и шорткода.

## Расположение документации

Контент amp.dev извлекается из двух репозиториев: [amp.dev](https://github.com/ampproject/amp.dev) и [AMPHTML](https://github.com/ampproject/amphtml) . Вся справочная документация по компонентам извлекается из AMPHTML либо из встроенных, либо из расширений.

- [Встроенные компоненты](https://github.com/ampproject/amphtml/tree/master/builtins)
- [Компоненты](https://github.com/ampproject/amphtml/tree/master/extensions)
- [Курсы](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/courses)
- [Примеры](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/examples)
- [Руководства и руководства](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/guides-and-tutorials)

Есть еще несколько документов, которые импортируются в amp.dev из AMPHTML. Они [перечислены в этом файле](https://github.com/ampproject/amp.dev/blob/future/platform/config/imports/spec.json) . Не обновляйте эти документы в репозитории amp.dev - ваши изменения будут перезаписаны при последующих сборках!

## Frontmatter

Frontmatter находится в верхней части каждого руководства и учебного пособия.

Пример:

```yaml
$title: Include Custom JavaScript in AMP Pages
$order: 7
formats:
  - websites
author: CrystalOnScript
contributors:
  - fstanis
description: For web experiences requiring a high amount of customization AMP has created amp-script, a component that allows the use of arbitrary JavaScript on your AMP page without affecting the page's overall performance.
```

<table>
  <tr>
   <td>
    <code>$title</code>
   </td>
   <td>Заголовок вашего документа, как он будет отображаться в оглавлении. Начните с заглавной буквы в первом слове, за исключением «AMP» и других имен собственных. Используйте амперсанд `&` вместо слова `and`.</td>
  </tr>
  <tr>
   <td>
    <code>$order</code>
   </td>
   <td>Определите, где в оглавлении появится ваш документ. Возможно, вам придется отредактировать `$ order` в других документах, чтобы он отображался в правильном месте.</td>
  </tr>
  <tr>
   <td>
    <code>formats</code>
   </td>
   <td>Перечислите возможности AMP, к которым имеет отношение ваш документ. Если ваш документ имеет отношение к веб-сайтам AMP и историям AMP, но не относится к рекламе AMP или электронной почте AMP, вашему фронтмену нужно следующее: `` форматы yaml: - веб-сайты - истории ``</td>
  </tr>
  <tr>
   <td>
<code>author</code>
   </td>
   <td>Автор ты! Используйте свое имя пользователя GitHub.</td>
  </tr>
  <tr>
   <td>
<code>contributors</code>
   </td>
   <td>Перечислите всех, кто внес свой вклад в ваш документ. Это поле не является обязательным.</td>
  </tr>
  <tr>
   <td>
<code>description</code>
   </td>
   <td>Напишите краткое описание своего руководства или учебника. Это помогает с поисковой оптимизацией, передавая вашу работу тем, кто в ней нуждается!</td>
  </tr>
  <tr>
   <td>
<code>tutorial</code>
   </td>
   <td>Добавьте `tutorial: true` к обложке веб-сайта, чтобы добавить рядом с ним значок учебника. Учебники находятся внизу своего раздела в оглавлении.</td>
  </tr>
</table>

# Шорткоды

Список шорткодов и их использования можно найти на сайте [documentation.md на GitHub](https://github.com/ampproject/amp.dev/blob/future/contributing/documentation.md#shortcodes) .

## Изображений

amp.dev построен с использованием AMP! Поэтому наши изображения должны соответствовать критериям [`amp-img`](../../../../documentation/components/reference/amp-img.md) . В процессе сборки используется следующий синтаксис для преобразования изображений в правильный формат `amp-img` .

<div class="ap-m-code-snippet">
<pre>{{ image('/static/img/docs/tutorials/custom-javascript-tutorial/image1.jpg', 500, 369, layout='intrinsic', alt='Image of basic amp script tutorial starter app') }}</pre>
</div>
