---
$title: Руководства и руководства по форматированию
$order: '3'
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

## Фильтрация разделов

Некоторые документы могут иметь отношение к нескольким форматам AMP, но для некоторых форматов может потребоваться дополнительное объяснение или информация, не относящаяся к другим. Вы можете отфильтровать эти разделы, заключив их в следующий шорткод.

<div class="ap-m-code-snippet">
<pre>&lsqb;filter formats="websites"]<br>This is only visible for [websites](?format=websites).<br>&lsqb;/filter]</pre>
</div>

[filter formats="websites"] Это видно только для [веб-сайтов](?format=websites) . [/filter]

[filter formats="websites, email"] Это видно для [веб-сайтов](?format=websites) и [электронной почты](?format=email) . [/filter]

[filter formats="stories"] Это видно для [историй](?format=stories) . [/filter]




## подсказки

Вы можете добавить подсказки и уточнения, заключив текст в следующий шорткод:

<div class="ap-m-code-snippet">
<pre>&lsqb;tip type="default"]<br>Default tip<br>[/tip]</pre>
</div>

[tip type="important"] Важно [/tip]

[tip type="note"] Примечание [/tip]

[tip type="read-on"] Продолжение чтения [/tip]




## Фрагменты кода

Поместите фрагменты кода в наборы из трех обратных кавычек, укажите язык в конце первого набора обратных кавычек.

<div class="ap-m-code-snippet">
<pre>```html<br>  // code sample<br>```</pre>
</div>





Если ваш код содержит двойные фигурные скобки, что часто бывает, если вы используете шаблоны [`amp-mustache`](../../../../documentation/components/reference/amp-mustache.md?format=websites) , вам необходимо обернуть часть кода:

<div class="ap-m-code-snippet">
<pre>```html<br>{% raw	%}<br>  // code with double curly braces<br>{% endraw	%}<br>```</pre>
</div>

### Фрагменты кода в списках

Python-Markdown имеет некоторые ограничения. Используйте следующий синтаксис при включении фрагментов кода в списки:

<div class="ap-m-code-snippet">
<pre>1. First:<br>    &lsqb;sourcecode:html]<br>      <br>        <p>Indented content.</p><br>      <br>    &lsqb;/sourcecode]<br>  2. Second<br>  3. Third</pre>
</div>

## Предварительный просмотр примеров кода

Примеры кода могут иметь предварительный просмотр и / или ссылку на версию [AMP Playground](https://playground.amp.dev/) .

<div class="ap-m-code-snippet">
  <pre>  &lsqb;example preview="default: none|inline|top-frame"<br>          playground="default: true|false"<br>          imports="{custom-element-10},{custom-element-21},..."           template="{custom-template2}"]   ```html     // code sample   ```   &lsqb;/example]   {/custom-template2}{/custom-element-21}{/custom-element-10}</pre>
</div>

Примечание: предварительный просмотр будет автоматически преобразован в текущий выбранный формат при его открытии на игровой площадке 🤯!

Используйте атрибут `preview` чтобы определить, как создается предварительный просмотр:

- **none** : предварительный просмотр не будет создан

- **inline** : предварительный просмотр примера отображается над исходным кодом. Встроенный предварительный просмотр возможен только для обычных примеров веб - сайта , если код не содержит каких - либо `head` элементов. Используйте эту опцию для маленьких примеров , которые не нуждаются в каком - либо стиле или другие `head` элементах (импорт не учитывается, так как они определяются через `imports` атрибут).

- **top-frame** : предварительный просмотр примера отображается над исходным кодом внутри iframe. Ориентацию можно переключать между `portrait` и `landscape` режимами. Вы можете предварительно выбрать ориентацию, указав дополнительный атрибут:

- **ориентация** : по `default: landscape|portrait`

Если требуются настраиваемые элементы, укажите их в атрибуте `imports` в виде списка, разделенного запятыми, с именем компонента, за которым следует двоеточие и версия. Если в вашем коде используется [`amp-mustache`](../../../../documentation/components/reference/amp-mustache.md?format=websites) укажите зависимость в атрибуте `template` .

Для содержания электронной почты со ссылками на ресурсы используйте заполнитель <code>{{server_for_email}}</code> в источнике.

### Встроенный образец

Вот простой встроенный образец. Вы можете определить CSS с помощью встроенных стилей:

<div class="ap-m-code-snippet">
<pre>  [example preview="inline" playground="true"]<br>    ```html<br>    <div style="background: red; width: 200px; height: 200px;">Hello World</div><br>    ```<br>  [/example]<br>  [/example]</pre>
</div>

Вот как это выглядит:

[example preview="inline" playground="true"]

```html
<div style="background: red; width: 200px; height: 200px;">Hello World</div>
```

[/example]
