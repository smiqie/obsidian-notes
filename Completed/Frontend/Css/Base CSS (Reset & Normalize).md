# Base CSS (Reset & Normalize)

- **Base CSS** - набор базовых стилей, которые обнуляют или нормализуют дефолтные стили браузера для всех проектов.

### BASE.CSS vs TYPOGRAPHY.CSS

- Смысл разделения: `base` задаёт наследуемую базу для всего проекта, `typography` описывает конкретные текстовые стили
	- Если нужно поменять шрифт проекта - изменяем только одно место в `base` (в `body{}`)

- **`typography.css`** - конкретные стили под элементы:

```css
h1 { font-size: 2.5rem; font-weight: 700; line-height: 1.2; }
h2 { font-size: 2rem; font-weight: 600; }
.text-sm { font-size: 0.875rem; }
```

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

- `height: 100%` - высота корневого элемента = высоте окна браузера (пригодится в большинстве ситуаций, нпр. для "прижимания" футера к низу)
- `scroll-behavior: smooth` - плавная прокрутка при клике на якорные ссылки
- `scrollbar-gutter: stable` - убирает скачок интерфейса по горизонтали при появлении/исчезновении скроллбара

---

# `body` - основной контейнер

```css
body {
    min-height: 100%;
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    
    /* настройка шрифтов для всего проекта */
    font-family: "Roboto", sans-serif;
    font-style: normal;
}
```

**Что делает:**

- `min-height: 100%` - минимальная высота body = высоте окна (для "прижимания" футера к низу) - работает с комбинацией `html{ height: 100%; }` при сбросе стилей
- `line-height: 1.5` - унифицированный межстрочный интервал для всего сайта (браузеры обычно ставят `~1.2` по умолчанию, но WCAG рекомендует минимум `1.5`)
- `-webkit-font-smoothing` и `-moz-osx-font-smoothing` - сглаживание шрифтов на macOS

---

# Ссылки (`<a>`)

```css
a {
    color: inherit;
    text-decoration: none;
}

a:visited {
    color: inherit;
}

/* специфичность = 0, легко переопределить без войны специфичности */
a:where([class]) {
	display: inline-flex; 
}
```


**Что делает:**

- `color: inherit` - убирает дефолтный синий браузера, цвет берётся от родителя (лучше для дизайна)
- `a:visited` - отдельный селектор нужен потому что браузер применяет стиль посещённых ссылок поверх обычных, простого `inherit` на `a` не хватает

- `text-decoration: none` - убирает подчёркивание

- `a:where([class]){ display: inline-flex; }` - нормализация высоты элемента ссылки при его инспектировании в DevTools
	- Когда `a` - `inline`, DevTools показывает высоту через `line-height`, а не реальный контент. `inline-flex` считает высоту правильно
	- `:where()` обнуляет специфичность, чтобы не мешать твоим стилям

---

# Кнопки и интерактивные элементы

```css
button,
label,
a {
    cursor: pointer;
}

button {
    border: none;
    background: none;
    -webkit-tap-highlight-color: transparent;
}

fieldset {
    border: none;
}

button[disabled],
button[aria-disabled="true"] {
    cursor: not-allowed;
    opacity: 0.6;
}

input,
textarea,
select,
button,
label {
    font: inherit;
}
```

**Что делает:**

- `cursor: pointer` - курсор-рука для всех интерактивных элементов (UX)
- `font: inherit` - наследуют шрифт от родителя (по умолчанию у кнопок и полей свой шрифт)
- `border: none` - убирает дефолтные рамки у кнопок и fieldset
- `background: none` - убирает дефолтный фон кнопок
- `-webkit-tap-highlight-color: transparent` - убирает серую подсветку при тапе на мобильных (iOS/Android)

* `button[disabled]` - заблокированная кнопка, недоступна и выпадает из фокуса клавиатуры
* `button[aria-disabled="true"]` - визуально заблокирована (курсор + прозрачность), но остаётся в фокусе - скринридер может объяснить пользователю почему кнопка недоступна


---

# Списки (`<ul>`, `<ol>`)

```css
ul,
ol {
    list-style: none;
}
```

**Что делает:**

- `list-style: none` - убирает маркеры списков

---

# Изображения (`<img>` & `<video>`)

```css
img,
video {
    display: block;
}
```

**Что делает:**

- `display: block` - убирает небольшой отступ снизу у изображений и видео (по умолчанию `inline`)

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
    font-weight: inherit;
}
```

**Что делает:**

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