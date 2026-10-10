---
## Front matter
title: "Домашняя работа №3"
subtitle: "Отчет"
author: "Устинова Виктория Вадимовна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучение посредством Wireshark кадров Ethernet, анализ PDU протоколов транспортного и прикладного уровней стека TCP/IP.

# Задание

1. Изучение возможностей команды ipconfig для ОС типа Windows (ifconfig
для систем типа Linux).
2. Определение MAC-адреса устройства и его типа.
3. Установить на домашнем устройстве Wireshark.
4. С помощью Wireshark захватить и проанализировать пакеты ARP и ICMP
в части кадров канального уровня
5. С помощью Wireshark захватить и проанализировать пакеты HTTP, DNS в части
заголовков и информации протоколов TCP, UDP, QUIC.
6. С помощью Wireshark проанализировать handshake протокола TCP.


# Выполнение лабораторной работы

С помощью команды ipconfig для ОС типа Windows или ifconfig(рис. [-@fig:001]).

![Показан адаптер ethernet 2 с ipv4-адерсом 192.168.56.1 маской 255.255.255.0 и ipv6 адресом канала fe80::492e:29... . Адаптер open vpn connect dco -среда передачи недоступна](image/1.jpg){#fig:001 width=70%}

Ипользуйте разные опции команды ifconfig(рис. [-@fig:002]).

![Показаны беспроводная сети 3 4 5 и 2 с описанием qualcommm WCN685x wifi 6E Dual Band Simultaneous DHCP включен ](image/2.jpg){#fig:002 width=70%}

Пояснить детально информацию о текущем сетевом соединении, включая адреса, срок аренды, DHCP-сервер и DNS-серверы.(рис. [-@fig:003]).

![Показаны IPv6-адреса, IPv4-адрес 192.168.1.169, маска 255.255.255.0, основной шлюз 192.168.1.1, DHCP-сервер 192.168.1.1, DNS-серверы fd0a:e190:4b8a::1 и 192.168.1.1.](image/3.jpg){#fig:003 width=70%}

Использовать разные опции команды ipconfig и пояснить полученную информацию..(рис. [-@fig:004]).

![Команда ipconfig /displaydns выводит кэш DNS: записи word-edit.officeapps.live.com, app-geo.wac.trafficmanager.net и mrc-shed.wac.trafficmanager.net с типом записи 5 и CNAME-записями.](image/4.jpg){#fig:004 width=70%}

Определить MAC-адреса сетевых интерфейсов на компьютере.(рис. [-@fig:005]).

![Выведены подключения: Беспроводная сеть (Qualcomm WCN685, 38-D5-7A-E8-A1-D9), Ethernet 2 (VirtualBox Host, 0A-00-27-00-00-1E), OpenVPN Connect, Pritunl DCO 1, Pritunl 1, Pritunl DCO 2, Pritunl 2, Pritunl 3, Pritunl DCO 3.](image/5.jpg){#fig:005 width=70%}

Пропинговать шлюз по умолчанию командой ping 192.168.1.1 -n 4.(рис. [-@fig:006]).

![Все 4 пакета успешно доставлены, время 13–16 мс, TTL 64, потерь 0%.](image/6.jpg){#fig:006 width=70%}

В Wireshark остановить захват трафика, прописать фильтр arp or icmp и убедиться, что отображаются только пакеты ARP или ICMP.(рис. [-@fig:007]).

![В списке пакетов видны ARP-запросы (Who has 192.168.1.169? Tell 192.168.1.1) и ICMP Echo request/reply между 192.168.1.169 и 192.168.1.1.](image/7.jpg){#fig:007 width=70%}

Очистить ARP-кэш командой arp -d * и снова пропинговать шлюз командой ping 192.168.1.1 -n 4.(рис. [-@fig:008]).

![Все 4 пакета успешно доставлены, время 12–13 мс, TTL 64, потерь 0%.](image/8.jpg){#fig:008 width=70%}

Изучить эхо-запрос и эхо-ответ ICMP, а также кадры ARP. Изучить данные в полях заголовка Ethernet II.(рис. [-@fig:009]).

![Видны ARP-запросы, ICMP Echo request/reply между 192.168.1.169 и 192.168.1.1, а также ARP-ответы с MAC-адресом f8:f0:82:fb:0f:50.](image/9.jpg){#fig:009 width=70%}

 Начать новый процесс захвата трафика и пропинговать по имени известный адрес, например ping rudn.ru -n 4.(рис. [-@fig:010]).

![Выполнен ping rudn.ru (37.18.93.135), превышен интервал ожидания для запроса, 100% потерь.](image/10.jpg){#fig:010 width=70%}

Изучить запросы и ответы протоколов ARP и ICMP, определить MAC-адреса источника и получателя, определить тип MAC-адресов.(рис. [-@fig:011]).

![Видны ARP-запросы и ICMP Echo request к 37.18.93.135 без ответа, MAC-адреса f8:f0:82:fb:0f:50 и 38:d5:7a:e8:a1:d9.](image/11.jpg){#fig:011 width=70%}

Пропинговать по имени известный адрес, например ping ya.ru -n 4.(рис. [-@fig:012]).

![Выполнен ping ya.ru (77.88.55.242), все 4 пакета успешно доставлены, время 8–19 мс, TTL 56, потерь 0%.](image/12.jpg){#fig:012 width=70%}

Изучить запросы и ответы протоколов ARP и ICMP, определить MAC-адреса источника и получателя.(рис. [-@fig:013]).

![Видны ARP-запросы и ICMP Echo request/reply между 192.168.1.169 и 77.88.55.242, MAC-адреса f8:f0:82:fb:0f:50 и 38:d5:7a:e8:a1:d9.](image/13.jpg){#fig:013 width=70%}

 Изучить детали эхо-ответа ICMP в Wireshark, включая Ethernet II и IPv4. (рис. [-@fig:014]).

![Frame 631 — 74 байта, Ethernet II (Src Nagtech_fb:0f:50, DstCloudNetwork_e8:a1:d9), IPv4 (Src 77.88.55.242, Dst 192.168.1.169), ICMP](image/14.jpg){#fig:014 width=70%}

Изучить детали эхо-запроса ICMP в Wireshark, включая Ethernet II и IPv4.(рис. [-@fig:015]).

![Frame 630 — 74 байта, Ethernet II (Src CloudNetwork_e8:a1:d9, Dst Nagtech_fb:0f:50), IPv4 (Src 192.168.1.169, Dst 77.88.55.242), ICMP.](image/15.jpg){#fig:015 width=70%}

Изучить кадры данных протокола ARP, данные в полях заголовка Ethernet II.(рис. [-@fig:016]).

![Frame 427 — 42 байта, Ethernet II (Src Nagtech_fb:0f:50, Dst CloudNetwork_e8:a1:d9), ARP (reply).](image/16.jpg){#fig:016 width=70%}

 В Wireshark в строке фильтра указать http и проанализировать информацию по протоколу TCP в случае запросов и ответов.(рис. [-@fig:017]).

![ВВидны HTTP-запросы GET /, GET /favicon.ico, GET /hypertext/WWW/TheProject.html и ответы HTTP/1.1 200 OK, 400 Bad request между 192.168.1.169 и 188.184.67.127.](image/17.jpg){#fig:017 width=70%}

 В Wireshark в строке фильтра указать dns и проанализировать информацию по протоколу UDP в случае запросов и ответов.(рис. [-@fig:018]).

![Видны DNS-запросы и ответы между fd0a:e190:4b8a:0:e9 и fd0a:e190:4b8a::1: Standard query 0x4c9a A nav-edge.smartscreen.microsoft.com, Standard query 0x9a1 HTTPS info.cern.ch CNAME webafs902.cern.ch.](image/18.jpg){#fig:018 width=70%}

В Wireshark в строке фильтра указать quic и проанализировать информацию по протоколу QUIC в случае запросов и ответов.(рис. [-@fig:019]).

![Видны QUIC-пакеты Protected Payload (KP0) с DCID=041240ea0d808731 и Initial, DCID=a6390fd80ed99a8a, PKN 1 и 2, между 192.168.1.169 и 184.51.252.54, 23.196.236.27.](image/19.jpg){#fig:019 width=70%}

Проанализировать handshake протокола TCP, привести пример с пояснениями изменения значений соответствующих сообщений.(рис. [-@fig:020]).

![Видны TCP-пакеты SYN, SYN-ACK, ACK между 192.168.1.169 и 188.184.67.127, HTTP GET / HTTP/1.1, HTTP/1.1 200 OK, FIN, ACK.](image/20.jpg){#fig:020 width=70%}

В Wireshark в меню «Статистика» выбрать «График Потока» и привести пояснения по изменениям значений соответствующих сообщений при установлении соединения по TCP.(рис. [-@fig:021]).

![На графике потока отображены этапы TCP-соединения: SYN, SYN-ACK, ACK, GET / HTTP/1.1, HTTP/1.1 200 OK, FIN, ACK, GET /favicon.ico.](image/21.jpg){#fig:021 width=70%}

# Выводы

В ходе работы были изучены возможности команды ipconfig для ОС Windows и определены MAC-адреса сетевых интерфейсов. С помощью Wireshark захвачены и проанализированы пакеты ARP и ICMP в части кадров канального уровня, изучены поля заголовка Ethernet II. Проанализированы протоколы транспортного уровня TCP, UDP и QUIC при работе HTTP и DNS. Изучен трёхступенчатый handshake протокола TCP и построен график потока. Получены практические навыки анализа сетевого трафика.

# Ответы

1. Что такое MAC-адрес и какова его структура?

MAC-адрес — уникальный идентификатор сетевого интерфейса, 48 бит. Первые 24 бита — идентификатор производителя (OUI), последние 24 бита — идентификатор интерфейса.

2. Что такое трёхступенчатый handshake TCP?

Процесс установления TCP-соединения: клиент отправляет SYN, сервер отвечает SYN-ACK, клиент подтверждает ACK. После этого соединение считается установленным.

3. Какие протоколы транспортного уровня применяются в стеке TCP/IP?

TCP (ориентированный на соединение) и UDP (без установления соединения).

4. Что такое QUIC и для чего он применяется?

QUIC — протокол транспорта для HTTP, работающий поверх UDP, с мультиплексированием потоков и шифрованием, эквивалентным TLS/SSL.

5. Какие поля содержит заголовок Ethernet II?

MAC-адрес назначения, MAC-адрес источника, тип протокола.

6. Как определить MAC-адреса сетевых интерфейсов в Windows?

Командой getmac /v или ipconfig /all.

7. Для чего используется фильтр arp or icmp в Wireshark?

Для отображения только пакетов ARP и ICMP при анализе трафика.

8. Какие типы MAC-адресов бывают?

Индивидуальные и групповые; глобально администрируемые и локально администрируемые.

## Литературный список

1. Wireshark Documentation. — URL: https://www.wireshark.org/docs/

2. RFC 9000. QUIC: A UDP-Based Multiplexed and Secure Transport. — 2021.

3. Королькова А. В., Кулябов Д. С. Сетевые технологии. Лабораторный практикум.

4. tcpdump Documentation. — URL: http://www.tcpdump.org/
