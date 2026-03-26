# Arrays

**Массив** - структура данных для хранения упорядоченных коллекций (список пользователей, товаров, элементов и т.д.)

**Элемент массива** - значение с числовым индексом (начиная с `0`)

---

# Объявление и инициализация

```js
// Литерал массива (основной способ)
const arr = [];
const numbers = [1, 10, 21];

// Через конструктор
const arr = new Array();
const arr = new Array(1, 2, 34, true); // результат аналогичен литералу
```

Под капотом массив хранит пары ключ-значение, где ключ - индекс:

```js
// numbers = [1, 10, 21]
// 0: 1
// 1: 10
// 2: 21
// length: 3
```

**Смешанный массив** - может содержать значения любых типов:

```js
const mixedArray = [1, 2, "hello", true, undefined, null, {}, []];
```

---

# Вложенные массивы

- **это** массив, содержащий другой массив как элемент
	- двумерный - один уровень вложенности, трёхмерный - два и т.д.

```js
const nested = [1, 2, [3, 4], [5, 6], [7, [8, 9]]];

console.log(nested[0]);       // 1  — 1й уровень
console.log(nested[2][0]);    // 3  — 2й уровень
console.log(nested[4][1][0]); // 8  — 3й уровень (в реальной разработке так лучше не делать)
```

---

# Доступ к элементам и изменение

```js
const numbers = [1, 10, 21];

console.log(numbers[0]); // 1
console.log(numbers[2]); // 21

let x = numbers[1];      // копируем значение → x = 10

numbers[1] = 100;        // изменяем элемент (даже если массив объявлен как const) → numbers[1] = 10
```

---

# Копирование массива

```js
const numbers = [10, 20, 30];
const copiedArray = numbers;

console.log(numbers === copiedArray); // true - одна ссылка, один объект в памяти
```

---

# Свойства экземпляра

## `.length`

```js
const numbers = [1, 2, 3];

console.log(numbers.length); // 3
```

- **Описание:** возвращает количество элементов в массиве
- **Возвращает:** число

---

# Методы экземпляра

## `.push(element)`

```js
const arr = [1, 2, 3];

arr.push(4);
console.log(arr); // [1, 2, 3, 4]
```

- **Описание:** добавляет новый элемент в конец массива
- **Параметры:**
	- `element` - добавляемое значение
- **Возвращает:** новую длину массива
- **Мутабельность:** изменяет исходный массив
  
- Один из самых популярных методов
- Предпочтительнее чем `.unshift()` - добавление в конец дешевле по производительности

---
## `.unshift(element)`

```js
const arr = [1, 2, 3];

arr.unshift(0);
console.log(arr); // [0, 1, 2, 3]
```

- **Описание:** добавляет новый элемент в начало массива, остальные элементы смещаются
- **Параметры:**
	- `element` - добавляемое значение
- **Возвращает:** новую длину массива
- **Мутабельность:** изменяет исходный массив

---
## `.pop()`

```js
const arr = [1, 2, 3, 4, 5];

const last = arr.pop();
console.log(last); // 5
console.log(arr);  // [1, 2, 3, 4]
```

- **Описание:** удаляет последний элемент массива
- **Возвращает:** удалённый элемент
- **Мутабельность:** изменяет исходный массив

---
## `.shift()`

```js
const arr = [1, 2, 3, 4, 5];

const first = arr.shift();
console.log(first); // 1
console.log(arr);   // [2, 3, 4, 5]
```

- **Описание:** удаляет первый элемент массива
- **Возвращает:** удалённый элемент
- **Мутабельность:** изменяет исходный массив
  
---
## `.sort(compareFn)`

```js
const arr = [5, 3, 1, 4, 2];

arr.sort((a, b) => a - b); // по возрастанию → [1, 2, 3, 4, 5]
arr.sort((a, b) => b - a); // по убыванию   → [5, 4, 3, 2, 1]
```

- **Описание:** сортирует массив на месте
- **Параметры:**
	- `compareFn` - колбэк-функция сравнения `(a, b) => ...`
- **Возвращает:** отсортированный массив
- **Мутабельность:** изменяет исходный массив

- **Часто используется в реальной разработке**

---
## `.toSorted(compareFn)`

```js
const arr = [5, 3, 1, 4, 2];

const sorted = arr.toSorted((a, b) => a - b);
console.log(sorted); // [1, 2, 3, 4, 5]
console.log(arr);    // [5, 3, 1, 4, 2] — не изменился
```

- **Описание:** то же самое, что и `.sort()`, но не изменяет исходный массив
- **Параметры:**
	- `compareFn` - колбэк-функция сравнения `(a, b) => ...`
- **Возвращает:** **новый** отсортированный массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `.reverse()`

```js
const arr = [1, 2, 3, 4, 5];

arr.reverse();
console.log(arr); // [5, 4, 3, 2, 1]
```

- **Описание:** переворачивает порядок элементов
- **Возвращает:** перевёрнутый массив
- **Мутабельность:** изменяет исходный массив

---
## `.toReversed()`

```js
const arr = [5, 3, 1, 4, 2];

const sorted = arr.toSorted((a, b) => a - b);
console.log(sorted); // [1, 2, 3, 4, 5]
console.log(arr);    // [5, 3, 1, 4, 2] — не изменился
```

- **Описание:** то же самое, что и `.reverse()`, но не изменяет исходный массив
- **Возвращает:** **новый** перевёрнутый массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `.concat(...arrays)`

```js
const arr1 = [1, 2];
const arr2 = [3, 4];

const result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]
```

- **Описание:** объединяет два или более массива
- **Параметры:**
	- `...arrays` - массивы для объединения
- **Возвращает:** новый массив
- **Мутабельность:** **не** изменяет исходные массивы
  
---
## `.toString()`

```js
const arr = [1, 2, 3];

console.log(arr.toString()); // "1,2,3"
```

- **Описание:** преобразует массив в строку
- **Возвращает:** строку
- **Мутабельность:** **не** изменяет исходный массив
  
---
## `.join(separator)`

```js
const arr = [1, 2, 3];

console.log(arr.join(""));   // "123"
console.log(arr.join(" "));  // "1 2 3"
console.log(arr.join("-"));  // "1-2-3"
```

- **Описание:** преобразует массив в строку
- **Параметры:**
	- `separator` - разделитель между элементами (по умолчанию `,`)
- **Возвращает:** строку
- **Мутабельность:** **не** изменяет исходный массив

---
## `.includes(value)`

```js
const skills = ["html", "css", "js"];

console.log(skills.includes("js"));  // true
console.log(skills.includes("ts"));  // false
```

- **Описание:** проверяет, есть ли элемент в массиве
- **Параметры:**
	- `value` - искомое значение
- **Возвращает:** `true` / `false`
- **Мутабельность:** **не** изменяет исходный массив

---
## `.at(index)`

```js
const arr = [1, 2, 3, 4, 5];

console.log(arr.at(1));  // 2
console.log(arr.at(-1)); // 5 — последний элемент
console.log(arr.at(-2)); // 4
```

- **Описание:** возвращает элемент по индексу (поддерживает отрицательные индексы)
- **Параметры:**
	- `index` - индекс элемента (может быть отрицательным)
- **Возвращает:** элемент массива или `undefined`
- **Мутабельность:** **не** изменяет исходный массив

---
## `.slice(start, end)`

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

const first2 = phones.slice(0, 2); // [{ id: 1 }, { id: 2 }]
const last2  = phones.slice(-2);   // [{ id: 3 }, { id: 4 }]
```

- **Описание:** копирует часть массива от `start` до `end`
- **Параметры:**
	- `start` - индекс начала
	- `end` - индекс конца (не включается, необязательный)
- **Возвращает:** новый массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `.splice(start, deleteCount, ...items)`

```js
// =============== ПРИМЕР: 1. =============== 
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

// Удаление
phones.splice(2, 1);
// удалён { id: 3, title: "Nokia 3310" }

// Вставка без удаления
phones.splice(1, 0, { id: 5, title: "iPhone 16" });
// вставлен в позицию 1, ничего не удалено, возвращает []


// =============== ПРИМЕР: 2 ===============
// --- УДАЛЕНИЕ ЭЛЕМЕНТА (ПЛОХОЙ СПОСОБ, через delete) ---
delete phones[2]; 

// Элемент удален, но "дырка" (empty) осталась!
console.log(phones); // [ {id:1...}, {id:2...}, <1 empty item>, {id:4...} ]

console.log(phones.length); // 4 (длина НЕ изменилась, хотя элементов три)

console.log(phones[2]);     // undefined
```

- **Описание:** изменяет массив - удаляет элементы и/или вставляет новые на их место
- **Параметры:**
	- `start` - индекс, с которого начинать
	- `deleteCount` - сколько элементов удалить
	- `...items` - элементы для вставки (необязательные)
- **Возвращает:** массив удалённых элементов
- **Мутабельность:** изменяет исходный массив

- **Пример из реальной практики:** удобен для drag-and-drop - удалить из одной колонки и вставить в другую

---
## `.toSpliced(start, deleteCount, ...items)`

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

// Удаляем один элемент с индекса 2 
const cleanPhones = phones.toSpliced(2, 1);

// Создаем НОВЫЙ массив с вставленным iPhone 16
const updatedPhones = phones.toSpliced(1, 0, { id: 5, title: "iPhone 16" });
```

- **Описание:** то же самое, что и `.splice()`, но не изменяет исходный массив
- **Параметры:**
	- `start` - индекс, с которого начинать
	- `deleteCount` - сколько элементов удалить
	- `...items` - элементы для вставки (необязательные)
- **Возвращает:** новый измененный массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `.flat(depth)`

```js
const nested = [1, 2, [3, 4], [5, 6], [7, [8, 9]]];

console.log(nested.flat());         // [1, 2, 3, 4, 5, 6, 7, [8, 9]]
console.log(nested.flat(2));        // [1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log(nested.flat(Infinity)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

- **Описание:** преобразует вложенный массив в плоский (разворачивает подмассивы в один основной массив)
- **Параметры:**
	- `depth` - глубина разворачивания (по умолчанию `1`)
		- `Infinity` - все уровни
- **Возвращает:** новый плоский массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `.indexOf(value, fromIndex)`

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

console.log(skills.indexOf("js"));    // 3
console.log(skills.indexOf("js", 4)); // -1 — поиск начался с индекса 4
```

- **Описание:** возвращает индекс первого вхождения элемента
- **Параметры:**
	- `value` - что ищем
	- `fromIndex` - с какого индекса начинать поиск (необязательный)
- **Возвращает:** индекс или `-1` если не найдено
- **Мутабельность:** **не** изменяет исходный массив

---
## `.lastIndexOf(value, fromIndex)`

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "css"];

console.log(skills.lastIndexOf("css"));    // 6
console.log(skills.lastIndexOf("css", 4)); // 6 — поиск начался с индекса 4
```

- **Описание:** возвращает индекс последнего вхождения элемента
- **Параметры:**
	- `value` - что ищем
	- `fromIndex` - с какого индекса начинать поиск (необязательный)
- **Возвращает:** индекс или `-1` если не найдено
- **Мутабельность:** **не** изменяет исходный массив

---
## `.some(callback)`

```js
// =============== ПРИМЕР: 1 ===============
const skills = ["html", "css", "scss", "js", "git"];
const hasJs = skills.some((value) => value === "js"); // true


// =============== ПРИМЕР: 2 (Пример с параметром index) ===============
const tasks = ["Купить хлеб", "Выучить JS", "Помыть кота", "Сделать OET"];

// Проверяем: есть ли среди ЧЕТНЫХ позиций задача "Выучить JS"?
const isJsOnEvenPower = tasks.some((value, index) => {
    return value === "Выучить JS" && index % 2 === 0; 
});

console.log(isJsOnEvenPower); // false (потому что "Выучить JS" на индексе 1, а это нечетное)


// ============ ПРИМЕР: 3 (Пример с параметром index и array) ============
// Проверка температуры процессора (ищем резкий скачок)
const temps = [40, 42, 41, 85, 45]; // на 4-м шаге резкий скачок!

const hasSpike = temps.some((value, index, array) => {
    if (index === 0) return false; // У первого замера нет предыдущего, пропускаем
    
    const prevTemp = array[index - 1]; // Берем предыдущее значение из этого же массива
    return value > prevTemp + 30;     // Если текущая Т выше предыдущей на 30 градусов — это скачок
});

console.log(hasSpike); // true
```

- **Описание:** проверяет, удовлетворяет ли **хотя бы один элемент** условию
- **Параметры:** `callback(value, index, array)` - функция-предикат:
	- `value` - текущий элемент массива (например, `"html"`)
	- `index` - порядковый номер элемента (0, 1, 2...)
	- `array` - сам исходный массив, который мы перебираем (используется редко)
- **Возвращает:** `true` / `false`
- **Мутабельность:** **не** изменяет исходный массив

> **Предикат** - особый тип колбэка, который только проверяет условие и возвращает `true` или `false`

---

## `.every(callback)`

```js
const skills = ["html", "css", "scss", "js", "git"];

// --- ВАРИАНТ 1: Масштабируемый (Recommended) --- 
// Скобки вокруг аргумента оставлены намеренно
const allJs = skills.every((value) => value === "js"); // false


// --- ВАРИАНТ 2: Лаконичный (Shorthand) ---
// Без скобок вокруг одного аргумента и без return
const allJs = skills.every(value => value === "js"); // false

```

- **Описание:** проверяет, удовлетворяют ли **все элементы** условию
- **Параметры:** `callback(value, index, array)` - функция-предикат:
	- ==см. --> параметры some()==
- **Возвращает:** `true` / `false`
- **Мутабельность:** **не** изменяет исходный массив

**Пример с объектами:**

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
];

const everyHasTitle = phones.every((phone) => "title" in phone); // true
const someHasTitle  = phones.some((phone) => "title" in phone);  // true
```

---
## `.find(callback)`

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

const nokia = phones.find((phone) => phone.title === "Nokia 3310");
// { id: 3, title: "Nokia 3310" }
```

- **Описание:** возвращает первый элемент, удовлетворяющий условию
- **Параметры:** `callback(value, index, array)` - функция-предикат:
	- ==см. --> параметры some()==
- **Возвращает:** элемент или `undefined`
- **Мутабельность:** **не** изменяет исходный массив

---
## `.findIndex(callback)`

```js
const phones = [
    { id: 1, title: "Samsung A50" },
    { id: 2, title: "iPhone 10" },
    { id: 3, title: "Nokia 3310" },
    { id: 4, title: "Xiaomi" },
];

const nokiaIndex = phones.findIndex((phone) => phone.title === "Nokia 3310"); // 2
```

- **Описание:** возвращает индекс первого элемента, удовлетворяющего условие
- **Параметры:** `callback(value, index, array)` - функция-предикат:
	- ==см. --> параметры some()==
- **Возвращает:** индекс или `-1`
- **Мутабельность:** **не** изменяет исходный массив

**Совет:** если одна логика нужна в нескольких методах - выносить в колбэк:

```js
const isNokia = (phone) => phone.title === "Nokia 3310";

phones.find(isNokia);
phones.findIndex(isNokia);
```

> `.some() / .every()` → `true/false`, `.find()` → сам элемент, `.findIndex()` → индекс элемента

---
## `.filter(callback)`

```js
// (1) Фильтрация строк
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

const withC = skills.filter((skill) => skill.includes("c"));
// ["css", "scss", "react"]

// (2) Фильтрация чисел
const evenNumbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].filter((num) => num % 2 === 0);
// [2, 4, 6, 8, 10]

// (3) Фильтрация объектов
const clients = [
    { id: 1, level: 3, name: "Lucy",  status: "online"  },
    { id: 2, level: 1, name: "Rick",  status: "offline" },
    { id: 3, level: 3, name: "Jack",  status: "online"  },
    { id: 4, level: 2, name: "Helen", status: "online"  },
    { id: 5, level: 1, name: "Alice", status: "offline" },
    { id: 6, level: 1, name: "Derek", status: "offline" },
    { id: 7, level: 3, name: "Nick",  status: "online"  },
];

const highLevel = clients.filter((client) => client.level === 3);
// [Lucy, Jack, Nick]
```

- **Описание:** возвращает новый массив со всеми элементами, прошедшими условие (фильтрует исходный массив и возвращает новый)
- **Суть работы:** Он создаёт **новый** массив, пропуская каждый элемент через «сито» (предикат)
	- Если вернулось **`true`** - элемент залетает в новый массив
	- Если вернулось **`false`** - элемент отбрасывается (скипается)
- **Параметры:** `callback(value, index, array)`
	- ==см. --> параметры some()==
- **Возвращает:** новый массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `.map(callback)`

```js
const clients = [
    { id: 1, level: 3, name: "Lucy",  status: "online"  },
    { id: 2, level: 1, name: "Rick",  status: "offline" },
    { id: 3, level: 3, name: "Jack",  status: "online"  },
    { id: 4, level: 2, name: "Helen", status: "online"  },
];

// Вытащить только имена
const names = clients.map((client) => client.name);
// ["Lucy", "Rick", "Jack", "Helen"]

// Явный return (при фигурных скобках обязателен)
const names = clients.map((client) => {
    return client.name; // без return — получим массив из undefined
});
```

- **Описание:** вызывает функцию для каждого элемента и возвращает массив результатов
- **Параметры:**  `callback(value, index, array)`
	- ==см. --> параметры some()==
- **Возвращает:** новый массив той же длины
- **Мутабельность:** **не** изменяет исходный массив

---
## `.reduce(callback, initial)`

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const sum = numbers.reduce((acc, value) => acc + value, 0);

console.log(sum); // 55
```
- **Описание:** сворачивает массив в одно значение, вызывая функцию для каждого элемента
- **Параметры:**
	- `callback(accumulator, value, index, array)`:
	    - `accumulator` - накопленный результат (при первом вызове = `initial`)
	    - `value` - текущий элемент
		    - ==см. --> параметры some()==
	- `initial` - начальное значение `accumulator`
- **Возвращает:** накопленное значение (`accumulator`)
- **Мутабельность:** **не** изменяет исходный массив

---
## `.forEach(callback)`

```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

skills.forEach((value) => console.log(value));
skills.forEach((value, index) => console.log(value, index));
skills.forEach((value, index, array) => console.log(array));

// Ошибка,т.к. нельзя вызвать .filter() у undefined
numbers.forEach(n => n * 2).filter(n => n > 10); 
```

- **Описание:** вызывает функцию для каждого элемента массива
- **Параметры:** `callback(value, index, array)`
	- ==см. --> параметры some()==
- **Возвращает:** `undefined`
	- `.forEach()` используется для **побочных эффектов** (side effects)
	- Он гибче в плане действий «вовне», но не подходит для **цепочек преобразований** (method chaining), т.к. разрывает их своим `undefined`
- **Мутабельность:** **не** изменяет исходный массив

**Передача колбэка по ссылке:**

```js
const skills = ['JS', 'React', 'Node'];

// ВАРИАНТ 1: Анонимная стрелочная функция / Самый частый способ
skills.forEach((value) => console.log(value));


// ВАРИАНТ 2: Передача по ссылке / Выносим, если логика большая или функцию нужно использовать в другом месте
const logValues = (value) => {
  console.log(`Skill: ${value}`);
};
skills.forEach(logValues); // Передаем ИМЯ функции, без скобок!


// ВАРИАНТ 3: Function Declaration / Отличается от варианта 2 только способом объявления (всплытие/hoisting)
function logValuesClassic(value) {
  console.log(value);
}
skills.forEach(logValuesClassic);
```

- Анонимная функция прямо в скобках - стандартный способ. Вынос в переменную - если логика слишком большая

---
---
---

# Статические методы класса Array


## `Array.isArray(value)`

```js
console.log(Array.isArray([1, 2, 3])); // true
console.log(Array.isArray(123));        // false
```

- **Описание:** проверяет, является ли переданное значение массивом
- **Параметры:**
	- `value` - проверяемое значение
- **Возвращает:** `true` / `false`
- **Мутабельность:** **не** изменяет исходный массив

---
## `Array.of(...values)`

```js
const arr = Array.of(1, 2, "text", true);
console.log(arr); // [1, 2, "text", true]
```

- **Описание:** создаёт массив из переданных значений
- **Параметры:**
	- `...values` - элементы нового массива
- **Возвращает:** новый массив
- **Мутабельность:** **не** изменяет исходный массив

---
## `Array.from(iterable)` 

```js
console.log(Array.from("1234")); // ["1", "2", "3", "4"]
```

- **Описание:** создаёт массив из строки, Map, Set или другого итерируемого объекта
- **Параметры:**
	- `iterable` - строка, массив, Map, Set и т.д.
- **Возвращает:** новый массив
- **Мутабельность:** **не** изменяет исходный массив

---

# Деструктуризация

- Копирует значения из массива в переменные по порядку. Не изменяет исходный массив

```js
const names = ["Max", "Alex", "Stacy"];

// Без деструктуризации
const nameMax  = names[0];
const nameAlex = names[1];

// С деструктуризацией
const [nameMax, nameAlex, nameStacy] = names;
// nameMax = "Max", nameAlex = "Alex", nameStacy = "Stacy"
```

**Значение по умолчанию** - если элемента нет в массиве:

```js
const names = ["Kate"];

const [nameKate, nameOlga = "Olga"] = names;
// nameKate = "Kate", nameOlga = "Olga"
```

**Пример с React** - `useState` возвращает массив из двух элементов:

```js
const [counter, setCounter] = useState(0);
```

---

# Spread и Rest

## Spread (`...`) - оператор расширения

- Раскладывает массив на отдельные значения
- Часто встречается на практике

```js
const names1 = ["Kate"];
const names2 = ["Max", "Alex", "Stacy"];

const allNames = [...names1, "Nick", "Dima", ...names2];
// ["Kate", "Nick", "Dima", "Max", "Alex", "Stacy"]
```

**Со строкой:**

```js
console.log([..."Hi"]); // ["H", "i"]
```

**С `Math.max` / `Math.min`:**

```js
const numbers = [1, 24, 546, 12];

console.log(Math.max(...numbers)); // 546
console.log(Math.min(...numbers)); // 1
```

---

## Rest (`...`) — остаточные параметры

- Собирает несколько значений в массив
- Работает противоположно spread

```js
const sum = (...numbers) => {
    let total = 0;
    for (const value of numbers) {
        total += value;
    }
    return total;
};

console.log(sum(1, 2, 3, 4)); // 10 (можем передать сколько угодно чисел)
```

**При деструктуризации** - собирает оставшиеся элементы:

```js
const names = ["Max", "Alex", "Stacy"];

const [firstName, ...restNames] = names;
// firstName = "Max", restNames = ["Alex", "Stacy"]
```

**Важно:** rest всегда должен стоять последним в функции (в списке параметров):

```js
const fn = (arg1, arg2, ...rest) => {}; // ✅
const fn = (arg1, ...rest, arg2) => {}; // ❌ SyntaxError
```

---

# Практические примеры

## Цепочка методов

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

const result = clients
    .map((client) => ({
        age: Math.floor(Math.random() * 50 + 18), // добавили свой ключ
        name: client.name,
        status: client.status,
    }))
    .map((client) => {
        client.status = client.status === "online" ? "online 🟢" : "offline 🔴";
        return client;
    })
    .filter((client) => client.status.startsWith("online"));
// онлайн-клиенты со случайным возрастом и иконками статуса
```

## `reduce` - подсчёт категорий

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
        result[book.category]++;
    } else {
        result[book.category] = 1; // создаём динамический ключ
    }
    return result;
}, {});

console.log(categoryMap); // { fantasy: 3, science: 2 }
```