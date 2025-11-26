# RAG Dataset Spec as Code

Репозиторий для ведения ТЗ на датасет для RAG как код: входные файлы → цепочка промптов → единый Dataset Requirements Specification в `target/rag_dataset_spec/` + автоматические PDR-логи в `pdrs/`.

## Что внутри
- `input/` — бизнес-контекст RAG, примеры вопросов, инвентарь источников (без правок).
- `prompts/` — цепочка промптов 10→50 для построения DRS и `90-rag-prompt-run-pdr.md` для фиксации решений.
- `target/rag_dataset_spec/` — итоговый DRS: контекст, инфопотребности, источники, схема/метаданные, качество/обновление, безопасность/доступ.
- `pdrs/` — машинные PDR-записи по каждому запуску ключевых промптов.
- `HOWTO_RAG_DATASET.md` — краткая инструкция по запуску.

## Основной workflow (только про датасет)
1. Контекст → инфопотребности: `prompts/10-rag-context-to-info-needs.md`, входы `input/01_business_context.md` + `02_example_questions.md`, выход `target/rag_dataset_spec/02_info_needs.md` (+ PDR).
2. Инфопотребности → источники/границы: `20-rag-sources-and-scope.md`, вход `02_info_needs.md` + `input/03_sources_inventory.md`, выход `03_sources_and_scope.md` (+ PDR).
3. Источники → схема/метаданные: `30-rag-schema-and-metadata.md`, выход `04_schema_and_metadata.md` (+ PDR).
4. Качество/покрытие/обновление: `40-rag-quality-and-refresh.md`, выход `05_quality_and_coverage.md` (+ PDR).
5. Безопасность/доступ: `50-rag-security-and-access.md`, выход `06_security_and_access.md` (+ PDR).

## Принципы
- Узкий фокус: только требования к датасету RAG (не полный продукт, не проектирование пайплайна).
- Каждая итерация фиксирует допущения и решения в `pdrs/`.
- Все артефакты читаются и поддерживаются как код, без неявных договоренностей.
