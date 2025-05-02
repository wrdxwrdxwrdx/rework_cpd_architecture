## DataHandler(StepProcessor) <<Interface>>

Генерация/Чтение данных. В DataGenerationStep эти данные будут записываться в БД

+ МЕТОДЫ:

  + get_data(**dict[str, Any]): Iterator[dict[str, Any]] *На размышление:* можно ли заменить Any, на float

    Постепенно выдает словари **название параметра: значение**. 	
    
    **ВАЖНО** На выход обязательно выдавать ВСЕ заданные имена из **output_step_names** и **output_storage_names**. Это будет проверятся в **validate_output**

​		