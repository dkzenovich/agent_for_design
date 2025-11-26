# pdrs/

Автоматические reasoning-логи (PDR) для крупных промптов (StRS, Impact, SyRS, Traceability, Baseline и т.п.).
Создавать новый файл при каждом запуске, если промпт меняет артефакты в `target/docs` или `baseline/docs`.

Рекомендуемый формат файла: `YYYYMMDD-HHMM-<prompt-name>.md`

Шаблон содержимого:
```
# PDR: <prompt-name>
## Timestamp
<UTC или локальное время>

## Inputs
- Файлы/версии (git hash или версия, если доступно)
- Контекст (кратко)

## Assumptions
- ...

## Reasoning / Decisions
- Какие смысловые решения приняты для текста/диаграмм

## Artifacts Changed
- target/docs/src/... (списком)
- baseline/docs/... (если затронуто)
```
