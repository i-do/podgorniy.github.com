##DOM##


##Темы##
* выборка
* модификация



##Выборка##


##document.getElementsByTagName##
* возвращает массивоподобный объект
* живая коллекция


##Приемы работы##

	var divs;
	var i;

	divs = document.getElementsByTagName('div');
	for (i = 0; i < divs.length; i += 1) {
		divs[i].className += (' item-' + i);
	}


##Когда надо пробегаться по всем узлам##
* найти узел, до которого не добраться иным способом (пример)
* добавить классов для дальнейшей стилизации



##getElementById##
* самый быстрый селектор
* подразумевает наличие элемента на странице в единственном экземпляре
* бажный ие


##Сюрприз от ие##
Аттрибут name тоже [считается](http://dl.dropboxusercontent.com/u/951144/js-course/examples/ie-getElementById-bug.html)


##Потенциальные проблемы##
	
	var main;
	main = document.getElementById('main');
	modifyNode(main);


##Пожелезнее##
<small>но не пуленепробиваемый</small>
	
	var mains;
	mains = document.querySelectorAll('#main');
	Array.prototype.forEach.call(mains, modifyNode);


##querySelector(All)##
* мертвая коллекция
* css селекторы как аргументы
* querySelector возвращает ссылку на первый соответствующий элемент
* querySelectorAll возвращает коллекцию соответствующих элементов



##Хождение по DOM##


##parentNode##
ссылка на родителя


##Для чего##
* проверка, находится ли элемент в DOM
* поиск ближайщего родителя по условию [closest](https://github.com/podgorniy/javascript-toolbox/blob/master/top_walker.js)
* удаление элемента



##Удаление##
	
	// js
	var table;
	table = document.querySelector('table');
	table.parentNode.removeChild(table);


##Удаление поуниверсальнее##

	function remove (domNode) {
		var parent;
		if (domNode && (parent = domNode.parentNode)) {
			parent.removeChild(domNode);
		}
	}



##Удаление еще поуниверсальнее##

	function isNode (obj) {
		return 'nodeType' in obj;
	}

	function isIterable (obj) {
		return typeof obj !== 'function' && 'length' in obj;
	}

	function remove () {
		Array.prototype.forEach.call(arguments, function (nodeOrCollection) {
			var papa;
			if (isIterable(nodeOrCollection)) {
				remove.apply(this, nodeOrCollection);
			} else if (isNode(nodeOrCollection) && (papa = nodeOrCollection.parentNode)) {
				papa.removeChild(nodeOrCollection);
			}
		});
	}


##nextSibling##
Разное поведение в ие и не в ие


##next##
	
	function next (node) {
		while (node && (node = node.nextSibling)) {
			if (node.nodeType !== 8 && node.nodeType !== 3){
				return node;
			}
		}
	}



##Изменение DOM##
* document.write
* appendChild, insertBefore
* innerHTML
* setAttribute


##document.write##
Дописывание html налету  
Например для синхронной доставки другого скрипта


##document.write##
* нельзя выполнять после DOM ready
* нельзя выполнять в асинхронных скриптах
* если добавляемый скрипт не доступен, страница долго висит



##appendChild, insertBefore##
Вставка узла (узел надо создать, или получить ссылку на уже существующий)  
для insertBefore надо иметь ссылку на узел, перед которым вставлять


##appendChild, insertBefore##
* appendChild – вставка в хвост всех children (http://jsfiddle.net/podgorniy/nKDpt/)
* insertBefore - вставка в любое место среди детей (но не в хвост)


##Динамическая вставка скриптов##
с помощью appendChild можно добавлять скрипты (асинхронно)


##Генерирование html##
appendChild, insertBefore + createElement


##removeChild##
ссылки на узел сохраняются, и с ним можно продолжать работать  
обработчики сохраняются



##innerHTML##
* создание и удаление элементов
* из строки в DOM
* проблемы с таблицами в ие


##innerHTML##
	
	// js
	document.body.innerHTML = '<h1>That\'s all</h1>';
	console.log(document.body.innerHTML);


##innerHTML и обработчики##
Убивает обработчики  
ссылки на узлы остаются<sup>*</sup>




##Модификации и live collection##
* [перемещение](http://dl.dropboxusercontent.com/u/951144/js-course/examples/liveCollectionsFuckup.html)
* [удаление](http://dl.dropboxusercontent.com/u/951144/js-course/examples/liveCollectionsFuckup2.html)