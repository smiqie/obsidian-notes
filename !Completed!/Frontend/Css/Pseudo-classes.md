# 1. Теория

- **Псевдоклассы** - специальные селекторы, которые выбирают элементы по определённым условиям (порядок среди соседей, состояние hover/focus, наличие класса и т.д.)

---
# 2. Псевдоклассы порядка (:child)

## `:first-child`

```css
li:first-child { color: red; }
```

- выбирает элемент, если он **первый** дочерний у своего родителя

## `:last-child`

```css
li:last-child { border-bottom: none; }
```

- выбирает элемент, если он **последний** дочерний у своего родителя

## `:nth-child(odd)`

```css
li:nth-child(odd) { background: #f0f0f0; }
```

- выбирает все **нечётные** элементы среди дочерних у родителя (1, 3, 5, 7...)

## `:nth-child(even)`

```css
li:nth-child(even) { background: #e0e0e0; }
```

- выбирает все **чётные** элементы среди дочерних у родителя (2, 4, 6, 8...)

## `:nth-child()` и `:nth-last-child()` - выбор по порядку

```css
/* Каждый 3-й элемент, начиная с 3-го */
li:nth-child(3n) { 
  border-bottom: none; 
}

/* Каждый 3-й элемент, начиная с 5-го */
li:nth-child(3n + 5) { 
  border-bottom: none; 
}

/* Первые 4 элемента */
li:nth-child(-n + 4) { 
  border-bottom: none; 
}
```

- `:nth-child(3n)` - каждый 3-й элемент у своего родителя, начиная с 3-го
- `:nth-child(3n + 5)` - каждый 3-й элемент, начиная с индекса указанного после `+`
- `:nth-child(-n + 4)` - первые 4 элемента (нестандартный пример применения)
- **`:nth-last-child()` - то же самое, но отсчет с конца**

## `:only-child` - единственный ребенок

```html
<ul>
  <li>Item1</li>
  <li>Item2</li>
</ul>

<ul>
  <li>единственный элемент</li>
</ul>
```

```css
li:only-child { 
  border-bottom: none; 
}
```

- выбирает элемент, который является единственным дочерним элементом своего родителя
- используется редко, но позволяет сэкономить десятки строчек JavaScript костылей

---
# 3. Псевдокласс отрицания

# `:not()` - инверсия селектора

```css
/* все элементы кроме первого */
li:not(:first-child) { 
  margin-top: 10px; 
}

/* все div без класса is-active */
div:not(.is-active) { 
  display: none; 
}

/* все элементы кроме первого и последнего */
li:not(:first-child):not(:last-child) { 
  margin: 10px 0; 
}
```

- инвертирует селектор - выбирает всё, **кроме** указанного условия
- помогает сократить большое количество CSS кода если правильно использовать
- можно комбинировать несколько `:not()`

---

# 4. Псевдоклассы состояния (интерактивные)

## `:hover`

```css
button:hover { 
  background: #0056b3; 
}

/* комбинация двух псевдоклассов */
button:hover:focus { 
  background: darkblue; 
}
```

- срабатывает при наведении курсора (на touch-устройствах нестабилен)
- **хороший UX** - добавлять на любые интерактивные элементы (кнопки, ссылки, поля ввода, чекбоксы, селекты, радио-кнопки)

## `:focus`

```css
input:focus { 
  outline: 2px solid blue; 
}
```

- срабатывает когда элемент в фокусе (через Tab или клик мышкой)
- в большинстве браузеров фокус сохраняется после клика мышью (выглядит как "залипание") - **плохой UX**
	- **решение проблемы залипания:** использовать `:focus-visible`
- работает с интерактивными элементами и элементами с `tabindex`

## `:focus-visible`

```css
button:focus-visible { 
  outline: 3px solid orange; 
}
```

- аналог `:focus`, но срабатывает **только** при клавиатурной навигации
- решает проблему лишнего outline после клика мышью

## `:active`

```css
a:active { 
  color: red; 
}
```

- срабатывает в момент нажатия на элемент (на долю мгновения или если зажать ЛКМ)

## `:visited`

```css
a:visited { 
  color: purple; 
}
```

- применяется к уже посещённым ссылкам

## `:disabled`

```css
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

- состояние элементов с атрибутом `disabled` (`button`, `input`, `textarea`, `select`, `option`, `optgroup`, `fieldset`)
- позволяет переопределить стили `disabled` по умолчанию (заданные браузерами)

## `:checked`

```css
input:checked { 
  box-shadow: 0 0 0 3px hotpink; 
}
```

- состояние отмеченных `checkbox`/`radio` или элементов с атрибутом `checked`

### **Кастомный чекбокс (популярная задача):**

```css
.visually-hidden {
  position: absolute !important;
  width: 1px !important;
  height: 1px !important;
  margin: -1px !important;
  border: 0 !important;
  padding: 0 !important;
  white-space: nowrap !important;
  clip-path: inset(100%) !important;
  clip: rect(0 0 0 0) !important;
  overflow: hidden !important;
}

.checkbox {
  display: flex;
  column-gap: 0.5em;
  user-select: none;
}

.checkbox-control:not(:checked) + .checkbox-emulator::after {
  display: none;
}

.checkbox-emulator {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  width: 1em;
  height: 1em;
  border: 2px solid lightskyblue;
  border-radius: 5px;
  background-color: paleturquoise;
}

.checkbox-emulator::after {
  content: "✓";
  color: green;
}
```

```html
<label class="checkbox">

  <input class="checkbox-control visually-hidden" id="checkbox-1"                  type="checkbox"/>
  
  <span class="checkbox-emulator"></span>
  <span class="checkbox-label">Checkbox 1</span>
  
</label>
```

**Как это работает:**

- настоящий `<input>` скрывается доступным способом (`.visually-hidden`)
- стилизуется соседний элемент-«эмулятор» (`.checkbox-emulator`)
- галочка показывается только при `:checked` через `.checkbox-control:not(:checked) + .checkbox-emulator::after`