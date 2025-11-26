# Как использовать (RAG Dataset Spec as Code)

## Входные данные
- `input/01_business_context.md` — кто пользователь, зачем ему RAG, как меряем успех.
- `input/02_example_questions.md` — реальные/ожидаемые вопросы, диалоги, частота.
- `input/03_sources_inventory.md` — список систем/хранилищ, типы документов, ограничения ИБ/правовые.

## Запуск цепочки промптов
1) `prompts/00-system-persona.md` — прогреть контекст, задать стиль и ограничения.
2) `prompts/10-rag-context-to-info-needs.md` — из контекста и вопросов получить `target/rag_dataset_spec/02_info_needs.md`.
3) `prompts/20-rag-sources-and-scope.md` — сопоставить инфопотребности и источники → `03_sources_and_scope.md`.
4) `prompts/30-rag-schema-and-metadata.md` — схема документа, поля, метаданные → `04_schema_and_metadata.md`.
5) `prompts/40-rag-quality-and-refresh.md` — требования к качеству/покрытию/обновлению → `05_quality_and_coverage.md`.
6) `prompts/50-rag-security-and-access.md` — классы данных, маскирование, доступы → `06_security_and_access.md`.

## PDR (обязательно после каждого шага 10/20/30/40/50)
- Используйте `prompts/90-rag-prompt-run-pdr.md`.
- Имя файла: `pdrs/YYYY-MM-DDTHH-MM-SS_<prompt>.md`.
- Фиксируйте: какие входы читались, какие решения/допущения приняты, что добавили/отбросили, какие артефакты изменены.

## Мини-checklist перед ревью
- В `02_info_needs.md` инфопотребности сгруппированы в IN-NEED-XXX с ролями и критичностью.
- В `03_sources_and_scope.md` для каждого IN-NEED отмечены источники (Primary/Secondary/Excluded) и фильтры отбора.
- В `04_schema_and_metadata.md` описаны обязательные/необязательные поля и правила маппинга/обогащения.
- В `05_quality_and_coverage.md` заданы метрики полноты/чистоты/актуальности и режим обновления.
- В `06_security_and_access.md` зафиксированы классы данных, маскирование и правила доступа по ролям.
