- IIFE --> imeditely invoked function expression (немедленно вызывающаяся функция)
- у var есть глоабльная область видимости , и раньше когда вар не могли окграничить локальной областью видимости то придумали подход IIFE - по факту эта шутка больше не юзается но ее нужно значть для рабьоты с легаси кодом (может встретиться)
- пример
```js
// таким хитрым способ можно ограничить глобальную облатсь у перемнной вар
(function() {
	var message = "Hello user!"; 
	console.log(message);
})();

console.log(message); // Reference Error: message is not defined
```

- пример с аргументами
```js
(function(name) {
	var message = "Hello user!"; 
	console.log(message, name);
})("Anna");

console.log(message); // Reference Error: message is not defined
```
