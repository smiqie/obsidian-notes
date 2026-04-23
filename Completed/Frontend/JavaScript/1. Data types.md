# Data Types

---

# Типы данных в JavaScript

|Тип|Категория|Пример|Описание|
|---|---|---|---|
|`number`|примитивный|`10`, `3.14`|целые и дробные числа|
|`string`|примитивный|`'Hello'`, `"World"`|текст|
|`boolean`|примитивный|`true`, `false`|логические значения|
|`undefined`|примитивный|`undefined`|неинициализированная переменная|
|`null`|примитивный|`null`|явно пустое значение|
|`bigint`|примитивный|`9007199254740991n`|большие числа|
|`symbol`|примитивный|`Symbol('id')`|уникальные идентификаторы|
|`object`|ссылочный|`{a: 1}`, `[1,2,3]`|объекты, массивы, функции|

---

# Примитивные типы

## `number` - числа

```js
const age = 25;           // целое число
const price = 19.99;      // дробное число
```

- целые и дробные числа
- хранятся в **стеке**

**Читаемость больших чисел:**

```js
const million = 1_000_000; // ✅ удобно читать
const billion = 1000000000; // ❌ неудобно читать
```

**Специальное значение `NaN` (Not a Number):**

```js
const result = 'text' / 2; // NaN
console.log(typeof NaN);   // 'number'
```

---

## `string` - строки

```js
const name = 'Alex';
const city = "Moscow";
const message = `Hello, ${name}!`; // шаблонная строка
```

- текст в одинарных `'`, двойных `"` или обратных кавычках `` ` ``
- хранятся в **стеке**

---

## `boolean` - логические значения

```js
const isActive = true;
const isEnabled = false;
```

- только два значения: `true` или `false`
- хранятся в **стеке**

**Именование boolean переменных:**

- обычно начинаются с `is`, `has`, `can`
	- примеры: `isActive`, `isEnabled`, `isConfirmed`, `isLoading`, `hasAccess`, `canEdit`

---

## `undefined` - неопределенное значение

```js
let x;
console.log(x); // undefined

function test() {
    // функция без return возвращает undefined
}
console.log(test()); // undefined

const user = document.querySelector('.user'); // если элемент не найден - undefined
```

- возникает **автоматически** когда:
    - переменная объявлена, но не присвоено значение
    - функция не возвращает значение (нет `return`)
    - элемент не найден на странице
- хранится в **стеке**

❌ **Плохой тон** (присваивать undefined вручную):

```js
let name = undefined;
```

✅ **Хорошо** (использовать null):

```js
let name = null;
```

---

## `null` - пустое значение

```js
let data = null; // переменная пока пустая, ждём значение
```

- используется для **явного** обнуления значения
- обычно присваивают переменным, значение которых еще не получено (например, с сервера)
- хранится в **стеке**

**Разница между `null` и `undefined`:**

- `null` - значение **присвоено** (явно пустое)
- `undefined` - значение **не присвоено** (отсутствует)

```js
let a = null;      // явно пустое
let b;             // неопределенное (undefined)
```

**Особенность `typeof null`:**

```js
console.log(typeof null); // 'object' ❌
```

- `typeof null` возвращает `'object'` - это **баг** в JavaScript
- так сложилось исторически (ошибка была оставлена для совместимости со старыми проектами)
- на самом деле `null` - это **примитивный** тип

---

## `bigint` - большие числа

```js
const big = 9007199254740991n;
const huge = 123456789012345678901234567890n;
```

- для чисел больше `Number.MAX_SAFE_INTEGER` (9007199254740991)
- добавляется `n` в конце числа
- хранятся в **стеке**

**Операции только с другими bigint:**

```js
2n + 1;   // ❌ ошибка
2n + 1n;  // ✅ работает

const result = 4385769843265874326587432687564328756874326528743265n + 324324324n; // ✅
```

- чаще всего используется просто `number`
	- `bigint` для узких/специфических проектов

---

## `symbol` - уникальные идентификаторы

```js
const id = Symbol('123');
const userId = Symbol('user');

console.log(id === Symbol('123')); // false (каждый Symbol уникален)
```

- создает **уникальное** и **неизменяемое** значение
- используется для уникальных идентификаторов в объектах
- хранится в **стеке**
- используется **не очень часто**

**Пример использования:**

```js
const id = Symbol('id');

const user = {
    name: 'Alex',
    [id]: 123 // уникальное свойство
};

console.log(user[id]); // 123
```

---

# Ссылочный тип

## `object` - объекты

```js
const person = {
    name: 'Alex', // ключ: значение
    age: 18
};
```

- данные хранятся в **куче** (переменная хранит **ссылку** на объект в памяти), а в стеке хранится ссылка на данные

**Сокращенная запись (если ключ и значение совпадают):**

```js
const id = Symbol('123');
const isActive = true;

const person = {
    name: 'Alex',
    age: 18,
    id: id,       // можно сократить
    isActive: isActive // можно сократить
};

// Сокращенная запись
const person = {
    name: 'Alex',
    age: 18,
    id,        // ✅ id: id
    isActive   // ✅ isActive: isActive
};
```

---

## Массивы (arrays) - ссылочный тип

```js
const numArray = [1, 2, 3, 4, 5];
const users = ['Alex', 'John', 'Jane'];
```

- массив - это **объект** (не самостоятельный тип данных)
- хранится в **куче**

---

## Функции (functions) - ссылочный тип

```js
function info() {
    return 'hi';
}

console.log(typeof info); // 'function'
```

- функция - это **объект**
- хранится в **куче**
- объявляется с помощью ключевого слова `function`
- `return` - возвращает значение из функции

---

# Проверка типа данных - `typeof`

```js
console.log(typeof 10);        // 'number'
console.log(typeof 'text');    // 'string'
console.log(typeof true);      // 'boolean'
console.log(typeof undefined); // 'undefined'
console.log(typeof null);      // 'object' ❌ (баг)
console.log(typeof 123n);      // 'bigint'
console.log(typeof Symbol());  // 'symbol'
console.log(typeof {});        // 'object'
console.log(typeof []);        // 'object'
console.log(typeof function(){}); // 'function'
```