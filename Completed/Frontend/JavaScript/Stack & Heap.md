# Stack & Heap

---

# Хранение в памяти

## Примитивные типы - Stack (стек)

Значения примитивных типов хранятся **прямо в переменной** (в стеке):

```js
const name = 'Alex';
const age = 25;
```

> **Примитивные типы:** `undefined`, `null`, `boolean`, `number`, `string`, `symbol`, `bigint`
> 
> Хранятся **напрямую** в переменной

## Ссылочные типы - Heap (куча)

Значения ссылочных типов хранятся **не в переменной напрямую**, а **в области памяти называемой кучей (heap)**, а переменная хранит только **ссылку (адрес)** на эту область памяти:

```js
const person = {
    name: 'Nika',
    age: 20
};
```

**Как хранится:**

- **Stack (стек)** - переменная `person` хранит ссылку на данные
- **Heap (куча)** - данные объекта `{ name: 'Nika', age: 20 }`

> **Ссылочные типы:** объекты (в том числе массивы и функции) и экземпляры пользовательских классов
> 
> Переменная хранит **ссылку**, данные в **куче**

---

# Присваивание переменных

## Примитивные типы - копирование значения

```js
const name = 'Alex';
const age = 25;
const person = {
    name: 'Nika',
    age: 20
};
```

**В памяти:**

- Stack: `name = 'Alex'`
- Stack: `age = 25`
- Stack: `person` → ссылка на кучу
- Heap: `{ name: 'Nika', age: 20 }`

> При присваивании примитива создается **новое значение** в стеке

## Ссылочные типы - копирование ссылки

```js
const person = {
    name: 'Nika',
    age: 20
};

const newPerson = person; // копируется ссылка, НЕ объект!

newPerson.name = 'Sam';
newPerson.age = 35;

console.log(person.name); // 'Sam' (изменился!)
console.log(person.age);  // 35 (изменился!)
```

**Что происходит:**

- `person` хранит ссылку на объект в куче
- `newPerson = person` копирует **ссылку**, не создает новый объект
- Обе переменные указывают на **один и тот же объект** в куче
- Изменение через `newPerson` изменяет объект, на который ссылается и `person`

**В памяти:**

- Stack: `person` → ссылка на кучу
- Stack: `newPerson` → **та же ссылка** на кучу
- Heap: `{ name: 'Sam', age: 35 }` (один объект)

> **Важно:** у нескольких ссылочных переменных может быть одна ссылка на данные (на общую область памяти)

---

# Примеры

## Пример 1: Изменение объекта через разные переменные

```js
const person = {
    name: 'Nika',
    age: 20
};

const newName = name; // примитив - копируется значение
const newPerson = person; // объект - копируется ссылка

newPerson.name = 'Sam';
newPerson.age = 35;

console.log(person); // { name: 'Sam', age: 35 } ← изменился!
console.log(newPerson); // { name: 'Sam', age: 35 }
```

> Обе переменные ссылаются на **один объект** в памяти

---

## Пример 2: Несколько ссылок на один объект

```js
const obj = { value: 10 };

const ref1 = obj;
const ref2 = obj;
const ref3 = obj;

ref1.value = 20;

console.log(obj.value);  // 20
console.log(ref2.value); // 20
console.log(ref3.value); // 20
```

> Все переменные указывают на **один объект** в куче

---

# Сравнение

## Примитивы - сравниваются по значению

```js
const a = 10;
const b = 10;

console.log(a === b); // true (одинаковые значения)
```

## Ссылочные типы - сравниваются по ссылке (адресу)

```js
const obj1 = { value: 10 };
const obj2 = { value: 10 };

console.log(obj1 === obj2); // false (разные объекты в памяти)

const obj3 = obj1;
console.log(obj1 === obj3); // true (одна и та же ссылка)
```

> Два объекта с одинаковым содержимым **НЕ равны**, если это разные объекты в памяти

---

# Копирование объектов

## Поверхностное копирование (shallow copy)

```js
const person = { name: 'Alex', age: 25 };

// Способ 1: spread оператор
const copy1 = { ...person };

// Способ 2: Object.assign
const copy2 = Object.assign({}, person);

copy1.name = 'John';

console.log(person.name); // 'Alex' (не изменился)
console.log(copy1.name);  // 'John'
```

> Создается **новый объект** с копией свойств, а не копирование ссылки