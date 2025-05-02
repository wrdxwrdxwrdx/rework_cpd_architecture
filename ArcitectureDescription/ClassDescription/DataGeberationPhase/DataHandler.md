## DataHandler(StepProcessor)

Генерация/Чтение данных. В DataGenerationStep этиданные будут записываться в БД

+ МЕТОДЫ:

  + get_data(): Iterator[dict[str, Any]] *На размышление:* можно ли заменить Any, на float

    Постепенно выдает словари **название параметра: значение**. 