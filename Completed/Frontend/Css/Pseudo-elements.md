- **Псевдоэлементы** - элементы, которые не существуют в HTML разметке и создаются через CSS с помощью специальных селекторов

---

# `::before` и `::after` - универсальные псевдоэлементы

```css
.box::before {
  content: "";
  display: block;
  width: 50px;
  height: 50px;
  background: red;
}

.box::after {
  content: "✓";
  color: green;
}
```

- позволяют прицепить к практически любому элементу на странице вспомогательный элемент **(используются в верстке очень часто)**
- по умолчанию являются **строчными** элементами (`display: inline`)
- может быть максимум 2 псевдоэлемента у элемента (один `::before` и один `::after`)
- **обязательно** нужно прописывать свойство `content`, иначе элемент не появится
- `::before` - добавляет элемент в начало
- `::after` - добавляет элемент в конец


**Возможные значения `content`:**

- `""` - пустая строка (самое частое - используется для добавления других CSS свойств)
- `"text"` - текст или эмодзи
- `url('path/to/image.png')` - изображение
- `attr(data-example)` - значение атрибута элемента из HTML
- `open-quote` / `close-quote` - кавычки
- счетчики нумерованных списков

- **Практическое применение:**
	- можно элементу делать `position: relative`, а псевдоэлементу `position: absolute`
		- **псевдоэлементы позволяют сделать код чище**

---

# `::placeholder` - стилизация placeholder

```css
/* стилизуем все placeholder'ы на странице */
::placeholder {
  color: red;
  background-color: lightgray;
}

/* стилизуем placeholder конкретного input */
input::placeholder {
  color: gray;
  font-style: italic;
}
```

- `::placeholder` - позволяет получить доступ к `placeholder` у полей `input` или `textarea`
	- прописывается через атрибут `placeholder` в HTML разметке
- на placeholder действуют только параметры **текста** и **фона**
	- **в большинстве случаев от placeholder требуется только поменять цвет текста**

---

# `::file-selector-button` - кнопка выбора файла

```css
input::file-selector-button {
  padding: 12px;
  color: red;
  background-color: yellow;
  border: 3px dashed black;
  border-radius: 10px;
}
```

- `::file-selector-button` - позволяет получить доступ к кнопке с предложением выбрать файл
	- нпр.  у поля `<input type="file">`

---

# `::first-letter` - первая буква

```css
.title::first-letter {
  margin-right: 15px;
  padding: 12px 24px;
  font-size: 3rem;
  border: 3px solid skyblue;
  background-color: blue;
  box-shadow: 0 0 10px 0 rgb(0 0 0 / 0.75);
}
```

- `::first-letter` - позволяет получить доступ к первой буквы любого элемента с текстовым содержимым

---

# `::first-line` - первая строка

```html
<p>
  First Line
  Second Line
</p>
```

```css
p::first-line {
  text-transform: uppercase;
  color: red;
  background-color: lightcoral;
  box-shadow: 0 0 10px 0 rgb(0 0 0 / 0.75);
}
```

- `::first-line` - позволяет получить доступ к первой строке любого элемента с текстовым содержимым
- **нужно внимательно смотреть на ширину блока с текстом**
	- лучше сразу ограничить блок, чтобы точно знать что к первой строке применятся стили
	- можно через `<br>`, но это костыль

---

# `::selection` - выделение текста

```css
p::selection {
  color: orange;
  background-color: coral;
  text-shadow: 2px 2px 2px black;
  text-decoration: underline;
}
```

- `::selection` - позволяет обратиться к состоянию текста при его выделении
- **в реальной практике зачастую меняют только цвет текста и фона**

---

# `::marker` - маркеры списков

```css
li::marker {
  color: red; /* цвет маркера */
}

/* or */
li::marker {
  content: "→"; /* заменяем оригинальный маркер */
}
```

- `::marker` - позволяет обратиться к маркерам у элементов списков (`<ul>`, `<ol>`)
	- можно менять цвет или заменять символ маркера