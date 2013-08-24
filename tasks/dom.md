#Задачи


## Сгенерировать список
Сгенерировать список из массива данных. [Пример данных](https://gist.github.com/podgorniy/3eba738b183538bdd3bd). Ссылки, среди тегов которых есть object, сделать на голубом фоне. При клике на списке - отсортировать (сортировать описания) по алфавиту (А-Я). Если список уже отсортирован по алфавиту - отсортировать в обратном порядке (Я-А). JSON нужно мочь менять без труда. [Как список может выглядеть](http://grab.by/pEyg).

## Написать функции для работы с классами
###addClass(node, className)
Не должна добавлять класс, если этот класс уже есть у функции.

	/**
	 * Adds classes to node element. Does not add class, if it's already presents.
	 * @param {DOMNode} node     
	 * @param {String} className 
	 */
	function addClass(node, className) {
		
	}

###hasClass(node, className)
className может быть как строкой так и массивом строк

	/**
	 * returns true, in case node has all classes from className
	 * @param  {DOMNode}  node
	 * @param  {String|Array} className
	 * @return {Boolean}
	 */
	function hasClass(node, className) {
	
	}

###removeClass(node, className)
Удаляет классы у узла. Если название класса повторяется, удаляются все вхождения повторяющихся классов.

	/**
	 * Removes all classes, that match className (which can be either string or array)
	 * @param  {DOMNode} node      
	 * @param  {String|Array} className
	 */
	function removeClass(node, className) {
	
	}

##Пройти по DOM дереву вверх
Вызывает callback с каждым родителем node, возвращает тот узел, для которого callback вернет не falsy значение.

	/**
	 * Returns first element, of node parents, that matches callback returned true for.
	 * @param  {DOMNode}   node
	 * @param  {Function} callback
	 * @return {DOMNode}
	 */
	function closest(node, callback) {
	
	}

##Получить массив элементов уникальных типов

##Проверить корректность работы предыдущей функции

##Починить функцию next
[Все попытки](https://gist.github.com/podgorniy/2b8aa64b8dc3448c1f29)