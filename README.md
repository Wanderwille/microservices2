# # Домашнее задание к занятию «Микросервисы: подходы» - Подус Сергей

Вы работаете в крупной компании, которая строит систему на основе микросервисной архитектуры.
Вам как DevOps-специалисту необходимо выдвинуть предложение по организации инфраструктуры для разработки и эксплуатации.


## Задача 1: Обеспечить разработку

Предложите решение для обеспечения процесса разработки: хранение исходного кода, непрерывная интеграция и непрерывная поставка. 
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- облачная система;
- система контроля версий Git;
- репозиторий на каждый сервис;
- запуск сборки по событию из системы контроля версий;
- запуск сборки по кнопке с указанием параметров;
- возможность привязать настройки к каждой сборке;
- возможность создания шаблонов для различных конфигураций сборок;
- возможность безопасного хранения секретных данных (пароли, ключи доступа);
- несколько конфигураций для сборки из одного репозитория;
- кастомные шаги при сборке;
- собственные докер-образы для сборки проектов;
- возможность развернуть агентов сборки на собственных серверах;
- возможность параллельного запуска нескольких сборок;
- возможность параллельного запуска тестов.

Обоснуйте свой выбор.

## Задача 2: Логи

Предложите решение для обеспечения сбора и анализа логов сервисов в микросервисной архитектуре.
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- сбор логов в центральное хранилище со всех хостов, обслуживающих систему;
- минимальные требования к приложениям, сбор логов из stdout;
- гарантированная доставка логов до центрального хранилища;
- обеспечение поиска и фильтрации по записям логов;
- обеспечение пользовательского интерфейса с возможностью предоставления доступа разработчикам для поиска по записям логов;
- возможность дать ссылку на сохранённый поиск по записям логов.

Обоснуйте свой выбор.

## Задача 3: Мониторинг

Предложите решение для обеспечения сбора и анализа состояния хостов и сервисов в микросервисной архитектуре.
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- сбор метрик со всех хостов, обслуживающих систему;
- сбор метрик состояния ресурсов хостов: CPU, RAM, HDD, Network;
- сбор метрик потребляемых ресурсов для каждого сервиса: CPU, RAM, HDD, Network;
- сбор метрик, специфичных для каждого сервиса;
- пользовательский интерфейс с возможностью делать запросы и агрегировать информацию;
- пользовательский интерфейс с возможностью настраивать различные панели для отслеживания состояния системы.

Обоснуйте свой выбор.

## Ответ:

1. На данный момент, решений для поставленных очень много, вот несколько из них:

- GitLab CI/CD - думаю, это один из самых универсальных инструментов, поскольку он предлагает различные функции: просмотр кода, CI/CD, непрерывное развертывание и так далее.  Для использования собственных докер образов можно использовать docker hub

- Jenkins - Бесплатный кроссплатформенный CI/CD-инструмент с открытым исходным кодом на базе Java. Он обеспечивает непрерывную интеграцию, а также облегчает непрерывную доставку. Для использования собственных докер образов можно использовать docker hub или artifactory.

- TeamCity - Надежный и качественный CI-сервер. Команды часто выбирают TeamCity для большого количества функций аутентификации, развертывания и тестирования, а также поддержки Docker.

Думаю, что самый лучший выбор будет GitLab, он очень популярный и удобен в использовании, но в нем нельзя хранить секреты, так же он хорошо администрируется. 

2. Под требования в задаче идеально подходит стэк ELK. Очень известное решение, очень много информации по нему.

Состав:
- FileBeat - агент, собирающий данные с машины и направляющий в Elasticsearch.
- Logstash - служба обрабатывающая данные: фильтрует, парсит на составляющие поля, агрегирует строки, обогащает данные при необходимости и т.п. передает данные в системы потребители при необходимости.
- Elasticsearch - инструмент аналитики и полнотекстового поиска, позволяет хранить, оперативно получать нужные данные больших объемов.
- Kibana - Web визуальный инструмент для Elasticsearch, позволяет управлять индексами Elasticsearch, выполнять непосредственный визуальный поиск, строить Dashbord-ы для удобства оперативного анализа логов (данных).

3. Для мониторинга, на мой взгляд, лучшим решением будет стек prometheus + grafana + node exporter. Комплекс соответствует всем вышеуказанным требованиям.

- широкоизвестный стек
- большое количество собираемых метрик
- Удобный UI.


