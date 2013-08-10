##Заготовка для файла домашнего задания
Пара функций, которая может пригодиться.

	'use strict';

	function isArray (obj) {
		return Object.prototype.toString.call(obj) === '[object Array]';
	}
	
	function isObject (obj) {
		return Object.prototype.toString.call(obj) === '[object Object]';
	}

#Задачи

###Преобразовать объект в query-string
На входе - одноуровневый объект, значения свойств объекта - строки или числа.

	toSearchString({}); // ''
	toSearchString({test: true}); // 'test=true'
	toSearchString({num: 10, test: true}); // 'num=10&test=true'
	toSearchString({num: 10, test: true, user: 'admin'}); // 'num=10&test=true&user=admin'

###Из двумерного массива сделать одномерный
На первом уровне может быть как массив, так и не массив.
	
	flatten([[1], 1, 1]); // [1, 1, 1]
	flatten([[[1]], 1]); // [[1], 1]
	flatten([[[1]], 1]); // [[1], 1]
	flatten([]); // []
	flatten([{}]); // [{}]
	flatten([[{}], []]); // [{}, []]


###Из одномерного массива, сделать двумерный
Функция принимает 2 аргумента: массив и число. Число показывает количество элементов в подмассивах

	toMatrix([1,2,3,4,5,6,7,8,9], 3); // [[1,2,3], [4,5,6], [7,8,9]]
	toMatrix([1,2,3,4,5,6,7], 3); // [[1,2,3], [4,5,6], [7]]
	toMatrix([1,2,3], 5); // [[1,2,3]]
	toMatrix([], 3); // []

###Создать объект из массивов ключей и значений
Функция принимает аргументами 2 массива: первый - массив ключей, второй - значений. Если ключей меньше, чем значений, игнорировать не вмещающиеся значения. Если ключей больше, чем значений, установить значения в undefined

	createObject(['name', 'age'], ['Vasiliy', 45]); // {name: 'Vasiliy', age: '45'}
	createObject(['name', 'age'], ['Vasiliy']); // {name: 'Vasiliy', age: undefined}
	createObject(['name'], ['Vasiliy', 45]); // {name: 'Vasiliy'}
	createObject([], []); // {}

###Проверить является ли массив подмножеством другого массива
Функция принимает аргументами 2 массива. Возвращает true, если все элементы второго массива являются элементами первого. Массивы могут содержать любые значения

	contains([1,2,3,4,5,6,7,8,9], [1,2]); // true
	contains([1,2,3,4,5,6,7,8,9], [1,2]); // true
	contains([1,2,3,4,5,6,7,8,9], []); // true
	contains([1,2,3,4,5,6,7,8,9], [0]); // false
	contains([], [0]); // false
	contains([], []); // true
	contains([1], [1]); // true
