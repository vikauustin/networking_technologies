---
## Front matter
title: "лабораторная работа №1"
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

Установка и настройка GNS3 и сопутствующего программного обеспечения.

# Задание

1. Установить GNS3-all-in-one, GNS3 VM, проверить корректность запуска (см.
раздел 1.4).
2. Импортировать в GNS3 образ маршрутизатора FRR (см. раздел 1.5.1).
3. Импортировать в GNS3 образ маршрутизатора VyOS (см. раздел 1.5.2).
4. Проверить корректность работы маршрутизаторов FRR и VyOS (см. раздел
1.5.3).

# Выполнение лабораторной работы

Установить GNS3-all-in-one. При установке через менеджер пакетов Chocolatey необходимо выбрать компоненты GNS3-Desktop, GNS3-VM, Tools. (рис. [-@fig:001]).

![Выбираем их в окне установщика](image/1.jpg){#fig:001 width=70%}

При установке GNS3 указать тип виртуальной машины, в которой будет работать GNS3 VM. В данном случае выбирается VirtualBox.
(рис. [-@fig:002]).

![В окне установщика выбран тип VM — VirtualBox, нажата кнопка Install.](image/2.jpg){#fig:002 width=70%}

Установить GNS3 VM для VirtualBox. Распаковать архив с образом и импортировать GNS3 VM.ova через меню Файл → Импорт конфигураций, выбрав политику MAC-адреса «Сгенерировать новые MAC-адреса всех сетевых адаптеров».(рис. [-@fig:003]).

![В окне импорта указаны параметры виртуальной системы GNS3 VM (2 процессора, 4096 МБ ОЗУ).](image/3.jpg){#fig:003 width=70%}

Уточнить параметры настройки виртуальной машины GNS3 VM. В разделе «Система» проверить ресурсы: не менее 4096 МБ памяти и не менее 2 ЦП. Настроить вложенную виртуализацию, включив флажок «Включить Nested VT-x/AMD-V».(рис. [-@fig:004]).

![Во вкладке «Процессор» установлены 2 ЦП, включён флажок Nested VT-x/AMD-V.](image/4.jpg){#fig:004 width=70%}

Запустить GNS3 VM в VirtualBox. Для корректной работы GNS3 необходимо задать кодировку для отображения свойств VirtualBox командой VBoxManage setproperty language C.(.рис. [-@fig:005]).

![GNS3 VM запущена, показаны версии сервера, VM, Ubuntu, QEMU, IP-адрес 192.168.56.101 и порт 80.](image/5.jpg){#fig:005 width=70%}

Запустить приложение gns3 и в мастере настройки указать настройки локального сервера. Выбрать IP-адрес привязки хоста, находящегося в подсети VirtualBox.(рис. [-@fig:006]).

![В мастере настройки указаны протокол HTTP, хост localhost, порт 80 TCP, логин admin.](image/6.jpg){#fig:006 width=70%}

Создать новый проект в GNS3 через меню File → New blank project и назвать его, например, network..(рис. [-@fig:007]).

![В окне создания проекта введено имя «network».](image/7.jpg){#fig:007 width=70%}

Импортировать в GNS3 образ маршрутизатора FRR. В окне выбора файлов указать версию FRR, например FRR version 8.2.2, и нажать Next.(рис. [-@fig:008]).

![ В списке версий FRR выбрана версия 8.2.2 со статусом Ready to install..](image/8.jpg){#fig:008 width=70%}

Настроить образ маршрутизатора FRR. В окне конфигурации шаблона во вкладке General settings в поле «On close» выбрать Send the shutdown signal (ACPI).(рис. [-@fig:009]).

![В настройках шаблона FRR указаны RAM 256 МБ, vCPUs 1, Boot priority HDD, On close — Send the shutdown signal (ACPI).](image/9.jpg){#fig:009 width=70%}

Импортировать в GNS3 образ маршрутизатора VyOS. В окне выбора файлов указать версию VyOS Universal Router version 1.3.3 и нажать Import.(рис. [-@fig:010]).

![В списке версий VyOS выбрана версия 1.3.3 со статусом Ready to install.](image/10.jpg){#fig:010 width=70%}

Проверить корректность работы маршрутизатора FRR. В терминале должно появиться приглашение frr#, после чего ввести команду show version.(рис. [-@fig:011]).

![В терминале FRR выполнена команда show version, показана версия FRRouting 8.2.2.](image/11.jpg){#fig:011 width=70%}

Проверить корректность работы маршрутизаторов FRR и VyOS. Убедиться, что оба устройства запущены и доступны через консоль.(рис. [-@fig:012]).

![В Topology Summary отображаются узлы FRR-1 и VyOSUniversalRouter-1 с адресами консолей.](image/12.jpg){#fig:012 width=70%}

# Выводы

В ходе работы были установлены GNS3-all-in-one и GNS3 VM, проверена корректность их запуска. Освоены импорт и настройка
образов маршрутизаторов FRR и VyOS, а также проверка их работоспособности через консоль. Получены практические навыки подготовки экспериментального стенда для эмуляции компьютерных сетей.



