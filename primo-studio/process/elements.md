# Работа с элементами

Все доступные компоненты процесса находятся в панели **Элементы**. Компоненты сгруппированы по тематике. Например, в группе **Приложение Excel** находятся все элементы, работающие с Excel.

В верхней части панели расположена поисковая строка для быстрого поиска элементов.

![](<../../.gitbook/assets/image (887).png>)

Под поисковой строкой можно увидеть иконки групп:

* **Часто используемые** — для быстрого доступа к элементам, которые вы применяете в проекте чаще всего.
* **Избранные** — для быстрого доступа к избранным элементам. В избранное элемент добавляется вручную. Для этого вызовите контекстное меню элемента и выберите пункт **Добавить в Избранные**:

![](<../../.gitbook/assets/image (947).png>)

## Добавление элемента в процесс

Добавить элемент можно одним из следующих способов:
* Перетаскиванием — выберите на панели элементов компонент и перетащите его в нужную часть процесса.
* Командой контекстного меню. Выберите элемент на панели элементов, вызовите его контекстное меню, выберите **Вставить после выделенного**. Чтобы успешно применить эту команду, в процессе уже должны быть другие элементы, среди которых следует активировать элемент, после которого вы хотите произвести вставку.


## Свойства элемента

Каждый элемент обладает набором уникальных параметров или, иначе, *свойств*. Параметры элемента настраиваются в панели **Свойства**. Чтобы увидеть свойства элемента, добавьте его в процесс и нажмите на элемент.

Панель **Свойства** состоит из нескольких информационных блоков:
* в верхней части отображается внутреннее наименование элемента и его уникальный идентификатор (ComponentId);
* в центральной — список свойств;
* в нижней части — краткое описание этих свойств (*справка*).

![](<../../.gitbook/assets/0 (173).png>)

Свойства могут быть отображены в виде обычного списка или в виде групп. Для переключения режимов используйте кнопки ![](<../../.gitbook/assets/1 (124).png>).

Все элементы обладают набором общих свойств:

1. **Наименование** — имя элемента, которое отображается в его заголовке и в журнале. Для удобства возможно изменить название элемента внутри процесса, например, когда используются несколько одинаковых компонентов.
1. **Отключить логирование** — позволяет отключить запись логов в консоли (только для данного элемента). Например, если он оперирует конфиденциальными данными. Существует возможность централизованно включить/отключить логирование для всех новых элементов, добавляемых в проект. Для этого перейдите в раздел **Файл > Настройки > Общие > Элементы** и установите нужное значение в чекбоксе **Отключить логирование у новых элементов**.
1. **Продолжить при ошибке** — сценарий будет выполняться даже в том случае, если при выполнении элемента возникла ошибка.
1. **Скриншот завершения** — позволяет сделать снимок экрана в момент завершения работы элемента. Эти скриншоты сохраняются в папку `.Screenshots`, которая создается автоматически внутри папки с процессом.
1. **Скриншот ошибки** — при возникновении ошибки будет сделан снимок экрана.
1. **Пауза до (мс)** — добавляет паузу перед выполнением элемента. Пауза может понадобиться, например, в случае, если сайт, с которым планируется выполнить определенное действие, долго загружается, и требуется подождать, прежде чем переходить к следующему элементу в процессе. Аналогичную роль выполняет элемент [Ожидание](https://docs.primo-rpa.ru/primo-rpa/g_elements/el_basic/els_logic/el_logic_wait)
1. **Пауза после (мс)** — добавляет паузу после выполнения элемента.

Частные свойства описаны в статьях, посвященных конкретным элементам. Описание всех встроенных элементов в Primo RPA Studio (Windows) можно найти [здесь](https://docs.primo-rpa.ru/primo-rpa/g_elements/el_basic). 

Вносить изменения в свойства можно также в слотах самого элемента:

![](<../../.gitbook/assets/2 (10).png>)


### Значения свойств

Значения бывают следующих видов:

* **Константа** — обычный текст (например, как в свойстве **Наименование**) или чекбокс (например, **Продолжить при ошибке**). В случае текста рядом часто можно увидеть кнопку переключения межу режимами **Код** и **Без кода** — <img src="../../.gitbook/assets/image (803).png" alt="" data-size="line"> / <img src="../../.gitbook/assets/image (916).png" alt="" data-size="line">. В состоянии **Без кода** введенные данные будут интерпретироваться как константы либо как имена переменных (то есть не будут считаться кодом).
* **Переменная** — выбирается из списка переменных, созданных для данного процесса, и выглядит как выпадающий список:

   ![](<../../.gitbook/assets/3 (7).png>)

* **Вычисляемое значение** — выражение на том языке программирования, который был выбран при создании процесса (C#, Python либо JavaScript). Даже в случае, если необходимо указать обычную строку, ее текст необходимо заключить в кавычки, а спецсимволы внутри строки экранировать по правилам выбранного языка (описание языков не входит в тематику данного руководства). Вычисляемое свойство всегда содержит кнопку «…»:

    ![](<../../.gitbook/assets/4 (5).png>)

    При нажатии кнопки «…» откроется форма редактирования выражения:

    ![](<../../.gitbook/assets/001 (19).png>)
* **Шаблон поиска** — выражение, описывающее [шаблон поиска](https://docs.primo-rpa.ru/primo-rpa/primo-studio/process/searchpatterns) элемента управления. Наличие шаблона поиска зависит от типа элемента.

## Работа со скриншотами внутри элемента

Некоторые элементы содержат в себе функцию **Сделать скриншот**, которая позволяет сделать снимок выбранного сегмента экрана. Скриншоты могут помочь пользователям быстрее понять, с чем работает тот или иной элемент в процессе.

![](<../../.gitbook/assets/6 (7).png>)

Чтобы создать скриншот, нажмите на **Сделать скриншот** и выделите сегмент экрана. Созданный скриншот отобразится на панели элемента:

![](<../../.gitbook/assets/7 (1).png>)

Дополнительно скриншот сохранится в папку проекта `.Resources`. Название скриншота представляет собой ID элемента, к которому относится изображение.
 
Управление скриншотом осуществляется через контекстное меню скриншота. Доступны команды:
* **Сделать скриншот** — позволяет заменить текущий скриншот.
* **Очистить** — позволяет удалить скриншот.

**Соблюдайте следующие рекомендации при работе с функцией скриншотов:**
1. Используйте только один монитор. 
1. Если вы используете RDP-сессию, убедитесь, что:
   * масштаб удаленного рабочего стола равен 100%;
   * отключено интеллектуальное изменение размера.


## Аннотация

К каждому элементу процесса можно добавить краткое описание (*аннотацию*). Описание будет отображаться сразу под названием элемента. 

Чтобы добавить аннотацию, активируйте панель элемента и нажмите в правом верхнем углу восклицательный знак — появится область для ввода текста. 

![](<../../.gitbook/assets/image (845).png>)

## Контекстное меню элемента

Дополнительные действия с элементами можно осуществить при вызове контекстного меню. При нажании правой клавишей мыши доступны команды:
 * Вырезать
 * Копировать
 * Закомментировать элементы — элемент будет помещен в контейнер [Закомментировать](https://docs.primo-rpa.ru/primo-rpa/g_elements/el_basic/els_logic/el_logic_commentout) и проигнорируется при запуске/отладке процесса. При выборе сразу нескольких элементов, элементы будут закомментированы массово. Команда недоступна для корневой последовательности.
 * Раскомментировать элементы — команда отображается только для контейнера **Закомментировать**, в котором находятся закомментированные элементы.
 * Перенести элемент в try/catch — помещает выделенный элемент или элементы в контейнер [Try-Catch](https://docs.primo-rpa.ru/primo-rpa/g_elements/el_basic/els_logic/el_logic_trycatch).
 * Перенести в новую последовательность — вызывает окно создания последовательности, после чего переносит выбранный элемент эту последовательность. Команда недоступна для корневой последовательности.
 * Запуск с элемента — запускает процесс с выбранного элемента.
 * Включить логирование. ***Функция доступна с версии 1.24.10***
 * Отключить логирование. ***Функция доступна с версии 1.24.10***
 * **Помощь** — открывает в браузере страницу с описанием элемента из документации.

## Пакетное включение логирования элементов

С версии Студии 1.24.10 добавлена возможность массового управления логированием элементов. Теперь можно отключить или включить логирование для нескольких активностей сразу. Чтобы это сделать:

1. Выберите необходимые элементы, зажав клавишу *Shift* и выделив первую и последнюю активности в списке.
2. Нажмите правой клавишей мыши на выделенные элементы и выберите опцию *Отключить логирование* или *Включить логирование*.


 ![](<../../.gitbook/assets1/Loggirovanie.png>)

 
{% hint style="info" %} Информация об исключении будет логироваться независимо от настроек пакетного логирования элемента Исключение. {% endhint %}



### Отображение свойств элементов и редактор синтаксиса

С версии 1.25.1 добавлена возможность отображать часто используемые свойства элементов процесса непосредственно на панели элемента. Теперь вводимые данные в параметрах активности автоматически синхронизируются с соответствующими свойствами элемента, отображаемыми в правой части окна. Эта функция позволяет ускорить настройку и контроль параметров.

 ![](<../../.gitbook/assets1/svoistva_na_elemente.png>)

Для активации данной функции:  
1. Перейдите в раздел *Файл → Настройки → Общие → Элементы*.  
2. Выберите версию *v2*.  
3. Для процессов с типом *"Диаграмма"* установите галочку *"Отображать дизайн элементов диаграммы"*.  

 ![](<../../.gitbook/assets1/new_elem_v2.png>)


Кроме того, встроен **редактор синтаксиса (IntelliSense)**, поддерживающий автозаполнение методов и программных выражений.  

Для активации редактора синтаксиса:  
1. Перейдите в раздел *Файл → Настройки*.  
2. Установите галочку в параметре *"Использовать строчный редактор"*.  
Редактор включен по умолчанию.

 ![](<../../.gitbook/assets1/redaktor_sintaksisa.png>)


С помощью встроенного редактора синтаксиса вы можете проверять правильность введённых выражений. При вводе некорректного выражения редактор подсветит ошибку, выделив проблемное место красным подчёркиванием.  

 ![](<../../.gitbook/assets1/oshibka_syntst.png>)




