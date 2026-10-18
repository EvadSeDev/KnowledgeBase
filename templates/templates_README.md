# Templates

Справочник по шаблонам KnowledgeBase.

Цель этого каталога — обеспечить единый формат хранения знаний, расследований и отчетов.

Использование шаблонов позволяет:

- быстрее создавать документы;
- не забывать важные разделы;
- упрощать поиск информации;
- сохранять единый стиль документации;
- превращать опыт в накопленную экспертизу.

---

# Общие правила

## Используйте шаблон перед созданием документа

Плохо:

```text
Создать пустой файл
Начать писать с нуля
Каждый раз придумывать структуру
```

Хорошо:

```text
Создать файл
Скопировать шаблон
Заполнить разделы
Сохранить
```

---

## Не удаляйте разделы без причины

Если информация отсутствует:

```text
Не выявлено
Не требуется
Не применимо
```

лучше оставить раздел, чем удалять его.

---

## Один документ = одна цель

Примеры:

```text
Daily Report
→ только ежедневная аналитика

RCA
→ только расследование

Knowledge Article
→ только знания

Project Card
→ только информация о проекте
```

---

# Список шаблонов

## daily-template.md

### Назначение

Ежедневный отчет.

### Использовать когда

Каждый рабочий день.

### Результат

Документ:

```text
daily/YYYY-MM-DD.md
```

### Основные разделы

- Executive Summary
- Daily Engineering Analytics
- Question Analysis
- Lessons Learned
- Growth Analysis
- Action Plan

### Цель

Ответить на вопросы:

```text
Что я сделал?

Чему научился?

Что стоит сохранить?

Что делать дальше?
```

---

## weekly-template.md

### Назначение

Недельный обзор.

### Использовать когда

В конце недели.

### Результат

Документ:

```text
weekly/YYYY-WXX.md
```

### Основные разделы

- Achievements
- Investigations
- Root Causes
- Lessons Learned
- Progress To Senior
- Next Week Plan

### Цель

Понять:

```text
Что удалось за неделю?

Какие проблемы повторяются?

Какие знания накапливаются?
```

---

## monthly-template.md

### Назначение

Месячный обзор.

### Использовать когда

В последний рабочий день месяца.

### Результат

Документ:

```text
monthly/YYYY-MM.md
```

### Основные разделы

- Executive Summary
- Skill Growth
- Knowledge Growth
- Middle → Senior Progress
- Development Plan

### Цель

Ответить на вопрос:

```text
Как изменились мои компетенции за месяц?
```

---

## rca-template.md

### Назначение

Root Cause Analysis.

### Использовать когда

Если найдена или исследуется корневая причина проблемы.

### Результат

Документ:

```text
rca/RCA-<topic>.md
```

### Основные разделы

- Symptom
- Expected Result
- Actual Result
- Hypotheses
- Investigation
- Root Cause
- Solution
- Validation
- Prevention

### Цель

Ответить на вопрос:

```text
Почему возникла проблема?

Как её исправить?

Как предотвратить повторение?
```

---

## investigation-template.md

### Назначение

Исследование.

### Использовать когда

Причина проблемы пока неизвестна.

### Отличие от RCA

Investigation:

```text
Причина еще не найдена.
```

RCA:

```text
Причина уже найдена.
```

### Основные разделы

- Context
- Problem
- Hypotheses
- Checks
- Findings
- Next Steps

### Цель

Формализация процесса расследования.

---

## lesson-template.md

### Назначение

Lessons Learned.

### Использовать когда

Появилось новое полезное знание.

### Результат

Добавляется в:

```text
lessons-learned/
```

### Основные разделы

- Situation
- What Happened
- Conclusion
- Future Usage

### Цель

Сохранить опыт для будущего использования.

---

## project-template.md

### Назначение

Карточка проекта.

### Использовать когда

Появляется новый проект.

### Результат

Документ:

```text
projects/<project-name>.md
```

### Основные разделы

- Purpose
- Technologies
- Repository
- Jira
- Contacts
- Architecture Notes
- Common Problems

### Цель

Быстро вспомнить контекст проекта.

---

## knowledge-article-template.md

### Назначение

Статья в Knowledge Base.

### Использовать когда

Одно и то же знание использовалось несколько раз.

### Результат

Документ:

```text
knowledge-base/<technology>/<topic>.md
```

### Основные разделы

- Overview
- Problem
- Solution
- Examples
- Best Practices
- References

### Цель

Создание долговременной инженерной Wiki.

---

# Как выбрать шаблон

```text
Ежедневная работа
↓
daily-template.md

Недельный обзор
↓
weekly-template.md

Месячный обзор
↓
monthly-template.md

Причина неизвестна
↓
investigation-template.md

Причина найдена
↓
rca-template.md

Получен новый урок
↓
lesson-template.md

Новый проект
↓
project-template.md

Знание используется регулярно
↓
knowledge-article-template.md
```

---

# Рекомендуемый жизненный цикл знания

```text
Работа
↓
Daily Report
↓
Lesson Learned
↓
Investigation
↓
RCA
↓
Knowledge Base Article
↓
Playbook
```

Не каждое знание проходит все этапы.

Но наиболее ценные знания обычно доходят до этапа:

```text
Knowledge Base
```

или

```text
Playbook
```

---

# Definition of Done

Шаблон считается использованным правильно если:

✅ Документ создан по шаблону

✅ Основные разделы заполнены

✅ Выводы сформулированы явно

✅ Информация пригодна для повторного использования

✅ Через 6 месяцев документ будет понятен без дополнительного контекста