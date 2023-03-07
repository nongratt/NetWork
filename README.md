# NetWork

 - [Сетевые технологии](#Сетевые-технологии)
  - [Основы](#TCP-IP)
  - [Модель](#Уровневая-модель-TCP/IP)
     - [Канальный](#Канальный)
     - [Межсетевой](#Межсетевой)
     - [Транспортный](#Траспортный)
     - [Прикладной](#Прикладной)
  - [PORT](#Зачем-нужны-порты)
  - [DNS](#Зачем-нужен-DNS)
     - [Как работает DNS](#Как-работает-DNS)
  - [NAT](#NAT)
     - [Виды](#Виды-NAT)


## TCP IP

Стек протоколов TCP/IP (Transmission Control Protocol/Internet Protocol, протокол управления передачей/протокол интернета) — сетевая модель, описывающая процесс передачи цифровых данных. Она названа по двум главным протоколам, по этой модели построена глобальная сеть интернет.

## Уровневая модель TCP/IP
Модель TCP/IP разделена на уровни, документами, определяющими сертификации модели, являются RFC 1122 и RFC1123 (ниже примеры на рус документацию)
Эти стандарты описывают четыре уровня абстракции модели TCP/IP: прикладной, транспортный, межсетевой и канальный

https://rfc.com.ru/rfc1122.htm
https://rfc.com.ru/rfc1123.htm

![12](https://github.com/nongratt/NetWork/blob/main/images/B87412C8-7267-428F-A43D-825EA59CA0ED.png)

### Канальный
Канальный уровень (link layer)
Предназначение канального уровня — дать описание тому, как происходит обмен информацией на уровне сетевых устройств, определить, как информация будет передаваться от одного устройства к другому. Информация здесь кодируется, делится на пакеты и отправляется по нужному каналу, т.е. среде передачи.

Этот уровень также вычисляет максимальное расстояние, на которое пакеты возможно передать, частоту сигнала, задержку ответа и т.д. Все это — физические свойства среды передачи информации. На канальном уровне самым распространенным протоколом является Ethernet, который мы рассмотрим в конце статьи.

### Межсетевой

Межсетевой уровень (internet layer)
Глобальная сеть интернет состоит из множества локальных сетей, взаимодействующих между собой. Межсетевой уровень используется, чтобы описать обеспечение такого взаимодействия.

Межсетевое взаимодействие — это основной принцип построения интернета. Локальные сети по всему миру объединены в глобальную, а передачу данных между этими сетями осуществляют магистральные и пограничные маршрутизаторы.

Именно на межсетевом уровне функционирует протокол IP, позволивший объединить разные сети в глобальную. Как и протокол TCP, он дал название модели, рассматриваемой в статье.

### Транспортный
Постоянные резиденты транспортного уровня — протоколы TCP и UDP, они занимаются доставкой информации.

TCP (протокол управления передачей) — надежный, он обеспечивает передачу информации, проверяя дошла ли она, насколько полным является объем полученной информации и т.д. TCP дает возможность двум конечным устройствам производить обмен пакетами через предварительно установленное соединение. Он предоставляет услугу для приложений, повторно запрашивает потерянную информацию, устраняет дублирующие пакеты, регулируя загруженность сети. TCP гарантирует получение и сборку информации у адресата в правильном порядке.

UDP (протокол пользовательских датаграмм) — ненадежный, он занимается передачей автономных датаграмм. UDP не гарантирует, что всех датаграммы дойдут до получателя. Датаграммы уже содержат всю необходимую информацию, чтобы дойти до получателя, но они все равно могут быть потеряны или доставлены в порядке отличном от порядка при отправлении.

UDP обычно не используется, если требуется надежная передача информации. Использовать UDP имеет смысл там, где потеря части информации не будет критичной для приложения, например, в видеоиграх или потоковой передаче видео. UDP необходим, когда делать повторный запрос сложно или неоправданно по каким-то причинам.

Протоколы транспортного уровня не интерпретируют информацию, полученную с верхнего или нижних уровней, они служат только как канал передачи, но есть исключения. RSVP (Resource Reservation Protocol, протокол резервирования сетевых ресурсов) может использоваться, например, роутерами или сетевыми экранами в целях анализа трафика и принятия решений о его передаче или отклонении в зависимости от содержимого.


### Прикладной
В модели TCP/IP отсутствуют дополнительные промежуточные уровни (представления и сеансовый) в отличие от OSI. Функции форматирования и представления данных делегированы библиотекам и программным интерфейсам приложений (API) — своего рода базам знаний, содержащим сведения о том, как приложения взаимодействуют между собой. Когда службы или приложения обращаются к библиотеке или API, те в ответ предоставляют набор действий, необходимых для выполнения задачи и полную инструкцию, каким образом эти действия нужно выполнять.

Протоколы прикладного уровня действуют для большинства приложений, они предоставляют услуги пользователю или обмениваются данными с «коллегами» с нижних уровней по уже установленным соединениям. Здесь для большинства приложений созданы свои протоколы. Например, браузеры используют HTTP для передачи гипертекста по сети, почтовые клиенты — SMTP для передачи почты, FTP-клиенты — протокол FTP для передачи файлов, службы DHCP — протокол назначения IP-адресов DHCP и так далее.

## Зачем нужны порты?
Представьте, что у вас дома 2 компьютера и они подключены к одному роутеру. Для всего интернета IP адрес этих компьютеров одинаковый (так как внешний IP, который виден в интернете есть только у роутера). В этом случае, чтобы обратиться к конкретному компьютеру, нужен порт. Например, на роутере настроено, что у одного из компьютеров открыт порт 8245. Роутер имеет IP 95.84.208.79. Тогда обратиться к этому компьютеру можно так:

95.84.208.79:8245

IP адрес — это номер квартиры друга.
Порт — это комната, в которой живёт друг

## Зачем нужен DNS

Фундаментальная технология современной интернет-среды, которая отвечает за хранение и обработку информации о доменных адресах. Инструмент используется для преобразования доменных имен в IP-адреса в момент отправки пользователем запроса на сервер. IP-адрес — уникальный числовой идентификатор устройства. Он позволяет узнать, откуда загружается страница нужного сайта. Получается, технология DNS служит своеобразной «телефонной книгой», в которой хранится база доменных имен и их адресов.
### Как работает DNS
Пользователь вводит запрос в строке браузера. Тот в свою очередь перенаправляет его DNS-серверу, который ищет совпадения между доменным именем и IP. При обнаружении совпадений браузер делает запрос по IP-адресу сервера и получает в ответ нужную информацию, после чего браузер отображает ее. Если совпадения не обнаружены, тогда запрос перенаправляется корневому серверу.
Корневой сервер снова перенаправляет запрос серверу первого уровня, а тот отправляет запрос серверу второго уровня. Процесс продолжается до тех пор, пока совпадение не будет найдено.
Как только IP-адрес найден, браузер направляет запрос серверу, получает ответ и отображает полученную информацию.
## NAT

NAT — технология, которая преобразует приватные IP-адреса во внешние и наоборот. Благодаря этому VM получает доступ в интернет.

Частная сеть может подключаться к интернету через один публичный IP-адрес (или пул адресов), предоставленный провайдером.

Преобразования NAT также позволяют скрывать топологию внутренней сети от внешних пользователей, что затрудняет несанкционированный доступ к ресурсам сети.

### Виды NAT
Статическая адресная трансляция (Static NAT) - сопоставление адресов один к одному между локальными и глобальными адресами;
Динамическая адресная трансляция (Dynamic NAT) - сопоставление адресов “многие ко многим” между локальными и глобальными адресами;
Port Address Translation (PAT) - многоадресное сопоставление адресов между локальными и глобальными адресами c использованием портов. Также этот метод известен как NAT Overload
