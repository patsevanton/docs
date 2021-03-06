# Бюллетени безопасности

На этой странице приводятся рекомендации специалистов {{ yandex-cloud }} о вопросах безопасности.


## 15.06.2020 — Special Register Buffer Data Sampling Attack (aka CrossTalk)


### Описание

Для некоторых моделей процессоров Intel компания VUSec [обнаружила новую атаку](https://www.vusec.net/projects/crosstalk/) под названием Special Register Buffer Data Sampling Attack (или CrossTalk). Данная атака позволяет злонамеренному процессу получить результаты, возвращаемые инструкциями RDRAND и RDSEED из другого процесса, при этом злонамеренный и легитимный процессы могут выполняться на разных физических ядрах процессора. Атаке присвоен номер [CVE-2020-0543](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-0543).

Отчет от Intel: [Deep Dive: Special Register Buffer Data Sampling](https://software.intel.com/security-software-guidance/insights/deep-dive-special-register-buffer-data-sampling).


### Влияние на сервисы {{ yandex-cloud }}

Модели процессоров, используемые в {{ yandex-cloud }}, **не подвержены атаке** CrossTalk.


## 28.08.2019 — TCP SACK


### Описание
Специалисты Netflix обнаружили три уязвимости в ядре Linux:
* [CVE-2019-11477](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11477)
* [CVE-2019-11478](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11478)
* [CVE-2019-11479](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11479)

Оригинальный отчёт от Netflix: [NFLX-2019-001](https://github.com/Netflix/security-bulletins/blob/master/advisories/third-party/2019-001.md).

Разбор уязвимости от Red Hat: [TCP SACK PANIC](https://access.redhat.com/security/vulnerabilities/tcpsack).


### Влияние на сервисы {{ yandex-cloud }}
* Инфраструктура {{ yandex-cloud }} была оперативно защищена и обновлена.
* Образы операционных систем, доступные пользователям Yandex Compute Cloud, были обновлены как только появились соответствующие исправления. Таким образом, новые виртуальные машины, создаваемые в Yandex Compute Cloud, не подвержены указанным уязвимостям.


## 19.08.2019 — Несколько доменов Yandex Object Storage внесены в Public Suffix List


### Описание

Список доменов, внесенных в Public Suffix List:
* yandexcloud.net
* storage.yandexcloud.net
* website.yandexcloud.net

Домены из списка Public Suffix List получают свойства доменов верхнего уровня, как, например, домены .ru или .com:
* Браузеры не будут сохранять сookie, установленные на перечисленные домены.
* Браузеры не позволят поменять заголовок запроса `Origin` страницы на корневые домены.

Больше информации можно найти в [нашем блоге](https://cloud.yandex.ru/blog/posts/2019/08/storage-domains).


### Влияние на сервисы {{ yandex-cloud }}

Данные изменения позволят повысить безопасность пользователей {{ yandex-cloud }}.
