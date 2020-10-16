---
"$title": Рекламируйте в AMP Stories
"$order": '3'
description: Истории AMP - это полноэкранный интерактивный интерфейс, который погружает читателей в контент. Реклама с помощью объявлений AMP Story обеспечивает плавный и бесперебойный ...
formats:
- stories
author: CrystalOnScript
---

Истории AMP - это полноэкранный интерактивный интерфейс, который погружает читателей в контент. Реклама с помощью объявлений AMP Story обеспечивает беспроблемную и бесперебойную интеграцию в путь пользователя, удерживая его вовлеченным и довольным платформой.

##Ad Placement <br>Unlike AMP web pages, where the amount and location of ads is designated by the placement of multiple [`amp-ad`](../../../documentation/components/reference/amp-ad.md) components, AMP Stories rely on a single  [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) component to dictate ad quantity and placement.

Расширение [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) - это оболочка для компонента [`amp-ad`](../../../documentation/components/reference/amp-ad.md) которая динамически вставляет одно или несколько объявлений, пока пользователь просматривает контент истории. Чтобы обеспечить лучший пользовательский опыт:

1. Объявления предварительно обрабатываются средой выполнения AMP Stories, а затем вставляются. Это гарантирует, что пользователям никогда не будет показано пустое или выгруженное объявление.

2. Плотность рекламы оптимизирована с учетом соотношения содержания, чтобы предотвратить перенасыщение. Расширение [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) решает, когда и где вставлять рекламу по мере продвижения пользователя.

Среда выполнения AMP выполняет вызов объявления как можно раньше и размещает первую страницу где-то после первых двух страниц и никогда не ставит последнюю страницу.

<amp-anim width="360" height="640" src="/static/img/docs/stampads/stamp_gif_ad.gif">
  <amp-img placeholder width="360" height="640" src="/static/img/docs/stampads/stamp_gif_still.png">
  </amp-img>
</amp-anim>

[tip type="note"] **ПРИМЕЧАНИЕ.** Более длинная история AMP создает больше возможностей для размещения рекламы. Точное размещение рекламного алгоритма со временем будет оптимизироваться. [/tip]

## Взаимодействие с пользователем <br>Пользователи могут проходить мимо рекламы так же, как и на обычных страницах историй; нажав правые две трети экрана.

{{ image('/static/img/docs/stampads/story_ad_ui.png', 304, 512, layout='intrinsic', alt='Image showing the area users can tap to skip an ad', caption='Users can progress past ads by tapping the right two thirds of the screen.', align='' ) }}

Пользователи могут напрямую взаимодействовать с рекламой, нажав кнопку [призыва к действию](story_ads_best_practices.md#call-to-action-button-text-enum) , отображаемую системой в нижней трети всех объявлений AMP Story. Нажатие на кнопку может отправить пользователя в одно из следующих мест, настроенных создателем рекламы:

- Веб-страница AMP
- Веб-страница без AMP
- Магазин приложений или магазин Google Play
- [Рекламная история](story_ads_best_practices.md#sponsored-story)

{{ image('/static/img/docs/stampads/sponsored_story.png', 1600, 597, layout='intrinsic', alt='Image showing that usersare redirected to an ad landing destination, but can return to the story.', caption='Users are redirected to an ad landing destination, but can return to the story.', align='' ) }}

## Настроить <br>AMP-истории не могут поддерживать [`amp-ad`](../../../documentation/components/reference/amp-ad.md) прямо на странице. Вместо этого все объявления выбираются и отображаются расширением [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) . Компонент [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) должен быть размещен как прямой дочерний элемент [`amp-story`](../../../documentation/components/reference/amp-story.md) .

[sourcecode:html]
<amp-story>
  <amp-story-auto-ads>
    <script type="application/json">
      {
        "ad-attributes": {
          // ad server configuration
        }
      }
    </script>
  </amp-story-auto-ads>
  <amp-story-page>
  ...
</amp-story>
[/sourcecode]

В отличие от обычного [`amp-ad`](../../../documentation/components/reference/amp-ad.md) , `<fallback>` или `<placeholder>` не требуются, так как объявления AMP Story будут отображаться только после полной визуализации.

## Интеграция поддержки сервера объявлений <br>Самый простой способ включить рекламу в историю AMP - это показать рекламу с поддерживаемого сервера объявлений.

Рекламные серверы, которые в настоящее время поддерживают объявления AMP Story:

- [Google Ad Manager (ранее DoubleClick)](advertise_amp_stories.md#google-ad-manager)

Если вы являетесь рекламным сервером, заинтересованным в показе сюжетных объявлений, свяжитесь с нами, заполнив вопрос на [GitHub](https://github.com/ampproject/amphtml/issues/new) . Команда AMP с радостью свяжется с вами!

Издатели также могут размещать персонализированные объявления, если у них есть собственный сервер объявлений. [Процесс подробно описан здесь](https://github.com/ampproject/amphtml/blob/master/extensions/amp-story/amp-story-ads.md#publisher-placed-ads) .

## Google Менеджер рекламы<a name="google-ad-manager"></a>

Информация о сервере объявлений указывается в компоненте [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) в начале истории AMP.

Вы должны указать объект конфигурации JSON в компоненте [`amp-story-auto-ads`](../../../documentation/components/reference/amp-story-auto-ads.md) который определяет, как должны выбираться и отображаться объявления. Следующие поля необходимы для показа и рекламы в Google Ad Manager:

- `"type"` должен быть указан как `"doubleclick"`
- `"data-slot"` должен быть связан с вашим рекламным блоком.

[sourcecode:html]
<amp-story>
  <amp-story-auto-ads>
    <script type="application/json">
      {
        "ad-attributes": {
          "type": "doubleclick",
          "data-slot": "/30497360/a4a/amp_story_dfp_example"
        }
      }
    </script>
  </amp-story-auto-ads>
  <amp-story-page>
  ...
</amp-story>
[/sourcecode]

Эти пары ключ-значение копируются в элемент [`amp-ad`](../../../documentation/components/reference/amp-ad.md) созданный для истории. Дополнительная информация, необходимая для элемента, может быть добавлена вместо `additional_data` , например, `targeting` .

[sourcecode:html]
<amp-story>
  <amp-story-auto-ads>
    <script type="application/json">
     {
       "ad-attributes": {
         "type": "doubleclick",
         "data-slot": "/30497360/a4a/amp_story_dfp_example",
         "additional_data": "additional_data_information"
       }
     }
    </script>
  </amp-story-auto-ads>
  <amp-story-page>
  ...
</amp-story>
[/sourcecode]

[tip type="note"] Read [Traffic custom creatives in AMP Stories](https://support.google.com/admanager/answer/9038178) for information about uploading ads to Google Ad Manager and checkout our guide on [Best practices for creating an AMP Story ad](story_ads_best_practices.md). [/tip]
