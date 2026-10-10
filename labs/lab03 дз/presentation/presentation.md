---
## Front matter
lang: ru-RU
title: Лабораторная работа №3
subtitle: Анализ трафика в Wireshark
author:
  - Устинова В. В.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 10 октября 2026

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Устинова Виктория Вадимовна
  * студент НПИбд-01-24
  * Российский университет дружбы народов


:::
::: {.column width="30%"}

:::
::::::::::::::

## Цель работы

Изучение посредством Wireshark кадров Ethernet, анализ PDU протоколов транспортного и прикладного уровней стека TCP/IP.

## Задание

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

## Вывод ipconfig: адаптер Ethernet 2.

С помощью команды ipconfig для ОС типа Windows или ifconfig

![Показан адаптер ethernet 2 с ipv4-адерсом 192.168.56.1 маской 255.255.255.0 и ipv6 адресом канала fe80::492e:29... . Адаптер open vpn connect dco -среда передачи недоступна](image/1.jpg){#fig:001 width=70%}

## Вывод ipconfig: беспроводные адаптеры.

Ипользуйте разные опции команды ifconfig

![Показаны беспроводная сети 3 4 5 и 2 с описанием qualcommm WCN685x wifi 6E Dual Band Simultaneous DHCP включен ](image/2.jpg){#fig:002 width=70%}

## Подробная информация о беспроводной сети.

Пояснить детально информацию о текущем сетевом соединении, включая адреса, срок аренды, DHCP-сервер и DNS-серверы

![Показаны IPv6-адреса, IPv4-адрес 192.168.1.169, маска 255.255.255.0, основной шлюз 192.168.1.1, DHCP-сервер 192.168.1.1, DNS-серверы fd0a:e190:4b8a::1 и 192.168.1.1.](image/3.jpg){#fig:003 width=70%}

## Использование ipconfig /displaydns.

Использовать разные опции команды ipconfig и пояснить полученную информацию

![Команда ipconfig /displaydns выводит кэш DNS: записи word-edit.officeapps.live.com, app-geo.wac.trafficmanager.net и mrc-shed.wac.trafficmanager.net с типом записи 5 и CNAME-записями.](image/4.jpg){#fig:004 width=70%}

## Определение MAC-адресов через getmac.

Определить MAC-адреса сетевых интерфейсов на компьютере.

![Выведены подключения: Беспроводная сеть (Qualcomm WCN685, 38-D5-7A-E8-A1-D9), Ethernet 2 (VirtualBox Host, 0A-00-27-00-00-1E), OpenVPN Connect, Pritunl DCO 1, Pritunl 1, Pritunl DCO 2, Pritunl 2, Pritunl 3, Pritunl DCO 3.](image/5.jpg){#fig:005 width=70%}

## Пинг шлюза по умолчанию.

Пропинговать шлюз по умолчанию командой ping 192.168.1.1 -n 4.

![Все 4 пакета успешно доставлены, время 13–16 мс, TTL 64, потерь 0%.](image/6.jpg){#fig:006 width=70%}

## Фильтр ARP и ICMP в Wireshark.

В Wireshark остановить захват трафика, прописать фильтр arp or icmp и убедиться, что отображаются только пакеты ARP или ICMP

![В списке пакетов видны ARP-запросы (Who has 192.168.1.169? Tell 192.168.1.1) и ICMP Echo request/reply между 192.168.1.169 и 192.168.1.1.](image/7.jpg){#fig:007 width=70%}

## Очистка ARP-кэша и повторный пинг.

Очистить ARP-кэш командой arp -d * и снова пропинговать шлюз командой ping 192.168.1.1 -n 4.

![Все 4 пакета успешно доставлены, время 12–13 мс, TTL 64, потерь 0%.](image/8.jpg){#fig:008 width=70%}

## Анализ ARP и ICMP после очистки кэша.

Изучить эхо-запрос и эхо-ответ ICMP, а также кадры ARP. Изучить данные в полях заголовка Ethernet II.

![Видны ARP-запросы, ICMP Echo request/reply между 192.168.1.169 и 192.168.1.1, а также ARP-ответы с MAC-адресом f8:f0:82:fb:0f:50.](image/9.jpg){#fig:009 width=70%}

## Пинг rudn.ru.

 Начать новый процесс захвата трафика и пропинговать по имени известный адрес, например ping rudn.ru -n 4.

![Выполнен ping rudn.ru (37.18.93.135), превышен интервал ожидания для запроса, 100% потерь.](image/10.jpg){#fig:010 width=70%}

## Анализ ARP и ICMP при ping rudn.ru.

Изучить запросы и ответы протоколов ARP и ICMP, определить MAC-адреса источника и получателя, определить тип MAC-адресов

![Видны ARP-запросы и ICMP Echo request к 37.18.93.135 без ответа, MAC-адреса f8:f0:82:fb:0f:50 и 38:d5:7a:e8:a1:d9.](image/11.jpg){#fig:011 width=70%}

## Пинг ya.ru.

Пропинговать по имени известный адрес, например ping ya.ru -n 4.

![Выполнен ping ya.ru (77.88.55.242), все 4 пакета успешно доставлены, время 8–19 мс, TTL 56, потерь 0%.](image/12.jpg){#fig:012 width=70%}

## Анализ ARP и ICMP при ping ya.ru.

Изучить запросы и ответы протоколов ARP и ICMP, определить MAC-адреса источника и получателя.

![Видны ARP-запросы и ICMP Echo request/reply между 192.168.1.169 и 77.88.55.242, MAC-адреса f8:f0:82:fb:0f:50 и 38:d5:7a:e8:a1:d9.](image/13.jpg){#fig:013 width=70%}

## Детали ICMP-ответа.

 Изучить детали эхо-ответа ICMP в Wireshark, включая Ethernet II и IPv4.

![Frame 631 — 74 байта, Ethernet II (Src Nagtech_fb:0f:50, DstCloudNetwork_e8:a1:d9), IPv4 (Src 77.88.55.242, Dst 192.168.1.169), ICMP](image/14.jpg){#fig:014 width=70%}

## Детали ICMP-запроса.

Изучить детали эхо-запроса ICMP в Wireshark, включая Ethernet II и IPv4

![Frame 630 — 74 байта, Ethernet II (Src CloudNetwork_e8:a1:d9, Dst Nagtech_fb:0f:50), IPv4 (Src 192.168.1.169, Dst 77.88.55.242), ICMP.](image/15.jpg){#fig:015 width=70%}

## Детали ARP-ответа.

Изучить кадры данных протокола ARP, данные в полях заголовка Ethernet II

![Frame 427 — 42 байта, Ethernet II (Src Nagtech_fb:0f:50, Dst CloudNetwork_e8:a1:d9), ARP (reply).](image/16.jpg){#fig:016 width=70%}

## Анализ HTTP-трафика.

 В Wireshark в строке фильтра указать http и проанализировать информацию по протоколу TCP в случае запросов и ответов

![ВВидны HTTP-запросы GET /, GET /favicon.ico, GET /hypertext/WWW/TheProject.html и ответы HTTP/1.1 200 OK, 400 Bad request между 192.168.1.169 и 188.184.67.127.](image/17.jpg){#fig:017 width=70%}

## Анализ DNS-трафика.

 В Wireshark в строке фильтра указать dns и проанализировать информацию по протоколу UDP в случае запросов и ответов

![Видны DNS-запросы и ответы между fd0a:e190:4b8a:0:e9 и fd0a:e190:4b8a::1: Standard query 0x4c9a A nav-edge.smartscreen.microsoft.com, Standard query 0x9a1 HTTPS info.cern.ch CNAME webafs902.cern.ch.](image/18.jpg){#fig:018 width=70%}

## Анализ QUIC-трафика.

В Wireshark в строке фильтра указать quic и проанализировать информацию по протоколу QUIC в случае запросов и ответов

![Видны QUIC-пакеты Protected Payload (KP0) с DCID=041240ea0d808731 и Initial, DCID=a6390fd80ed99a8a, PKN 1 и 2, между 192.168.1.169 и 184.51.252.54, 23.196.236.27.](image/19.jpg){#fig:019 width=70%}

## Анализ handshake TCP.

Проанализировать handshake протокола TCP, привести пример с пояснениями изменения значений соответствующих сообщений.

![Видны TCP-пакеты SYN, SYN-ACK, ACK между 192.168.1.169 и 188.184.67.127, HTTP GET / HTTP/1.1, HTTP/1.1 200 OK, FIN, ACK.](image/20.jpg){#fig:020 width=70%}

## График потока TCP.

В Wireshark в меню «Статистика» выбрать «График Потока» и привести пояснения по изменениям значений соответствующих сообщений при установлении соединения по TCP.

![На графике потока отображены этапы TCP-соединения: SYN, SYN-ACK, ACK, GET / HTTP/1.1, HTTP/1.1 200 OK, FIN, ACK, GET /favicon.ico.](image/21.jpg){#fig:021 width=70%}

## Выводы

В ходе работы были изучены возможности команды ipconfig для ОС Windows и определены MAC-адреса сетевых интерфейсов. С помощью Wireshark захвачены и проанализированы пакеты ARP и ICMP в части кадров канального уровня, изучены поля заголовка Ethernet II. Проанализированы протоколы транспортного уровня TCP, UDP и QUIC при работе HTTP и DNS. Изучен трёхступенчатый handshake протокола TCP и построен график потока. Получены практические навыки анализа сетевого трафика.
