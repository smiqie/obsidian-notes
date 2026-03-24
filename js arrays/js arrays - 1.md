
- методы массивов:

- полоезная штука (что делает?)
```js
const numbers = new Array(1, 2, 3, 4, 5);
const lastValue = numbers.pop(); // сохраняем значение удаленное из массива для будущизх операций с ней?
```
- статические меторды массива (т.к. находятся в рамках объекта Эррей)
	1. `Array.isArray(123)` - возвращает булеан значение, в зависимости от того явлется ли переданнный обхъект массивом или нет
	2. `const arr = Array.of(1, 2, "text")` - создает массив из переданных щначений, аргументы - элементы которые будут даовблены в массив
	3. `const arr = Array.from("1234")` - создает массив из перпеданной строки - разбирает строка на символы и возвращет массив -- `['1', '2', '3', '4']` помимо строки можно передать массив, мап, сет и тд




- деструктуризация - не измняет исхгодный массив а просто копирует значения

```js
const names = ["Max", "Alex", "Stacy"];
// 1й способ - много кода
const nameMax = names[0]; 
const nameAlex = names[1];

// 2й способ - испольузется часто в разработке и более элегантный (деструктурируюбщее присваивание)
const [nameMax, nameAlex, dfsdsaf] = names; // nameMax = "Max", nameAlex="Alex", dfsdsaf = "Stacy" - элеенты присваиваются по порядку


//
const names = ["Kate"];
const [nameKate, nameOlga] = names; // nameKate = "Kate", nameOlga = undefined
const [nameKate, nameOlga = "Olga"] = names; // присваиваем значение по умолчанию / те есть ли элемента в массиве нету то присваиваем знаечние по умолчанию


// ПРИМЕР С РЕАКТОМ
// почти в кажом компоненте есть хуки, самый попялрный это useState
// оченб чатсо почти в кажом компоненте где етсь какоето состояние увидим такую запись
const [counter, setCounter] = useState(0);
// по стуи useState это функция НО функция с приставуой use принято считать хуком, useState возвращает кортеж
```



- **оператор** расширения (оч чатсо встречается на практике) spread

```js
// адача: есть два массива  с именами, мы хоти их объекенить в новый массив + добавить имена от себя (по сути могли бы использвоать конкат но этот способ лучше)
const names1 = ["Kate"];
const names2 = ["Max", "Alex", "Stacy"];

// это оператор состоит из 3х точек, по сути берет и расклдывает массив идущий после гнего на значения 
const allNames = [...names, "Nick", "Dima", ...names2];

// также работает и со строками (т.к стркоа по сути тож массив)
const strHi = "Hi";
console.log([...strHi]); // ['H', 'i']

// гнаходим наибольший и наимешьий элеемнт массива с помозщбю оператора спрэд
const numbers = [1, 24, 546, 12];
console.log(Math.max(...numbbers)); // по сути ралсожит весь массив на значения а max уже вернет маскимальное из них
```

- rest - по сути тоже мождно назвать опертоаром (остаточные параметры) - по сути работает противоположно, не раскалдывает массив а наоборрот собирает его из кусочков
```js
// пример
const sum (...numbers) => {
	const sum = 0;
	for(const value of numbers){
		sum += value;
	}
	return sum;
}

// можем передавтаь сколько гуодно аргументов 
sum(1, 2, 3, 4);
sum(1, 2, 3); 


// ================ еше пример
const names = ["Max", "Alex", "Stacy"];
const [firstName, ...restNames] = names; // присваиваем 1е значение перемнной firstName (firstName = "Max"), а все остальные знаечния массива присваиваем перменной restNames (по стуи оа будет явлться массиво с 2мя значениями)
```

- важно! остаточные парметры всегда должны рапсологаться в конце функции - как последний параметр/аргумент (если унее несколько аргументов)
	```js
	// correct
	const fn = (ar1, ar2, ...rest) => {}
	
	// ne pravilno
	const fn = (ar1, ...rest, ar2) => {}
	```

- spread & rest очень удобные штуки и используются повсеместно


---

# самые полезные методы ькоторый используются ОЧЕНЬ часто в релаьной разработке

- 
```js
const skills = ["html", "css", "scss", "js", "git", "ts", "react"];

// forEach - перебор массива
skills.forEach((value) => console.log(value)); // пробьегает по массиву, принимает колюэк функцию, value - элемент массива на каждой итерации после => идет то что мы делаем? 
skills.forEach((value, index) => console.log(value, index)); // колбэк фукнкци яомжет принимать 2 аргуемнты (1йф само значение второй его индекс)
skills.forEach((value, index, thisArray) => console.log(thisArray)); // также есть 3 й аругмент (названия аргументам можно давать любые), возвращает весь б массив на кажой итерации

// или иожем сделтаь так
const logValues = (value) => console.log(value); // создаем перемнну. с  колюэк функцией?
skills.forEach(logValues); // и передаем ее как ссылку (без скобок!)

// различие между 1м и 2м способом -- 1й мы передавали функцию сразу в скобках - как ананимную (обычно так и делают!!!) - но елси логика слишком большая можно использовать 2й вариант

// также есть 3й вариант
const logValues = (value) => console.log(value); 
function logValuesFr(value){ console.log(value); } // можем также доавблять сотальные аругемнты - index и thisArray
skills.forEach(logValuesFr);
```


```js

// если в лябда условие? ток 1 аргмент его не обзательно ложить в скобочки
// но лучши чтобы они всегда были - лучше для расширения кода  в будущем
const evenNumbers = [1,2,3,4,5,6,7,8,9,10].filter(num => num % 2 === 0);
```


2 НАИМОШНЕШИХ МТЕОДОВ - ИСПОЛЬЗУЮТСЯ ПОТСОЯННО

```js
 // 2й пример, получаем тот же массив но так с 2мя полями вместо 4х (т.е. все остальные вырезали под нужный нам вид)
const clientNamesAndStatuses = clients.map(client => {
	 return {
		 age: Math.random() * 50 + 30, // добавлии свой ключ
		 name: client.name,
		 status: client.status
	 }
 }).map(client => { // дальше для полей со статусом сделли красивые значки в допустим профиле
	 if(client.status === "online"){
		 client.status = "online 🟢";
	 } else{
		 client.status = "offline 🔴";
	 }
	 
	 return client;
 }).filter(client => client.status.startsWith("on")); // и в конце получили массив только тех пользователей что онлайн
```

- 
```js
// сумма всех элементов массива / мождно не ток числа пердавать в метод редюс
const numbers = [1,2,3,4,5,6,7,8,9,10];
const sumAllNumbers = numbers.reduce((accumulator, currentValue) => {
	return accumulator + currentValue;
}, [0]); // initiial = исходное знаечние accumulator (в данном примере accumulator = 0) 

// или еще корчое // у initiial можно писать со скобками а можно без?
const sumAllNumbers = numbers.reduce((sum, value) => sum + value, 0;



//
const books = [
	{id: 1, title: "Harry Potter", price: 59, category: "fantacy"},
	{id: 2, title: "добавь свои имена и снизу тож", price: 108, category: "science"},
	{id: 3, title: "", price: 149, category: "fantacy"},
	{id: 4, title: "", price: 173, category: "science"},
	{id: 5, title: "", price: 73, category: "fantacy"},
];


const categoryMap = books.reduce((res, book) => {
	if(book.category in res){
		res[book.category]++; // уеличиваем колво
	} else{
		res[book.category] = 1; // добавляем динамичсекий ключ в объект
	}
	return res;
}, {}); // передаем не 0 а - {} (т.к. хотим сделать пустой объект?)
```
