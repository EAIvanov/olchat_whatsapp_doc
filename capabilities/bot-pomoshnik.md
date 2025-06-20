# Бот-помощник

Для расширения функциональных возможностей чата с клиентом, можно подключить и настроить бота-помощника OLChat. Бот обладает следующими функциями:

* Обновление изображения контакта в CRM при добавлении в чат
* Изменение заголовков чатов по шаблону
* Привязка аналитики в поле CRM
* Установка бота, которому передаётся управление после бота OLChat
* [upravlenie-sostavom-uchastnikov-grupp-s-pomoshyu-komand-v-chate.md](../gruppovye-chaty/upravlenie-sostavom-uchastnikov-grupp-s-pomoshyu-komand-v-chate.md "mention")

### Установка бота

Для включения и настройки бота-помощника в левом меню портала войдите в приложение **OLChat  — значок «•••» (меню вызова настроек коннектора) — Бот-помощник.** Нажмите на кнопку «Установить».

<figure><img src="../.gitbook/assets/image (1367).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Если отключено создание сущностей и контакта такого в CRM-системе ещё нет, то номер  в заголовке чата отображаться не будет даже при установленном боте-помощнике.
{% endhint %}

### Настройка бота

После установки, вы увидите сообщение: «Бот OLChat успешно установлен». Произведите дальнейшую настройку Бота OLChat:

1. Установите чекбокс «Обновлять изображение контакта в CRM при добавлении в чат» в активное положение, если хотите, чтобы при начале нового диалога с клиентом производилась установка и обновление изображения контакта клиента в CRM из его профиля WhatsApp.
2. Настройка «Шаблон названия чата» позволяет автоматически переименовывать чат открытой линии по заранее подготовленному шаблону. Изначально чат берёт имя из профиля WhatsApp, но может меняться с помощью нашего бота. \
   В названии можно использовать параметры. Чтобы выбрать параметр нажмите на значок **«•••»** и из выпадающего списка параметров CRM выберите нужные. Выбранный параметр подставится в строку с названием шаблона.
3. Настройка «Привязать параметр аналитики к полю CRM» позволяет передавать параметры аналитики Roistat, ClientID, UserID и т.д. в любое строковое пользовательское поле. Необходимо создать поле заранее и в выпадающем списке выбрать то поле лида, в которое необходимо записывать параметры аналитики. Данная настройка будет работать только в том случае, если выбрано автоматическое создание лидов или сделок в настройках линии.

{% hint style="info" %}
Выбор поля «Привязать параметр аналитики к полю CRM»  может быть недоступен, если выбрано ручное создание сущности из чата в разделе Очереди в настройках Открытой линии.
{% endhint %}

4. Если в чате отрытой линии вы используете других ботов, в настройке «Бот, которому передаётся управление после бота OLChat» в выпадающем списке выберите бота, который начнёт работу после бота OLChat.

{% hint style="warning" %}
В настройке «Шаблон названия чата» не рекомендуем использовать в качестве параметров такие поля из CRM, как: Телефон, E-mail, Мессенджер, Комментарий, поля привязки к сущности (будет отображаться ID сущности), Поля виджетов других приложений и множественные поля. При использовании данных полей отображение их в шаблоне может быть некорректным.
{% endhint %}

{% hint style="info" %}
Если вы выбираете поля для подстановки Имя и Фамилия - бот берет информацию из Лида.
{% endhint %}

Нажмите на кнопку «Сохранить» после устновки нужных настроек.

Также, для корректной работы чат-бота, рекомендуем перейти в открытую линию, которая подключена к данному коннектору и в разделе Чат-боты установить следующие оптимальные настройки, как показано на скриншоте ниже:

<figure><img src="../.gitbook/assets/image (544).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Если вы не хотели бы видеть уведомление в чате "OLChat покинул чат", то в поле "Когда отключать чат-бота" должно быть настроено "После завершения диалога".
{% endhint %}

Чтобы выключить бота OLChat необходимо перейти в настройки открытой линии, которая подключена к данному коннектору и в разделе Чат-боты снять галочку «При обращении клиента назначить ответственным чат-бота». Сохраните настройку. Бот OLChat будет отключен.

![](<../.gitbook/assets/image (278).png>)
