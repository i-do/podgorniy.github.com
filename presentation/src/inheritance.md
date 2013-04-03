#Наследование#



##new##
Создание объектов из функций-конструкторов <small>(любая функция может быть конструктором)</small>


##Стандартные конструкторы##

* Object
* Array
* Function
* RegExp
* Date


##Явное использование конструкторов##

* Date
* RegExp (генерация regexp из строки на лету)
* Function (создание функции из строки, хак областей видимости)


##Неявное использование конструкторов##
При работе с литералами



##Поиск свойств в объекте##
Откуда берутся стандартные методы


##Поиск свойства в объекте##
Возвращается первое найденное свойство из цепочки прототипов

* проверка наличия свойства непосредственно в объекте
* проверка наличия свойтва в цепочке прототипов


##\_\_proto\_\_##

* Механизм наследования
* Ссылка на объект или на null


##Стандартные \_\_proto\_\_##
	
	// js
	var arr = [];
	console.dir(arr.__proto__);
	console.dir(arr.__proto__.__proto__);
	console.dir(arr.__proto__.__proto__.__proto__);


##this в методах из цепи прототипов##
this ссылается на объект, из которого вызывали метод



##Образование цепочки прототипов##


##Установка \_\_proto\_\_##

1. В момент создания объекта
2. Ссылается на \[Constructor\].prototype


##prototype##
Свойство любой функции, хранит ссылку на объект


##prototype##
	
	// js
	var arr = [];
	console.log(arr.__proto__ === Array.prototype);
	var obj = {};
	console.log(obj.__proto__ === Object.prototype);


##prototype##

	function F() {}
	var f = new F();
	f.__proto__ === F.prototype;


##Выводы##

* при добавлении свойств в \[Constructor\].protototype, они появятся у всех экземпляров класса (все зависимости от времени их создания)


##Выводы##
	
	// js
	var a = {};
	Object.prototype.test = true;
	console.log(a.test, ({}).test); // true, true


##Выводы##

* При присвоении нового объекта \[Constructor\].prototype, это повлияет только на вновь создаваемые объекты


##Выводы##

	function F() {}
	F.prototype.test = true;
	var f1 = new F();
	F.prototype = {
		foo : true
	};
	var f2 = new F();
	console.log(f1.test, f1.foo); // true, undefined
	console.log(f2.test, f2.foo); // undefined, true



##Стандартные методы работы с прототипами##

* instanceof
* constructor
* hasOwnProperty


##instanceof##
Проверяет наличие prototype конструктора в цепи прототипов


##instanceof##

	// js
	console.log([] instanceof Array); // true
	console.log([] instanceof Object); // true


##instanceof##
Не работает с объектами из iframe


##Лучше instanceof##
	
	function getType(obj) {
		return Object.prototype.toString.call(obj);
	}
	console.log(getType({}));
	console.log(getType([]));
	console.log(getType(1));
	console.log(getType(undefined));
	console.log(getType(null));


##hasOwnProperty##
Метод, который проверяет, содержится ли свойство или метод непосредственно в экземпляре класса


##hasOwnProperty##
	
	// js
	var a = {};
	a.hasOwnProperty('toString'); // false
	a.toString = function () {return 'fffoooo'};
	a.hasOwnProperty('toString'); // true


##constructor##
Свойство объекта, ссылающееся на функцию, сконструировавшую этот объект
	
	// js
	console.log(({}).constructor === Object); // true
	console.log(([]).constructor === Array); // true



##in и for in##
Оба метода работают со свойствами как в объекте, так и со свойствами в цепочке прототипов


##in##
	
	// js
	var a = {
		test : true
	};
	Object.prototype.foo = true;

	console.log('test' in a); // true
	console.log('foo' in a); // true


##for ... in##
Перебор всех перечисляемых* свойств из цепи прототипов


##Расширение прототипов##

* Пользовательские конструкторы
* Совместимость с новыми стандартами


##Когда расширение прототипа вредно##
	
	Object.prototype.maxId = 999;
	var girlsRate = {
		'masha' : 5,
		'olya' : 4,
		'anya' : 6,
		'valya' : 4
	};
	var maxRate = 0,
		maxRatedGirl;
	for (var name in girlsRate) {
		if (girlsRate[name] > maxRate) {
			maxRate = girlsRate[name];
			maxRatedGirl = name;
	    }
	};
	maxRatedGirl; // 'maxId'


##hasOwnProperty##
решит проблему



##Пользовательские конструкторы##


##Именование конструкторов##
С большой буквы
	
	// js
	function Person () {}
	console.log (new Person());


##Подсветка конструкторов в firebug##
	
	// js
	function F () {}
	F.prototype.foo = function () {};
	console.log(F)


##this##
При вызове функции как конструктора this вернет ссылку на создаваемый объект


##this##
	
	var f;
	var fCopy;
	function F () {
		fCopy = this;
	}
	f = new F();
	console.log(f === fCopy);	// this


##this##
	
	function F () {
		console.log(this.constructor === F); // true
	}
	new F();


##Возвращаемое значение##

* без return конструктор вернет создаваемый объект
* иначе вернется объект, возвращаемый в return


##Возвращаемое значение##
	
	function F() {
		this.test = true;
		return {
			foo : true
		};
	}
	var f = new F();
	console.log(f.test); // undefined
	console.log(f.foo); // true
	console.log(f.constructor); // Object


##Возвращаемое значение##
Конструктор возвращаемого объекта не подменяется на конструктор, который вернул объект
	
	function F () {
		return {}
	}
	var f = new F();
	console.log(f instanceof F); // false



##Наконец пример##


##Counter##

	function Counter(startCount) {
	    this.count = startCount || 0;
	}

	Counter.prototype.inc = function () {
	    this.count += 1;
	    return this;
	};

	Counter.prototype.dec = function () {
	    this.count -= 1;
	    return this;
	};

	Counter.prototype.get = function () {
	    return this.count;
	};

	var counter = new Counter(10);
	counter.inc().inc().get(); // 12



##Задачи##
* Абстрагирование
* Повторное использование кода


##Абстрагирование##
Высокоуровневые абстракции


##Пример абстрагирования##

	var orderTitles;
	orderTitles = ['First', 'Second', 'Third'];
	orderTitles.forEach(function (item, index) {
		console.log(item, index);
	});


##Пример отсутствия абстрагирования##

	var orderTitles;
	var i;

	orderTitles = ['First', 'Second', 'Third'];
	for (i = 0; i < orderTitles.length; i += 1) {
		console.log(orderTitles[i], i);
	}


##Абстрагирование — это хорошо, но ##
без фанатизма