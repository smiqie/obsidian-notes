# Working with Numbers

---

# Способы создания числа

```js
// 1. Динамическая типизация (ЛУЧШИЙ СПОСОБ)
let a = 10;

// 2. Функция Number()
let b = Number(10);

// 3. Оператор new (НЕ РЕКОМЕНДУЕТСЯ)
let c = new Number(100);
```

**Разница между способами:**

```js
let a = 10;
let b = Number(10);
let c = new Number(100);

console.log(typeof a); // 'number'
console.log(typeof b); // 'number'
console.log(typeof c); // 'object' ❌

// Чтобы получить значение из объекта Number:
console.log(c.valueOf()); // 100
```

**Вывод:** лучше использовать 1-й или 2-й способ. 3-й способ создает `object`, а не `number`!

---

# Свойства объекта `Number`

## `Number.MAX_VALUE` - максимальное число

```js
console.log(Number.MAX_VALUE); // 1.7976931348623157e+308
```

- максимальное число которое может быть у типа `number`

## `Number.MIN_VALUE` - минимальное положительное число

```js
console.log(Number.MIN_VALUE); // 5e-324
```

- минимальное **положительное** число (близкое к нулю)

## `Number.MAX_SAFE_INTEGER` - максимальное безопасное целое число

```js
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
```

- максимальное целое число для безопасных вычислений

## `Number.MIN_SAFE_INTEGER` - минимальное безопасное целое число

```js
console.log(Number.MIN_SAFE_INTEGER); // -9007199254740991
```

- минимальное целое число для безопасных вычислений

## `Number.POSITIVE_INFINITY` - положительная бесконечность

```js
console.log(Number.POSITIVE_INFINITY); // Infinity

100 / 0; // Infinity
```

## `Number.NEGATIVE_INFINITY` - отрицательная бесконечность

```js
console.log(Number.NEGATIVE_INFINITY); // -Infinity

-100 / 0; // -Infinity
```

## `Number.NaN` - Not a Number

```js
console.log(Number.NaN); // NaN

'Word' / 100; // NaN
```

---

# Методы у экземпляров чисел

## `toFixed()` - округление дробной части

```js
let num = 20.222;

num.toFixed(2);  // '20.22' (2 знака после запятой)
num.toFixed(1);  // '20.2' (1 знак после запятой)
num.toFixed(0);  // '20' (без дробной части)
num.toFixed();   // '20' (без дробной части)
```

**Параметры:**

- количество знаков после запятой (по умолчанию `0`)

**Важно:** возвращает **строку**!

```js
let result = parseFloat(10.12345.toFixed(3)); // 10.123 number
```

## `toPrecision()` - точное количество цифр

```js
let num = 20.222;

num.toPrecision(3); // '20.2' (всего 3 цифры)
num.toPrecision(4); // '20.22' (всего 4 цифры)
num.toPrecision(2); // '20' (всего 2 цифры)
```

**Параметры:**

- общее количество **значащих цифр** (отсчет от начала числа, не от дробной части)

**Важно:** возвращает **строку**!

## `toString()` - преобразование в строку

```js
let num = 123;

num.toString(); // '123'
```

- преобразует число в строку

## `valueOf()` - получение значения

```js
let num = new Number(100);

console.log(num.valueOf()); // 100
```

- возвращает примитивное значение числа
- используется когда число создано через `new Number()`

---

# Особенности работы с числами

## Деление на ноль

```js
100 / 0;    // Infinity
-100 / 0;   // -Infinity
```

---

## NaN (Not a Number)

```js
'Word' / 100;  // NaN
NaN + 10;      // NaN
NaN * 2;       // NaN
```

- любая операция с `NaN` возвращает `NaN`

---

# Диапазон безопасных целых чисел

```js
Number.MIN_SAFE_INTEGER; // -9007199254740991
Number.MAX_SAFE_INTEGER; //  9007199254740991
```

- для чисел **больше** этого диапазона нужно использовать `BigInt`