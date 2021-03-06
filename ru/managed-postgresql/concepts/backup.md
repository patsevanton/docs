# Резервные копии

{{ mpg-short-name }} обеспечивает автоматическое и ручное резервное копирование баз данных. Резервные копии занимают место в объеме хранилища, выделенном для кластера. Если суммарный объем данных и резервных копий превышает объем хранилища, превышение [тарифицируется](../pricing.md).

Резервная копия автоматически создается раз в день. Отключить автоматическое создание резервной копии невозможно, и изменить промежуток хранения автоматических копий (по умолчанию 7 дней) пока тоже нельзя.

Время начала резервного копирования задается при создании или изменении кластера. Резервное копирование начнется в течение получаса от указанного времени. По умолчанию начало резервного копирования устанавливается на 22:00 UTC (Coordinated Universal Time). 

Чтобы восстановить кластер из резервной копии, [следуйте инструкциям](../operations/cluster-backups.md).

## Создание резервной копии {#size}

Резервные копии могут быть автоматическими и ручными, но вне зависимости от типа, резервные копии создаются по следующей схеме:
- Первая и каждая седьмая резервные копии — полные резервные копии всех баз данных.  
- Остальные резервные копии — инкрементные, хранится только разница с предыдущей резервной копией, что позволяет экономить хранилище.

После создания резервная копия сжимается для дальнейшего хранения. На текущий момент отображение точного размера резервной копии недоступно.

## Хранение резервной копии {#storage}

Резервные копии хранятся во внутреннем хранилище Яндекса в виде бинарных файлов и шифруются с помощью [GPG](https://ru.wikipedia.org/wiki/GnuPG). У каждого кластера свои ключи шифрования.

Все резервные копии (автоматические и ручные) хранятся 7 дней. Чтобы гарантированно восстановиться на автоматическую резервную копию семидневной давности, может хранится до двух полных резервных копий.

## Проверка резервной копии {#verify}

### Проверка целостности резервной копии {#integrity}

Целостность резервных копий проверяется на синтетических данных интеграционными тестами сервиса. Резервные копии пользовательских кластеров на текущий момент не проверяются. 

### Проверка восстановления из резервной копии {#capabilities}

Для проверки возможностей резервного копирования [восстановите кластер из резервной копии](../operations/cluster-backups.md) и проверьте целостность ваших данных.