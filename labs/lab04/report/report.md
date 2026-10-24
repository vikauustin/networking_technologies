---
## Front matter
title: "Лабораторная работа №4"
subtitle: "дресация IPv4 и IPv6.Двойной стек"
author: "Устинова Виктория Вадимовна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl
notice: |
  @*

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

Изучение принципов распределения и настройки адресного пространства на устройствах сети.

# Задание

Настроить двойной стек адресации IPv4 и IPv6 в локальной сети. В соответствии с таблицей адресации настроить интерфейсы оконечных устройств (PC1, PC2, Server) и маршрутизатора FRR. Проверить связь между устройствами с помощью команд ping и trace. Посмотреть захваченный трафик ARP, ICMP, ICMPv6 на соединении сервера с коммутатором и пояснить извлеченную информацию.

# Теоретические сведения

Технология двойного стека (Dual Stack) позволяет сетевому интерфейсу одновременно иметь как IPv4-, так и IPv6-адрес. Это обеспечивает связь устройства с узлами обеих версий протокола без потери совместимости.

В IPv6 адрес локальной связи (Link-Local, префикс FE80::/10) генерируется автоматически и используется для служебного обмена внутри сегмента. Глобальные адреса узлам часто назначаются автоматически с помощью сообщений Router Advertisement от маршрутизатора.

# Выполнение лабораторной работы

Построить топологию сети с двумя локальными подсетями, маршрутизаторами frr and vyos, коммутаторами, оконечными устройствами и сервером(рис. [-@fig:001]).

![В рабочей области GNS3 размещены устройства PC1-PC4, server,коммутаторы msk-vvustinova-sw-01..05, маршрутизаторы msk-vvustinova-gw-01 (frr), msk-vvustinova-gw-02 vyos](image/1.jpg){#fig:001 width=70%}

Соединить устройства в соответствии с топологией и включить захват трафика на соединении сервера с коммутатором.(рис. [-@fig:002]).

![Показаны порты соединений (e0, e1, eth0, eth1, eth2). К серверу подключен коммутатор sw-05 через порт e7.](image/2.jpg){#fig:002 width=70%}

Задать IP-адресацию для PC1 и просмотреть конфигурацию IPv4 и IPv6.(рис. [-@fig:003]).

![Выполнена команда show ip: IP/MASK 172.16.20.10/25, GATEWAY 172.16.20.1. В show ipv6 показан LINK-LOCAL SCOPE fe80::250:79ff:fe66:6800/64.](image/3.jpg){#fig:003 width=70%}

Задать IPv4-адресацию для PC2 и просмотреть конфигурацию.(рис. [-@fig:004]).

![Выполнена команда ip 172.16.20.138/25 172.16.20.129, настройки сохранены. show ip показывает IP/MASK 172.16.20.138/25, GATEWAY 172.16.20.129.](image/4.jpg){#fig:004 width=70%}

Задать IPv4-адресацию для сервера.(рис. [-@fig:005]).

![ Выполнена команда ip 64.100.1.10/24 64.100.1.1, адрес успешно назначен.](image/5.jpg){#fig:005 width=70%}

Настроить IPv4-адресацию на интерфейсах локальной сети маршрутизатора FRR msk-vvustinova-gw-01 согласно таблице.(рис. [-@fig:006]).

![Задан hostname, интерфейсам eth0, eth1, eth2 назначены адреса 172.16.20.1/25, 172.16.20.129/25 и 64.100.1.1/24 соответственно, выполнены команды no shutdown и write memory.](image/6.jpg){#fig:006 width=70%}

Проверить конфигурацию маршрутизатора и настройки IPv4-адресации.(рис. [-@fig:007]).

![show running-config отображает конфигурацию интерфейсов. show interface brief показывает, что eth0, eth1 и eth2 находятся в состоянии up с назначенными адресами.](image/7.jpg){#fig:007 width=70%}

Проверить подключение с помощью команд ping и trace. Узлы PC1 и PC2 должны отправлять эхо-запросы друг другу и на сервер.(рис. [-@fig:008]).

![Ping до 64.100.1.10 завершается тайм-аутом. Trace до 172.16.20.138 доходит до узла. Trace до 64.100.1.10 прерывается на 172.16.20.1 с ошибкой Destination host unreachable.](image/8.jpg){#fig:008 width=70%}

Проверить связь между PC2, PC1 и сервером.(рис. [-@fig:009]).

![Ping до 172.16.20.10 успешно проходит (5 пакетов). Ping до 64.100.1.10 завершается тайм-аутом.](image/9.jpg){#fig:009 width=70%}

Посмотреть захваченный на соединении сервера двойного стека с коммутатором трафик ARP, ICMP, ICMPv6 и пояснить извлеченную информацию.(рис. [-@fig:010]).

![В Wireshark видны широковещательные ARP-запросы от узла с MAC 0c:4d:27:58:00:02: Who has 64.100.1.10? Tell 64.100.1.1.](image/10.jpg){#fig:010 width=70%}


# Выводы

В ходе работы были приобретены практические навыки по установке и базовому конфигурированию HTTP-сервера Apache. Освоены запуск веб-сервера, анализ логов error_log и access_log, настройка межсетевого экрана и SELinux. Настроен виртуальный хостинг по двум DNS-адресам server.user.net и www.user.net, проверена его работа через браузер клиента. Создан скрипт автоматической установки и настройки HTTP-сервера для Vagrant.

# Список литературы
 
1. Кулябов Д. С. Адресация IPv4 и IPv6. Двойной стек: лабораторная работа 4. Методические указания к курсу «Сетевые технологии». 2026.

2. Олифер В. Г., Олифер Н. А. Компьютерные сети. Принципы, технологии, протоколы: Юбилейное издание. СПб.: Питер, 2020. 1008 с.

3. Таненбаум Э., Уэзеролл Д. Компьютерные сети. 5-е изд. СПб.: Питер, 2012. 960 с.
RFC 1918. Address Allocation for Private Internets [Электронный ресурс]. URL: https://www.rfc-editor.org/rfc/rfc1918 (дата обращения: 24.10.2026).

4. RFC 4291. IP Version 6 Addressing Architecture [Электронный ресурс]. URL: https://www.rfc-editor.org/rfc/rfc4291 (дата обращения: 24.10.2026).

5. RFC 4861. Neighbor Discovery for IP version 6 (IPv6) [Электронный ресурс]. URL: https://www.rfc-editor.org/rfc/rfc4861 (дата обращения: 24.10.2026).

6. RFC 4862. IPv6 Stateless Address Autoconfiguration [Электронный ресурс]. URL: https://www.rfc-editor.org/rfc/rfc4862 (дата обращения: 24.10.2026)
