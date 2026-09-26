---
## Front matter
title: "Лаборатораня работа №2"
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

Построение простейших моделей сети на базе коммутатора и маршрутизаторов FRR и VyOS в GNS3, анализ трафика посредством Wireshark.

# Задание

1. Построить в GNS3 топологию сети, состоящей из коммутатора Ethernet и двух
оконечных устройств (персональных компьютеров).
2. Задать оконечным устройствам IP-адреса в сети 192.168.1.0/24. Проверить
связь.
1. С помощью Wireshark захватить и проанализировать ARP-сообщения.
2. С помощью Wireshark захватить и проанализировать ICMP-сообщения.
1. Построить в GNS3 топологию сети, состоящей из маршрутизатора FRR, коммутатора Ethernet и оконечного устройства.
2. Задать оконечному устройству IP-адрес в сети 192.168.1.0/24.
3. Присвоить интерфейсу маршрутизатора адрес 192.168.1.1/24
4. Проверить связь.
. Построить в GNS3 топологию сети, состоящей из маршрутизатора VyOS, коммутатора Ethernet и оконечного устройства.
2. Задать оконечному устройству IP-адрес в сети 192.168.1.0/24.
3. Присвоить интерфейсу маршрутизатора адрес 192.168.1.1/24
4. Проверить связь.

# Выполнение лабораторной работы

Построить в GNSS3 топологию сети , состоящей из коммутатора Ethernet и двух оконечных устройств VPCS соеденить VPCS с куммутатором и отобразить обозначения интерфейсов(рис. [-@fig:001]).

![В рабочей области рзмещены PC1-vvustinova, коммутатор msk-vvustinova-sw-01 и PC2-vvustinova соединенные через интерфейсы e0 and e1](image/1.jpg){#fig:001 width=70%}

Просмотреть синтаксис возможных для ввода команд VPCS, набрав /?. Задать IP-адрес первому узлу.(рис. [-@fig:002]).

![Выведена справка по командам VPCS, выполнен ip 192.168.1.11/24 192.168.1.1 и save.](image/2.jpg){#fig:002 width=70%}

Задать IP-адрес второму VPCS в сети 192.168.1.0/24.(рис. [-@fig:003]).

![ Выполнена команда ip 192.168.1.12/24 192.168.1.1, адрес сохранён командой save.](image/3.jpg){#fig:003 width=70%}

Проверить связь между оконечными устройствами с помощью команды ping.(рис. [-@fig:004]).

![С PC1 выполнен ping 192.168.1.11, все пакеты успешно доставлены.](image/4.jpg){#fig:004 width=70%}

Включить захват трафика на соединении между PC1 и коммутатором и проанализировать полученную информацию в Wireshark.(рис. [-@fig:005]).

![ В Wireshark видны пакеты Router Solicitation (ICMPv6) и Gratuitous ARP для адресов 192.168.1.11 и 192.168.1.12.](image/5.jpg){#fig:005 width=70%}

Выполнить ping с опцией -1 (ICMP) для проверки связи.
(рис. [-@fig:006]).

![Выполнена команда ping 192.168.1.11 -1 -c 1, получен ответ за 2.227 мс.](image/6.jpg){#fig:006 width=70%}

Проанализировать в Wireshark пакеты ARP и ICMP при ping-запросе.(рис. [-@fig:007]).

![Видны ARP-запросы и ICMP Echo request/reply между узлами 192.168.1.11 и 192.168.1.12..](image/7.jpg){#fig:007 width=70%}

Выполнить ping с опцией -2 (UDP) для проверки связи.(рис. [-@fig:008]).

![Выполнена команда ping 192.168.1.11 -2 -c 1, получен ответ за 0.899 мс.](image/8.jpg){#fig:008 width=70%}

Выполнить ping с опцией -3 (TCP) для проверки связи и проанализировать TCP-сессию.(рис. [-@fig:009]).

![Выполнена команда ping 192.168.1.11 -3 -c 1, в Wireshark видны этапы SYN, SYN-ACK, ACK, ECHO, FIN..](image/9.jpg){#fig:009 width=70%}

Построить в GNS3 топологию сети, состоящей из VPCS, коммутатора Ethernet и маршрутизатора FRR. Присвоить устройствам имена по заданному шаблону.(рис. [-@fig:010]).

![В рабочей области размещены PC1-vvustinova, коммутатор msk-vvustinova-sw-0x и маршрутизатор msk-vvustinova-gw-01.](image/10.jpg){#fig:010 width=70%}

Hастроить IP-адресацию для интерфейса узла PC1 и проверить её командой show ip.(рис. [-@fig:011]).

![Показаны IP-адрес 192.168.1.10/24, шлюз 192.168.1.1 и MAC-адрес 00:50:79:66:68:00.](image/11.jpg){#fig:011 width=70%}

Настроить маршрутизатор FRR: задать hostname msk-vvustinova-gw-01, назначить интерфейсу eth0 адрес 192.168.1.1/24, сохранить конфигурацию.(рис. [-@fig:012]).

![Выполнены команды configure terminal, hostname, interface eth0, ip address, no shutdown, write memory. Показан вывод show interface brief.](image/12.jpg){#fig:012 width=70%}

Проанализировать в Wireshark ICMP-пакеты при ping между узлом и маршрутизатором.(рис. [-@fig:013]).

![  Видны ICMP Echo request и reply между 192.168.1.10 и 192.168.1.1, а также ARP-запросы.](image/13.jpg){#fig:013 width=70%}

Проверить подключение: узел PC1 должен успешно отправлять эхо-запросы на адрес маршрутизатора 192.168.1.1. Также требовалось построить топологию с маршрутизатором VyOS и настроить его интерфейс eth0.(рис. [-@fig:014]).

![Выполнен ping 192.168.1.1, все пакеты успешно доставлены. На топологии с VyOS: компьютер не выдержал нагрузки и не смог загрузить маршрутизатор VyOS, поэтому проверка связи с ним не выполнялась](image/14.jpg){#fig:014 width=70%}

# Выводы

В  ходе работы были построены простейшие модели сети на базе коммутатора и маршрутизатора FRR в GNS3. Освоены настройка IP-адресации на VPCS и маршрутизаторе FRR, проверка связи с помощью утилиты ping. Проведён анализ трафика в Wireshark: изучены ARP-запросы, ICMP-, UDP- и TCP-пакеты. Попытка развернуть маршрутизатор VyOS не удалась из-за нехватки ресурсов компьютера, однако принципы настройки VyOS были изучены теоретически.

# ответы на контрольные вопросы

1. Какие три основных режима VTY существуют в FRR?

Режим просмотра VTY (только чтение), режим включения VTY (чтение и запись), другие режимы VTY.

2. Какие команды используются для перемещения по CLI в FRR?

Ctrl+f/LEFT, Ctrl+b/RIGHT, Alt+f, Alt+b, Ctrl+a, Ctrl+e.

3. Какие расширенные команды CLI доступны в FRR?

Ctrl+c (прервать ввод), Ctrl+z (завершить сеанс настройки), Ctrl+n/DOWN, Ctrl+p/UP, Tab (завершение команды), ? (справка).

4. Как настроить IP-адрес на интерфейсе в FRR?

configure terminal, interface eth0, ip address 192.168.1.1/24, no shutdown, exit, write memory.

5. Какие два режима существуют в VyOS?

Operational mode (символ $) и configuration mode (символ #).

6. Как настроить IP-адрес на интерфейсе в VyOS?

configure, set interfaces ethernet eth0 address 192.168.10.10/24, commit, save.

7. Для чего используется команда commit в VyOS?

Для фиксации текущего набора изменений конфигурации.

8. Для чего используется команда save в VyOS?

Для сохранения изменений конфигурации после перезагрузки.

9. Как выйти из режима конфигурации VyOS без применения изменений?

Команда exit discard.

10. Что анализируется в Wireshark при ping?

ARP-запросы (разрешение MAC-адресов), ICMP Echo request/reply, а также UDP- и TCP-пакеты при использовании соответствующих опций ping.

