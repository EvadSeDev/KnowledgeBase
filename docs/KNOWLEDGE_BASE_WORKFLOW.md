# Knowledge Base Workflow v4

Практическое руководство по использованию Engineering Knowledge Base.

## Installation

### Требования
- Windows 10/11
- IntelliJ IDEA
- Git
- GitHub Copilot (рекомендуется)

### Получение KnowledgeBase

```powershell
git clone <repository-url>
```

### Рекомендуемое расположение

```text
D:\Documents\KnowledgeBase
```

# Подключение KnowledgeBase к IntelliJ IDEA

## Сценарий 1. Отдельный проект (рекомендуется)

File → Open → D:\Documents\KnowledgeBase → New Window

## Сценарий 2. Подключение как модуль

### Шаг 1
Открыть основной проект.

### Шаг 2
File → New → Module from Existing Sources...

### Шаг 3
Выбрать каталог:

```text
D:\Documents\KnowledgeBase
```

### Шаг 4
Open

### Шаг 5
Next → Next → Next

### Шаг 6
Finish

### Результат
В Project View должны появиться основной проект и KnowledgeBase.

# Ежедневный процесс

## Шаг 1. Создать Daily Report

Создать файл:

```text
daily/YYYY/YYYY-MM-DD.md
```

## Шаг 2. Создать Daily Report на основе шаблона

Открыть:

```text
templates/daily-template.md
```

Создать:

```text
daily/YYYY/YYYY-MM-DD.md
```

Скопировать содержимое шаблона в новый файл и сохранить.

В результате должны присутствовать разделы:
- Executive Summary
- Daily Engineering Analytics
- Question Analysis
- Investigations
- Lessons Learned
- Growth Analysis
- Action Plan

## Шаг 3. Заполнить шаблон через Copilot

Открыть:

```text
prompts/PROMPT_PROFESSIONAL_GROWTH.md
```

В Copilot использовать запрос:

Agent mode 
```text
Отредактируй файл:

daily/2026/2026-10-18.md

Заполни существующий Daily Report на основании сегодняшней работы.

Используй:

- текущую беседу;
- открытые файлы;
- результаты анализа;
- материалы исследований;
- контекст проекта.

Правила:

- заполняй существующие разделы документа;
- не создавай новый документ;
- не добавляй второй экземпляр отчёта;
- не дублируй заголовки;
- не меняй структуру документа;
- не удаляй существующие разделы;
- замени шаблонные значения фактическим содержимым;
- если данных недостаточно, напиши "Недостаточно данных";
- не придумывай задачи или расследования, которых не было;
- используй только Markdown.

Важно:

Не добавляй новый заголовок:

# Professional Growth Analytics

Он уже существует в файле.

Заполняй только существующие разделы.

Верни diff для применения.
```

## Шаг 4. Сохранить результат

Вставить ответ Copilot в:

```text
daily/YYYY/YYYY-MM-DD.md
```

и сохранить файл.

## Шаг 5. Выделить Lessons Learned

Задать вопрос:

```text
Что сегодня узнал такого, что поможет мне через месяц?
```

Создавать Lesson Learned если:
- найден новый подход;
- найдена особенность технологии;
- найден полезный способ диагностики;
- получен важный опыт.

Хранить в:

```text
lessons-learned/
```

Не создавать если знание уже сохранено или относится только к одной задаче.

## Шаг 6. Проверить необходимость RCA

Вопрос:

```text
Найдена ли причина проблемы?
```

Если нет — оставить результаты в Investigation или Daily Report.

Создавать RCA если:
- расследование длилось более 30 минут;
- найден Root Cause;
- проблема может повториться;
- проблема важна для других разработчиков.

Хранить:

```text
rca/RCA-<topic>.md
```

Использовать:

```text
templates/rca-template.md
```

## Минимальный результат дня

Каждый день должен породить минимум один артефакт:
- Daily Report
- Lesson Learned
- RCA
- Knowledge Base Article

# Еженедельный процесс

Создать:

```text
weekly/YYYY-WXX.md
```

Использовать:

```text
PROMPT_WEEKLY_REVIEW.md
```

# Ежемесячный процесс

Создать:

```text
monthly/YYYY-MM.md
```

Использовать:

```text
PROMPT_MONTHLY_REVIEW.md
```

# Обновление системы

Перед обновлением:

```powershell
git add .
git commit -m "Backup before update"
```

Получить изменения:

```powershell
git pull
```

# Definition of Done

✅ Daily Report создан
✅ Lesson Learned сохранён
✅ RCA создан при необходимости
✅ Новые знания сохранены
✅ План на завтра сформирован
