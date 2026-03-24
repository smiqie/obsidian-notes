# Arraysfsfdsf

**Массив** - структура данных для хранения упорядоченных коллекций (список пользователей, товаров, элементов и т.д.)

**Элемент массива** - значение с числовым индексом (начиная с `0`)

---

# Создание массива

## Способ 1: литерал массива

```js
const arr = [];
```

## Способ 2: через `new Array()`

```js
const arr = new Array();
const arr = new Array(1, 2, 34, true); // результат аналогичен литералу
```

---

# Элементы массива

## Обычный массив

```js
const numbers = [1, 10, 21];

/* Под капотом:
   0: 1
   1: 10
   2: 21
   length: 3
*/
```

---

## Смешанный массив

```js
const mixedArray = [1, 2, "hello", true, undefined, null, {}, []];
```

---

## Двумерный массив

```js
const matrix = [
    [1, 2, 3],
    [4, 5, 6]
];
```

- Массив, который содержит в себе другой массив как элемент

---

# Доступ к элементам

## По индексу

```js
const numbers = [1, 10, 21];

console.log(numbers[0]); // 1
console.log(numbers[2]); // 21
```

---

## Копирование значения

```js
const numbers = [1, 10, 21];

let x = numbers[1]; // x = 10
```

---

## Изменение элемента

```js
const numbers = [1, 10, 21];

numbers[1] = 100;
console.log(numbers[1]); // 100
```

- Можно изменять элементы `const` массива (меняется содержимое, не ссылка)

---

## Вложенные массивы

```js
const nested = [1, 2, [3, 4], [5, 6], [7, [8, 9]]];

console.log(nested[0]);       // 1       — 1й уровень
console.log(nested[2][0]);    // 3       — 2й уровень
console.log(nested[4][1][0]); // 8       — 3й уровень (в реальной разработке так лучше не делать)
```

---

## Свойство `length`

```js
const numbers = [1, 2, 3];

console.log(numbers.length); // 3
```

---

# Копирование массива

## Присваивание — копирование ссылки

```js
const numbers = new Array(10, 20, 30);
const copiedArray = numbers;

console.log(numbers === copiedArray); // true (один объект в памяти)
```

---

# Методы массива

## Добавление элементов

```js
const arr = [1, 2, 3, 4, 5];

arr.unshift(111); // добавляет в начало → [111, 1, 2, 3, 4, 5]
arr.push(777);    // добавляет в конец  → [1, 2, 3, 4, 5, 777]
```

- `push` предпочтительнее `unshift` — добавление в конец дешевле по производительности

---

## Удаление элементов

```js
const arr = [1, 2, 3, 4, 5];

arr.shift(); // удаляет из начала и возвращает удалённый элемент → arr = [2, 3, 4, 5]
arr.pop();   // удаляет из конца и возвращает удалённый элемент  → arr = [1, 2, 3, 4]
```

---

## Сохранение удалённого значения

```js
const numbers = [1, 2, 3, 4, 5];

const lastValue = numbers.pop(); // сохраняем для дальнейших операций
console.log(lastValue); // 5
```

---

## Сортировка

```js
const arr = [5, 3, 1, 4, 2];

arr.sort((a, b) => a - b); // по возрастанию  → [1, 2, 3, 4, 5]
arr.sort((a, b) => b - a); // по убыванию     → [5, 4, 3, 2, 1]

arr.toSorted((a, b) => a - b); // то же, но НЕ мутирует исходный массив (новый метод)
```

---

## Разворот массива

```js
const arr = [1, 2, 3, 4, 5];

arr.reverse();   // переворачивает массив и изменяет его напрямую → [5, 4, 3, 2, 1]
arr.toReversed(); // то же, но НЕ мутирует исходный массив
```

---

## Объединение массивов

```js
const arr1 = [1, 2];
const arr2 = [3, 4];

const newArr = arr1.concat(arr2); // → [1, 2, 3, 4]
```

- Не мутирует исходные массивы — возвращает новый

---

## Преобразование в строку

```js
const arr = [1, 2, 3];

console.log(arr.toString()); // "1,2,3" (через запятую без пробелов)
console.log(arr.join(""));   // "123"   (без разделителя)
console.log(arr.join(" "));  // "1 2 3" (через пробел)
```

- `join` — как `toString`, но можно задать любой разделитель

---

## Проверка наличия элемента

```js
const arr = [1, 2, 3];
const skills = ["html", "css", "js"];

console.log(arr.includes(1));      // true
console.log(skills.includes("ts")); // false
```

---

## Доступ по индексу (с поддержкой отрицательных)

```js
const arr = [1, 2, 3, 4, 5];

console.log(arr.at(1));  // 2
console.log(arr.at(-1)); // 5 (последний элемент)
```

---

## Выборка части массива

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

const newPhones = phones.slice(0, 2);
// [{ id: 1 ... }, { id: 2 ... }] — от 0го до 2го индекса (2й не включается)
```

- Не мутирует исходный массив

---

## Удаление / вставка элементов — `splice`

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

phones.splice(2, 1);
// удаляем 1 элемент начиная с индекса 2, возвращает удалённый элемент, мутирует массив

phones.splice(1, 0, { id: 5, title: "iPhone 16" });
// с индекса 1, удаляем 0 элементов, вставляем новый — вернёт []

const phones2026 = phones.toSpliced(2, 1, { id: 5, title: "iPhone 16" });
// то же, но НЕ мутирует исходный массив (новый метод)
```

- Удобен для drag-and-drop (удалить из одной колонки, вставить в другую)

---

# Статические методы

```js
Array.isArray(123);             // false — является ли аргумент массивом?
Array.isArray([1, 2, 3]);       // true

const arr = Array.of(1, 2, "text"); // создаёт массив из переданных аргументов

const arr = Array.from("1234"); // создаёт массив из строки → ['1', '2', '3', '4']
// также принимает: массив, Map, Set и т.д.
```

---

# `flat` — разворачивание вложенных массивов

```js
const nested = [1, 2, [3, 4], [5, 6], [7, [8, 9]]];

console.log(nested.flat());         // [1, 2, 3, 4, 5, 6, 7, [8, 9]] — 1 уровень вложенности
console.log(nested.flat(2));        // [1, 2, 3, 4, 5, 6, 7, 8, 9]   — 2 уровня
console.log(nested.flat(Infinity)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]   — все уровни
```

---

# Деструктуризация

```js
const names = ["Max", "Alex", "Stacy"];

// Без деструктуризации
const nameMax  = names[0];
const nameAlex = names[1];

// С деструктуризацией (используется часто)
const [nameMax, nameAlex, nameStacy] = names;
// nameMax = "Max", nameAlex = "Alex", nameStacy = "Stacy"
```

---

## Значение по умолчанию

```js
const names = ["Kate"];

const [nameKate, nameOlga = "Olga"] = names;
// nameKate = "Kate", nameOlga = "Olga" (элемента нет — берётся дефолт)
```

---

## Пример с React

```js
// useState возвращает массив из 2х элементов — деструктурируем его
const [counter, setCounter] = useState(0);
```

---

# Spread — оператор расширения (`...`)

**Раскладывает** массив на отдельные значения

```js
const names1 = ["Kate"];
const names2 = ["Max", "Alex", "Stacy"];

const allNames = [...names1, "Nick", "Dima", ...names2];
// ["Kate", "Nick", "Dima", "Max", "Alex", "Stacy"]
```

---

## Spread со строкой

```js
const str = "Hi";

console.log([...str]); // ['H', 'i']
```

---

## Spread с `Math.max` / `Math.min`

```js
const numbers = [1, 24, 546, 12];

console.log(Math.max(...numbers)); // 546
console.log(Math.min(...numbers)); // 1
```

---

# Rest — остаточные параметры (`...`)

**Собирает** несколько значений в массив. Работает противоположно spread.

```js
const sum = (...numbers) => {
    let total = 0;
    for (const value of numbers) {
        total += value;
    }
    return total;
};

console.log(sum(1, 2, 3, 4)); // 10
console.log(sum(1, 2, 3));    // 6
```

---

## Rest при деструктуризации

```js
const names = ["Max", "Alex", "Stacy"];

const [firstName, ...restNames] = names;
// firstName = "Max", restNames = ["Alex", "Stacy"]
```

---

## Важно: rest всегда последний

```js
// ✅ Правильно
const fn = (arg1, arg2, ...rest) => {};

// ❌ Ошибка
const fn = (arg1, ...rest, arg2) => {};
```

---

# Методы перебора

## `forEach` — перебор массива

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

skills.forEach((value) => console.log(value));
// перебирает массив, value — элемент на каждой итерации

skills.forEach((value, index) => console.log(value, index));
// 2й аргумент — индекс элемента

skills.forEach((value, index, array) => console.log(array));
// 3й аргумент — весь массив
```

---

## Передача колбэка по ссылке

```js
const logValues = (value) => console.log(value);

skills.forEach(logValues); // передаём без скобок!
```

- Анонимная функция прямо в скобках — стандартный способ
- Вынос в переменную — если логика слишком большая

---

## `indexOf` / `lastIndexOf`

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

console.log(skills.indexOf("js"));     // 3  — индекс первого вхождения
console.log(skills.indexOf("js", 4));  // -1 — поиск с 4го индекса, не найдено

console.log(skills.lastIndexOf("js")); // индекс последнего вхождения
```

- `-1` — элемент не найден

---

## `some` / `every`

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

const hasJs = skills.some((value) => value === "js");   // true  — хотя бы один совпадает
const allJs = skills.every((value) => value === "js");  // false — все должны совпадать
```

---

## `some` / `every` с массивом объектов

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

const everyHasTitle = phones.every((phone) => "title" in phone); // true
const someHasTitle  = phones.some((phone) => "title" in phone);  // true
```

---

## `find` / `findIndex`

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

const nokia = phones.find((phone) => phone.title === "Nokia 3310");
// { id: 3, title: "Nokia 3310" } — возвращает первый найденный элемент

const nokiaIndex = phones.findIndex((phone) => phone.title === "Nokia 3310");
// 2 — возвращает индекс первого найденного элемента
```

- `some` → `true/false`, `find` → сам элемент

---

## Совет: не дублируй колбэки

```js
// ❌ Дублирование логики
phones.find((phone) => phone.title === "Nokia 3310");
phones.findIndex((phone) => phone.title === "Nokia 3310");

// ✅ Лучше вынести
const isNokia = (phone) => phone.title === "Nokia 3310";
phones.find(isNokia);
phones.findIndex(isNokia);
```

---

## `filter` — фильтрация массива

Возвращает **новый массив** со всеми элементами, прошедшими условие

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

const filteredSkills = skills.filter((skill) => skill.includes("c"));
// ["css", "scss", "react"]
```

---

```js
const evenNumbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].filter((num) => num % 2 === 0);
// [2, 4, 6, 8, 10]
```

---

```js
const clients = [
    { id: 1, level: 3, name: "Lucy",  status: "online"  },
    { id: 2, level: 1, name: "Rick",  status: "offline" },
    { id: 3, level: 3, name: "Jack",  status: "online"  },
    { id: 4, level: 2, name: "Helen", status: "online"  },
    { id: 5, level: 1, name: "Alice", status: "offline" },
    { id: 6, level: 1, name: "Derek", status: "offline" },
    { id: 7, level: 3, name: "Nick",  status: "online"  },
];

const highLevelClients = clients.filter((client) => client.level === 3);
// [Lucy, Jack, Nick]
```

---

## `map` — преобразование массива

Вызывает функцию для каждого элемента и возвращает **новый массив результатов**

```js
const clients = [
    { id: 1, level: 3, name: "Lucy",  status: "online"  },
    { id: 2, level: 1, name: "Rick",  status: "offline" },
    { id: 3, level: 3, name: "Jack",  status: "online"  },
    { id: 4, level: 2, name: "Helen", status: "online"  },
    { id: 5, level: 1, name: "Alice", status: "offline" },
    { id: 6, level: 1, name: "Derek", status: "offline" },
    { id: 7, level: 3, name: "Nick",  status: "online"  },
];

const clientNames = clients.map((client) => client.name);
// ["Lucy", "Rick", "Jack", "Helen", "Alice", "Derek", "Nick"]
```

---

## Явный `return` в `map`

```js
// Неявный return (стрелочная функция без фигурных скобок)
const clientNames = clients.map((client) => client.name);

// Явный return (нужен при фигурных скобках)
const clientNames = clients.map((client) => {
    return client.name; // без return — вернётся массив из undefined
});
```

---

## Цепочка методов

```js
const result = clients
    .map((client) => ({
        age: Math.floor(Math.random() * 50 + 18),
        name: client.name,
        status: client.status,
    }))
    .map((client) => {
        client.status = client.status === "online" ? "online 🟢" : "offline 🔴";
        return client;
    })
    .filter((client) => client.status.startsWith("online"));
// массив только онлайн-клиентов с иконками и случайным возрастом
```

---

## `reduce` — вычисление единого значения

```js
/*
arr.reduce((accumulator, item, index, array) => {
    // ...
}, initial);

accumulator — результат предыдущего вызова (= initial при первом вызове)
item        — текущий элемент
initial     — начальное значение accumulator
*/
```

---

### Сумма элементов

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const sum = numbers.reduce((accumulator, value) => accumulator + value, 0);
console.log(sum); // 55
```

---

### Подсчёт категорий

```js
const books = [
    { id: 1, title: "Harry Potter",    price: 59,  category: "fantasy" },
    { id: 2, title: "A Brief History", price: 108, category: "science" },
    { id: 3, title: "The Hobbit",      price: 149, category: "fantasy" },
    { id: 4, title: "Cosmos",          price: 173, category: "science" },
    { id: 5, title: "Dune",            price: 73,  category: "fantasy" },
];

const categoryMap = books.reduce((result, book) => {
    if (book.category in result) {
        result[book.category]++;       // увеличиваем счётчик
    } else {
        result[book.category] = 1;    // создаём динамический ключ
    }
    return result;
}, {}); // начальное значение — пустой объект

console.log(categoryMap); // { fantasy: 3, science: 2 }
```