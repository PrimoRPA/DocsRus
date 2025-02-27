# Аргументы

Аргумент является переменной, предназначенной для обмена между процессами. Он отличается от обычной переменной наличием свойства **Направление**, которое определяет, сможет ли аргумент получать и передавать данные в вызывающий процесс. 

**Направление** имеет следующие значения:

* IN — аргумент передает данные в подпроцесс.
* OUT – аргумент возвращает данные из подпроцесса. 
* IN\_OUT – аргумент работает на передачу и на возврат данных.

![Панель «Аргументы»](<../../.gitbook/assets/6 (5).png>)

Чтобы вызвать один процесс (далее — подпроцесс) из другого, необходимо перетащить его из панели **Проект** в треугольник, определяющий место вызова подпроцесса в сценарии.

![Вызов подпроцесса](../../.gitbook/assets/7.png)

Для подключения к аргументам подпроцесса нажмите кнопку ![](<../../.gitbook/assets/8 (3).png>). В открывшемся окне, в колонке **Назначение**, укажите выражения на выбранном языке программирования (C#, Python или JavaScript) либо имена переменных, используемых при взаимодействии с подпроцессом. По завершении редактирования закройте окно.

![Окно с аргументами подпроцесса](../../.gitbook/assets/9.png)


### Редактирование аргумента
Список всех аргументов отображается на панели **Аргументы**. Для вызова окна редактирования дважды кликните строку с аргументом, значение которого нужно изменить. 

:small_blue_diamond: ***Примечание**. Рекомендуем изменять имя аргумента не в окне редактирования, а по нажатию специальной кнопки **Переименовать аргумент** ![](<../../.gitbook/assets/Переименовать переменную.png>). Только в этом случае изменения применятся ко всему процессу, в котором аргумент используется.*

## Использование аргументов в Оркестраторе

По умолчанию аргументы можно редактировать, только открыв проект в Студии. Возможность редактирования из Оркестратора настраивается дополнительно, в разрезе каждого процесса проекта. Изменять в Оркестраторе можно только аргументы с направлениями **In** и **InOut**. При этом процесс проекта, к которому относятся аргументы, может быть любым — стартовым и нестартовым. 

Общий алгоритм по использованию аргументов проекта в Оркестраторе выглядит так:
1. При создании процесса RPA-проекта в Studio установите параметр **Использовать аргументы Оркестратора**\*.

   ![](<../../.gitbook/assets/process-with-args-2.png>)
   
2. Создайте в этом процессе аргументы. Проверьте, что всем аргументам в процессе заданы правильные направления. 
3. [Загрузите](https://docs.primo-rpa.ru/primo-rpa/primo-studio/projects/publish) архив RPA-проекта в Оркестратор – аргументы добавятся автоматически вместе с проектом.
4. На странице Оркестратора **RPA-проекты > Все RPA-проекты** для проекта с аргументами станет доступна кнопка **Аргументы**. По ее нажатию отобразятся значения по умолчанию всех аргументов проекта. Просмотреть возможно аргументы любых направлений, представленных в проекте: **In**, **InOut**, **Out**. Однако значения на этой странице предназначены только для просмотра, отредактировать их невозможно.
5. Чтобы запустить проект с аргументами через Оркестратор, используйте задания. Тип запуска задания, вручную или автоматически, не имеет значения.
6. Чтобы изменить значения аргументов проекта, перейдите на страницу Оркестратора **Задания** и выделите нужное задание в таблице. Если задание выполняет проект с аргументами, то для него станет доступна кнопка **Аргументы**. Иначе она будет неактивной.

   Нажмите кнопку **Аргументы** на странице заданий и укажите новое значение для тех аргументов, которые вы хотите изменить. Помните, что даже при наличии в проекте аргументов с типом **Out**, для редактирования будут доступны только аргументы с направлениями **In** и **InOut**.
7. Чтобы увидеть как менялись значения аргументов от запуска к запуску, перейдите на страницу **RPA-проекты > Все RPA-проекты > Аргументы** (см. пункт 4). На странице просмотра аргументов установите чекбокс **История запусков**. В результате вы увидите все значения аргументов, которые были заданы в Оркестраторе до запуска проекта и получены от робота после завершения/в процессе выполнения проекта.

Более подробно работа с аргументами через интерфейс Оркестратора описана в разделе [Аргументы проекта](https://docs.primo-rpa.ru/primo-rpa/orchestrator/orchestrator-user/tasks-overview/tasks-arguments).

> \**Процесс Main.ltw по умолчанию создается с выключенной настройкой. В этом случае необходимо его отредактировать: выберите процесс на панели «Проект» и вызовите команду контекстного меню **Редактировать элемент**. После чего установите галочку и нажмите **ОК**.*





