---
icon: star
---

# OLChat Link Modifier — автоматическая подстановка ID посетителя в ссылки мессенджеров

Скрипт OLChat Link Modifier добавляет идентификатор посетителя в ссылки WhatsApp и Telegram на вашем сайте. Это помогает автоматически отслеживать источник обращений.

## Для чего это нужно?

Когда посетитель нажимает на кнопку связи через WhatsApp или Telegram на вашем сайте, скрипт добавляет уникальный идентификатор в начальное сообщение. Это позволяет:

* Понять, откуда пришел клиент
* Связать обращение с конкретным посетителем сайта
* Отследить эффективность разных каналов привлечения

## Быстрая установка

1. Скопируйте следующий код
2. Вставьте его на ваш сайт перед закрывающим тегом `</body>`
3. Настройте
4. Готово!

```html
<script>
window.olchatLinkModifier = {
  config: {
    messageTemplate: "Здравствуйте! Мой код запроса: {visit_id}",
    idSource: "ym",
    modifyWhatsApp: true,
    modifyTelegram: true,
    modifyB24Widget: true
  },
  visitorId: null,
  updateConfig: function(newConfig) {
    Object.assign(this.config, newConfig);
  }
};
!function(){const c=window.olchatLinkModifier.config;function w(i,m){if(c.modifyWhatsApp!==true)return;const s=encodeURIComponent(m.replace(/{visit_id}/g,i)),l=document.querySelectorAll('[href*="//wa.me"],[href*="//api.whatsapp.com/send"],[href*="//web.whatsapp.com/send"],[href^="whatsapp://send"]');for(let j in l)if(l.hasOwnProperty(j)){try{const a=l[j],u=new URL(a.href);a.href=u.origin==="https://wa.me"?`${u.protocol}//${u.host}${u.pathname}?text=${s}`:u.protocol==="whatsapp:"?`${u.protocol}${u.host}${u.pathname}?phone=${u.searchParams.get('phone')}&text=${s}`:`${u.protocol}//${u.host}${u.pathname}?phone=${u.searchParams.get('phone')}&text=${s}`}catch(e){}}}function t(i){if(c.modifyTelegram!==true)return;const l=document.querySelectorAll('[href*="//t.me"],[href^="tg://resolve"]');for(let j in l)if(l.hasOwnProperty(j)){try{const a=l[j],u=new URL(a.href);a.href=u.origin==="https://t.me"?`${u.protocol}//${u.host}${u.pathname}?start=${i}`:u.protocol==="tg:"?`${u.protocol}${u.host}${u.pathname}?domain=${u.searchParams.get('domain')}&start=${i}`:a.href}catch(e){}}}function b(i){if(c.modifyB24Widget!==true)return;const b24w=setInterval(()=>{const l=document.querySelector('[data-b24-crm-button-widget=openline_olchat_wa_connector_2]');if(l!==null){clearInterval(b24w);l.href=l.href.replace(/\{visit_id\}/,i)}},250)}function g(){try{switch(c.idSource){case"calltouch_site_id":if(typeof window.ct==="function")return window.ct("calltracking_params")[0].siteId;break;case"calltouch_session_id":if(typeof window.ct==="function")return window.ct("calltracking_params","mod_id")[0].sessionId;break;case"roistat":const r=document.cookie.match(/roistat_visit=([^;]+)/);if(r)return r[1];break;case"ym":const y=document.cookie.match(/_ym_uid=([^;]+)/);if(y)return y[1];break;case"ga":const g=document.cookie.match(/_ga=GA\d\.\d\.(\d+\.\d+)/);if(g)return g[1];break}}catch(e){}return null}const d=setInterval(()=>{if(document.readyState==="complete"){clearInterval(d);window.olchatLinkModifier.visitorId=g();if(window.olchatLinkModifier.visitorId){w(window.olchatLinkModifier.visitorId,c.messageTemplate);t(window.olchatLinkModifier.visitorId);b(window.olchatLinkModifier.visitorId)}}},250)}();
</script>
```

## Настройка

### Основные настройки

* **Шаблон сообщения**: Измените текст, который автоматически подставляется в WhatsApp
* **Источник ID**: Выберите, откуда брать идентификатор (Calltouch, Roistat, Яндекс.Метрика или Google Analytics)
* **Выбор мессенджеров**: Включите или отключите подстановку ID для разных типов ссылок и для виджета Битрикс24

### Измените текст сообщения

Измените параметр `messageTemplate` в конфигурации:

```
messageTemplate: "Добрый день! Интересует ваш товар. Мой код: {visit_id}"
```

{% hint style="info" %}
Текст сообщения должен совпадать с текстом указанным в настройках приложения OLChat
{% endhint %}

### Укажите источник  кода  аналитики

```
idSource: "источник кода аналитики",
```

| Система аналитики    | idSource               |
| -------------------- | ---------------------- |
| Яндекс.Метрика       | `ym`                   |
| Roistat              | `roistat`              |
| Calltouch Session ID | `calltouch_session_id` |
| Calltouch Site ID    | `calltouch_site_id`    |
| Google Analytics     | `ga`                   |

## Параметры подстановки текста в ссылки

### Параметр modifyWhatsApp

Отвечает за модификацию всех видов ссылок WhatsApp на сайте:

* Ссылки вида `https://wa.me/+79001234567`
* Ссылки вида `https://api.whatsapp.com/send?phone=79001234567`
* Ссылки вида `whatsapp://send?phone=79001234567`

При установке `modifyWhatsApp: true` скрипт добавляет идентификатор посетителя в параметр `text` этих ссылок.

### Параметр modifyTelegram

Отвечает за модификацию всех ссылок Telegram на сайте:

* Ссылки вида `https://t.me/username`
* Ссылки вида `tg://resolve?domain=username`

При установке `modifyTelegram: true` скрипт добавляет идентификатор посетителя в параметр `start` этих ссылок.

### Параметр modifyB24Widget

Отвечает за модификацию ссылок WhatsApp в виджете Битрикс24. Если на сайте используется стандартный виджет Битрикс24, то при установке `modifyB24Widget: true` скрипт найдёт кнопку WhatsApp и добавит в неё идентификатор посетителя.

## Проверка работы

### Визуальная проверка

После установки скрипта:

1. Откройте ваш сайт
2. Нажмите на кнопку WhatsApp или Telegram
3. В открывшемся диалоге проверьте текст сообщения — в нем должен быть ваш уникальный идентификатор

### Проверка через консоль браузера

Вы можете проверить работу скрипта через консоль браузера:

1. Откройте ваш сайт
2. Нажмите F12 (или Cmd+Option+I на Mac) для открытия инструментов разработчика
3. Перейдите во вкладку "Console" (Консоль)
4. Выполните следующие команды для проверки:

```javascript
javascriptCopy// Проверка получения ID посетителя
console.log("ID посетителя:", window.olchatLinkModifier.visitorId);

// Проверка всех настроек скрипта
console.log("Конфигурация:", window.olchatLinkModifier.config);

// Проверка ссылок WhatsApp (если есть на странице)
document.querySelectorAll('[href*="wa.me"], [href*="whatsapp.com"]').forEach(link => {
  console.log("WhatsApp ссылка:", link.href);
});

// Проверка ссылок Telegram (если есть на странице)
document.querySelectorAll('[href*="t.me"]').forEach(link => {
  console.log("Telegram ссылка:", link.href);
});
```

Если скрипт работает корректно, вы увидите ID посетителя и ссылки мессенджеров с добавленными параметрами.
