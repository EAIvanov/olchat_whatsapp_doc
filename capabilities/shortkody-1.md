---
hidden: true
---

# Copy of Шорткоды

Шорткоды – это конструкции, которые позволяют гибко использовать различные типы сообщений. С их помощью можно выполнять какое-либо действие непосредственно в текстовом сообщении. Они могут быть использованы в роботах, бизнес-процессах, в карточке CRM, в чатах и группах для отправки приложением OLChat файлов, голосовых сообщений, ссылок, визиток и месторасположения (геометки).

{% hint style="danger" %}
Функционал превью для ссылки временно не работает. Наша команда уже работает над этой возможностью.
{% endhint %}

Ниже представлен список поддерживаемых шорткодов:

| Описание                                   |                                                                                      Шорткод                                                                                     |                                                                                                            Условные обозначения                                                                                                            |
| ------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Файл с диска                               |                                                                 \[=disk:<mark style="color:red;">file\_id</mark>]                                                                |                                                              <mark style="color:red;">file\_id</mark> – ID файла на Битрикс.Диск. Желательно использовать файлы из Общей папки                                                             |
| Файл по ссылке                             |                                                                   \[=file:<mark style="color:red;">url</mark>]                                                                   |                                                                                         <mark style="color:red;">url</mark> – прямая ссылка на файл                                                                                        |
| Файл из поля crm                           |                   \[=crm\_file:<mark style="color:red;">crm\_type</mark>\|<mark style="color:green;">crm\_id</mark>\|<mark style="color:purple;">field</mark>]                   |                     <p><mark style="color:red;">crm_type</mark> – тип сущности</p><p><mark style="color:green;">crm_id</mark> – ID сущности</p><p><mark style="color:purple;">field</mark> – ID поля в сущности**  </p>                    |
| Файл из прикрепленного файла поля crm      |                                                              \[=crm\_file:<mark style="color:red;">file\_id</mark>]                                                              |                                                                                 <mark style="color:red;">file\_id</mark> – ID прикрепленного файла поля CRM                                                                                |
| Голосовое по ссылке                        |                                                                   \[=voice:<mark style="color:red;">url</mark>]                                                                  |                                                                                         <mark style="color:red;">url</mark> – прямая ссылка на файл                                                                                        |
| Голосовое из поля crm                      |                   \[=crm\_voice:<mark style="color:red;">crm\_type</mark>\|<mark style="color:green;">crm\_id</mark>\|<mark style="color:purple;">field</mark>]                  |                      <p><mark style="color:red;">crm_type</mark> – тип сущности</p><p><mark style="color:green;">crm_id</mark> – ID сущности</p><p><mark style="color:purple;">field</mark> – ID поля в сущности**</p>                     |
| Голосовое из прикреплённого файла поля crm |                                                              \[=crm\_voice:<mark style="color:red;">file\_id</mark>]                                                             |                                                                                 <mark style="color:red;">file\_id</mark> – ID прикрепленного файла поля CRM                                                                                |
| Визитка                                    |                                                                  \[=vcard:<mark style="color:red;">phone</mark>]                                                                 |                                                                                       <mark style="color:red;">phone</mark> – номер телефона визитки                                                                                       |
| Ссылка с автосбором информации             |                                                                   \[=link:<mark style="color:red;">url</mark>]                                                                   |                                                                                          <mark style="color:red;">url</mark> – ссылка для отправки                                                                                         |
| Месторасположение                          | \[=location:<mark style="color:red;">lat</mark>\|<mark style="color:green;">lng</mark>\|<mark style="color:purple;">address</mark>\|<mark style="color:blue;">address\_2</mark>] | <p><mark style="color:red;">lat</mark> – Широта</p><p><mark style="color:green;">lng</mark> – Долгота</p><p><mark style="color:purple;">address</mark> – Адрес</p><p><mark style="color:blue;">address_2</mark> – вторая строка адреса</p> |
| Ссылка на youtube видео                    |                                                                \[=youtube:<mark style="color:red;">v\_code</mark>]                                                               |                                                                                             <mark style="color:red;">v\_code</mark> – код видео                                                                                            |

\*\* - ID поля в сущности <mark style="color:purple;">field</mark> подставляется в следующем виде: UF\_CRM\_000000. О том, как узнать ID поля в сущности, написано [здесь](https://docs.olchat.io/roboty-i-aktiviti/sozdanie-pryamoi-ssylki-na-fail#ukazanie-id-polya-v-kotorom-nakhoditsya-otpravlyaemyi-fail).

{% hint style="warning" %}
Значения, выделенные в таблице <mark style="color:red;">таким</mark>, <mark style="color:green;">таким</mark> и <mark style="color:purple;">таким</mark> цветами **обязательны** к заполнению для корректной работы шорткода.

Значения, выделенные в таблице <mark style="color:blue;">данным</mark> цветом, **не обязательны** к заполнению. Их отсутствие не повлияет на корректную работу шорткода.
{% endhint %}

Подробнее про настройку отправки файла в зависимости от источника [читайте здесь.](https://docs.olchat.io/roboty-i-aktiviti/sozdanie-pryamoi-ssylki-na-fail)

Варианты использования шорткодов:

* Быстрые ответы в чате
* В шаблонах сообщений в приложении
* В роботах и бизнес-процессах
* В карточке сущности в виджете

{% hint style="info" %}
Шорткоды дают возможность в одном сообщении указывать последовательность отправки, но это не означает, что всё будет отправлено в одном шаблоне.
{% endhint %}

#### Пример использования шорткодов

Предположим, что нам необходимо отправить карту с местоположением, заданным координатами широты и долготы. Для этого воспользуемся шорткодом Месторасположение: **\[=location:\<lat>|\<lng>|\<address>|<\<address\_2>>]**

Подготовим конструкцию для отправки:

1. Вместо **\<lat>** подставим значение: **50.260704.** Это координата широты.&#x20;
2. Вместо **\<lng>** подставим значение: **127.537495.** Это координата долготы.
3. Вместо **\<address>** напишем адрес места. В нашем случае это: **Зейская улица, 173.**
4. Параметр **<\<address\_2>>** является необязательным, его можно оставить незаполненным либо дописать дополнительный текст адреса: **Благовещенск, Амурская область.**

Соберём подготовленные данные в единое целое:

> **\[=location:50.260704|127.537495|Зейская улица, 173|Благовещенск, Амурская область]**

Полученный шорткод отправим клиенту, используя виджет в карточке сделки

<figure><img src="../.gitbook/assets/image (561).png" alt=""><figcaption></figcaption></figure>

В результате, в WhatsApp придёт сообщение такого вида:

<figure><img src="../.gitbook/assets/image (784).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
Используя роботы и активити бизнес-процессов, данную конструкцию шорткода можно собирать и отправлять в автоматическом режиме, указывая в значениях переменные и поля, откуда робот или активити должны взять информацию.
{% endhint %}
