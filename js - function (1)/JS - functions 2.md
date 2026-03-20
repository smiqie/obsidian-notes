

## 15. Function Declaration - объявление функции с поомзбю клчевого слова function? функцию можно вызвать до ее объявления?

```js
// объявлние функции с параметрами и возвращемым значением
function greet(name) {
    return `Hello, ${name}!`;
}

// объявлние функции без возвращаемого значения и параметров
function sayHello() {
    console.log("Hello!");
}

greet('Max'); // можно вызвать до объявления
sayHello();
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

JS при обработке кода поднимает все функции с ключевым словом `function` наверх их области видимости, как будто они объявлены в начале файла.

**Arguments:**

```js
function sum() {
    console.log(arguments); // [1, 2, 3]
    return arguments[0] + arguments[1];
}

sum(1, 2, 3);
```



## 17. Function Expression

Функция записывается как выражение и присваивается переменной.

```js
const greet = function(name) {
    return `Hello, ${name}!`;
};

greet('Max');


ILI

const log = console.log; // ложим функцию в перменную как ссылку
log("test"); // пример использования
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
