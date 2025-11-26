---
mode: 'agent'
description: 'Определить инженерные метрики оценки RAG (Retrieval/Generation) и стратегию валидации'
---

# 40-rag-quality-and-refresh

<context>
Спроектировать систему оценки качества RAG-пайплайна. Определить целевые метрики для Генератора (LLM) и Ретривера (Поиска), требования к "Золотому датасету" (Golden Dataset) и процесс непрерывной оценки (Continuous Evaluation).
</context>

<inputs>
- `target/rag_dataset_spec/02_info_needs.md` — классы вопросов (Simple/Multi-hop/Reasoning).
- `target/rag_dataset_spec/04_schema_and_metadata.md` — структура данных.
</inputs>

<outputs>
- `target/rag_dataset_spec/05_quality_and_coverage.md` — спецификация метрик, пороговые значения (Thresholds), стратегия валидации (LLM-as-a-Judge).
- PDR: `pdrs/YYYY-MM-DDTHH-MM-SS_40-rag-quality-and-refresh.md`
</outputs>

<steps>
1) Определить метрики **Оценки Генерации (Generation Metrics)** для каждого `IN-NEED-XXX`:
   - **Faithfulness (Достоверность):** Требования к отсутствию галлюцинаций (reference-free относительно ответа, но reference-based относительно контекста).
   - **Answer Relevancy:** Требования к соответствию интенту вопроса (отсутствие "воды").

2) Определить метрики **Оценки Извлечения (Retrieval Metrics)**:
   - **Context Precision:** Требования к ранжированию (борьба с Lost-in-the-Middle).
   - **Context Recall:** Требования к полноте (нашли ли все факты для идеального ответа).
   - **Context Relevancy:** Требование к соотношению сигнал/шум в чанках.

3) Сформулировать требования к **Golden Dataset** для расчета этих метрик:
   - Какие поля обязательны для Recall (например, `expected_output`).
   - Какие поля нужны для Precision (например, `relevant_doc_ids` / `gold_context`).
   - Необходимость "Состязательных" (Adversarial) примеров для проверки Faithfulness.

4) Описать стратегию **Continuous Evaluation (CI/CD)**:
   - Триггеры запуска тестов (смена промпта, модели эмбеддинга, размера чанка).
   - Пороговые значения (Pass/Fail thresholds), например "Faithfulness > 0.9".

5) (Опционально) Сохранить требования к "свежести" (Data Freshness) самого индекса, если это критично для бизнеса (лаг обновления источника).
</steps>

<constraints>
- Использовать терминологию Ragas/DeepEval (Faithfulness, Context Recall, etc.).
- Четко разделять метрики, требующие `expected_output` (Ground Truth), и метрики, работающие без него.
- Не описывать ручное тестирование; фокус на автоматизированную оценку через LLM-судей.
</constraints>

<audit_log>
- В PDR зафиксировать: выбранные метрики для разных типов вопросов (нужен ли Context Recall для болталки?), пороговые значения, требования к составу Золотого датасета.
</audit_log>