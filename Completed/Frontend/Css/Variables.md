# CSS (Variables)

```css
/* объявление CSS переменных */
:root {
  --color-main: #20855e;
  --color-accent: red;
  --border-radius: 10px;
}

/* использование переменных */
button {
  background-color: var(--color-main);
  border-radius: var(--border-radius);
}

/* с резервным значением */
.btn {
  box-shadow: var(--box-shadow, 2px 2px 2px green);
}
```

- **CSS переменные** = токены = кастомные свойства
- позволяют хранить значения для последующего переиспользования

---

# Объявление переменных

```css
body {
  /* нужно написать 2 дефиса, затем название */
  --color-main: #20855e;      /* kebab-case - использовать для большинства */
  --colorAccent: red;         /* camelCase - использовать для некоторых */
  --BORDER_RADIUS: 10px;      /* UPPER_CASE - редко */
}
```

- объявление происходит в рамках какого-то селектора (регистр может быть любой)

---

# Использование переменных

```css
button {
  /* использование через функцию var() */
  background-color: var(--color-main);
  
  /* с резервным значением через запятую */
  box-shadow: var(--box-shadow, 2px 2px 2px green);
}
```

- в var() обычно указывают только одно значение
  
**Резервное значение** применяется только в 2 случаях:
1. переменная не объявлена вовсе
2. переменная объявлена, но в недоступной области видимости

---

# Область видимости переменных

```html
<div class="box-1">
  1
  <div class="box-2">
    2
    <div class="box-3">
      3
    </div>
  </div>
</div>
```

```css
.box-1 {
  --custom-border: 2px solid red;
  border: var(--custom-border);
}

.box-2 {
  --custom-border: 5px solid blue;  /* переопределение */
  border: var(--custom-border);
}

.box-3 {
  border: var(--custom-border);  /* использует значение из .box-2 */
}
```

- при объявлении переменной мы привязываем её к определённому селектору
- переменная становится доступна для текущего элемента и всех вложенных элементов
- вложенные элементы могут **переопределять** переменные

---

# Переменные в качестве значений других переменных

```css
body {
  --color-main: green;
}

.btn {
  --buttonTextColor: var(--color-main);  /* ссылка на другую переменную */
  color: var(--buttonTextColor);
}
```

---

# Глобальные переменные (:root)

```css
/* :root = html, но с большей специфичностью */
:root {
  /* цвета */
  --color-light: #FFFFFF;
  --color-dark: #171414;
  --color-main: #20855e;
  --color-accent: #ffc67c;
  --color-gray: #FAFAFA;
  --color-success: #7dbd6d;
  --color-error: #a41b1b;
  
  /* тени */
  --box-shadow-1: 0 0 2px 4px rgb(0 0 0 / 0.5);
  --box-shadow-2: 12 12 2px 2px rgb(0 0 0 / 0.25);
  
  /* шрифты */
  --font-family-base: 'Roboto', sans-serif;
  --font-family-accent: 'Montserrat', sans-serif;
  
  /* контейнер */
  --container-width: 1200px;
  --container-padding-x: 15px;
  
  /* отступы */
  --section-gap-y: 80px;
  
  /* параметры transition */
  --transition-timing-function: ease-in;
  --transition-duration: 0.2s;
  
  /* z-index слои */
  --layer-default: 0;
  --layer-tooltip: 50;
  --layer-tooltip-control: 75;
  --layer-modal: 100;
  --layer-modal-control: 150;
  --layer-overlay-menu: 200;
  --layer-overlay-control: 250;
  --layer-admin-panel: 500;
  --layer-preloader: 1000;
}
```

- переменные, объявленные в `:root`, доступны **во всём проекте**
- используйте **kebab-case** для глобальных переменных

**Что записывать в глобальные переменные:**

- палитра цветов
- тени
- параметры шрифтов
- параметры контейнера
- вертикальные отступы между секциями
- параметры transition
- значения z-index
- ширина скроллбара
- параметры полей ввода
- стилизация состояния фокуса

💡 В глобальные переменные записывают параметры, которые используются **неоднократно** в проекте - чтобы управлять ими из одного места

### Дополнительные примеры глобальных переменных

```css
:root {
  /* базовые параметры шрифта */
  --base-font-family: 'Heebo', sans-serif;
  --base-font-weight: 400;
  --base-line-height: 1.5;
  --base-font-size: 16px;
  
  /* размеры контейнера */
  --scrollbar-width: 60px;
  --site-width: 1920px;
  --grid-width: 1220px;
  --grid-padding: 15px;
  --section-padding-y: 120px;
  
  /* параметры полей ввода */
  --input-height: 44px;
  --input-size: 100%;
  --input-padding-x: 20px;
  --input-padding-y: 0;
  --input-border-size: 0;
  
  /* стилизация фокуса */
  --focus-outline: 4px dashed var(--focus-outline-color);
  --focus-line-color: var(--light);
  
  /* параметры круглого элемента */
  --round-block-size: 60px;
  
  /* параметры для слоев */
  --layer-controls: 50;
  --layer-section: 75;
  --layer-overlay: 100;
  --layer-overlay-controls: 150;
  --layer-overlay-controls-150: 150;
  --layer-admin: 300;
  --layer-preloader: 1000;
  --layer-admin-list: 35%;
}
```

---
# Локальные переменные компонентов

```css
:root {
  /* глобальные переменные - kebab-case */
  --color-light: #ffffff;
  --color-dark: #000000;
  --color-main: #0c136e;
  --color-accent: #64c7bf;
  --color-secondary: #fff300;
}

/* локальные переменные - camelCase */
/* могут ссылаться на глобальные перменные */
.button {
  --buttonTextColor: var(--color-main);
  --buttonBgColor: var(--color-accent);
  --buttonBorderColor: transparent;
  
  display: inline-flex;
  align-items: center;
  height: 40px;
  padding-inline: 24px;
  color: var(--buttonTextColor);
  background-color: var(--buttonBgColor);
  border: 2px solid var(--buttonBorderColor);
  border-radius: 5px;
}

/* модификация через переопределение */
.button.yellow {
  --buttonBgColor: var(--color-secondary);
}

.button.transparent {
  --buttonTextColor: var(--color-dark);
  --buttonBgColor: transparent;
  --buttonBorderColor: var(--color-dark);
}
```

```html
<button class="button">Main button</button>
<button class="button yellow">Yellow button</button>
<button class="button transparent">Transparent button</button>
```

**Нейминг:**
- **глобальные переменные** → `kebab-case`
- **локальные переменные** → `camelCase`

**Зачем нужны локальные переменные:**
- упрощают модификацию компонентов
- избегают дублирования кода
- достаточно переопределить переменную, а не все свойства

---

## Плохой подход (без локальных переменных)

- HTML разметка (одинакова для обоих подходов)

```html
<button class="button">
  <span class="button-icon-before">☀️</span>
  <span class="button-label">Main button</span>
  <span class="button-icon-after">🌙</span>
</button>

<button class="button yellow">
  <span class="button-icon-before">☀️</span>
  <span class="button-label">Yellow button</span>
  <span class="button-icon-after">🌙</span>
</button>

<button class="button transparent">
  <span class="button-icon-before">☀️</span>
  <span class="button-label">Transparent button</span>
  <span class="button-icon-after">🌙</span>
</button>
```

```css
/* базовые стили кнопки */
.button {
  display: inline-flex;
  align-items: center;
  column-gap: 0.5em;
  background-color: transparent;
  border: none;
}

/* стили для иконок */
.button-icon-before,
.button-icon-after {
  color: var(--color-main);
}

/* стили для лейбла */
.button-label {
  display: inline-flex;
  align-items: center;
  height: 40px;
  padding-inline: 12px;
  color: var(--color-main);
  background-color: var(--color-accent);
  border: 2px solid transparent;
  border-radius: 5px;
}

/* МОДИФИКАЦИЯ: yellow - приходится дублировать селекторы для каждого элемента */
.button.yellow .button-label {
  background-color: var(--color-secondary);  /* меняем только цвет фона лейбла */
}

.button.yellow .button-icon-before,
.button.yellow .button-icon-after {
  color: var(--color-secondary);  /* меняем цвет обеих иконок */
}

/* МОДИФИКАЦИЯ: transparent - снова дублирование */
.button.transparent .button-label {
  color: var(--color-dark);             /* меняем цвет текста */
  background-color: transparent;        /* убираем фон */
  border: 2px solid var(--color-dark);  /* добавляем рамку */
}

.button.transparent .button-icon-before,
.button.transparent .button-icon-after {
  color: var(--color-dark);  /* меняем цвет обеих иконок */
}

/* 
ПРОБЛЕМЫ:
❌ Для каждой модификации нужно прописывать стили для КАЖДОГО вложенного элемента
❌ Много дублирования селекторов (.button-icon-before, .button-icon-after)
❌ Если добавить еще модификаций — код станет огромным
❌ Если добавить еще элементов в кнопку — придется дублировать еще больше
❌ Сложно поддерживать и масштабировать
*/
```

## Хороший подход (с локальными переменными)

-  HTML разметка та же самая

```css
/* базовые стили кнопки + объявление локальных переменных */
.button {
  /* ЛОКАЛЬНЫЕ ПЕРЕМЕННЫЕ - все параметры в одном месте */
  --buttonIconColor: var(--color-main);
  --buttonTextColor: var(--color-main);
  --buttonBgColor: var(--color-accent);
  --buttonBorderColor: transparent;
  
  display: inline-flex;
  align-items: center;
  column-gap: 0.5em;
  background-color: transparent;
  border: none;
}

/* стили для иконок - используют переменную */
.button-icon-before,
.button-icon-after {
  color: var(--buttonIconColor);  /* вместо прямого цвета - переменная */
}

/* стили для лейбла - используют переменные */
.button-label {
  display: inline-flex;
  align-items: center;
  height: 40px;
  padding-inline: 12px;
  color: var(--buttonTextColor);        /* переменная */
  background-color: var(--buttonBgColor);  /* переменная */
  border: 2px solid var(--buttonBorderColor);  /* переменная */
  border-radius: 5px;
}

/* МОДИФИКАЦИЯ: yellow - ВСЕГО 3 СТРОКИ! */
.button.yellow {
  --buttonBgColor: var(--color-secondary);  /* меняем только одну переменную */
  /* все вложенные элементы автоматически получат новый цвет */
}

/* МОДИФИКАЦИЯ: transparent - ВСЕГО 5 СТРОК! */
.button.transparent {
  --buttonTextColor: var(--color-dark);     /* меняем цвет текста */
  --buttonBgColor: transparent;             /* убираем фон */
  --buttonBorderColor: var(--color-dark);   /* добавляем рамку */
  /* все вложенные элементы автоматически обновятся */
}

/* 
ПРЕИМУЩЕСТВА:
✅ Для модификации достаточно переопределить переменные - НЕ НУЖНО трогать вложенные элементы
✅ Код модификации в 3-5 строк вместо 10-15
✅ Легко добавлять новые модификации
✅ Если добавить новые элементы - они автоматически подхватят переменные
✅ Легко поддерживать и масштабировать
✅ Видно ВСЕ параметры компонента в одном месте
*/
```

💡 **Разница очевидна**: код с локальными переменными **в 2-3 раза короче** и **намного проще** в поддержке!

💡 Чтобы модифицировать компоненты, достаточно **лаконично в пару строк** переопределить переменные

---

# Изящное решение для фоновых изображений

## Проблема с inline-стилями

```html
<section class="banner">
  <h1 class="banner-title">Banner Title</h1>
</section>
```

```css
.banner {
  min-height: 100vh;
  background: url('./bg.jpg') center/cover no-repeat;
}
```

**Если сайт работает на CMS** и бэкенд добавляет фон через инлайновые стили:

```html
<!-- инлайновые стили имеют максимальный приоритет -->
<section class="banner" style="background-image: url('./bg.jpg');">
  <h1 class="banner-title">Banner Title</h1>
</section>
```

```css
.banner {
  min-height: 100vh;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  
  /* чтобы переопределить inline-стили, нужен !important (плохая практика) */
  background-image: url('./other-bg.jpg') !important;
}
```

**Проблема:** переопределить `background-image` из inline-стилей в CSS можно только через `!important`

## Решение через CSS переменные - упрощаем жизнь бэкэндеру

```html
<!-- вместо background-image используем переменную -->
<section class="banner" style="--bgImg: url('./bg.jpg');">
  <h1 class="banner-title">Banner Title</h1>
</section>
```

```css
.banner {
  min-height: 100vh;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  
  /* используем переменную */
  background-image: var(--bgImg);
}

/* легко переопределить без !important */
.banner-no-image {
  background-image: none;
  background-color: red;
}
```

**Преимущества:**

- можно переопределять фон на уровне CSS без `!important`
- гибкость: можно убрать изображение или заменить на цвет
- не нарушается каскад стилей
- упрощается работа контент-менеджеру на CMS

---

# Практические примеры

## Тёмная/светлая тема

```css
:root {
  --bg-color: #fff;
  --text-color: #000;
}

[data-theme="dark"] {
  --bg-color: #1a1a1a;
  --text-color: #fff;
}

body {
  background-color: var(--bg-color);
  color: var(--text-color);
}
```

## Адаптивные значения

```css
:root {
  --container-width: 1200px;
  --section-padding-y: 80px;
}

@media (max-width: 768px) {
  :root {
    --container-width: 100%;
    --section-padding-y: 40px;
  }
}

.container {
  max-width: var(--container-width);
}

.section {
  padding-block: var(--section-padding-y);
}
```

## Динамические сетки

```css
.grid {
  --columns: 3;
  --gap: 20px;
  
  display: grid;
  grid-template-columns: repeat(var(--columns), 1fr);
  gap: var(--gap);
}

.grid-4-cols {
  --columns: 4;
}

.grid-dense {
  --gap: 10px;
}
```