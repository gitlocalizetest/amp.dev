---
$title: Guías para formatos y tutoriales
$order: 3
description: Requisitos relacionados con el formato de los archivos para amp.dev
formats:
- websites
- stories
- ads
- email
author: CrystalOnScript
---

Las guías HELLO y tutoriales se presentan en [Markdown](https://www.markdownguide.org/), con un texto preliminar adicional y formato en código corto.

## Ubicación de la documentación

El contenido de amp.dev se extrae de dos repositorios, [amp.dev](https://github.com/ampproject/amp.dev) y [AMPHTML](https://github.com/ampproject/amphtml). Toda la documentación de referencia sobre los componentes se extrae de AMPHTML, ya sea de los componentes integrados o de las extensiones.

- [Componentes integrados ](https://github.com/ampproject/amphtml/tree/master/builtins)
- [Componentes](https://github.com/ampproject/amphtml/tree/master/extensions)
- [Cursos](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/courses)
- [Ejemplos](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/examples)
- [Guías y tutoriales](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/guides-and-tutorials)

Muchos otros documentos se importan hacia amp.dev desde AMPHTML. Estos se [registran en este archivo](https://github.com/ampproject/amp.dev/blob/future/platform/config/imports/spec.json). No actualice estos documentos en el repositorio de amp.dev, ¡sus cambios se sobrescribirán en las siguientes versiones!

## Texto preliminar

El texto premiliminar se encuentra en la parte superior de cada guía y tutorial.

Ejemplo:

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
   <td>Es el título de su documento tal como aparecerá en la Tabla de contenidos. Escriba con mayúscula la primera letra de la primera palabra, excepto en el caso de “AMP” y otros nombres propios. Utilice el símbolo et “&” en lugar de la palabra “y”.</td>
  </tr>
  <tr>
   <td>
    <code>$order</code>
   </td>
   <td>Define en qué lugar de la Tabla de contenidos aparece su documento. Posiblemente deba editar el “$order” en otros documentos para que aparezca en la posición correcta.</td>
  </tr>
  <tr>
   <td>
    <code>formats</code>
   </td>
   <td>Hace una lista de las experiencias de AMP para las que su documento es importante. Si su documento era relevante para los sitios web e historias de AMP, pero no para los anuncios o el correo electrónico de AMP, colocaría lo siguiente en su texto preliminar:     ```formatos yaml:           - sitios web           - historias     ```</td>
  </tr>
  <tr>
   <td>
<code>author</code>
   </td>
   <td>¡Usted es el autor! Utilice su nombre de usuario de GitHub.</td>
  </tr>
  <tr>
   <td>
<code>contributors</code>
   </td>
   <td>Sirve para mencionar a todas las personas que hayan contribuido en su documento. Este campo es opcional.</td>
  </tr>
  <tr>
   <td>
<code>description</code>
   </td>
   <td>Se utiliza para escribir una descripción breve de la guía o tutorial. Esto ayuda a la optimización de los motores de búsqueda, ¡permitiendo que su trabajo llegue a todas las personas que lo necesitan!</td>
  </tr>
  <tr>
   <td>
<code>tutorial</code>
   </td>
   <td>Agregue “tutorial: true” al texto preliminar para que el sitio web agregue el icono del tutorial junto a él. Los tutoriales se encuentran la parte inferior de su sección en la Tabla de contenidos.</td>
  </tr>
</table>

# Códigos cortos

Para consultar una lista de códigos cortos y la manera de utilizarlos, vaya a [documentation.md en GitHub](https://github.com/ampproject/amp.dev/blob/future/contributing/documentation.md#shortcodes).

## Imágenes

¡amp.dev se desarrolló con AMP! Por lo tanto, nuestras imágenes deben coincidir con los criterios [`amp-img`](../../../../documentation/components/reference/amp-img.md). El proceso de desarrollo utiliza la siguiente sintaxis para convertir las imágenes al formato adecuado `amp-img`.

<div class="ap-m-code-snippet">
<pre>{{ image('/static/img/docs/tutorials/custom-javascript-tutorial/image1.jpg', 500, 369, layout='intrinsic', alt='Image of basic amp script tutorial starter app') }}</pre>
</div>

## Filtro de secciones

Algunos documentos pueden ser importantes para varios de los formatos de AMP, pero algunos formatos posiblemente requieran descripciones adicionales o información que no sea relevante para los demás. Puede filtrar estas secciones envolviéndolas con el siguiente código corto.

<div class="ap-m-code-snippet">
<pre>&lsqb;filter formats="websites"]<br>This is only visible for [websites](?format=websites).<br>&lsqb;/filter]</pre>
</div>

[filter formats="websites"] Este solamente es visible para [sitios web](?format=websites). [/filter]

[filter formats="websites, email"] Este es visible para [sitios web](?format=websites) y [correos electrónicos](?format=email).[/filter]

[filter formats="stories"] Este es visible para [historias](?format=stories). [/filter]




## Sugerencias

Puede agregar sugerencias y textos destacados envolviendo el texto con el siguiente código corto:

<div class="ap-m-code-snippet">
<pre>&lsqb;tip type="default"]<br>Default tip<br>[/tip]</pre>
</div>

[tip type="important"] Importante [/tip]

[tip type="note"] Nota [/tip]

[tip type="read-on"] Continuar leyendo [/tip]




## Fragmentos de código

Coloque los fragmentos de código dentro de los conjuntos con tres comillas simples, y especifique el idioma al final del primer conjunto de comillas simples.

<div class="ap-m-code-snippet">
<pre>```html<br>  // code sample<br>```</pre>
</div>

```css
  // code sample
```

```js
  // code sample
```





Si su código contiene llaves dobles, lo cual sucede con frecuencia si utiliza plantillas [`amp-mustache`](../../../../documentation/components/reference/amp-mustache.md?format=websites), entonces debe envolver esa parte del código:

<div class="ap-m-code-snippet">
<pre>```html<br>{% raw	%}<br>  // code with double curly braces<br>{% endraw	%}<br>```</pre>
</div>

### Fragmentos de código en listas

El Python-Markdown tiene algunas limitaciones. Cuando incluya fragmentos de código en las listas, utilice la siguiente sintaxis:

<div class="ap-m-code-snippet">
<pre>1. First:<br>    &lsqb;sourcecode:html]<br>      <br>        <p>Indented content.</p><br>      <br>    &lsqb;/sourcecode]<br>  2. Second<br>  3. Third</pre>
</div>

## Previsualización de los ejemplos del código

Los ejemplos del código pueden tener una previsualización y/o enlace hacia una versión de [AMP Playground](https://playground.amp.dev/).

<div class="ap-m-code-snippet">
  <pre>  &lsqb;example preview="default: none|inline|top-frame"<br>          playground="default: true|false"<br>          imports="<custom-element-1>,<custom-element-2>,..."           template="<custom-template>"]   ```html     // code sample   ```   &lsqb;/example]   </custom-template></custom-element-2></custom-element-1></pre>
</div>

Nota: ¡La previsualización se transformará automáticamente al formato seleccionado actualmente cuando se abra en el Playground 🤯!

Utilice el atributo `preview` para definir cómo se generará la previsualización:

- **none**: No se generará ninguna previsualización

- **inline**: La previsualización del ejemplo se muestra sobre el código fuente. Solo es posible generar una vista previa sobre la función inline para ejemplos normales de sitios web si el código no contiene ningún elemento `head`. Utilice esta opción para ejemplos pequeños que no necesiten estilo u otros elementos de tipo `head` (las importaciones no cuentan, ya que estas se especifican mediante el atributo `imports`).

- **top-frame**: La previsualización del ejemplo se muestra sobre el código fuente dentro de un iframe. Es posible alternar la orientación entre el modo `portrait` y el `landscape`. Puede seleccionar previamente la orientación especificando el atributo adicional:

- **orientation**: `default: landscape|portrait`

Si se necesitan elementos personalizados, especifíquelos en el atributo `imports` como una lista separada por comas con el nombre del componente seguido de dos puntos y la versión. Si su código utiliza [`amp-mustache`](../../../../documentation/components/reference/amp-mustache.md?format=websites), en su lugar, especifique la dependencia con el atributo `template`.

Cuando el contenido de los correos electrónicos tenga enlaces hacia recursos utilice el marcador de posición <code>{{server_for_email}}</code> en la fuente.

### Ejemplo Inline

Aquí puede observar un ejemplo de una inserción simple inline. Puede definir la hoja de estilos en cascada (CSS) mediante los estilos inline:

<div class="ap-m-code-snippet">
<pre>  [example preview="inline" playground="true"]<br>    ```html<br>    <div style="background: red; width: 200px; height: 200px;">Hello World</div><br>    ```<br>  [/example]<br>  [/example]</pre>
</div>

El código se ve de la siguiente manera:

[example preview="inline" playground="true"]

```html
<div style="background: red; width: 200px; height: 200px;">Hello World</div>
```

[/example]

Advertencia: los ejemplos inline están insertados directamente dentro de la página. Esto podría generar conflictos si los componentes ya se utilizan en la página (por ejemplo, `amp-consent`).

### Previsualización del Top-Frame

Use la previsualización del top-frame siempre que necesite especificar elementos del encabezado o definir estilos globales dentro de `<style amp-custom>`.

Importante: No agregue ningún código boilerplate AMP basado en el formato AMP al encabezado, ya que este se agregará automáticamente. ¡Solamente agregue al encabezado los elementos que sean necesarios para el ejemplo!

<div class="ap-m-code-snippet">
<pre>[example preview="top-frame"<br>         playground="true"]<br>    ```html<br>    <head><br>      <script async custom-element="amp-youtube" src="https://cdn.ampproject.org/v0/amp-youtube-0.1.js"></script><br>      <style amp-custom><br>        body {<br>          background: red;<br>        }<br>      </style><br>    </head><br>    <body><br>      <h1>Hello AMP</h1><br>      <amp-youtube width="480"<br>        height="270"<br>        layout="responsive"<br>        data-videoid="lBTCB7yLs8Y"><br>      </amp-youtube><br>    </body><br>    ```<br>  [/example]</pre>
</div>

El código se ve de la siguiente manera:

[example preview="top-frame" playground="true"]

```html
<head>
  <script async custom-element="amp-youtube" src="https://cdn.ampproject.org/v0/amp-youtube-0.1.js"></script>
  <style amp-custom>
    body {
      background: red;
    }
  </style>
</head>
<body>
  <h1>Hello AMP</h1>
  <amp-youtube width="480"
    height="270"
    layout="responsive"
    data-videoid="lBTCB7yLs8Y">
  </amp-youtube>
</body>
```

[/example]

### Historias de AMP

Utilice `preview="top-frame"` junto con `orientation="portrait"` para previsualizar las historias de AMP.

<div class="ap-m-code-snippet">
<pre>[example preview="top-frame"<br>         orientation="portrait"<br>         playground="true"]<br>    ```html<br>    <head><br>      <script async custom-element="amp-story"<br>          src="https://cdn.ampproject.org/v0/amp-story-1.0.js"></script><br>      <style amp-custom><br>        body {<br>          font-family: 'Roboto', sans-serif;<br>        }<br>        amp-story-page {<br>          background: white;<br>        }<br>      </style><br>    </head><br>    <body><br>      <amp-story standalone><br>        <amp-story-page id="cover"><br>          <amp-story-grid-layer template="vertical"><br>            <h1>Hello World</h1><br>            <p>This is the cover page of this story.</p><br>          </amp-story-grid-layer><br>        </amp-story-page><br>        <amp-story-page id="page-1"><br>          <amp-story-grid-layer template="vertical"><br>            <h1>First Page</h1><br>            <p>This is the first page of this story.</p><br>          </amp-story-grid-layer><br>        </amp-story-page><br>      </amp-story><br>    </body><br>    ```<br>  [/example]</pre>
</div>

El código se ve de la siguiente manera:

[example preview="top-frame" orientation="portrait" playground="true"]

```html
  <head>
    <script async custom-element="amp-story"
        src="https://cdn.ampproject.org/v0/amp-story-1.0.js"></script>
    <style amp-custom>
      body {
        font-family: 'Roboto', sans-serif;
      }
      amp-story-page {
        background: white;
      }
    </style>
  </head>
  <body>
    <amp-story standalone>
      <amp-story-page id="cover">
        <amp-story-grid-layer template="vertical">
          <h1>Hello World</h1>
          <p>This is the cover page of this story.</p>
        </amp-story-grid-layer>
      </amp-story-page>
      <amp-story-page id="page-1">
        <amp-story-grid-layer template="vertical">
          <h1>First Page</h1>
          <p>This is the first page of this story.</p>
        </amp-story-grid-layer>
      </amp-story-page>
    </amp-story>
  </body>
```

[/example]

### URL absolutas para el correo electrónico de AMP

Observe cómo utilizamos <code>{{server_for_email}}</code> para crear un endpoint de la URL absoluta si está integrada dentro del correo electrónico de AMP.

<div class="ap-m-code-snippet">
<pre>  [example preview="top-frame" playground="true"]<br>    ```html<br>    <div class="resp-img">       <amp-img alt="flowers" src="%7B%7Bserver_for_email%7D%7D/static/inline-examples/images/flowers.jpg" layout="responsive" width="640" height="427"></amp-img>     </div><br>    ```<br>  [/example]</pre>
</div>

El código se ve de la siguiente manera:

[example preview="top-frame" playground="true"]

```html
<div class="resp-img">
  <amp-img alt="flowers"
    src="{{server_for_email}}/static/inline-examples/images/flowers.jpg"
    layout="responsive"
    width="640"
    height="427"></amp-img>
</div>
```

[/example]

### Cómo escapar las plantillas mustache

Este es un ejemplo de `top-frame` donde se utiliza un endpoint con acceso remoto. Las plantillas Mustache deben escaparse en los ejemplos mediante los códigos <code>{% raw %}</code> y <code>{% endraw %}</code>:

<div class="ap-m-code-snippet">
  <pre>[example preview="top-frame"<br>        playground="true"<br>        imports="amp-list:0.1"<br>        template="amp-mustache:0.2"]<br>    ```html<br>    <amp-list width="auto" height="100" layout="fixed-height"<br>      src="{{server_for_email}}/static/inline-examples/data/amp-list-urls.json"><br>      <template type="amp-mustache">{% raw %}<br>        <div class="url-entry"><br>          <a href="{{url}}">{{title}}</a><br>        </div><br>      {% endraw %}<br>      </template><br>    </amp-list><br>    ```<br>[/example]</pre>
</div>

El código se ve de la siguiente manera:

[example preview="top-frame" playground="true" imports="amp-list:0.1" template="amp-mustache:0.2"]

```html
<amp-list width="auto" height="100" layout="fixed-height"
  src="{{server_for_email}}/static/inline-examples/data/amp-list-urls.json">
  <template type="amp-mustache">{% raw %}
    <div class="url-entry">
      <a href="{{url}}">{{title}}</a>
    </div>
    {% endraw %}
  </template>
</amp-list>
```

[/example]

## Enlaces

Puede vincular otras páginas con la sintaxis para enlaces markdown estándar:

```md
 [link](../../../courses/beginning-course/index.md)
```

Cuando en amp.dev se realiza una vinculación hacia otra página, la referencia será una ruta del archivo que esté relacionada con el archivo de destino.

### Anclajes

Puede vincular secciones específicas de un documento utilizando anclajes:

```md
[link to example section](#example-section)
```

Cree el destino del anclaje utilizando `<a name="#anchor-name></a>` antes de vincular una sección sin anclajes. Un buen lugar para hacerlo es la parte final del encabezado de la sección:

```html
## Example section <a name="example-section"></a>
```

Cuando realice un anclaje, solamente debe utilizar letras, dígitos, guiones y guiones bajos. Para el anclaje, emplee nombres cortos en inglés que coincidan con el título o que describan la sección. Asegúrese de que el nombre del anclaje sea exclusivo dentro del documento.

Cuando se traduce una página, no deben modificarse los nombres del anclaje y es necesario que permanezcan en inglés.

Cuando cree un anclaje que se utilizará un enlace desde otra página, también debe crear el mismo anclaje en todas las traducciones.

### Filtro del formato AMP

Los componentes de los documentos, guías, tutoriales y ejemplos pueden filtrarse mediante el formato AMP, como los sitios web o las historias de AMP. Cuando los vincule con dicha página, debe especificar de manera explícita un formato, el cual sea compatible con el destino, para ello agregue el siguiente parámetro de formato al enlace:

```md
 [link](../../learn/amp-actions-and-events.md?format=websites)
```

Solo cuando esté seguro de que el destino es compatible con **todos** los formatos que se despliegan en su página puede omitir el parámetro.

### Referencias hacia los componentes

Un enlace hacia los documentos de referencia de un componente automáticamente señalará la última versión si su enlace omite esa parte de la versión. Cuando desee señalar de manera explícita una versión especifique el nombre completo:

```md
 [latest version](../../../components/reference/amp-carousel.md?format=websites)
 [explicit version](../../../components/reference/amp-carousel-v0.2.md?format=websites)
```

## Estructura de los documentos

### Títulos, encabezados y apartados

La primera letra de la primera palabra de los títulos, encabezados y apartados se escribe en mayúsculas, las siguientes se escriben en minúsculas. Entre las posibilidades se incluyen AMP y otros nombres propios. Ningún encabezado se llama `Introduction`, la introducción generalmente se encuentra después del título del documento.

### Cómo nombrar los documentos

Debe nombrar los documentos según la convención para la escritura de nombres establecida mediante guiones.

<table>
  <tr>
   <td>
<strong>Qué hacer</strong>
   </td>
   <td>
<strong>Qué no hacer</strong>
   </td>
  </tr>
  <tr>
   <td>hello-world-tutorial.md</td>
   <td>hello_world_tutorial.md</td>
  </tr>
  <tr>
   <td>website-fundamentals.md</td>
   <td>websiteFundamentals.md</td>
  </tr>
  <tr>
   <td>actions-and-events.md</td>
   <td>actionsandevents.md</td>
  </tr>
</table>
