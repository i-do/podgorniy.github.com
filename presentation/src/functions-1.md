#Функции#



##Функция##
Исполняемый объект


##Исполняемый##
Выполняет некоторые действия (с или без побочных эффектов) и вычисляется в значение

	function hi() {
		return 'hi';
	};

	console.log(hi());


##Объект##

* Имеет свойства и методы объекта (+ методы и свойства, характерные для функций)  
* Присваивается и сравнивается по ссылке  
* Передается как аргумент и возвращается как результат


##Объект##

	var hi = function () {
		return 'hi';
	};

	var hello = function () {
		return 'hi';
	};

	var hiReference;

	console.log(hi === hello); // false
	hiReference = hi;
	hello = hi;
	console.log(hi === hello); // true



##Объявление##
* function declaration
* function expression


##function declaration##
	
	function main() {
		// function body
	}


##function expression##
	
	var main = function () {
		// function body
	}


##В чем разница##
способ и время создания переменных и присвоение в них ссылки на функцию  
function declaration доступна до своего фактического объявления в коде


##function declaration##

	main(); // "Lala"
	function main() {
		alert('Lala');
	}


##function expression##

	main(); // TypeError: 'undefined' is not a function
	var main = function() {
		alert('Lala');
	}



##Рекомендации к объявлению функций##
* Не объявляйте функции в блоках ветвления
* Объявляйте функции до их фактического использования


##Возвращаемое значение##
Любое значение, например другая функция

	// js
	function main () {
		return true;
	}
	
	function main () {
		return function () {
			return true;
		};
	}


##Объявление функции с аргументами##
	
	function main (items, callback) {
		// useful stuff
	}


##Вызов функции с аргументами##
* В момент вызова инициализируются переменные с именами аргументов
* Переменные создаются даже, если аргументы не были переданы
* В функцию можно передать любое количество аргументов


##Вызов функции с аргументами##
	
	function main (items, callback) {
		console.log(items, callback);
	}

	main([1,2,3], function () {}); // [1,2,3], function
	main([1,2,3]); // [1,2,3], undefined
	main(); // undefined, undefined


##Вызов функции с аргументами##
	
	function getData (dataSrc, getLatest) {
		if (getLatest || !isInCache(dataSrc)) {
			return requestData(dataSrc);
		} else {
			return getFromCache(dataSrc);
		}
	}

	getData('latestReviews', true);
	getData('users');


##По по ссылке и по значению##
		
	var obj = {};
	var primitive = 10;

	function getData (obj, primitive) {
		obj.test = true;
		primitive += 1;
	}
	
	getData(obj, primitive);
	console.log(obj);		// {test:true}
	console.log(primitive); // 10


##Рекурсивный вызов
Вызов функции из самой себя


##Область видимости переменной##
Это область, в которой к переменной можно обратиться  
(переменная "видна" в этой области видимости)


##Область видимости##
Каждая функция создает область видимости


##Область видимости

	(function () {
		// scope		
	}());


##Переменные и область видимости##
Переменные, объявленные в функции, недоступны за пределами этой функции

	function main () {
		var a = 10;
	}
	a; // ReferenceError


##Переменные и область видимости

Переменные видны во всей области видимости, где они объявлены (даже раньше фактического описания объявления)

	console.log(a);
	var a = 10;
	console.log(a);


##Переменные и область видимости##
Из функции доступны переменные той области видимости, в **которой она объявлена** (а не той, где вызвана).

	var a = 10;

	function main () {
		console.log(a);
	}

	main();


##Переменные и область видимости##
Область видимости, в которой вызывается функция, не влияет на переменные, доступные функции
	
	var a = 20;
	var main = (function () {
		var a = 10;
		return function () {
			console.log(a);
		};
	}());

	main(); // 10


##Переменные и область видимости##
	
	function main () {
		function p () {}
		function f () {
			console.log(p);
		}
		return function () {
			f();
		};
	}

	var a = main();
	a(); //


##Замыкание

	var f = (function () {
		var privateMember;

		privateMember = {test: true};
		return function () {
			console.log(privateMember);
		};
	}());

	f();



##this##
Оператор, возвращающий ссылку на контекст выполнения  
<small>(обычно объект, в котором содежится вызываемый метод, или конструируемый объект)</small>  
Связан только со способом вызова функции  
<small>Не связан с областью видимости, местом хранения функции, способом ее объявления итд.</small>


##this##
Вызов функции, как метода объекта

	var obj = {
		test: function () {
			console.log(this);
		}
	};
	obj.test();


##this##
Что вернет this, определяется способом вызова функции

	var obj = {};
	var test = function () {
		console.log(this);
	};
	obj.test = test;
	obj.test();
	test();


##Функции как методы

* Методы стандартных объектов
* Преобразование примитивов в объекты на момент выполнения метода


##call и apply?##
* передать аргументы массивом
* явно задать значение <strong>this</strong>


##call, apply##
	
	function sum (a, b) {
		return a + b;
	}
	
	sum(10, 20);                 // 30
	sum.call(window, 10, 20);    // 30
	sum.apply(window, [10, 20]); // 30


##Call и Apply##
Задание контекста выполнения функции (что вернет this)

	var obj = {};
	function test () {
		console.log(this);
	}
	test.call(obj);


##Xитрости##
* Максимальное значение в массиве
* Преобразование в массив


##Максимальное значение в массиве##
	
	// js
	var arr = [10, 9, 2, 1, 21, 8];
	Math.max.apply(Math, arr);


##Преобразование в массив##
	
	var arrOfLinks;
	var links;

	links = document.links;
	arrOfLinks = Array.prototype.slice.call(links);
	console.log(links, );


##объект arguments##
Массивоподобный объект с аргументами, переданными в функцию


##arguments – массивоподобный##
Не имеет методов массива, но имеет свойство length
	
	function sum () {
		console.log(arguments);			// [10, 20, 30, 40, 50]
		console.log(arguments.slice);	// undefined
	}
	sum(10, 20, 30, 40, 50);


##Массивоподобные объекты
array, jQuery(), document.links


##Превращение в массив##
	
	function sum () {
		var args;
		args = [].slice.call(arguments);
		console.log(args, args.slice);
		args = Array.prototype.slice.call(arguments);
		console.info(args, args.slice);
	}
	sum(10, 20, 30, 40, 50);



##Применение функций##

* Инкапсуляция
* Декомпозиция
* Наследование



##Декомпозиция##
Разбиение задачи на подзадачи, смысловые куски



##Инкапсуляция##
Ограничение доступа к данным


##Модуль##
	
	(function () {
		'use strict';

		// your code
	}());


##Модуль##
	
	var counter = (function () {
		'use strict';

		var counter = 0;

		return {
			inc : function () {counter += 1;},
			dec : function () {counter -= 1;},
			get : function () {return counter}
		};
	}());



##Наследование##
Code reuse. Функции участвуют в в создании цепочек прототипов + являются методами объекта.
