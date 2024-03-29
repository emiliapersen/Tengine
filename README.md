# СРАВНЕНИЕ ИТ-СЕРВЕРОВ

NGINX и Tengine - популярные веб-серверы, причем Tengine является форком NGINX, созданным командой Taobao. У них много общего, включая возможность выполнять функции веб-серверов, обратных прокси-серверов и балансировщиков нагрузки. Однако Tengine предлагает несколько улучшений по сравнению с NGINX, что делает его привлекательным выбором для конкретных случаев использования.

Повышение производительности:
Tengine продемонстрировал значительные улучшения производительности по сравнению с NGINX. В тестовых тестах Tengine показал улучшение производительности на 200% при использовании accept_mutex (принять блокировку) параметра, который используется в NGINX по умолчанию. Без accept_mutex производительность Tengine была на 60% выше, чем у NGINX.
Эти улучшения связаны с реализацией в Tengine SO_REUSEPORT опции сокета, которая позволяет нескольким процессам привязываться к одному и тому же порту, тем самым улучшая обработку входящих подключений.

Конфигурация и возможности:
Конфигурационные файлы Tengine в целом аналогичны файлам NGINX, с заметными отличиями в директивах, таких как reuse_port, worker_cpu_affinity и accept_mutex. Поддержка Tengine worker_cpu_affinity auto упрощает настройку привязки процессора, что может повысить производительность.
Tengine наследует все функции NGINX-1.4.7, что делает его на 100% совместимым с NGINX. Однако в нем также представлено несколько новых функций, таких как поддержка динамической загрузки модулей (DSO), небуферизованные загрузки на внутренние серверы, дополнительные методы балансировки нагрузки, такие как согласованное хеширование и сохранение сеанса, поддержка фильтра тела ввода и расширенные возможности ведения журнала.

Примеры использования и влияние на реальный мир:
Ненаучный тест, включающий загрузку файла объемом 1 ГБ в кластер объектного хранилища, показал, что Tengine значительно сократил время загрузки по сравнению с NGINX. Это улучшение было связано со способностью Tengine отключать буферизацию запросов, что невозможно в NGINX без дополнительной настройки 4.
Небуферизованная обработка запросов в Tengine оказалась особенно полезной в средах с большими объемами загрузки, таких как Ceph Object Gateway и Openstack Swift. Эта функция обеспечивает более эффективную передачу данных и снижает нагрузку на прокси-серверы.

Сравнение веб-серверов по показателям с GitHub

|               |     Watch     |      Fork     |      Star     |     Tags      |
| ------------- | ------------- | ------------- | ------------- | ------------- |
|     NGINX     |      975      |      6500     |     20000     |      560      |
|    TENGINE    |      891      |      2500     |     12500     |      37       |

Сравнение веб-серверов по показателям Google trends за последние 90 дней 

![2024-03-24_17-54-38](https://github.com/emiliapersen/Tengine/assets/107800469/bc135c23-8d57-4ea4-8a6f-bf9844337c3f)

ВЫВОД 

Tengine имеет ряд преимуществ перед Nginx, такие как поддержка балансировки нагрузки методом чередования IP-адресов, автоматическое увеличение числа рабочих процессов при увеличении нагрузки, а также поддержка сжатия HTML страниц и динамического модуля ngx_http_concat.
Однако Nginx остается более популярным и широко используемым веб-сервером, что означает, что большинство документации, советов и решений проблем можно легче найти для Nginx. Также Nginx имеет более широкое сообщество поддержки и больше разработчиков, что обеспечивает быстрые обновления и исправления ошибок.
Таким образом, в настоящее время Nginx остается более предпочтительным веб-сервером для многих разработчиков и администраторов, благодаря своей надежности, производительности и широкой поддержке сообщества.

