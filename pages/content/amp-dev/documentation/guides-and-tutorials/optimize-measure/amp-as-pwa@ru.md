---
"$title": Легкий автономный доступ и повышенная производительность
"$order": '1'
description: Service Worker - это прокси на стороне клиента, который находится между вашей страницей и вашим сервером и используется для создания фантастических оффлайн-приложений, быстрой загрузки ...
formats:
- веб-сайты
author: CrystalOnScript
contributors:
- пбакаус
---

[Сервисные работники](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) обеспечивают богатый опыт работы в автономном режиме и единообразный пользовательский интерфейс в различных сетях. Кэшируя ресурсы в браузере, веб-приложение может предоставлять пользователю данные, активы и автономные страницы, чтобы поддерживать его интерес и информированность.

Помните: Service Worker не сможет взаимодействовать с AMP-кешированной версией вашей страницы. Используйте его для дальнейших путешествий к месту вашего происхождения.

## Установить Service Worker

Service Worker - это клиентский прокси-сервер, который находится между вашей страницей и вашим сервером и используется для создания фантастических возможностей в автономном режиме, сценариев быстрой загрузки оболочки приложений и отправки push-уведомлений.

[tip type="note"] **ПРИМЕЧАНИЕ.** Если концепция Service Workers нова для вас, прочтите [введение на WebFundamentals](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers) . [/tip]

Ваш Service Worker должен быть зарегистрирован на данной странице, иначе браузер не найдет и не запустит его. По умолчанию это делается с помощью [небольшого количества JavaScript](https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/registration) . На страницах AMP вы используете компонент [`amp-install-serviceworker`](../../../documentation/components/reference/amp-install-serviceworker.md) для достижения того же.

For that, first include the [`amp-install-serviceworker`](../../../documentation/components/reference/amp-install-serviceworker.md) component via its script in the `<head>` of your page:

[sourcecode:html]
<script async custom-element="amp-install-serviceworker"
  src="https://cdn.ampproject.org/v0/amp-install-serviceworker-0.1.js"></script>
[/sourcecode]

Затем добавьте следующее где-нибудь в свой `<body>` (измените, чтобы указать на вашего фактического Service Worker):

[sourcecode:html]
<amp-install-serviceworker
      src="https://www.your-domain.com/serviceworker.js"
      layout="nodisplay">
</amp-install-serviceworker>
[/sourcecode]

Если пользователь переходит на ваши AMP-страницы из вашего источника (в отличие от первого щелчка, который обычно обслуживается из AMP-кеша), Service Worker берет на себя и может делать [множество интересных вещей](https://developers.google.com/web/fundamentals/instant-and-offline/offline-ux) .

## Сервисный работник AMP

Если вы здесь, вы создаете страницы с помощью AMP. Команда AMP безмерно заботится о том, чтобы на первое место ставить пользователя и предоставлять ему доступ к сети мирового класса. Чтобы эти впечатления были единообразными, команда AMP создала сервисного работника специально для AMP!

[tip type="default"] **TIP –**  Follow our tutorial to learn to use the [AMP Service Worker in your PWA](/content/amp-dev/documentation/guides-and-tutorials/optimize-measure/amp_to_pwa.md). [/tip]

### Установка AMP Service Worker

Установите AMP Service Worker с минимальными шагами:

- Импортируйте код AMP Service Worker в свой файл Service Worker. [sourcecode:js] importScripts ('https://cdn.ampproject.org/sw/amp-sw.js'); [/sourcecode]

- Установите Service worker с помощью следующего кода. [sourcecode:js] AMP_SW.init (); [/sourcecode]

- Готово.

### Автоматическое кеширование

AMP Service Worker автоматически кэширует файлы сценариев AMP и документы AMP. Кэшируя файлы сценариев AMP, они мгновенно становятся доступными для браузера пользователей, что позволяет работать в автономном режиме и ускорять страницы в нестабильных сетях.

Если вашему приложению требуются определенные типы кэширования документов, AMP Service Worker позволяет настроить. Например, добавление списка запрещенных для документов, которые всегда должны запрашиваться из сети. В следующем примере замените `Array<RegExp>` массивом регулярных выражений, представляющих документы, которые вы хотите избежать кэширования.

[sourcecode:js] AMP_SW.init( documentCachingOptions: { denyList?: Array<regexp>; } ); [/sourcecode]</regexp>

Подробнее о [настройке кэширования документов здесь](https://github.com/ampproject/amp-sw/tree/master/src/modules/document-caching) .

### Оптимизация работника службы AMP

Чтобы использовать AMP Service Worker в полной мере, необязательные поля должны быть настроены для кэширования необходимых ресурсов и предварительной выборки ссылок.

Активы, которые стимулируют посещение пользователем страницы, например видео, важные изображения или загружаемый PDF-файл, должны быть кэшированы, чтобы к ним можно было снова получить доступ, если пользователь не в сети.

[sourcecode:js] AMP_SW.init (assetCachingOptions: [{regexp: /.(png|jpg)/, cachingStrategy: 'CACHE_FIRST'}],); [/sourcecode]

Вы можете настроить стратегию кэширования и определить список запрещенных.

Ссылки на страницы, которые могут потребоваться вашим пользователям, могут быть загружены заранее, что позволит им получить доступ в автономном режиме. Это делается путем добавления атрибута `data-prefetch` к тегу ссылки.

[sourcecode:html]
<a href='....' data-rel='prefetch' />
[/sourcecode]

### Офлайн-опыт

Сообщите пользователю, что он перешел в автономный режим, и что ему следует попробовать перезагрузить сайт, когда он снова в сети, добавив автономную страницу. AMP Service Worker может кэшировать как страницу, так и ее ресурсы.

[sourcecode:js] AMP_SW.init ({offlinePageOptions: {url: '/offline.html'; активы: ['/images/offline-header.jpg'];}}) [/sourcecode]

Успешная офлайн-страница выглядит так, как будто она является частью вашего сайта, благодаря согласованному пользовательскому интерфейсу с остальной частью приложения.

### Принудительное обновление

Команда работает над реализацией функции принудительного обновления / удаления, если ваш AMP Service Worker необходимо отключить или изменить, если развертывание для пользователей пошло не так.

Чтобы эффективно управлять серверным воркером, вы должны понимать, как [стандартное HTTP-кеширование влияет на то, как ваш сервис-воркер поддерживает актуальность JavaScript](https://developers.google.com/web/updates/2018/06/fresher-sw) . Сервис-воркеры, обслуживаемые с соответствующими директивами HTTP-кеширования, могут устранять небольшие исправления ошибок, внося соответствующие изменения и повторно развертывая сервис-воркера в среде хостинга. Если вам нужно удалить сервис-воркера, неплохо держать под рукой простой, [не требующий](https://en.wikipedia.org/wiki/NOP) вмешательства файл сервис-воркера, например следующий:

```js
self.addEventListener('install', () => {
  // Skip over the "waiting" lifecycle state, to ensure that our
  // new service worker is activated immediately, even if there's
  // another tab open controlled by our older service worker code.
  self.skipWaiting();
});
```

[tip type="read-on"] [Подробнее](https://stackoverflow.com/questions/33986976/how-can-i-remove-a-buggy-service-worker-or-implement-a-kill-switch/38980776#38980776) об управлении развернутыми сервисными работниками. [/tip]

## Написать сотруднику таможенной службы

Вы можете использовать описанный выше метод, чтобы включить автономный доступ к вашему сайту AMP, а также расширить свои страницы, **как только они будут обслуживаться из источника** . Это потому, что вы можете изменить ответ через событие `fetch` Service Worker и вернуть любой ответ, который хотите:

[sourcecode:js] self.addEventListener ('выборка', функция (событие) {event.respondWith (caches.open ('mysite'). Then (function (cache) {return cache.match (event.request) .then (function ( ответ) {var fetchPromise = fetch (event.request) .then (function (networkResponse) {cache.put (event.request, networkResponse.clone ()); return networkResponse;})

```
    // Modify the response here before it goes out..
    ...

    return response || fetchPromise;
  })
})
```

); }); [/sourcecode]

Используя этот метод, вы можете изменить свою страницу AMP, добавив всевозможные дополнительные функции, которые в противном случае не [прошли бы проверку AMP](../../../documentation/guides-and-tutorials/learn/validation-workflow/validate_amp.md) , например:

- Динамические функции, требующие пользовательского JS.
- Компоненты, которые настраиваются / актуальны только для вашего сайта.
