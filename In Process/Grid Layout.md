# CSS Grid Layout

```css
/* базовый grid-контейнер */
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 100px 200px;
  gap: 20px;
}

/* inline-grid контейнер */
.inline-grid {
  display: inline-grid;
}
```

**Grid Layout (Гриды)** - современная CSS-фича для создания сложных сеток. Флексы и гриды отлично уживаются вместе - их можно и нужно комбинировать.

---

# Основные понятия

- **Грид-контейнер** - элемент с `display: grid` или `display: inline-grid`
- **Грид-элементы** - прямые дочерние элементы грид-контейнера
- **Грид-линии** - горизонтальные и вертикальные разделительные линии
- **Грид-ячейка** - пространство между соседними грид-линиями
- **Грид-полоса** - пространство между двумя соседними линиями (строка или столбец)
- **Грид-область** - пространство, ограниченное 4 грид-линиями

**Размеры по умолчанию:**

- `display: grid` - ширина на весь контейнер, высота под контент (как у блочных элементов)
- `display: inline-grid` - размеры зависят от содержимого (как у строчных элементов)

---






# Создание колонок: `grid-template-columns`

```css
/* 3 колонки с автоматической шириной */
.grid {
  grid-template-columns: auto auto auto;
}

/* фиксированные размеры */
.grid {
  grid-template-columns: 100px 200px 150px;
}

/* проценты */
.grid {
  grid-template-columns: 30% 50% 20%;
}
```

**Форматы значений:**

- `auto` - ширина зависит от содержимого
- `px`, `%`, `em`, `rem` - фиксированные значения
- Если элементов больше, чем колонок - они переносятся на новую строку

---

## Именованные грид-линии

```css
.grid {
  grid-template-columns:
    [first] 50px 
    [second] 70% 
    [third] auto 
    [fourth];
}
```

- имена прописываются в квадратных скобках
- видны в DevTools → Layout → Show line names
- повышают читаемость кода в сложных сетках
- можно использовать в позиционировании элементов

---

## Функция `repeat()`

```css
/* повторение одного значения */
.grid {
  grid-template-columns: repeat(3, 150px);
  /* = 150px 150px 150px */
}

/* несколько repeat() */
.grid {
  grid-template-columns: repeat(2, 150px) repeat(3, 50px);
  /* = 150px 150px 50px 50px 50px */
}
```

---

## Единица измерения `fr` (fraction)

```css
/* 3 равные колонки */
.grid {
  grid-template-columns: repeat(3, 1fr);
  /* каждая колонка = 1/3 ширины */
}

/* комбинация с фиксированными размерами */
.grid {
  grid-template-columns: 1fr 1fr 50px;
  /* 3-я колонка = 50px, остальное делится поровну */
}

/* разные пропорции */
.grid {
  grid-template-columns: 2fr 1fr 50px;
  /* оставшееся пространство делится на 3 части:
     1-я колонка = 2 части
     2-я колонка = 1 часть
     3-я колонка = 50px */
}
```

💡 `fr` - дробь, доля, часть. Делит доступное пространство на равные части.

---

## Функция `minmax()`

```css
.grid {
  grid-template-columns: minmax(200px, 35%) 1fr 50px;
  /* 1-я колонка: минимум 200px, максимум 35% от ширины */
}
```

- задает диапазон от минимального до максимального значения
- браузер сам регулирует размер в этих пределах

---

# Создание строк: `grid-template-rows`

```css
/* фиксированная высота первых 2 строк */
.grid {
  grid-template-rows: 40px 80px;
  /* остальные строки - по содержимому */
}

/* все значения как у grid-template-columns */
.grid {
  grid-template-rows: repeat(3, 100px);
}
```

Форматы значений **аналогичны** `grid-template-columns`.

---

# Автоматические строки и колонки

## `grid-auto-rows`

```css
/* первые 2 строки фиксированные, остальные - 15px */
.grid {
  grid-template-rows: 40px 80px;
  grid-auto-rows: 15px;
}

/* паттерн для строк */
.grid {
  grid-template-rows: 40px 80px;
  grid-auto-rows: 15px 30px;
  /* строки чередуются: 15px, 30px, 15px, 30px... */
}
```

## `grid-auto-columns` + `grid-auto-flow`

```css
.grid {
  display: grid;
  gap: 10px;
  
  /* первая колонка */
  grid-template-columns: 30%;
  
  /* паттерн для остальных колонок */
  grid-auto-columns: 50px 100px;
  
  /* элементы в одну строку, не переносятся */
  grid-auto-flow: column;
}
```

- `grid-auto-flow: column` - элементы не переносятся на новые строки
- элементы умещаются в одну строку по паттерну

---

# Шаблон сетки: `grid-template-areas`

```css
.grid-container {
  display: grid;
  grid-template-areas:
    "menu catalog advertisement"
    "menu catalog advertisement"
    "menu catalog ."
    "menu order order";
}

/* распределение элементов по областям */
.menu { grid-area: menu; }
.catalog { grid-area: catalog; }
.advertisement { grid-area: advertisement; }
.order { grid-area: order; }
```

```html
<div class="grid-container">
  <div class="menu">Меню</div>
  <div class="catalog">Каталог</div>
  <div class="advertisement">Реклама</div>
  <div class="order">Заказ</div>
</div>
```

- через пробел указываются строки
- в каждой строке перечисляются названия зон через пробел
- `.` (точка) - пустая ячейка
- названия могут быть любыми
- **важно:** указать имена для **каждой** ячейки

💡 Очень удобно для создания макетов страниц (header, sidebar, main, footer)

---

# Промежутки: `gap`

```css
/* одинаковые промежутки по вертикали и горизонтали */
.grid {
  gap: 20px;
}

/* разные промежутки */
.grid {
  gap: 20px 10px; /* вертикаль горизонталь */
}

/* отдельно */
.grid {
  row-gap: 20px;    /* промежуток между строками */
  column-gap: 10px; /* промежуток между колонками */
}
```

---

# Выравнивание содержимого

## `justify-content` (по горизонтали)

```css
.grid {
  justify-content: start;        /* по левому краю */
  justify-content: end;          /* по правому краю */
  justify-content: center;       /* по центру */
  justify-content: stretch;      /* растянуть (по умолчанию) */
  justify-content: space-between; /* равномерно, края прижаты */
  justify-content: space-around;  /* равномерно, отступы по краям в 2 раза меньше */
  justify-content: space-evenly;  /* равномерно везде */
}
```

## `align-items` (по вертикали)

```css
.grid {
  align-items: start;   /* по верху */
  align-items: end;     /* по низу */
  align-items: center;  /* по центру */
  align-items: stretch; /* растянуть на всю высоту */
}
```

## `place-items` (shorthand)

```css
/* вертикаль / горизонталь */
.grid {
  place-items: center end;
}

/* одинаковое значение для обоих осей */
.grid {
  place-items: center;
  /* = align-items: center; justify-content: center; */
}
```

---

# Позиционирование грид-элементов

## Указание линий по номерам

```css
.grid-element {
  /* по горизонтали: со 2-й по 4-ю линию */
  grid-column-start: 2;
  grid-column-end: 4;
  
  /* по вертикали: с 1-й по 3-ю линию */
  grid-row-start: 1;
  grid-row-end: 3;
}
```

## Сокращенная запись

```css
.grid-element {
  grid-column: 2 / 4; /* start / end */
  grid-row: 1 / 3;    /* start / end */
}
```

## Именованные линии

```css
.grid-container {
  grid-template-columns:
    [start] 1fr 
    [middle-before] 1fr 
    [middle-after] 1fr 
    [end];
}

.grid-element {
  grid-column: middle-before / end;
  grid-row: 1 / 3;
}
```

💡 Если можно задать понятные имена линиям - это повышает читаемость кода

---

## Ключевое слово `span`

```css
/* элемент займет 2 колонки */
.grid-element {
  grid-column: span 2;
  /* браузер сам подберет наилучшую позицию */
}

/* элемент займет 3 строки */
.grid-element {
  grid-row: span 3;
}
```

---

## Растягивание элемента на всю ширину

```css
/* способ 1: явное указание */
.wide {
  grid-column: 1 / 4; /* если 3 колонки */
}

/* способ 2: через span */
.wide {
  grid-column: span 3; /* если 3 колонки */
}

/* способ 3: автоматически (самое изящное) */
.wide {
  grid-column: 1 / -1;
  /* растянет на все колонки независимо от их количества */
}
```

```html
<div class="grid-container">
  <div class="grid-element">Element 1</div>
  <div class="grid-element wide">Element 2 (широкий)</div>
  <div class="grid-element">Element 3</div>
  <div class="grid-element">Element 4</div>
</div>
```

```css
.grid-container {
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(3, 1fr);
}
```

💡 `1 / -1` - самое удобное решение, работает при любом количестве колонок

---

# Порядок элементов: `order`

```css
.grid-element {
  order: -1; /* в самое начало */
}

.grid-element {
  order: 1;  /* в конец */
}

.grid-element {
  order: 0;  /* по умолчанию */
}
```

- меняет визуальный порядок элементов в сетке
- не влияет на порядок в HTML

---

# Практический пример: макет страницы

```css
.page {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: 80px 1fr 60px;
  gap: 20px;
  min-height: 100vh;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.aside { grid-area: aside; }
.footer { grid-area: footer; }
```

```html
<div class="page">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="main">Main content</main>
  <aside class="aside">Aside</aside>
  <footer class="footer">Footer</footer>
</div>
```

---

# Шпаргалка по Grid

|Свойство|Описание|Пример|
|---|---|---|
|`display: grid`|создает грид-контейнер|`display: grid;`|
|`grid-template-columns`|задает колонки|`repeat(3, 1fr)`|
|`grid-template-rows`|задает строки|`100px 200px auto`|
|`grid-template-areas`|задает шаблон сетки|`"header header"`|
|`gap`|промежутки между ячейками|`20px` или `20px 10px`|
|`grid-column`|позиция по горизонтали|`1 / 3` или `span 2`|
|`grid-row`|позиция по вертикали|`1 / 3` или `span 2`|
|`grid-area`|имя области из template|`header`|
|`fr`|доля доступного пространства|`1fr 2fr`|
|`minmax()`|диапазон размеров|`minmax(100px, 1fr)`|
|`repeat()`|повторение значений|`repeat(3, 1fr)`|

---

# Флексы vs Гриды

**Используй Flexbox когда:**

- одномерная раскладка (строка или столбец)
- выравнивание элементов
- элементы разных размеров
- простая навигация, кнопки, карточки

**Используй Grid когда:**

- двумерная раскладка (строки И столбцы)
- сложная сетка
- макет страницы целиком
- элементы должны строго выравниваться по сетке

💡 **Можно комбинировать:** Grid для общего макета страницы, Flexbox внутри отдельных блоков