## StepProcessor <<Interface>>

Интерфейс для классов, решающих задачу шага. В основном описывает обязательные данные для запуска и возвращяемые данные. 

+ ПОЛЯ:

  + input_storage_names: set[str] = {}

    Названия полей в БД, необходимых для работы Процессора.

  + output_step_names: set[str] = {}

    Названия полей в БД, которые будут записаны после работы Процессора.

  + input_step_names: set[str] = {}

    Названия полей, переданных с прошлого шага, нужные для запуска Процессора.

  + output_storage_names: set[str] = {}

    Названия полей, которые будут переданы в следующий шаг, после запуска Процессора.

  + call_data: dict[str, Any] = {}

    Словарь данных, переданных с прошлого шага.

  + config: Optional[Path] = None

    Конфиг запуска Процессора. Не обязателен, нужен только для специалезированных Процессоров.

+ МЕТОДЫ:

  + validate_output(output: dict[str, Any]): bool

    Проверяет подходит ли output заданным полям output_storage_names и output_step_names.  `set(output.keys()) >=  output_step_names + output_storage_names`

