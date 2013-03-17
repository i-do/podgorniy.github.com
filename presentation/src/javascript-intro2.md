#Javascript-intro#
part 2



##Освежим память##
* Примитивы
* Литералы
* Операторы
* Выражения



##Объекты##
Хеш, асоциативный массив, структура типа ключ-значение


##Объектный литерал##
	
	// js
	// пустой объект
	var obj = {}; 

	// объект с 2 свойствами
	var group = {
		type : "programming",
		attendeesNum : 90
	};


##Свойство объекта##
Ключ — это строка  
Доступ к значению  
Брать в скобки не обязательно <small>если нет пробелов</small>


##Объектный литерал##

	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 90
	};


##Значение — любой тип##
И объект в том числе
	
	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 90,
		"tutor" : {
			"name" : "Dmitry"
		}
	};


##Доступ к свойству объекта##
* Оператор "точка"
* Оператор "квадратные скобки"


##Доступ через точку##
	
	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 90,
		"tutor" : {
			"name" : "Dmitry"
		}
	};
	group.type;         // "programming"
	group.attendeesNum; // 90
	group.tutor.name;   // "Dmitry"


##Доступ через точку##
	
	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 90,
		"tutor" : {
			"name" : "Dmitry"
		}
	};
	var tutor;

	tutor = group.tutor;
	tutor.name; // "Dmitry"


##Доступ через квадратные скобки##
	
	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 90
	};
	group["type"];         // "programming"
	group["attendeesNum"]; // 90


##Доступ через квадратные скобки##
Обращение к свойству по динамически сгенерированному ключу


##Запись свойства в объект##
В левой части обращение к свойству, в правой — выражение

* через точку 
* через квадратные скобки


##Запись свойств##
	
	// js
	var group = {};
	group.type = "programming";
	group.attendeesNum = 90;
	group


##Циклические ссылки##
В свойстве объекта может содержаться ссылка на этот самый объект  
<small>в консоли выглядит забавно</small>
	
	// js
	var obj = {};
	obj.self = obj;


##Обращение к несуществующему свойству##

	var obj = {};
	obj.someProp; // undefined


##Обращение к свойству у undefined##

	var obj = {};
	obj.someProp;             // undefined
	obj.someProp.anotherProp; // TypeError


##Обращение к свойству у undefined##
	
	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 90,
		"tutor" : {
			"name" : "Dmitry"
		}
	};
	group.type;         // "programming"
	group.attendeesNum; // 90
	group.titor.name;   // TypeError



##Массивы##
Специальные объекты с доступом к свойствам по индексу (начиная с нулевого).

	// js
	var girls = ["Ann", "Jane", "Karolina"];
	girls[0] === 'Ann'; // true
	girls[2];           // "Karolina"


##Типизация##
Нетипизированы <small>(типизированные существуют)</small>.
	
	// js
	var stuff = [{}, 10, false, {prop: "value"}];
	stuff; // [[Object, 10, false, Object]]


##length##
Количество элементов в массиве.


##Добавление элемента в конец массива##
<small>Один из способов и далеко не оптимальный</small>

	var persons = ["Oleg", "Petr"];

	persons[persons.length] = "Evgen";
	persons; // ["Oleg", "Petr", "Evgen"]


##Обращение к несуществующему элементу массива##

	var persons = ["Oleg", "Petr"];
	persons[99]; // undefined




##По ссылке и по значению##
* сравнение и присвоение
* объекты — по ссылке
* примитивы — по значнию


##Присвоение по значнию##
	
	var num = 10;
	var numCopy;

	numCopy = num;
	num += 1;

	num;     // 11
	numCopy; // 10


##Присвоение по ссылке##
	
	// js
	var group = {};
	var groupLink;

	groupLink = group;
	group.visits = 3;

	group.visits;     // 3
	groupLink.visits; // 3


##Сравнение по ссылке##
	
	// js
	var obj1 = {};
	var obj2 = {};

	obj1 === obj2;    // false
	obj2 = obj1;

	obj1 === obj2;    // true
	obj2.test = true;
	obj1 === obj2;    // true



##Циклы##
* for
* for ... in

* while
* do ... while


##for##
	
	var arr = ['One', 'Two', 'Three'];
	var i;

	for (i = 0; i < arr.length; i += 1) {
		arr[i] += '-times'; 
	}
	arr; // ["One-times", "Two-times", "Three-times"]


##for##
	
	var arr = ['One', 'Two', 'Three'];
	var i = 0;

	for (; i < arr.length; i += 1) {
		arr[i] += '-times'; 
	}
	arr; // ["One-times", "Two-times", "Three-times"]


##for..in##
Обход свойств объектов


##for..in##
	
	// js
	var propertiesSet;
	var propertyName;
	var propsStr;

	propertiesSet = {
		width : 400,
		height : 300,
		position : 'absolute'
	};
	propsStr = '';

	for (propertyName in propertiesSet) {
		if (propsStr) {
			propsStr += '\n';
		}
		propsStr += (propertyName + ": " + 
			propertiesSet[propertyName]);
	}
	propsStr


##Break##
Прерывание цикла

	var girls = ['Oksana', 'Dasha', 'Masha',
		'Sasha', 'Valya'];
	var i;

	for (i = 0; i < girls.length; i += 1) {
		if (girls[i] === 'Masha') {
			break;
		}
	}
	i; // 2


##Continue##
Пропуск итерации

	var girls = ['Oksana', 'Dasha', 'Masha',
		'Sasha', 'Valya'];
	var i;

	for (i = 0; i < girls.length; i += 1) {
		if (girls[i] === 'Masha') {
			continue;
		}
		girls[i] += ' with flowers';
	}
	girls; // ["Oksana with flowers", 
		   //  "Dasha with flowers",
		   //  "Masha",
		   //  "Sasha with flowers",
		   //  "Valya with flowers"]