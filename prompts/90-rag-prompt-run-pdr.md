---
mode: 'agent'
description: 'Шаблон PDR: фиксировать входы, допущения и решения после запуска промпта'
---

# 90-rag-prompt-run-pdr

<context>
Короткий PDR после запуска промптов 10/20/30/40/50. Цель — зафиксировать допущения и выборы, чтобы через полгода было ясно, почему датасет выглядит так.
</context>

<inputs>
- Итоговые файлы, которые менялись в рамках запуска.
- Список входных файлов/контекста, который читался.
</inputs>

<outputs>
- Файл в `pdrs/` формата `YYYY-MM-DDTHH-MM-SS_<prompt>.md`.
</outputs>

<template>
```
# PDR: <prompt-name>
## Timestamp
<UTC или локальное время>

## Inputs
- <файл/версия>
- ...

## Assumptions
- ...

## Decisions / Reasoning
- ...

## Added / Changed / Excluded
- ...

## Artifacts Changed
- target/rag_dataset_spec/0X_*.md
```
</template>

<constraints>
- Если изменений нет — пишем это явно.
- Без общих слов: фиксируем конкретные допущения и решения.
</constraints>
