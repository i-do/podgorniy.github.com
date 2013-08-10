#Javascript-intro (part 2)#



##Объекты##
<small>Широкий и узкий смысл слова</small>


##Объекты##

* хеш-таблицы (hashmap, ключ-значение)
* множество, объединяющее некоторые типы данных ([не примитивы](?presentation=javascript-intro-1/#/4/1))


##Роль объектов (которые хеш таблицы)##

* Структуры данных
* Иерархия данных
* Наследование
* Абстрагирование


##Объектный литерал##
	
	// js
	// пустой объект
	var obj = {}; 

	// объект с 2 свойствами
	var group = {
		type : "programming",
		attendeesNum : 100500
	};


##Свойство объекта (ключ)##
Ключ, строка - название свойства объекта


##Значение — любой тип##
И объект в том числе
	
	// js
	var group = {
		type : programming,
		attendeesNum : 100500,
		tutor : {
			name : "Dmitry"
		}
	};


##Доступ к свойству объекта##
* Оператор "точка"
* Оператор "квадратные скобки"


##Доступ через точку##
	
	// js
	var group = {
		type : "programming",
		attendeesNum : 100500,
		tutor : {
			name : "Dmitry"
		}
	};
	group.type;         // "programming"
	group.attendeesNum; // 100500
	group.tutor.name;   // "Dmitry"


##Доступ через точку##
	
	// js
	var group = {
		type : "programming",
		attendeesNum : 100500,
		tutor : {
			name : "Dmitry"
		}
	};
	var tutor;

	tutor = group.tutor;
	tutor.name; // "Dmitry"


##Доступ через квадратные скобки##
	
	// js
	var group = {
		"type" : "programming",
		"attendeesNum" : 100500
	};
	group["type"];         // "programming"
	group["attendeesNum"]; // 100500


##Доступ через квадратные скобки##

* Обращение к свойству по динамически сгенерированному ключу  
* Доступ по ключу, находящимся в переменной


##Запись свойства в объект##
В левой части обращение к свойству, в правой — выражение

* через точку 
* через квадратные скобки


##Запись свойств##
	
	// js
	var group = {};
	group.type = "programming";
	group.attendeesNum = 100500;
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
		"attendeesNum" : 100500,
		"tutor" : {
			"name" : "Dmitry"
		}
	};
	group.type;         // "programming"
	group.attendeesNum; // 100500
	group.titor.name;   // TypeError



##Массивы##
Специальные объекты с доступом к свойствам по индексу (начиная с нулевого).

	// js
	var girls = ["Ann", "Jane", "Karolina"];
	girls[0] === 'Ann'; // true
	girls[2];           // "Karolina"


##Отсутствие типизации##
	
	// js
	var stuff = [{}, 10, false, {prop: "value"}];
	stuff; // [[Object, 10, false, Object]]


##length##
Количество элементов в массиве.


##Добавление элемента в конец массива##

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


##Присваивание по значению##
	
	var num = 10;
	var numCopy;

	numCopy = num;
	num += 1;

	num;     // 11
	numCopy; // 10


##Присваивание по ссылке##
	
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

	console.log(obj1 === obj2);    // false
	obj2 = obj1;

	console.log(obj1 === obj2);    // true
	obj2.test = true;
	console.log(obj1 === obj2);    // true


##Присваивание по ссылке##
Объекты передаются в функции по ссылке

	// js
	var person = {
		name: 'Vasya'
	};

	console.log(person.name, person.prop);

	function addProp (obj) {
		obj.prop = true;
	}

	addProp(person);
	console.log(person.name, person.prop);



##Ветвление##
* if-else
* тернарный оператор
* switch


##if-else##
Вычисляет выражение в условии и приводит к булевому.

	if (conditionStatement) {	
		// some code
	}	

	if (conditionStatement) {
		// !!conditionStatement === true
	} else {
		// !!conditionStatement === false
	}


##Всегда используйте скобки##
Несмотря на то, что в некоторых случаях можно опускать фигурные скобки
	
	// js
	if (condition)
		action();


##Всегда используйте скобки##
Слишком просто ошибиться

	// js
	if (condition);
		action(); // срабатывает всегда


##Вложенные условия##
	
	if (a) {
		z = 10;
	} else {
		if (b) {
			z = 20;
		} else {
			if (c) {
				z = 40;
			}
		}
	}


##Вложенные условия##
	
	if (a) {
		z = 10;
	} else if (b) {
		z = 20;
	} else if (c) {
		z = 30;
	}



##Тернарный оператор##
Вычисляется в один из операндов
	
	// js
	condition ? doIfTrue : doIfFalse;
	true ? "Правда" : "Ложь";   // "Правда"


##Эквивалент##
	
	// js
	condition ? a = 10 : b = 20;
	if (condition) {
	    a = 10;
	} else {
	    b = 20;
	}


##Помните про порядок##
	
	var isMale = false;
	var userName = "Linda";

	"Hello, " + isMale ? 
		"mr " :
		"miss " + userName; // "mr"


##Помните про порядок##
	
	var isMale = false;
	var userName = "Linda";

	"Hello, " + (isMale ? 
		"mr " : 
		"miss ") + userName; // "Hello, miss Linda"



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


##for..in##
Обход свойств объектов  
Все равно сколько свойств в объекте  
Нет необходимости знать имена свойств объекта, чтобы к ним доступиться


##for..in##
	
	// js
	var propertiesSet;
	var propertyName;

	propertiesSet = {
		width : 400,
		height : 300,
		position : 'absolute'
	};

	for (propertyName in propertiesSet) {
		console.log(propertyName, propertiesSet);
	}
