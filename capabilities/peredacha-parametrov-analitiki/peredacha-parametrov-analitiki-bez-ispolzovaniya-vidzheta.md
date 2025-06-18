# Передача параметров аналитики без использования виджета

{% hint style="info" %}
Для того, чтобы параметры аналитики были верно отработаны, вам необходимо в [Настройках коннектора](https://docs.olchat.io/ustanovka-i-nastroika/interfeisy-prilozheniya/opisanie-nastroek-konnektora) приложения OLChat настроить [Бот-помощник](https://docs.olchat.io/bot-pomoshnik), а также [Виджет на сайт](https://docs.olchat.io/vidzhet-dlya-saita).
{% endhint %}

### Настройка кнопки WhatsApp

Кроме стандартного виджета от Битрикс24, вы можете установить на сайт свою кнопку WhatsApp, зашить в неё приветственное сообщение и параметр для передачи идентификатора любого сервиса аналитики.&#x20;

Внешний вид кнопки может быть, например, таким:

<figure><img src="../../.gitbook/assets/image (1267).png" alt=""><figcaption></figcaption></figure>

В приветственном сообщении укажите параметр **{visit\_id}**, например, в таком виде: _Обязательно отправьте это сообщение и дождитесь ответа! Ваш номер:_ **{visit\_id}**

Код кнопки WhatsApp из приведённого выше примера может выглядеть следующим образом:

```markup
<a class="whatsapp_overplan" href="https://api.whatsapp.com/send?phone=79000000000&text=Обязательно отправьте это сообщение и дождитесь ответа! Ваш номер:{visit_id}" rel="noopener noreferrer">
  <div class="whatsapp-button"><i class="fa fa-whatsapp"></i></div>
</a>
```

```css
.whatsapp-button {
    position: fixed;
    right: 13px;
    bottom: 90px;
    transform: translate(-50%, -50%);
    background: #25D366; /*цвет кнопки*/
    border-radius: 50%;
    width: 55px; /*ширина кнопки*/
    height: 55px; /*высота кнопки*/
    color: #fff;
    text-align: center;
    line-height: 53px; /*центровка иконки в кнопке*/
    font-size: 35px; /*размер иконки*/
    z-index: 9999;
}
.whatsapp-button a {
    color: #fff;
}
.whatsapp-button:before,
.whatsapp-button:after {
    content: " ";
    display: block;
    position: absolute;
    border: 50%;
    border: 1px solid #25D366; /*цвет анимированных волн от кнопки*/
    left: -20px;
    right: -20px;
    top: -20px;
    bottom: -20px;
    border-radius: 50%;
    animation: animate 1.5s linear infinite;
    opacity: 0;
    backface-visibility: hidden; 
}
 
.whatsapp-button:after{
    animation-delay: .5s;
}
 
@keyframes animate
{
    0%
    {
        transform: scale(0.5);
        opacity: 0;
    }
    50%
    {
        opacity: 1;
    }
    100%
    {
        transform: scale(1.2);
        opacity: 0;
    }
}
```

### Настройка сайта

{% hint style="info" %}
В описанном ниже примере приведён модифицированный код для подстановки в параметр **{visit\_id}** значения идентификатора сервиса аналитики Calltouch.
{% endhint %}

Модифицируйте код на сайте следующим образом:

```javascript
<script>

	const wabutton = setInterval(() => {
        const l = document.querySelector('.whatsapp_overplan');
        if (l !== null) {
            const sessionId = window.ct('calltracking_params', 'mod_id')[0].sessionId;
            if (sessionId) {
                clearInterval(wabutton);
                l.href = l.href.replace(/\{visit_id\}/, sessionId);
            }
        }
    }, 250);

/* КОД КНОПКИ WHATSAPP */

/* КОД АНАЛИТИКИ CALLTOUCH */

</script>
```

После перехода по кнопке скрипт отработает и подставит в параметр {visit\_id} код сервиса аналитики:

<figure><img src="../../.gitbook/assets/image (1271).png" alt=""><figcaption></figcaption></figure>
