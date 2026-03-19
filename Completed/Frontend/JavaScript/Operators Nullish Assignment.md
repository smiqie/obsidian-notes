# Operators Nullish Assignment

---

# `??` - оператор нулевого слияния (Nullish Coalescing)

Возвращает **правый операнд**, если левый равен `null` или `undefined`. Иначе возвращает **левый операнд**.

```js
const res = null ?? 100;      // 100
const res = undefined ?? 0;   // 0
const res = "hi" ?? 100;      // "hi"
const res = false ?? 10;      // false (false !== null/undefined)
const res = 0 ?? 10;          // 0 (0 !== null/undefined)
```

> **Важно:** `??` срабатывает **только** на `null` и `undefined`
> 
> Не срабатывает на `false`, `0`, `''` (в отличие от `||`)

**Разница между `??` и `||`:**

```js
// || возвращает первое truthy значение
const a = 0 || 100;      // 100 (0 - falsy)
const b = false || 100;  // 100 (false - falsy)

// ?? возвращает правый только если левый null/undefined
const c = 0 ?? 100;      // 0 (0 !== null/undefined)
const d = false ?? 100;  // false (false !== null/undefined)
```

---

# Logical Assignment (логическое присваивание)

## `||=` - присваивание с ИЛИ

```js
let a = null;
a = a || 10; // 10

// Сокращение:
a ||= 10; // аналогично: a = a || 10;
```

> Присваивает значение, если переменная **falsy**

**Примеры:**

```js
let x = 0;
x ||= 5;  // x = 5 (0 - falsy)

let y = 'Hello';
y ||= 'Hi';  // y = 'Hello' (уже truthy, не изменится)
```

---

## `&&=` - присваивание с И

```js
let b = 1;
b = b && 2; // 2

// Сокращение:
b &&= 2; // аналогично: b = b && 2;
```

> Присваивает значение, если переменная **truthy**

**Примеры:**

```js
let x = 5;
x &&= 10;  // x = 10 (5 - truthy)

let y = 0;
y &&= 10;  // y = 0 (0 - falsy, не изменится)
```

---

## `??=` - присваивание с нулевым слиянием

```js
let c = undefined;
c = c ?? 10; // 10

// Сокращение:
c ??= 10; // аналогично: c = c ?? 10;
```

> Присваивает значение, если переменная **null или undefined**

**Примеры:**

```js
let a = null;
a ??= 10;  // a = 10 (null)

let b = undefined;
b ??= 20;  // b = 20 (undefined)

let c = false;
c ??= 10;  // c = false (false !== null/undefined, не изменится)

let d = 0;
d ??= 10;  // d = 0 (0 !== null/undefined, не изменится)
```

---

# Сравнение операторов присваивания

**`||=` - присваивает когда значение falsy**
```js
let a = 0;
a ||= 5;  // 5
```

**`&&=` - присваивает когда значение truthy**
```js
let b = 5;
b &&= 10;  // 10
```

**`??=` - присваивает когда значение null или undefined**
```js
let c = null;
c ??= 10;  // 10
```

**Примеры:**

```js
// ||= - для falsy значений
let a = '';
a ||= 'default';  // 'default'

// &&= - для truthy значений
let b = 'text';
b &&= 'updated';  // 'updated'

// ??= - только для null/undefined
let c = false;
c ??= 'default';  // false (не изменится)
```