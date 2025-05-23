## Step <<Interface>>

**ВАЖНО** Многие поля схожи с полями StepProcessor. В чем же разница? При разработке StepProcessor в эти поля указываются то, что будет точно получено/выдано. Тут же эти поля обозначают часть данных, нужная для работы (в том числе с возможностью переименования). В полях output мы сохраняем только часть данных, что отличается от данных выданных StepProcessor. При указании NONE поля будут взяты из StepProcessor

+ ПОЛЯ:

  + name: str = "Step"

    Имя шага для более информативных ошибок и логов.

  + input_storage_names: Optional[set[str]] = None

    Названия данных, нужных для работы шага, из БД.

  + output_storage_names: Optional[set[str] | dict[str: str]] = None

    Названия данных для сохранения в БД после работы Шага.

    Список, если не требуется изменение названия полей, иначе даем словарь, где указываем **старое название: новое**

    Пример: Генератор вохвращает поля {ТОЧКИ\_РАЗЛАДКИ, ЧИСЛОВОЙ\_РЯД, МАТОЖИДАНИЕ, ДИСПЕРСИЯ}. 

    1) Хотим записать только числовой ряд -> указываем {ЧИСЛОВОЙ\_РЯД}. 
    2) Хотим записать точки разладки и числовой ряд, но в будущем хотим использовать более простое название РАЗЛАДКИ -> указываем {ТОЧКИ\_РАЗЛАДКИ: РАЗЛАДКИ, ЧИСЛОВОЙ\_РЯД: ЧИСЛОВОЙ\_РЯД}

    **ЗАЧЕМ?** Есть проблема разных названий в разных шагах. Генерор возвращает ТОЧКИ\_РАЗЛАДКИ, а воркер хочет РАЗЛАДКИ. Так что можно заменить название. **НУЖНО ЛИ ЭТО? Не уверен**

  + input_step_names: Optional[set[str] | dict[str, str]]  = None

    Названия данных, нужных для работы шага, из предидущего шага.

    Список, если не требуется изменение названия полей, иначе даем словарь, где указываем **старое название: новое**

    **ЗАЧЕМ?** Хотим настроить гиперпараметры алгорима, а потом запустить на них сам алгоритм, тогда нужна возможность передачи данных между шагами. Но если для запуска нужны другие поля (при запуске будем распоковывать словарь через \*\*). Тогда используем словарь (смотреть пример для output_storage_names)

  + output_step_names: Optional[set[str] | dict[str, Any]] = None

    Названия данных, которые передаются на следующий шаг.

    Список, если не требуется изменение названия полей, иначе даем словарь, где указываем **старое название: новое**

    **ЗАЧЕМ?** Хотим настроить гиперпараметры алгорима, а потом запустить на них сам алгоритм, тогда нужна возможность передачи данных между шагами 

  + input_storage: Optional[Storage] = None

    БД откуда нужно брать данные. Optional т.к. не каждому шагу нужны данные на вход

  + output_storage: Optional[Storage] = None

    БД куда нужно сохранять данные. Optional т.к. не каждый шаг что-то сохраняет в БД

  + \_next: Optional[Step] = None

    Step реализует паттерн chain of responsibility. Это поле ответственно за хранение следующего шага эксперимента.

+ МЕТОДЫ:

  + \_\_call\_\_(): Optional[dict[str, Any]]

    Step реализует паттерн chain of responsibility. Этот метод ответственнен за выполнение задачи шага.

    **ЗАЧЕМ?** Optional[dict[str, Any]]. Если следующему шагу не нужны дополнитеьные данные, то метод возвращает None. В ином случае, возвращаем словарь **название параметра: значение**. 

  + set_next(next_step: Step, storage_names: set[str], step_names: set[str]): None

    Step реализует паттерн chain of responsibility. Этот метод ответственнен за сохранения следующего шага. При запуске метода так же проверяется возможность подключения шагов.

    storage_names -- какие есть поля в БД (нужно для проверки совместимости с предидущими шагами)

    step_names -- какие есть данные, передающиеся между шагами (нужно для проверки совместимости с предидущими шагами)

    next_step -- следующий шаг

    