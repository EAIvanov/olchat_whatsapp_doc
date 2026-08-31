---
hidden: true
---

# Copy of REST API для работы с WhatsApp

Мы добавили в Олчат REST API (программный интерфейс взаимодействия с сервером) для работы с WhatsApp. Теперь вы можете сформировать вебхук и использовать его для вызовов методов REST в своих сценариях автоматизации и при интеграции различных сервисов.

## Получение вебхука

Создать вебхук можно в приложении Олчат — «•••» (меню вызова настроек коннектора) — Настройки коннектора — Вебхук — Сгенерировать новый:

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

После создания его можно скопировать в буфер, нажав на кнопку «Скопировать вебхук». При необходимости вебхук можно изменить, нажав на кнопку «Сгенерировать новый»:

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

## Описание методов

Для простоты использования большая часть API (программных интерфейсов) допускает использование GET-запросов.

{% hint style="info" %}
Указанные ниже технические ограничения по запросам изменить или убрать невозможно.
{% endhint %}

{% hint style="info" %}
Для корректного срабатывания запросов в параметр «Номер телефона» необходимо вписывать значение через «7» в начале номера.
{% endhint %}

## Отправка сообщения

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/messages.text.send/`

Позволяет отправить текстовое сообщение на указанный номер телефона в WhatsApp.

Ограничение: 5 запросов в 3 секунды.

#### Параметры

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

<mark style="color:blue;">`GET`</mark>` ``https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/messages.file.send/`

Позволяет отправить файл на указанный номер телефона в WhatsApp. В качестве файла указывается прямая ссылка на файл. Подробнее в статье [#sozdanie-pryamoi-ssylki-na-fail](../roboty-i-aktiviti/sozdanie-pryamoi-ssylki-na-fail.md#sozdanie-pryamoi-ssylki-na-fail "mention").

Ограничение: 5 запросов в 3 секунды.

#### Параметры

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

## Проверка аккаунта на номере

<mark style="color:blue;">`GET`</mark>` ``https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/phone.check/`

Позволяет проверить наличие на номере аккаунта WhatsApp.

Ограничение: 3 запроса в 1 секунду.

ВАЖНО! Не злоупотребляйте этим методом, так как высока вероятность блокировки вашего аккаунта со стороны WhatsApp.

#### Path Parameters

| Name                                            | Type | Description    |
| ----------------------------------------------- | ---- | -------------- |
| phone\_number<mark style="color:red;">\*</mark> | str  | Номер телефона |

{% tabs %}
{% tab title="200: OK " %}

{% endtab %}
{% endtabs %}

## Проверка статуса линии

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/line.status.get/`

Позволяет проверить статус текущей линии.

Ограничение: 5 запросов в 3 секунды.

## Проверка статуса сообщения

<mark style="color:blue;">`GET`</mark> `https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/messages.status.get/`

Позволяет проверить статус сообщения.

Ограничение: 5 запросов в 3 секунды.

#### Path Parameters

| Name                                            | Type | Description    |
| ----------------------------------------------- | ---- | -------------- |
| phone\_number<mark style="color:red;">\*</mark> | str  | Номер телефона |
| message\_id<mark style="color:red;">\*</mark>   | str  | ID сообщения   |

{% tabs %}
{% tab title="200: OK " %}

{% endtab %}
{% endtabs %}

## Где можно использовать REST API

Предположим, что у вас есть сайт или интернет-магазин, который не интегрирован с Битрикс24, но нужно уведомить клиента, заполнившего форму WhatsApp, о том, что его заявка принята в работу или заказ оформлен.

Вы можете привязаться к событию заполнения формы и отправить запрос, содержащий метод отправки сообщения: `https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/messages.text.send/`.

* В качестве **phone\_number** передайте в запрос номер телефона из формы.
* В качестве **text** – ваш текст сообщения, например: «Мы получили вашу заявку, номер вашего заказа №00001».

Другие примеры использования REST API:

1. Уведомление о записи на приём из сторонней системы (например, запись на приём у стоматолога).
2. Отправка уведомления из 1С.
3. Сообщение с номера телефона для интегратора.

## Как добавить подпись к файлу, отправленному через REST API

Ниже приведен пример, написанный на Python с использованием библиотеки Requests:

```
import requests

webhook_url = "https://olchat.infocom.io/rest/webhook/wa/{{ваш token}}/v2/messages.file.send/"

payload = {
    "phone_number": "7985...",
    "text": "https://drive.google.com/uc?export=download&id=...",
    "publish_to_open_line": True,
    "caption": "Ваша корзина ждет! Завершите покупку и получите подарок"
}

response = requests.post(webhook_url, json=payload)
```

{% hint style="info" %}
Параметр publish\_to\_open\_line может принимать значения:

* true — публиковать в чат Открытой линии;
* false — не публиковать в чат Открытой линии.
{% endhint %}

При выполнении этого скрипта в чате Открытой линии будет отображено следующее сообщение:

<figure><img src="../.gitbook/assets/image (2107).png" alt=""><figcaption></figcaption></figure>

На стороне клиента это же сообщение будет выглядеть следующим образом:

<figure><img src="../.gitbook/assets/image (2106).png" alt=""><figcaption></figcaption></figure>

## Получение последних сообщений

**Метод**: messages.history.list

<mark style="color:blue;">`GET`</mark> <mark style="color:blue;">`https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/messages.history.list/`</mark>

Возвращает список недавних входящих и/или исходящих сообщений по линии.&#x20;

| Name            | Type    | Description                                                 |
| --------------- | ------- | ----------------------------------------------------------- |
| direction       | string  | Обязательный. `incoming`, `outgoing` или `all`              |
| period\_minutes | integer | Период в минутах (от 1 до 10080). По умолчанию 1440 (сутки) |

#### Особенности

* Возвращается только текстовое содержимое (медиафайлы не включаются).
* Максимальная глубина истории — 7 суток (10080 минут). Это ограничение платформы, увеличить его нельзя.
* Метод предназначен для получения свежих сообщений и определения времени последнего контакта. Для полной выгрузки истории чата используйте метод chats.history.list.

## Получение истории конкретного чата

**Метод**: chats.history.list

<mark style="color:blue;">`GET`</mark> <mark style="color:blue;">`https://olchat.infocom.io/rest/webhook/wa/{{token}}/v2/chats.history.list/`</mark>

Возвращает историю сообщений указанного чата.

| Name          | Type    | Description                                                                  |
| ------------- | ------- | ---------------------------------------------------------------------------- |
| phone\_number | string  | Номер телефона. Нужен ровно один из параметров: `phone_number` или `chat_id` |
| chat\_id      | string  | Идентификатор чата WhatsApp (`@c.us` или `@g.us`)                            |
| limit         | integer | Максимальное количество сообщений. По умолчанию 100                          |

#### **Особенности**

* По умолчанию возвращается 100 сообщений.
* Необходимо указать ровно один из параметров: `phone_number` или `chat_id`. При указании обоих приоритет имеет `phone_number`.
