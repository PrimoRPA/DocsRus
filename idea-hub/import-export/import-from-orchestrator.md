# Импорт данных из Оркестратора

Импорт данных из Оркестратора в Idea Hub позволяет получить имеющиеся в Оркестраторе данные о процессах, роботах, пользователях, департаментах и т.д. и перенести их для использования в Idea Hub.

IdeaHub получает данные о запусках, лицензиях, проектах, очередях и т.д. из баз данных Оркестратора, используя SQL запросы, которые запускаются скриптом `orc-data-fetch` и формируются в файлы формата CSV.

Сформированные CSV файлы сохраняются в специальным образом организованной структуре каталогов, откуда автоматически импортируются собственными средствами Idea Hub. Каталоги должны быть созданы в соответствии с инструкцией ниже (см. раздел 4 “Структура каталогов для импорта данных). 

**!!ВАЖНО!! При наличии у организации нескольких контуров, каждый контур должен иметь уникальное наименование. (Контуры - изолированные подсети внутри общей сети организации. В скриптах для обозначения контуров используется слово “environments”.)**


## Требования
* [Psql](https://postgrespro.ru/&sa=D&source=docs&ust=1702476704920204&usg=AOvVaw3K8f-Xb71DoDMk3Cu4xoJm);
* Cron (Linux) - поставляется по умолчанию во всех системах Linux;
* Менеджер паролей [pass](https://www.passwordstore.org/) (опционально для Linux);
* Доступ к серверам, на которых размещены базы данных Оркестратора;
* Пользователь, от имени которого будут выполняться запросы, должен иметь права на чтение следующих баз данных - именно к ним будут обращаться скрипты:  
  * ltools
  * ltoolsidentity
  * ltoolslicense
  * ltoolslogs



## Скрипты
Комплект поставки скриптов для импорта данных из Оркестратора в Idea Hub имеет следующую структуру:

![](<../.gitbook/assets/IdeaHub_OrchImport.png>)

Комплект поставки включает в себя скрипты для запуска на ОС Windows (`get_data.bat`, для PostgreSQL) и ОС Linux (`get_data.sh`). Для работы с MS SQL используется скрипт `get_data.ps1`.

**!!ВАЖНО!! Перед началом работы со скриптом сделайте копию файла скрипта (соответствующего используемой операционной системе и SQL) и вносите изменения (см. раздел “Параметры скрипта” ниже) в сделанную копию. Кроме того, при наличии в организации нескольких контуров, сделайте отдельную копию файла скрипта  для использования в каждом из них. Рекомендуется указывать название контура в имени копии файла скрипта, например: `get_data.prod.sh`, где prod - название контура.**

Папка запросов `orc-data-fetch/queries` (`queries_mssql` для MS SQL) содержит подпапки, в которых лежат запросы к соответствующим базам в с расширением SQL. Для корректной работы не удаляйте ничего из содержимого папок.
Результаты выполнения скриптов будут находиться в папке данных («output»).

**!!ВАЖНО!! Названия файлов с результатами выполнения запросов должны остаться такими, какими они были после выполнения скрипта. Их не нужно переименовывать.**

Скрипт должен запускаться на машине, у которой есть доступ к серверам баз данных Оркестратора; на этой машине также должно быть установлено приложение psql.

Скрипты могут запускаться по расписанию с помощью утилиты-планировщика задач Cron, позволяющей выполнять скрипты на сервере в назначенное время с заранее определенной периодичностью. Дополнительная информация по работе с Cron содержится в документе [“Инструкция по работе с Cron”](https://docs.primo-rpa.ru/primo-rpa/primo-idea-hub/cron).


## Параметры скрипта

Для каждой из копий файла скрипта, работающей с конкретным контуром, необходимо указать значения следующих переменных для каждой из баз данных:
1) `OUTPUT_FOLDER`: в эту переменную вносится имя каталога, в который будут записаны результирующие файлы. Имя каталога должно совпадать с именем контура, данные о котором будут вноситься в данный каталог. 
Каталог output-folder должен располагаться по пути `<...>/private/import-source/environments/<output-folder с названием контура>`. Часть пути, обозначенная <...>, может различаться на разных компьютерах. Узнать ее для конкретной машины можно при помощи команды `drush status`, выполняемой в корне сайта - в выводе команды будет содержаться, в том числе, путь к каталогу `private`, например:

![](../.gitbook/assets1/DrushStatus-output.png)

2) `DB_HOST_[ИМЯ_БАЗЫ_ДАННЫХ]`: IP адрес сервера, на котором расположена база данных.
   
4) `DB_USER_[ИМЯ_БАЗЫ_ДАННЫХ]`: имя пользователя для базы данных. Пользователь берется из переменной окружения DB_USER, либо из утилиты pass (primo/dblogin).
   
6) `DB_PASSWORD_[ИМЯ_БАЗЫ_ДАННЫХ]`: пароль, который нужно установить для подключения к базе данных. Пароль берется из переменной окружения DB_PASSWORD, либо из утилиты pass (primo/dbpassword) - см. пункт 5 ниже.
   
8) `USE_PASS`: указывает, будет ли использована утилита pass. Если этот параметр равен 1, тогда в переменных вида DB_PASSWORD_[ИМЯ_БАЗЫ_ДАННЫХ] нужно указать имя, под которым пароль хранится в утилите pass. Если значение этого параметра равно 0, тогда пароль будет использоваться в том виде, в котором он указан в явном виде в переменной DB_PASSWORD_[ИМЯ_БАЗЫ_ДАННЫХ].

При этом во всех случаях выше [ИМЯ_БАЗЫ_ДАННЫХ] - это имя конкретной базы данных, написанное в верхнем регистре.

Например, для базы данных ltools:  

Домен, на котором находится база данных ltools  
DB_HOST_LTOOLS=""  
Имя пользователя для базы данных ltools  
DB_USER_LTOOLS=""  
Пароль для пользователя базы данных ltools  
DB_PASSWORD_LTOOLS=""  


## Структура каталогов для импорта данных

Для реализации автоматического импорта данных из Оркестратора разместите файлы, полученные с помощью выполнения скриптов `orc-data-fetch`, по пути `PATH_TO_IDEAHUB/private/import-source/environments`. Термин “environments” используется для обозначения контуров - изолированных подсетей внутри общей сети организации.
Пример правильного размещения структуры каталогов:
 
PATH_TO_IDEAHUB  
-- private  
---- import-source  
------ environments  
-------- prom  
---------- projects.csv  
---------- machines.csv  
---------- robots.csv  
---------- ...  
-------- test  
---------- projects.csv  
---------- machines.csv  
---------- robots.csv  
---------- ...  
-------- something-else  
---------- projects.csv  
---------- machines.csv  
---------- robots.csv  
---------- ...  
 
Контуры в системе будут называться по имени каталога: `PATH_TO_IDEAHUB/private/import-source/environments/prom`, `PATH_TO_IDEAHUB/private/import-source/environments/test`, `PATH_TO_IDEAHUB/private/import-source/environments/something-else`, с изменением регистра первого символа на верхний, например "Prom", "Test", "Something-else".
 
Остальные файлы импорта:
- `PATH_TO_IDEAHUB/private/import-source/areas.xlsx`
- `PATH_TO_IDEAHUB/private/import-source/process.xlsx`
- `PATH_TO_IDEAHUB/private/import-source/users.xlsx`


 

