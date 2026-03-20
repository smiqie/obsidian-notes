- callback function = функция аргумент
	- ь.е. функция передается как аргумент в другую функцию и вызывается уже в другую функцию

- 1 пример
```js
function greeting(){
	console.log("Hello!")
}

// cb = сокращение от callback
function showGreeting(cb){ // аргумент функции 
	cb(); // вызываем его
}

showGreeting(greeting); // передаем нашу фнукцию без круглыъ скобок, т.е. по сути передаем ссылку на функцию а не вызываем ее
```

- 2 пример
```js
function getInfo(name, age){
	return `Name: ${name}\nAge: ${age}`;
}
function getInfoWithCurrentDate(callback){
	const now = new Date();
	console.log(`Today: ${now.toISOString()}\n${callback("Dima", 33)}`);
}

getInfoWithCurrentDate(getInfo);
```

- 3 вопрос
```js
// Fn - сокращение от слова function
function survey(qusetion, agreedFn, disagreedFn){
	if(confirm(qusteion)){
		agreedFn();
	}
	else{
		disagreedFn();
	}
}

// function () {console.log( "Ты согласился, что ты мой друг!" )} - создание функцции без названия...? чзх типо динамическое созданеи фнукции или че
survey(
	"Ты мой друг?",
	function () {console.log( "Ты согласился, что ты мой друг!" )},
	function () {console.log( "Ты согласился, что ты мой друг!" )},
);
```




























































































































































































































































































































