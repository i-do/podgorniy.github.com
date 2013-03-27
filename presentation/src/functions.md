#Функции#



##Функция##
Исполняемый объект


##Исполняемый##
Выполняет некоторые действия (с или без побочных эффектов) и вычисляется в значение


##Объект##
Имеет свойства и методы объекта (+ методы и свойства, характерные для функций), присваивается и сравнивается по ссылке



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
<del>способ и время создания переменных и присвоение в них ссылки на функцию</del>  
function declaration доступна до своего фактического объявления в коде


##function declaration##

	main(); // "Lala" – ok
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


##Как себя поведет подобный код##
	
	main(); // alert 1 or 2?
	if (true) {
	    function main () {alert(1);}
	} else {
	    function main () {alert(2);}
	}
	main(); // alert 1 or 2?



##Возвращаемое значение##
Во что вычислится вызов функции


##Возвращаемое значение##
	
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
* в момент вызова инициализируются переменные с именами аргументов
* переменные создаются даже, если аргументы не были переданы в функцию


##Объявление функции с аргументами##
	
	function main (items, callback) {
		// useful stuff
	}


##Аргументы функции##
* каждая функция может принимать любое количество аргументов
* стандартных механизмов для создания значения по умолчанию нет


##Вызов функции с аргументами##
	
	// js
	main(test);
	
	main({
		test: true
	});

	main(function () {
		return true
	});

	main(test, "10", foo);


##Вызов функции с аргументами##
	
	function getData (dataType, onlyFresh) {
		if (onlyFresh || !isInCache(dataType)) {
			return requestData(dataType);
		} else {
			return getFromCache(dataType);
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



##Разберемся с терминологией##
Контекст вызова (this)
Контекст выполнения (области видимости)



##Область видимости##
Любая функция создает область видимости

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


##Переменные и область видимости##
Функции доступны переменные области видимости, в которой она объявлена.

	var a = 10;

	function main () {
		console.log(a);
	}

	main();


##Переменные и область видимости##
Переменные, объявленные в функции, недоступны за ее пределами

	function main () {
		var a = 10;
	}
	a; // ReferenceError


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



##this##
Оператор, возвращающий ссылку на контекст  
<small>(обычно объект, в котором содежится вызываемый метод, или конструируемый объект)</small>  
Не связан с областью видимости, местом хранения функции, способом ее объявления итд.


##Для чего нужен this##
организация наследования


##this##

	var obj = {
		test: function () {
			console.log(this);
		}
	};
	obj.test();


##this##
Что вернет this, определяется способом вызова функции

	var obj = {};
	obj.test = function () {
		console.log(this);
	}
	obj.test();


##this##
Оператор ()  
<small>this вернет window или undefined</small>


##Для чего нужны call и apply?##
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
Явное указание что вернет this

	var obj = {};
	function test () {
		console.log(this);
	}
	test.call(obj);


##Повседневные хитрости##
* Максимальное значение в массиве
* Преобразование в массив


##Максимальное значение в массиве##
	
	// js
	var arr = [10, 9, 2, 1, 21, 8];
	Math.max.apply(Math, arr);


##объект arguments##
Массивоподобный объект с аргументами, переданными в функцию


##arguments – массивоподобный##
	
	function sum () {
		console.log(arguments);			// [10, 20, 30, 40, 50]
		console.log(arguments.slice);	// undefined
	}
	sum(10, 20, 30, 40, 50);


##Превращение в массив##
	
	function sum () {
		var args;
		args = [].slice.call(arguments);
		console.log(args, args.slice);
		args = Array.prototype.slice.call(arguments);
		console.info(args, args.slice);
	}
	sum(10, 20, 30, 40, 50);



##Применение##

* Декомпозиция
* Инкапсуляция
* Наследования



##Декомпозиция##
Разбиение задачи на подзадачи



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