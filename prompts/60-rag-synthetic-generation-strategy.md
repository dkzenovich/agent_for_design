---
mode: 'agent'
description: 'Разработать стратегию синтетической генерации данных (SDG) для покрытия сложных сценариев (Multi-hop, Reasoning)'
---

# 60-rag-synthetic-generation-strategy

<context>
Спроектировать пайплайн генерации синтетических тестовых данных (Synthetic Data Generation). Определить методы превращения документов в сложные вопросы (Evol-Instruct), стратегии создания состязательных примеров и механизмы валидации качества (Critique Agents).
</context>

<inputs>
- `target/rag_dataset_spec/02_info_needs.md` — требуемые типы сложности (Simple/Multi-hop/Reasoning).
- `target/rag_dataset_spec/03_sources_and_scope.md` — доступные источники и их пригодность для графа.
- `target/rag_dataset_spec/05_quality_and_coverage.md` — целевые метрики (Faithfulness, Recall).
</inputs>

<outputs>
- `target/rag_dataset_spec/07_synthetic_generation_strategy.md` — спецификация SDG: алгоритмы эволюции, промпты для генератора/критика, объемы выборки.
- PDR: `pdrs/YYYY-MM-DDTHH-MM-SS_60-rag-synthetic-generation-strategy.md`
</outputs>

<steps>
1) **Стратегия отбора "Зерна" (Seed Selection):**
   - Описать алгоритм выбора чанков-кандидатов из корпуса (случайная выборка vs кластеризация по темам).
   - Для Multi-hop: указать метод отбора пар чанков (через общие сущности/Граф Знаний).

2) **Дизайн Эволюции Вопросов (Evol-Instruct Tactics):**
   - Описать конкретные тактики усложнения вопросов для покрытия `IN-NEED-XXX`:
     - **Reasoning Evolution:** Добавление требований "сравни", "проанализируй", "сделай вывод".
     - **Multi-Context Evolution:** Объединение фактов из двух разных документов (требует Graph Readiness из шага 20).
     - **Conditioning:** Введение условий "если", "кроме", "в период...".

3) **Стратегия Состязательной Генерации (Adversarial/Negative):**
   - Описать генерацию вопросов, не имеющих ответа в контексте (для теста на Faithfulness/Refusal).
   - Описать генерацию вопросов с ложными предпосылками.

4) **Валидация и Фильтрация (Critique Agents):**
   - Задать критерии для LLM-критика (Critique Agent), который будет фильтровать синтетику:
     - Groundedness: Ответ действительно следует из контекста?
     - Clarity: Вопрос однозначен?
     - Difficulty: Вопрос достаточно сложен (не копипаст)?

5) **Объем и Распределение:**
   - Определить целевое количество пар (например, 50 Simple, 30 Reasoning, 20 Multi-hop, 10 Adversarial).
</steps>

<constraints>
- Стратегия должна гарантировать наличие поля `expected_output` (Ground Truth) для всех генерируемых пар (кроме Adversarial, где выход фиксирован).
- Не полагаться только на Simple вопросы; явно требовать % сложных кейсов.
</constraints>

<audit_log>
- В PDR зафиксировать: какие тактики эволюции выбраны, как решается проблема Multi-hop генерации (через граф или эвристики), какие риски качества синтетики приняты.
</audit_log>
