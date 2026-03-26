# Functions - Callbacks

**Callback** - функция, передаваемая как аргумент в другую функцию и вызываемая внутри неё

---

# Базовый пример

```js
function greeting() {
    console.log("Hello!");
}

// cb - сокращение от callback
function showGreeting(cb) {
    cb(); // вызываем переданную функцию
}

showGreeting(greeting); // передаём ссылку на функцию - без ()
```

---

# Callback с возвращаемым значением

```js
function getInfo(name, age) {
    return `Name: ${name}\nAge: ${age}`;
}

function getInfoWithDate(callback) {
    const now = new Date();
    console.log(`Today: ${now.toISOString()}\n${callback("Dima", 33)}`);
}

getInfoWithDate(getInfo);
```

---

# Анонимные функции как колбэки

```js
// Fn - сокращение от function
function survey(question, agreedFn, disagreedFn) {
    if (confirm(question)) {
        agreedFn();
    } else {
        disagreedFn();
    }
}

survey(
    "Ты мой друг?",
    function() { console.log("Ты согласился!"); },  // анонимная функция
    function() { console.log("Ты отказался!"); }
);
```

---

# Колбэки со стрелочными функциями

```js
const msg = (action1, action2) => {
    action1();
    action2();
};

// Анонимные стрелочные функции напрямую
msg(
    () => console.log("1"),
    () => console.log("2")
);

// Или через переменные (если логика большая)
const fn1 = () => console.log("1");
const fn2 = () => console.log("2");
msg(fn1, fn2);
```

---

# Функция возвращает функцию

```js
const validate = (hasAccess) =>
    hasAccess
        ? () => console.log("Доступ разрешён")
        : () => console.log("Доступ запрещён");

const logMsg = validate(false);
logMsg(); // "Доступ запрещён"
```

---

# Термины

**Предикат** - особый тип колбэка, который только проверяет условие и возвращает `true` или `false`

**Анонимная функция** - функция без имени, чаще всего передаётся как колбэк напрямую

```js
skills.forEach(function(value) {   // анонимная function
    console.log(value);
});

skills.forEach((value) => console.log(value)); // анонимная стрелочная
```