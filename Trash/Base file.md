# Base CSS (Reset & Normalize)

**Base CSS** - набор базовых стилей, которые обнуляют или нормализуют дефолтные стили браузера для всех проектов.

---

# Зачем нужен Base CSS?

- **Обнуление дефолтных стилей** - у разных браузеров разные стили по умолчанию (margin, padding, border и тд)
- **Единообразие** - проект выглядит одинаково во всех браузерах
- **Удобство** - не нужно каждый раз обнулять стили вручную
- **box-sizing: border-box** - размеры элементов становятся предсказуемыми

---

# Универсальный селектор - обнуление базовых стилей

```css
*,
*::after,
*::before {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
```

**Что делает:**

- `*` - применяется ко всем элементам на странице
- `*::after` и `*::before` - применяется к псевдоэлементам
- `box-sizing: border-box` - размеры элементов включают padding и border (предсказуемые размеры)
- `margin: 0` и `padding: 0` - обнуляем все отступы

---

# `html` - корневой элемент

```css
html {
    height: 100%;
    scroll-behavior: smooth;
    scrollbar-gutter: stable;
}
```

**Что делает:**

- `height: 100%` - высота корневого элемента = высоте окна браузера (пригодится для "прижимания" футера к низу)
- `scroll-behavior: smooth` - плавная прокрутка при клике на якорные ссылки
- `scrollbar-gutter: stable` - убирает скачок интерфейса по горизонтали при появлении/исчезновении скроллбара

---

# `body` - основной контейнер

```css
body {
    min-height: 100%;
    line-height: 1.5;
    font-family: 'Roboto', sans-serif;
    font-style: normal;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
```

**Что делает:**

- `min-height: 100%` - минимальная высота body = высоте окна (для "прижимания" футера к низу)
- `line-height: 1.5` - унифицированный межстрочный интервал для всего сайта
- `font-family` - базовый шрифт для всего сайта
- `-webkit-font-smoothing` и `-moz-osx-font-smoothing` - сглаживание шрифтов на macOS

---

# Ссылки (`<a>`)

```css
a {
    color: inherit;
    text-decoration: none;
    cursor: pointer;
}

a:visited {
    color: inherit;
}
```

**Что делает:**

- `color: inherit` - цвет ссылки наследуется от родителя (нет синего цвета по умолчанию)
- `text-decoration: none` - убирает подчеркивание
- `cursor: pointer` - курсор в виде руки при наведении
- `a:visited` - посещенные ссылки имеют тот же цвет

---

# Кнопки и интерактивные элементы

```css
button,
label,
a {
    cursor: pointer;
    font: inherit;
}

button {
    border: none;
    outline: none;
    background: none;
    -webkit-tap-highlight-color: transparent;
}

button[disabled],
button[aria-disabled="true"] {
    cursor: not-allowed;
    opacity: 0.6;
}

input,
textarea,
select {
    font: inherit;
}
```

**Что делает:**

- `cursor: pointer` - курсор-рука для всех интерактивных элементов
- `font: inherit` - наследуют шрифт от родителя (по умолчанию у кнопок и полей свой шрифт)
- `border: none` и `outline: none` - убирает дефолтные рамки у кнопок
- `background: none` - убирает дефолтный фон кнопок
- `-webkit-tap-highlight-color: transparent` - убирает серую подсветку при тапе на мобильных (iOS/Android)
- `button[disabled]` - заблокированные кнопки имеют курсор `not-allowed` и прозрачность

---

# Списки (`<ul>`, `<ol>`)

```css
ul,
ol {
    list-style: none;
    margin: 0;
    padding: 0;
}
```

**Что делает:**

- `list-style: none` - убирает маркеры списков
- `margin: 0` и `padding: 0` - обнуляет отступы

---

# Изображения (`<img>`)

```css
img {
    display: block;
    max-width: 100%;
    height: auto;
}
```

**Что делает:**

- `display: block` - убирает небольшой отступ снизу у изображений (по умолчанию `inline`)
- `max-width: 100%` - изображение не выходит за границы контейнера
- `height: auto` - высота подстраивается автоматически (сохраняет пропорции)

---

# Заголовки (`<h1>` - `<h6>`) и параграфы (`<p>`)

```css
h1,
h2,
h3,
h4,
h5,
h6,
p {
    margin: 0;
    padding: 0;
    font-weight: inherit;
}
```

**Что делает:**

- `margin: 0` - обнуляет дефолтные отступы
- `font-weight: inherit` - наследует жирность шрифта от родителя (по умолчанию у заголовков `bold`)

---

# Таблицы (`<table>`)

```css
table {
    border-collapse: collapse;
    border-spacing: 0;
}
```

**Что делает:**

- `border-collapse: collapse` - объединяет границы ячеек в одну (убирает двойные границы)
- `border-spacing: 0` - убирает расстояние между ячейками

---

# Формы (`<fieldset>`, `<legend>`)

```css
fieldset {
    margin: 0;
    padding: 0;
    border: none;
}

legend {
    padding: 0;
}
```

**Что делает:**

- обнуляет дефолтные стили у элементов форм

---

# Полный Base CSS (готовый к копированию)

```css
/* ========== УНИВЕРСАЛЬНЫЕ СТИЛИ ========== */
*,
*::after,
*::before {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    border: none;
}

/* ========== HTML & BODY ========== */
html {
    height: 100%;
    scroll-behavior: smooth;
    scrollbar-gutter: stable;
}

body {
    min-height: 100%;
    line-height: 1.5;
    font-family: 'Roboto', sans-serif;
    font-style: normal;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

/* ========== ССЫЛКИ ========== */
a {
    color: inherit;
    text-decoration: none;
    cursor: pointer;
}

a:visited {
    color: inherit;
}

/* ========== КНОПКИ И ИНТЕРАКТИВНЫЕ ЭЛЕМЕНТЫ ========== */
button,
label {
    cursor: pointer;
}

button {
    border: none;
    outline: none;
    background: none;
    font: inherit;
    -webkit-tap-highlight-color: transparent;
}

button[disabled],
button[aria-disabled="true"] {
    cursor: not-allowed;
    opacity: 0.6;
}

input,
textarea,
select {
    font: inherit;
}

/* ========== СПИСКИ ========== */
ul,
ol {
    list-style: none;
}

/* ========== ИЗОБРАЖЕНИЯ ========== */
img {
    display: block;
    max-width: 100%;
    height: auto;
}

/* ========== ЗАГОЛОВКИ И ПАРАГРАФЫ ========== */
h1,
h2,
h3,
h4,
h5,
h6,
p {
    font-weight: inherit;
}

/* ========== ТАБЛИЦЫ ========== */
table {
    border-collapse: collapse;
    border-spacing: 0;
}
```

---



## Добавил от себя:

- `-webkit-font-smoothing` и `-moz-osx-font-smoothing` для сглаживания шрифтов на macOS
- `button[disabled]` - стили для заблокированных кнопок (курсор + прозрачность)
- `background: none` для кнопок - убирает дефолтный фон
- `font-weight: inherit` для заголовков - чтобы можно было управлять жирностью
