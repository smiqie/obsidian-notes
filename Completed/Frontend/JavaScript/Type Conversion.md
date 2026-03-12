# Type Conversion

---

# Явное преобразование (explicit) - хорошая практика ✅

## Число → Строка

```js
let value = 10; // number

// 1. Конкатенация с пустой строкой
value = value + ""; // '10' string

// 2. Шаблонная строка
value = `${value}`; // '10' string
value = `${value} привет`; // '10 привет' string

// 3. Метод toString()
value = value.toString(); // '10' string

// 4. Функция String()
value = String(value); // '10' string (ЛУЧШИЙ СПОСОБ)
```

---

## Строка → Число

```js
let value = '10'; // string

// 1. Функция Number()
value = Number(value); // 10 number (ЛУЧШИЙ СПОСОБ)

// 2. Унарный оператор +
value = +value; // 10 number

// 3. parseInt() - для целых чисел
value = parseInt(value); // 10 number

// 4. parseFloat() - для дробных чисел
value = parseFloat(value); // 10 number
```

**Разница между `parseInt()` и `Number()`:**

```js
let value = '10a';

Number(value);    // NaN (строгое преобразование)
parseInt(value);  // 10 (парсит до первого нечислового символа)
```

- `parseInt()` - более серьезная функция, парсит строку до первого нечислового символа
- `Number()` - строгое преобразование, вернет `NaN` если строка не является числом

---

## Преобразование в Boolean

```js
Boolean(0);         // false
Boolean('');        // false
Boolean(null);      // false
Boolean(undefined); // false
Boolean(NaN);       // false

Boolean(1);         // true
Boolean('text');    // true
Boolean(' ');       // true (строка с пробелом)
Boolean([]);        // true
Boolean({});        // true
```

**Falsy values** (преобразуются в `false`):

- `0`
- `''` (пустая строка)
- `null`
- `undefined`
- `NaN`

**Truthy values** (все остальное) - преобразуются в `true`

---

# Неявное преобразование (implicit) - плохая практика ❌

```js
const num = 111;
const str = '222';

console.log(num + str);  // '111222' string (число → строка)
console.log('16' / '8'); // 2 number (строка → число)
```

**Не нужно все это запоминать!** Просто понять особенности языка. В коде писать такие конструкции - **плохая практика**!

**Могут спрашивать на собеседованиях!**

---

## Примеры неявного преобразования

```js
// Сложение (+) - приводит к строке
10 + '10';  // '1010' string

// Другие операторы - приводят к числу
10 * '10';  // 100 number
10 / '10';  // 1 number
10 - '10';  // 0 number
10 % '10';  // 0 number

// Boolean → Number
10 + true;  // 11 number (true = 1, false = 0)
10 + false; // 10 number

// null → Number
10 + null;  // 10 number (null = 0)

// undefined → Number
10 + undefined; // NaN (undefined не приводится к числу)

// NaN
10 + NaN;   // NaN

// Массивы и объекты
10 + [];    // '10' string
10 + {};    // '10[object Object]' string

// Boolean + Boolean
true + true; // 2 number (1 + 1)
```

---

# Рекомендации

✅ **Всегда используйте явное преобразование:**

```js
const num = 10;
const str = '5';

// ✅ Хорошо
const result = num + Number(str); // 15

// ❌ Плохо
const result = num + str; // '105'
```

✅ **Лучшие способы преобразования:**

- `String(value)` - для строки
- `Number(value)` - для числа
- `Boolean(value)` - для boolean