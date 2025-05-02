## DataGenerationStep(Step)

Самая первая фаза эксперимента -- генерация данных. DataGenerationStep генерирует/читает данные и записывает их в БД.

+ ПОЛЯ:

  + data_handler: DataHandler

    Объект который будет генерировать/читать данные с помощью метода **get_data**

  + config: Optional[Path] = None

    Файл конфигурации для генерации данных. Пример такого конфига можно найти в /CoR/normal_normal_config.yaml

  + saver: Optional[Saver] = None

    Объект для сохранения данных в БД

+ МЕТОДЫ:
  + \_\_call\_\_
    1) получает данные из data_handler (проходясь по итератору **get_data()**)
    2) запись данных в БД с помощью Saver.