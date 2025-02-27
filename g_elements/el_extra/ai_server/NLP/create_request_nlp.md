# Создать запрос NLP

![](<../../../../.gitbook/assets1/windows_items/library/Primo.AI.Server.Elements.WFPrimoAICreateRequestNlp.png>)

NLP-запрос — это задача по обработке текста на естественном языке (Natural Language Processing, NLP), которую выполняет большая языковая модель в AI Server. Ответ модели зависит от выбранного навыка:
* Генерация — модель создает текст на основе начального ввода или заданного контекста.
* Суммаризация — модель кратко излагает текст с ацентом на указанные темы.
* Экстракция — модель извлекает из текста информацию по заданным ключам поиска.
* Классификация — модель отвечает на запрос, исходя из заранее определенного списка возможных ответов.

Элемент **Создать запрос NLP** позволяет отправить запрос к LLM-модели и получить идентификатор запроса, который впоследствии можно использовать для просмотра ответа с помощью элемента [Получить результат NLP](https://docs.primo-rpa.ru/primo-rpa/g_elements/el_extra/ai_server/nlp/get_request_nlp).

## Перед началом работы

1. Установите в Студии библиотеку [Primo.AI.Server](https://docs.primo-rpa.ru/primo-rpa/g_elements/el_extra/ai_server).
1. Найдите на панели элементов группу **AI > NLP** и перетащите элемент **Создать запрос NLP** в процесс.
1. Настройте параметры подключения к Server AI в контейнере **Сервер Primo.AI**.
1. Убедитесь, что на стороне Server AI создан проект, в котором запущена модель с подходящим навыком и ключом маршрутизации.


## Свойства
Обязательные свойства отмечены символом `*`. Описание общих свойств см. в [этом разделе](https://docs.primo-rpa.ru/primo-rpa/primo-studio/process/elements#svoistva-elementa).

**Обработка:**

1. **Текст\*** *[String]* — входной текст для обработки LLM-моделью. Пример: `"Текст договора"`.
1. **Ключи ответа** *[List\<String>]* — проивольные ключи, которые помогут модели сформировать наиболее релевантный ответ. Ключи ответа зависят от NLP-навыка:
   * Для навыка экстракции укажите ключи поиска, по которым модель будет извлекать информацию из входного текста.  Пример: `new List<string>(){"дата договора", "стороны"}`.
   * Для навыка генерации можно не указывать ключи или передать в них структурные элементы ответа. Пример для генерации вакансии: `new List<string>(){"Обязанности", "Требования", "Будет плюсом", "Мы предлагаем"}`.
   * Для навыка суммаризации укажите основные темы, которые необходимо передать при кратком изложении текста. Пример: `new List<string>(){"основная идея", "факты", "выводы"}`. 
   * Для навыка классификации укажите классы, которые могут быть присвоены тексту. Пример классификации писем: `new List<string>(){"заявка", "спам"}`.  
1. **Длина ответа\*** *[Int32]* — максимальная длина ответа модели, которая измеряется в токенах. Для русского языка 1 слово ~ 1.5 токена. По умолчанию `256`.
1. **Изображение** [String] – путь к файлу изображения (форматы: JPG, PNG) для загрузки и последующей обработки. ***Функция доступна начиная с версии NuGet-пакета Primo.AI.Server 1.0.11***.
1. **Ключ маршрутизации\*** *[String]* — ключ маршрутизации запроса. Каждый ключ ассоциирован с навыком NLP-модели и должен существовать в Server AI. Пример ключа маршрутизации для навыка экстракции: `"nlp-extraction"`.
1. **Контекст** *[String]* — путь к файлу с контекстом (`.json`) на локальном диске. Файл контекста определяет поведение модели относительно запросов. По умолчанию с каждым ключом маршрутизации уже ассоциирован файл контекста на сервере. Используйте это свойство, если хотите заменить данный файл своим.
1. **Температура\*** *[Double]* — управляет уровнем случайности в ответах модели. При низкой температуре модель склоняется к выбору наиболее вероятных текстовых единиц, что приводит к более логичным и предсказуемым ответам. При высокой температуре модель генерирует более разнообразные ответы. По умолчанию `0.1`. В качестве максимального значения рекомендуется указывать не более `1.0`.
1. **Min p\*** *[Double]* — минимальный порог вероятности для выбора токенов в ответе, где `0.0` — любой токен, `1.0` — самый вероятный. Под токеном подразумевается единица текста: слово, символ и т.д. Чем выше порог, тем наиболее вероятные токены модель возьмет в ответ, исключая из выборки редкие или неуместные токены. По умолчанию `0.1`.

{% hint style="info" %}
Свойства **Температура** и **Min p** дополняют друг друга. Сначала отбирается диапазон вероятных токенов в соответствии с температурой, а затем токены дополнительно фильтруются по минимальному порогу. Таким образом, если вы хотите:
* максимально увеличить вариативность ответа, то указывайте температуру 1.0, а min p — 0.0.
* максимально снизить вариативность — указывайте температуру 0.1, а min_p 1.0.

Наиболее оптимальные значения — 0.1 для обоих свойств.

{% endhint %}


**Вывод:**
* **Результат** *[[System.Guid](https://learn.microsoft.com/ru-ru/dotnet/api/system.guid?view=net-5.0)]* — название переменной, в которой сохранится идентификатор запроса. 
