# REST API для работы с WhatsApp

Мы добавили в OLChat REST API для работы с WhatsApp! Теперь вы можете сформировать вебхук и использовать его для вызовов методов REST в своих сценариях автоматизации и при интеграции различных сервисов.

### Получение вебхука

Создать вебхук можно зайдя в приложение **OLChat — «•••» (меню вызова настроек коннектора)** **— Настройки коннектора — Вебхук — Сгенерировать новый:**

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

После создания, вебхук можно скопировать в буфер, нажав на кнопку «Скопировать вебхук». При необходимости вебхук можно изменить, нажав на кнопку «Сгенерировать новый»:

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

### Описание методов

Для простоты использования, большая часть API допускает использование GET-запросов.&#x20;

{% hint style="info" %}
Указанные ниже технические ограничения по запросам изменить или убрать невозможно.&#x20;
{% endhint %}

{% hint style="info" %}
Для корректного срабатывания запросов в параметр "Номер телефона" необходимо вписывать значение через " 7 " в начале номера.
{% endhint %}

## Отправка сообщения

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/sendText`

Позволяет отправить текстовое сообщение на указанный номер телефона в WhatsApp.

Ограничение: 5 запросов в 3 секунды

#### Path Parameters

| Name                                             | Type | Description                                                  |
| ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| phone\_number<mark style="color:red;">\*</mark>  | str  | Номер телефона                                               |
| body<mark style="color:red;">\*</mark>           | text | Тело сообщения                                               |
| send\_to\_imol<mark style="color:red;">\*</mark> | Y\|N | Отправка в чат Открытой Линии. Может принимать значение Y\|N |

{% tabs %}
{% tab title="200: OK " %}

{% endtab %}
{% endtabs %}

## Отправка файла

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/sendFile`

Позволяет отправить файл на указанный номер телефона в WhatsApp. В качестве файла указывается прямая ссылка на файл. Подробнее в статье [#sozdanie-pryamoi-ssylki-na-fail](../roboty-i-aktiviti/sozdanie-pryamoi-ssylki-na-fail.md#sozdanie-pryamoi-ssylki-na-fail "mention").

Ограничение: 5 запросов в 3 секунды

#### Path Parameters

| Name                                             | Type | Description                                                  |
| ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| phone\_number<mark style="color:red;">\*</mark>  | str  | Номер телефона                                               |
| body<mark style="color:red;">\*</mark>           | url  | Прямая ссылка на файл                                        |
| send\_to\_imol<mark style="color:red;">\*</mark> | Y\|N | Отправка в чат Открытой Линии. Может принимать значение Y\|N |
| caption                                          | str  | Текст подписи под картинкой                                  |

{% tabs %}
{% tab title="200: OK " %}

{% endtab %}
{% endtabs %}

## Проверка WA на номере

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/checkPhone`

Позволяет проверить наличие на номере аккаунта WhatsApp.

Ограничение: 3 запроса в 1 секунду

**ВАЖНО! Не злоупотребляйте этим методом, т.к. высока вероятность блокировки вашего аккаунта со стороны WhatsApp**

#### Path Parameters

| Name                                            | Type | Description    |
| ----------------------------------------------- | ---- | -------------- |
| phone\_number<mark style="color:red;">\*</mark> | str  | Номер телефона |

{% tabs %}
{% tab title="200: OK " %}

{% endtab %}
{% endtabs %}

## Проверка статуса линии

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/checkStatus`

Позволяет проверить статус текущей линии.

Ограничение: 5 запросов в 3 секунды

## Проверка статуса сообщения

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/checkMessageStatus`

Ограничение: 5 запросов в 3 секунды

#### Path Parameters

| Name                                            | Type | Description    |
| ----------------------------------------------- | ---- | -------------- |
| phone\_number<mark style="color:red;">\*</mark> | str  | Номер телефона |
| message\_id<mark style="color:red;">\*</mark>   | str  | ID сообщения   |

{% tabs %}
{% tab title="200: OK " %}

{% endtab %}
{% endtabs %}

### Где можно использовать REST API

Предположим, что у вас есть сайт или интернет-магазин который не интегрирован с Битрикс24, но, присутствует необходимость уведомить клиента заполнившего форму на WhatsApp о том, что его заявка принята в работу или заказ оформлен.

Вы можете привязаться к событию заполнения формы и отправить запрос, содержащий метод отправки сообщения: **https://olchat.infocom.io/rest/webhook/wa/\{{token\}}/sendText**

* В качестве **phone\_number** передайте в запрос номер телефона из формы
* В качестве **body** – ваш текст сообщения, например: «Мы получили вашу заявку, номер вашего заказа №00001»
* В **send\_to\_imol** передайте Y или N



Другие примеры использования REST API:

1. Уведомление о записи на приём из сторонней системы (например, запись на приём у стоматолога);
2. Отправка уведомления из 1С;
3. Сообщение с номера телефона для интегратора.
