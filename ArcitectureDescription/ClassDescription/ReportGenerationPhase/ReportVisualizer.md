## ReportVisualizer <<interface>>

Визуализация отчета, основываясь на работе ReportBuilder.

+ ПОЛЯ:

  + path\_to\_save: Path

    Место, куда сохранять результат

+ МЕТОДЫ:

  + draw(report_builder: ReportBuilder): None

    основываясь на полях ReportBuilder, визуализируем отчет

    **ВАЖНО** на вход подаются какие-то данные. Они достаются из БД и предидущих шагов. Важно что бы запрашиваемые параметры для запуска назывались так же, как и в **input_storage_names** и **input_step_names**. На выход тоже обязательно выдавать ВСЕ заданные имена из **output_step_names** и **output_storage_names**.  Это будет проверятся в **validate_output**

