---
"$title": Включить экспериментальные функции
"$order": '3'
description: Экспериментальные компоненты AMP - это выпущенные функции, которые еще не готовы к широкому использованию, поэтому они защищены статусом экспериментальных.
formats:
- веб-сайты
- истории
- Объявления
---

[Экспериментальные компоненты AMP](https://github.com/ampproject/amphtml/tree/master/tools/experiments) – это существующие функции, которые пока не готовы к массовому использованию.

Разработчики и пользователи могут отказаться от них, пока мы не сообщим об окончательной готовности. До этого момента применять экспериментальные компоненты следует с осторожностью, поскольку они могут вызывать ошибки и иногда дают непредсказуемые результаты.

[tip type="important"] Есть риск, что некоторые эксперименты никогда не будут включены в проект AMP. [/tip]

{% set experimental_components = g.docs('/content/amp-dev/documentation/components/reference')|selectattr('experimental')|list %} {% if experimental_components|length %} The following is a list of components that are currently in experimental status and are ready to be tested by developers for first user feedback:


<ul> {% for component in experimental_components %}   <li><a href="%7B%7B%20component.url.path%20%7D%7D">{{ component.title }}</a></li> {% endfor %} </ul> {% endif %}

## Включите канал разработки AMP

AMP Dev Channel - это способ настроить браузер на использование более новой версии библиотек AMP JS.

Выпуск AMP Dev Channel **может быть менее стабильным** и содержать функции, доступные не всем пользователям. Включите эту опцию, если вы хотите помочь тестировать новые версии AMP, сообщать об ошибках или создавать документы, для которых требуется новая функция, которая пока недоступна для всех.

Участие в Dev Channel позволяет:

- тестируйте и играйте с новыми функциями, которые еще не доступны для всех пользователей.
- используйте для обеспечения качества (QA), чтобы убедиться, что ваш сайт совместим со следующей версией AMP.

Если вы обнаружите проблему, которая возникает только в версии AMP для Dev Channel, сообщите [о проблеме](https://github.com/ampproject/amphtml/issues/new) с описанием проблемы. Всегда указывайте URL-адрес страницы, на которой воспроизводится проблема.

To opt your browser into the AMP Dev Channel, go to [the AMP experiments page](https://cdn.ampproject.org/experiments.html) and activate the "AMP Dev Channel" experiment. To get notified about important/breaking changes about AMP, subscribe to the [amphtml-announce](https://groups.google.com/forum/# !forum/amphtml-announce) mailing list.

## Как включить экспериментальный компонент

#### Подается с cdn.ampproject.org

Для контента, обслуживаемого с `https://*.cdn.ampproject.org` , перейдите в `/experiments.html` в субдомене Google AMP Cache и включите (или отключите) любой экспериментальный компонент, включив (или выключив) их.

Например, чтобы включить эксперименты с кешированными страницами AMP, источником которых является `www.example.com` , перейдите по `www-example-com.cdn.ampproject.org/experiments.html` .

Experiment opt-ins are saved to `localStorage` and only enables the experiment on AMP pages served from the current domain.

#### Обслуживается из других доменов

Для контента, обслуживаемого из доменов, отличных от CDN, эксперименты можно переключать в консоли разработчика, используя:

```js
AMP.toggleExperiment('experiment')
```

Любой файл AMP, включающий экспериментальные функции, не пройдет [проверку AMP](validation-workflow/validate_amp.md) . Удалите эти экспериментальные компоненты, чтобы получить готовые документы AMP.

## Включить эксперимент для определенного документа

Документ может выбрать участие в определенных экспериментах. Для этого поместите метатег имени `amp-experiments-opt-in` в заголовок HTML-документа перед сценарием AMP ( `https://cdn.ampproject.org/v0.js` ). Его значение содержания представляет собой строку идентификаторов экспериментов, разделенных запятыми.

```html
<head>
  ...
  <meta name="amp-experiments-opt-in" content="experiment-a,experiment-b">
  <!-- The meta tag needs to be placed before the AMP runtime script.-->
  <script async src="https://cdn.ampproject.org/v0.js"></script>
  ...
</head>
```

Таким образом, указанные эксперименты будут доступны для всех посетителей документа. Однако не все эксперименты допускают включение на уровне документа. Полный список разрешенных экспериментов см. В атрибуте `allow-doc-opt-in` в файле [`prod-config.json`](https://github.com/ampproject/amphtml/blob/master/build-system/global-configs/prod-config.json) . Обратите внимание, что согласие с документом может быть отменено отказом пользователя.

## Первоначальные испытания

[Origin trials](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/explainer.md) enable developers to use an experimental feature in production and provide essential feedback.

Традиционно функция в экспериментальном режиме может использоваться в разработке, но не может быть передана в производство. С помощью пробных версий Origin заинтересованные разработчики могут принять участие в тестировании экспериментальной функции в производственной среде со следующими ожиданиями:

- Тест ограничен по времени.
- Эта функция, вероятно, претерпит некоторые изменения после первоначальных испытаний.

Пробные версии Origin предоставляют возможность внедрить новую функцию и извлечь из нее пользу еще до того, как она станет полноценной. Функция будет существовать на сайте разработчика, а не охраняться экспериментом, и обратная связь может напрямую влиять на направление функции.

{% set trial_components = g.docs('/content/amp-dev/documentation/components/reference')|selectattr('origin_trial')|list %} {% if trial_components|length %} Components in the following list can currently be tested via an origin trial:


<ul> {% for component in trial_components %}   <li><a href="%7B%7B%20component.url.path%20%7D%7D">{{ component.title }}</a></li> {% endfor %} </ul> {% endif %}

### Включить пробную версию origin

Включите следующий `<meta>` тег `<head>` на каждой странице, на которой используется пробный эксперимент с исходным кодом:

```html
<meta name="amp-experiment-token" content="{copy your token here}">
```

Примечание. `"amp-experiment-token"` - это буквальная строка `"amp-experiment-token"` . Ни сам токен (который входит в атрибут содержимого), ни название эксперимента.
