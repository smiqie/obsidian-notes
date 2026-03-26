# Functions - Basics

- **Функция** - переиспользуемый блок кода, который выполняет одну задачу
	- Нужны чтобы не дублировать код

---

# Параметры и аргументы

- **Параметры** - переменные, указываемые в круглых скобках при **объявлении** функции
- **Аргументы** - значения, передаваемые при **вызове** функции

```js
function sum(num1, num2) { // num1, num2 - параметры
    console.log(num1 + num2);
}

sum(5, 5); // 5, 5 - аргументы
```

---

## Параметры по умолчанию

Параметры по умолчанию принято указывать **в конце**.

```js
function greet(name, greeting = "Hello") {
    return `${greeting}, ${name}!`;
}

greet("Max");         // "Hello, Max!"
greet("Max", "Hi");  // "Hi, Max!"
```

---

## Проверка параметров

Проверка на `null`, `undefined`, пустую строку и другие falsy-значения:

```js
function processData(data) {
    if (!data) {
        console.log("Нет данных");
        return;
    }
    // обработка данных
}
```

---

# `return`

- Возвращает значение из функции
- Без `return` функция возвращает `undefined`

```js
function sum(a, b) {
    return a + b;
}

const result = sum(2, 3);
console.log(result); // 5
```

---

# Лучшие практики

- Функция должна выполнять **только одну задачу**
- Имя начинается с **глагола** + уточняющее **существительное**: `validateEmail`, `isActive`, `calculateTotal`, `showMessage`
- При беглом чтении кода достаточно прочитать имя функции, чтобы понять что она делает

```js
// ✅ Понятно без чтения тела функции
checkUserPermissions();
fetchDataFromAPI();
renderUserProfile();
```