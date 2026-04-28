# Functions - Виды объявления

---

# Function Declaration

```js
greet("Max"); // можно вызвать до объявления

function greet(name) {
    return `Hello, ${name}!`;
}
```

- **Описание:** объявление функции с ключевым словом `function`
- **Особенности:**
    - ✅ Можно использовать до объявления (hoisting)
    - ✅ Доступ к неявной переменной `arguments`
    - ✅ Свой контекст `this`
    - ✅ Можно перезаписать

## Hoisting (всплытие)

```js
sayHi(); // ✅ работает

function sayHi() {
    console.log("Hi!");
}
```

- JS при обработке кода поднимает все `function` объявления наверх их области видимости, как будто они написаны в начале файла

## **`arguments`**

```js
function sum() {
    console.log(arguments); // { 0: 1, 1: 2, 2: 3 }
    return arguments[0] + arguments[1];
}

sum(1, 2, 3);
```

- `arguments` - неявная переменная, содержит все переданные аргументы
- Доступна только в Function Declaration и Function Expression

---

# Function Expression

```js
const greet = function(name) {
    return `Hello, ${name}!`;
};
greet("Max");

// =============================== доп.
// кладём функцию в переменную как ссылку (ЭТО НЕ Function Expression!)
const log = console.log; 
log("test");
// =============================== доп.

const myFunc = function() { ... }; // Function Expression
const myArrow = () => { ... };    // Arrow Function Expression
```

- **Описание:** функция записывается как выражение и присваивается переменной
- **Особенности:**
    - ❌ Нельзя использовать до объявления (код становится очевиднее)
    - ❌ Нельзя перезаписать (если используется `const`)
    - ✅ Доступ к `arguments`
    - ✅ Свой контекст `this`

## Использование до объявления

```js
greet("Max"); // ❌ ReferenceError

const greet = function(name) {
    return `Hello, ${name}!`;
};
```

## Перезапись

```js
const greet = function() { return "Hi"; };
greet = function() { return "Hello"; }; // ❌ TypeError — const нельзя перезаписать

let greet2 = function() { return "Hi"; };
greet2 = function() { return "Hello"; }; // ✅ с let можно
```

---

# Arrow Function - современный и удобный подход (ES6+)

```js
const greet = (name) => {
    return `Hello, ${name}!`;
};

// Короче - неявный return (без {} и return)
const greet = (name) => `Hello, ${name}!`;

// Ещё короче - если один аргумент, скобки необязательны (но лучше оставлять для будущего расширения сркипта)
const showName = name => `Hi, ${name}!`;

showName("Alex");
```

- **Описание:** современная короткая запись функции, присваивается переменной
- **Особенности:**
    - ❌ Нельзя использовать до объявления
    - ❌ Нет доступа к `arguments`
    - ❌ Нет своего `this` (берёт из родительской области видимости)
    - ✅ Неявный возврат (если одна строка без `{}`)

## Неявный возврат объекта

- Для объектов нужны круглые скобки - иначе `{}` воспримутся как тело функции:

```js
const sum = (a, b) => a + b;

const getUser = () => ({ name: "Max", age: 28 }); // () обязательны
```

## Копирование функции

```js
const fn1 = () => "text";
const fn2 = fn1; // копирование по ссылке
```
