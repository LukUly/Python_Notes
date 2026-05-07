# Модуль datetime

## Что это?
Модуль для работы с датами, временем и временными интервалами.

```python
import datetime as dt
```

---

## Основные типы

| Тип | Описание | Пример |
|-----|----------|--------|
| `date` | Дата (год, месяц, день) | 2024-12-31 |
| `time` | Время (час, минута, секунда) | 23:59:59 |
| `datetime` | Дата + время | 2024-12-31 23:59:59 |
| `timedelta` | Разница во времени | 5 days, 3:00:00 |

---

## date — работа с датой

### Создание и текущая дата

```python
# Текущая дата
today = dt.date.today()           # 2024-05-15

# Конкретная дата
birthday = dt.date(2007, 7, 1)    # 2007-07-01
```

### Атрибуты

```python
d = dt.date(2024, 12, 31)

d.year      # 2024
d.month     # 12
d.day       # 31
```

### Дни недели

```python
d = dt.date(2024, 12, 31)

d.weekday()      # 1 (пн=0, вт=1, ..., вс=6)
d.isoweekday()   # 2 (пн=1, вт=2, ..., вс=7)
```

---

## time — время

### Создание

```python
# Часы, минуты, секунды
t = dt.time(14, 30, 25)           # 14:30:25

# С микросекундами
t = dt.time(14, 30, 25, 500000)   # 14:30:25.500000
```

### Атрибуты

```python
t.hour        # 14
t.minute      # 30
t.second      # 25
t.microsecond # 500000
```

---

## datetime — дата и время вместе

### Создание и текущий момент

```python
# Текущие дата и время
now = dt.datetime.now()           # 2024-05-15 14:30:25.123456

# Конкретные дата и время
new_year = dt.datetime(2024, 12, 31, 23, 59, 59)

# Год, месяц, день — обязательно. 
# Время можно не указывать (будет 0)
date_only = dt.datetime(2024, 12, 31)  # 2024-12-31 00:00:00
```

### Атрибуты (все, что есть у date и time)

```python
now = dt.datetime.now()

now.year        # 2024
now.month       # 5
now.day         # 15
now.hour        # 14
now.minute      # 30
now.second      # 25
```

### Извлечение date и time

```python
now = dt.datetime.now()

now.date()      # вернёт dt.date (только дату)
now.time()      # вернёт dt.time (только время)
```

---

## timedelta — разница во времени

### Создание интервала

```python
# Разные способы
delta = dt.timedelta(days=5, hours=3, minutes=30)
delta = dt.timedelta(days=7)
delta = dt.timedelta(weeks=2)       # 14 дней
delta = dt.timedelta(hours=24)      # 1 день
```

**Что можно указывать:**
- `days`
- `seconds`
- `minutes` (превращаются в `seconds`)
- `hours` (превращаются в `seconds`)
- `weeks` (превращаются в `days`)

**Нельзя:** месяцы и годы (разное количество дней).

### Атрибуты timedelta

```python
delta = dt.timedelta(days=5, hours=3)

delta.days      # 5
delta.seconds   # 10800 (3 часа * 3600)
# months и years нет!
```

---

## Операции с датами и временем

### date + timedelta

```python
today = dt.date(2024, 5, 15)
delta = dt.timedelta(days=10)

future = today + delta      # 2024-05-25
past = today - delta        # 2024-05-05
```

### datetime + timedelta

```python
now = dt.datetime(2024, 5, 15, 12, 0)
delta = dt.timedelta(hours=5, minutes=30)

later = now + delta         # 2024-05-15 17:30:00
earlier = now - delta       # 2024-05-15 06:30:00
```

### Разница между датами

```python
date1 = dt.date(2024, 12, 31)
date2 = dt.date(2024, 5, 15)

diff = date1 - date2        # timedelta(230 days)
print(diff.days)            # 230
```

### Сравнение

```python
date1 = dt.date(2024, 12, 31)
date2 = dt.date(2024, 5, 15)

date1 > date2      # True
date1 < date2      # False
```

### Операции с timedelta

```python
d1 = dt.timedelta(days=4, hours=4)
d2 = dt.timedelta(days=1, hours=1)

d1 + d2     # 5 days, 5:00:00
d1 - d2     # 3 days, 3:00:00
d1 * 10     # 41 days, 16:00:00
d1 / 10     # 10:00:00
d1 / d2     # 4.0
```

---

## Форматирование: дата → строка (strftime)

### Базовое использование

```python
now = dt.datetime.now()

# Самые частые форматы
now.strftime("%d.%m.%Y")      # 15.05.2024
now.strftime("%Y-%m-%d")      # 2024-05-15
now.strftime("%H:%M:%S")      # 14:30:25
now.strftime("%d %B %Y")      # 15 May 2024
```

### Основные коды форматирования

| Код | Значение | Пример |
|-----|----------|--------|
| `%d` | День месяца (01-31) | 15 |
| `%m` | Месяц (01-12) | 05 |
| `%Y` | Год (4 цифры) | 2024 |
| `%y` | Год (2 цифры) | 24 |
| `%H` | Час (00-23) | 14 |
| `%I` | Час (01-12) | 02 |
| `%M` | Минуты (00-59) | 30 |
| `%S` | Секунды (00-59) | 25 |
| `%p` | AM/PM | PM |
| `%A` | Полный день недели | Tuesday |
| `%a` | Сокращённый день | Tue |
| `%B` | Полное название месяца | May |
| `%b` | Сокращённое название | May |

### Примеры комбинаций

```python
now = dt.datetime.now()

# Русскоязычный формат
now.strftime("%d.%m.%Y %H:%M")           # 15.05.2024 14:30

# ISO формат
now.strftime("%Y-%m-%dT%H:%M:%S")        # 2024-05-15T14:30:25

# "Сегодня 15 мая 2024 года, 14:30"
now.strftime("%d %B %Y года, %H:%M")     # 15 May 2024 года, 14:30

# День недели
now.strftime("%A")                       # Tuesday
```

---

## Парсинг: строка → дата (strptime)

### Базовое использование

```python
# Превращаем строку в datetime
date_str = "2024-12-31 23:59"
new_year = dt.datetime.strptime(date_str, "%Y-%m-%d %H:%M")

# Теперь можно использовать как datetime
print(new_year.year)   # 2024
print(new_year.hour)   # 23
```

### Примеры парсинга

```python
# Русский формат
date_str = "15.05.2024"
d = dt.datetime.strptime(date_str, "%d.%m.%Y")

# С временем
datetime_str = "15.05.2024 14:30:25"
d = dt.datetime.strptime(datetime_str, "%d.%m.%Y %H:%M:%S")

# С названием месяца
date_str = "15 May 2024"
d = dt.datetime.strptime(date_str, "%d %B %Y")
```

---

## Полезные примеры

### Сколько дней осталось до Нового года?

```python
today = dt.date.today()
new_year = dt.date(today.year + 1, 1, 1)
days_left = (new_year - today).days
print(f"До Нового года осталось {days_left} дней")
```

### Возраст по дате рождения

```python
birthday = dt.date(2010, 5, 20)
today = dt.date.today()
age = today.year - birthday.year

# Если день рождения ещё не был в этом году
if today < dt.date(today.year, birthday.month, birthday.day):
    age -= 1

print(f"Возраст: {age} лет")
```

### Проверка срока годности

```python
production = dt.date(2024, 5, 1)
expire_days = 30
expire_date = production + dt.timedelta(days=expire_days)

if dt.date.today() > expire_date:
    print("Срок годности истёк!")
else:
    print("Всё свежее")
```

### Вычисление дня недели для любой даты

```python
# Какой день недели был 12 июня 2000 года?
date = dt.date(2000, 6, 12)
weekdays = ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"]
print(weekdays[date.weekday()])  # Пн
```

### Текущее время в разных форматах

```python
now = dt.datetime.now()

print(now.strftime("%H:%M"))           # 14:30
print(now.strftime("%I:%M %p"))        # 02:30 PM
print(now.strftime("%H:%M:%S"))        # 14:30:25
```

---

## Обработка BOM в UTF-8

Если файл начинается с `\ufeff`:

```python
# Вместо encoding="utf-8" используйте:
with open("file.txt", encoding="utf-8-sig") as f:
    content = f.read()  # BOM автоматически удалится
```

---

## Обработка ошибок кодировки

```python
# Пропустить нечитаемые символы
open("file.txt", "r", encoding="utf-8", errors="ignore")

# Заменить на ?
open("file.txt", "r", encoding="cp1251", errors="replace")
```

---

## Краткая памятка

| Что нужно | Как сделать |
|-----------|-------------|
| Текущая дата | `dt.date.today()` |
| Текущие дата и время | `dt.datetime.now()` |
| Создать конкретную дату | `dt.date(год, месяц, день)` |
| Создать интервал | `dt.timedelta(days=5, hours=3)` |
| Прибавить дни | `date + timedelta` |
| Найти разницу | `date1 - date2` |
| Сравнить даты | `date1 > date2` |
| Дата → строка | `date.strftime("%d.%m.%Y")` |
| Строка → дата | `dt.datetime.strptime(строка, формат)` |
| День недели (0-6) | `date.weekday()` |
| День недели (1-7) | `date.isoweekday()` |

> **P. S.** Никогда не откладывай на `dt.date.today() + dt.timedelta(days=1)` то, что можно сделать `dt.date.today()`
