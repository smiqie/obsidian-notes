
---
## 16. Function Declaration

```js
function greet(name) {
    return `Hello, ${name}!`;
}

greet('Max'); // можно вызвать до объявления
```

**Особенности:**

- ✅ Можно использовать до объявления (hoisting - поднятие)
- ✅ Можно перезаписать
- ✅ Доступ к неявной переменной `arguments`
- ✅ Свой контекст `this`

**Hoisting:**

```js
sayHi(); // ✅ работает

function sayHi() {
    console.log('Hi!');
}
```

JS при обработке кода поднимает все `function` наверх их области видимости, как будто они объявлены в начале файла.

**Arguments:**

```js
function sum() {
    console.log(arguments); // [1, 2, 3]
    return arguments[0] + arguments[1];
}

sum(1, 2, 3);
```

---

## 17. Function Expression

Функция записывается как выражение и присваивается переменной.

```js
const greet = function(name) {
    return `Hello, ${name}!`;
};

greet('Max');
```

**Особенности:**

- ❌ Нельзя использовать до объявления (код становится очевиднее)
- ❌ Нельзя перезаписать (если используется `const`)
- ✅ Доступ к `arguments`
- ✅ Свой контекст `this`

**Использование до объявления:**

```js
greet('Max'); // ❌ ReferenceError

const greet = function(name) {
    return `Hello, ${name}!`;
};
```

**Перезапись:**

```js
const greet = function() { return 'Hi'; };
greet = function() { return 'Hello'; }; // ❌ TypeError с const

let greet2 = function() { return 'Hi'; };
greet2 = function() { return 'Hello'; }; // ✅ работает с let
```

---

## 18. Arrow Functions (современный подход)

```js
const greet = (name) => {
    return `Hello, ${name}!`;
};

// или короче
const greet = (name) => `Hello, ${name}!`;
```

**Особенности:**

- ❌ Нельзя использовать до объявления
- ❌ Нет доступа к `arguments`
- ❌ Нет своего `this` (берёт из родительской области)
- ✅ Неявный возврат (если одна строка)

**Неявный возврат:**

```js
const sum = (a, b) => a + b; // без return и {}

const getUser = () => ({ name: 'Max', age: 28 }); // для объектов нужны ()
```

**Копирование функций:**

```js
const fn1 = () => 'text';
const fn2 = fn1; // копирование по ссылке
```

**Функции-колбеки:**

```js
const msg = (action1, action2) => {
    action1();
    action2();
};

msg(
    () => console.log('1'),
    () => console.log('2')
);

// или с промежуточными переменными
const fn1 = () => console.log('1');
const fn2 = () => console.log('2');
msg(fn1, fn2);
```

**Функция возвращает функцию:**

```js
const validate = (hasAccess) => 
    hasAccess 
        ? () => console.log('Доступ разрешён')
        : () => console.log('Доступ запрещён');

const logMsg = validate(false);
logMsg(); // "Доступ запрещён"
```

---

## 19. Лучшие практики работы с функциями

- Функция должна выполнять только одну задачу

- Имя начинается с **глагола** + уточняющее **существительное** (нпр., validateEmail, isActive, calculateTotal и тд.)

- При беглом прочтении кода достаточно прочитать имя функции, чтобы понять что она делает.

```js
// ✅ Понятно без чтения тела функции
checkUserPermissions();
fetchDataFromAPI();
renderUserProfile();
```

---

## 20. Параметры функций

### Параметры и аргументы

```js
function greet(name, age) { // name, age - параметры
    console.log(name, age);
}

greet('Max', 28); // 'Max', 28 - аргументы
```

### Параметры по умолчанию

Параметры по умолчанию принято указывать **в конце**.

```js
// ✅ Хорошо
function greet(name, greeting = 'Hello') {
    return `${greeting}, ${name}!`;
}

greet('Max'); // "Hello, Max!"
greet('Max', 'Hi'); // "Hi, Max!"
```

### Проверка параметров

Проверка на `null`, `undefined`, пустую строку и другие falsy значения:

```js
function processData(data) {
    if (!data) {
        console.log('Нет данных');
        return;
    }
    // обработка данных
}
```