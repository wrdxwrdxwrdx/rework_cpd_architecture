## Reporter(StepProcessor)

Подсчет и визуализация отчета.

+ ПОЛЯ:

  + path\_to\_save: Path

    Место, куда сохранять отчет

  + report_builder: ReportBuilder

    Объект для подсчета данных для отчета

  + report_visualizer: ReportVisualizer

    Объект для визуализации отчета по готовому ReportBuilder

+ МЕТОДЫ:

  + create_report(**dict[str, Any]): None

    1. Считаем данные для отчета по данным (вызываем report_builder.build())
    2. Визуализируем отчет, имея уже подсчитанный ReportBuilder.

    **ВАЖНО** на вход подаются какие-то данные. Они достаются из БД и предидущих шагов. Важно что бы запрашиваемые параметры для запуска назывались так же, как и в **input_storage_names** и **input_step_names**. На выход тоже обязательно выдавать ВСЕ заданные имена из **output_step_names** и **output_storage_names**.  Это будет проверятся в **validate_output**

    **ВАЖНО** ReportBuilder и ReportVisualizer можно комбинировать, главное что бы ReportVisualizer пользовался только теми полями, которые есть в ReportBuilder.