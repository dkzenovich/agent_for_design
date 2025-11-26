---
mode: 'agent'
description: 'Спроектировать схемы данных: для RAG-корпуса (Knowledge Base) и для Золотого датасета (Evaluation)'
---

# 30-rag-schema-and-metadata

<context>
Определить структуры данных для двух ключевых артефактов:
1. **Knowledge Corpus Schema**: Формат документов в векторной базе (поля, чанкинг, метаданные).
2. **Golden Dataset Schema**: Формат тестовых пар для оценки качества (input, expected_output, gold_context).
</context>

<inputs>
- `target/rag_dataset_spec/03_sources_and_scope.md` — источники данных.
- Примеры структур документов/таблиц (если есть во входах).
</inputs>

<outputs>
- `target/rag_dataset_spec/04_schema_and_metadata.md` — спецификация двух схем.
- PDR: `pdrs/YYYY-MM-DDTHH-MM-SS_30-rag-schema-and-metadata.md`
</outputs>

<steps>
1) **Спроектировать схему Knowledge Corpus (База знаний):**
   - Основные поля: `doc_id`, `chunk_id`, `text_content`, `url/source`.
   - Метаданные для фильтрации: даты, категории, права доступа.
   - Правила чанкинга и обогащения (например, добавлять заголовок документа в каждый чанк).

2) **Спроектировать схему Golden Dataset (Тестовый набор):**
   - **Input:** Поле для вопроса/запроса пользователя.
   - **Expected Output (Ground Truth):** Эталонный ответ (обязателен для метрики Context Recall).
   - **Gold Context:** Список ID релевантных чанков/документов (обязателен для метрики Context Precision).
   - **Metadata:** Тип вопроса (Simple/Reasoning), сложность, требуемые инструменты.

3) **Определить связь схем (Mapping):**
   - Как `Gold Context` в датасете ссылается на `chunk_id` в корпусе (Foreign Key).

4) **Зафиксировать форматы обмена:**
   - JSONL / Parquet как стандарт для датасетов.
</steps>

<constraints>
- Схема Golden Dataset должна явно поддерживать поля, необходимые для метрик Ragas/DeepEval (expected_output, context).
- Не смешивать поля корпуса (где хранится знание) и поля датасета (где хранится тест).
</constraints>

<audit_log>
- В PDR обосновать выбор обязательных полей для Золотого датасета (почему нужен expected_output?).
</audit_log>