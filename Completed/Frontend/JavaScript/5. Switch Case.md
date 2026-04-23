# Switch Case

**Switch Case** - более наглядный способ сравнивать выражение с несколькими вариантами (в отличие от `if / else if / else`)

---

# Базовый синтаксис

```js
const day = 3;

switch (day) {
    case 1:
        console.log('Понедельник');
        break;
    case 2:
        console.log('Вторник');
        break;
    case 3:
        console.log('Среда');
        break;
    default:
        console.log('Другой день');
}
```

**Как работает:**

1. Сравнивает значение в `switch(day)` с каждым `case`
2. Если совпадение - выполняет код в этом `case`
3. `break` - завершает выполнение `switch`
4. `default` - выполнится если ни один `case` не подошел (аналог `else`)

**Важно:**

- `break` **обязателен** в каждом `case` (иначе код "провалится" в следующий `case`)
- `default` - `break` не обязателен (switch заканчивает работу)
- сравнение **строгое** (`===`), не приводит типы

---

# Объединение case

```js
const day = 3;

switch (day) {
    case 1:
    case 2:
    case 3:
        console.log('числа 1 / 2 / 3');
        break;
    case 4:
    case 5:
        console.log('числа 4 / 5');
        break;
    default:
        console.log('другое число');
}
```

- несколько `case` могут выполнять один и тот же код
- просто не ставим `break` между ними

---

# Строгое сравнение (===)

```js
const day = 3;

switch (day) {
    case 1:
        console.log('Один');
        break;
    case "3":
        console.log('СЮДА МЫ НЕ ПОПАДЕМ');
        break; // не попадем т.к. 3 !== "3"
    case 3:
        console.log('Три'); // ✅ попадем сюда
        break;
    default:
        console.log('другое число');
}
```

**Важно:** `switch` использует **строгое сравнение** (`===`)

- `3 !== "3"` - число не равно строке

---

# Проверка диапазонов - `switch(true)`

## Пример 1: оценки

```js
const score = 85;

switch (true) {
    case score >= 90:
        console.log('Отлично');
        break;
    case score >= 70:
        console.log('Хорошо'); // ✅ выполнится (85 >= 70 = true)
        break;
    case score >= 50:
        console.log('Удовлетворительно');
        break;
    default:
        console.log('Неудовлетворительно');
}
```

## Пример 2: время суток

```js
const today = new Date();
const hour = today.getHours(); // например, 14

switch (true) {
    case hour < 12:
        console.log('Good Morning!');
        break;
    case hour < 18:
        console.log('Good Day!'); // ✅ выполнится (14 < 18 = true)
        break;
    case hour < 22:
        console.log('Good Evening!');
        break;
    default:
        console.log('Good Night!');
}
```

## Пример 3

```js
switch (true) {
    case (age >= 0 && age <= 12):
        console.log("Ребёнок");
        break;
    case (age >= 13 && age <= 17):
        console.log("Подросток");
        break;
    case (age >= 18 && age <= 64):
        console.log("Взрослый");
        break;
    case (age >= 65):
        console.log("Пожилой человек");
        break;
    default:
        console.log("Некорректный ввод");
        break;
}
```

# Почему `switch(true)` для диапазонов?

**Как работает `switch`:**

```js
switch (выражение) {
    case значение1:
        // выполнится если выражение === значение1
}
```

**Обычный switch:**

```js
const day = 3;

switch (day) {       // day = 3
    case 1:          // 3 === 1? → false
        break;
    case 3:          // 3 === 3? → true ✅
        console.log('Три');
        break;
}
```

**Switch с диапазонами:**

```js
const score = 85;

switch (true) {           // true
    case score >= 90:     // true === (85 >= 90)? → true === false? → false
        break;
    case score >= 70:     // true === (85 >= 70)? → true === true? → true ✅
        console.log('Хорошо');
        break;
}
```

**Объяснение:**

1. В `switch(true)` мы **всегда** сравниваем с `true`
2. Каждый `case` содержит **условие** (например, `score >= 70`)
3. Это условие возвращает `true` или `false`
4. `switch` проверяет: `true === (результат условия)?`
5. Если условие вернуло `true` → совпадение найдено ✅
