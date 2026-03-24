# Objects

**Object** - используется для хранения коллекций различных значений

**Свойство объекта** - пара `ключ: значение`:
- **ключ** - строка (имя свойства)
- **значение** - любой тип данных

---

# Создание объекта

## Способ 1: литерал объекта

```js
const person = {
    name: "Dima",
    age: 33
};
```

## Способ 2: через `new Object()`

```js
const person = new Object();
```

---

# Свойства объекта

## Обычные свойства

```js
const person = {
    name: "Dima",
    age: 33,
    isDeveloper: true
};
```

---

## Вложенные объекты

```js
const person = {
    name: "Dima",
    address: {
        country: "Serbia",
        city: "Sombor",
        street: "Branka Radicivica 19"
    }
};
```

---

## Составные ключи (из нескольких слов)

```js
const person = {
    "last name": "Kora"  // ключ в кавычках
};
```

- Если ключ состоит из нескольких слов - нужны кавычки

---

## Числовые ключи

```js
const person = {
    0: "just 0"
};
```

- **Это плохая практика!**
- Число преобразуется в строку
- Обращение только через `person[0]` или `person["0"]`

---

## Сокращенная запись

```js
const id = "13#smI!sd@";

const person = {
    id  // аналогично: id: id
};
```

- Если ключ и значение совпадают - можно писать только ключ
- Часто используется при отправке данных на сервер
- **Под капотом:** JS-движок при чтении кода сам сопоставляет это слово с переменной в памяти:
	1. **Если совпадение найдено:** JS берет имя переменной как название ключа, а её содержимое - как значение
	2. **Если переменная НЕ найдена:** Программа просто упадет с ошибкой `ReferenceError: [имя] is not defined`

---

## Динамические ключи (вычисляемые свойства)

```js
const hobby = "favorite hobby";

const person = {
    [hobby]: "running, skiing, coding",  // ключ из переменной
};

// Динамичный/Гибкий способ (через переменную)
console.log(person[hobby]); // "running, skiing, coding"

// Статический способ (пишем строку вручную - жестко зашито в код)
console.log(person["favorite hobby"]); // "running, skiing, coding"
```

- **Суть:** Позволяют использовать значение переменной в качестве имени ключа объекта
	- Квадратные скобки `[]` - вычисляемое имя свойства
- Часто используется в реальной разработке

---

# Методы объекта (функции)

## Обычная функция

```js
const person = {
    greet: function() {
        console.log("Hello, Im Dima");
    }
};

person.greet(); // "Hello, Im Dima"
```

---

## Сокращенная запись метода

```js
const person = {
    greet() {
        console.log("Hello, Im Dima");
    }
};

person.greet(); // "Hello, Im Dima"
```

---

## Стрелочная функция

```js
const person = {
    greetSecond: () => console.log("Hello, Im Dmitry")
};

person.greetSecond(); // "Hello, Im Dmitry"
```

- ==Различие между обычной и стрелочной функцией в объекте (позже ознакомиться)==

---

# Доступ к свойствам

## Через точку (основной способ)

```js
const person = {
    name: "Dima",
    age: 33
};

console.log(person.name); // "Dima"
console.log(person.age);  // 33
```

---

## Через квадратные скобки

```js
const person = {
    name: "Dima",
    "last name": "Kora"
};

console.log(person["name"]);      // "Dima"
console.log(person["last name"]); // "Kora" (составной ключ)
```

- **Когда использовать:** 
	1. Составные ключи (из нескольких слов)
	2. Динамический доступ (ключ в переменной)

---

## Доступ к вложенным объектам

```js
const person = {
    address: {
        country: "Serbia",
        city: "Sombor"
    }
};

console.log(person.address);         // { country: "Serbia", city: "Sombor" }
console.log(person.address.country); // "Serbia"
console.log(person.address.city);    // "Sombor"
```

---

## Обращение к несуществующему свойству

```js
const person = {
    name: "Dima"
};

console.log(person.isPositive); // undefined
```

## Ошибка при вложенном обращении

```js
const person = {
    name: "Dima"
};

console.log(person.isPositive.qwerty); // ❌ TypeError
```

- **Ошибка:** `person.isPositive` = `undefined`, нельзя обратиться к свойству `undefined`

## Опциональная цепочка (`?.`)

```js
const person = {
    name: "Dima"
};

console.log(person.isPositive?.qwerty); // undefined (без ошибки)
```

- `?.` - если свойство `null` или `undefined`, вернет `undefined` без ошибки
- **Используется часто, но не лучшая практика**

---

# Изменение объекта

## Изменение свойства

```js
const person = {
    name: "Dima"
};

person.name = "Alex";
console.log(person.name); // "Alex"
```

- Можно изменять свойства `const` объекта (т.к. меняется содержимое, не ссылка)

---

## Копирование значения

```js
const person = {
    name: "Dima"
};

const prevName = person.name; // копируем значение
person.name = "Alex";

console.log(prevName);    // "Dima" (не изменилось)
console.log(person.name); // "Alex"
```

---

## Добавление нового свойства

```js
const person = {
    name: "Dima"
};

console.log(person.isHappy); // undefined

person.isHappy = true; // динамическое создание свойства

console.log(person.isHappy); // true
```

---

## Удаление свойства

```js
const person = {
    name: "Dima",
    age: 33
};

delete person.age;

console.log(person.age); // undefined
```

- **Синтаксис:** `delete объект.свойство` или `delete объект["свойство"]`

---

# Проверка наличия свойства

## Оператор `in`

```js
const person = {
    name: "Dima",
    age: 33
};

console.log("age" in person);  // true
console.log("city" in person); // false
```

- **Синтаксис:** `"ключ" in объект`
- **Возвращает:** `true` или `false`

---

# Копирование объектов

## Присваивание - копирование ссылки

```js
const person = {
    name: "Dima"
};

const newPerson = person; // копируется ссылка, НЕ объект!

console.log(newPerson === person); // true (одна ссылка)

newPerson.name = "Alex";
console.log(person.name); // "Alex" (изменился!)
```

- Обе переменные указывают на **один объект** в памяти