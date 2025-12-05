## `:first-child`

- выбирает элемент, если он первый дочерний у своего родителя

```css
li:first-child { color: red; }
```

## `:last-child`

- выбирает элемент, если он последний дочерний у своего родителя

```css
li:last-child { border-bottom: none; }
```

## `:focus`

- срабатывает, когда элемент получает фокус
- работает с интерактивными элементами и элементами с `tabindex`

```css
button:focus { box-shadow: 0 0 5px rgba(0,0,255,0.5); }
```

## `:hover`

- срабатывает, когда курсор наведён на элемент (на touch-устройствах нестабилен)

```css
/* комбинация двух псевдоклассов */ 
button:hover:focus { background-color: darkblue; }
```

## `:focus-within`

- срабатывает на родительском элементе, если любой из его потомков получил фокус

```css
form:focus-within {
  border: 2px solid blue;
  box-shadow: 0 0 10px rgba(0,0,255,0.3);
}
```

## `:placeholder-shown`

- срабатывает, когда placeholder видим (т.е. input пустой)
- только для элементов с атрибутом `placeholder` (исчезает при вводе текста)

```css
input:placeholder-shown { border-color: gray; }

input:not(:placeholder-shown) { border-color: green; }
```

## `:not()`

- инвертирует селектор - выбирает всё, кроме указанного условия

```css
li:not(:first-child) { margin-top: 10px; }

p:not(.special) { color: gray; }

li:not(:first-child):not(:last-child) { margin: 10px 0; }
```