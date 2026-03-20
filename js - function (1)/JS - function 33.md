
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
