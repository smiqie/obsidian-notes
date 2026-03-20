
## 18. Arrow Functions (современный и удобный подход)

```js
const greet = (name) => {
    return `Hello, ${name}!`;
};

// или короче (=> - по сути под капотом подразумевает в себе return?)
const greet = (name) => `Hello, ${name}!`;

// или короче еще короче (елси ток 1 аргумент мы его модет не класть в крулгые скобки)
const showName = name => `Hi, ${name}!`;

shoqName("Alex");
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
