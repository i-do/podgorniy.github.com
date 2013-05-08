#События#



##Событие##
Изменение состояния, действие.


##Обработчики событий##
Реакция на событие


##Идея событий##
1. Произошло событие
2. Последовала реакция (или нет)



##События браузера##
**Пользовательские (UI)**  
**Внутренние**


##NB##
Событие происходит, и при отсутствующих обработчиках <small>и зачем мне это знать, если это внешне никак не проявляется?</small>



##События браузера##
* Интерфейс для добавления обработчиков
* Объект события
* Поведение событий


##События, не имеющие интерфейсов##
Не все события имеют интерфейсы для того, чтобы добавить обработчики <small>с точки зрения разработчика</small>


##Какие события не имеют интерфейсов для обработки?##
* прокрутка страницы до самого низа
* нахождение на сайте более минуты



##Обработчики событий##
функции



##Компоненты и понятие связанности##



##Событийные паттерны##
* mediator
* observer



##mediator##
Объект, имеющий интерфейс для инициализации событий и добавления к ним обработчиков


##mediator##
<img src="http://codelab.ru/data/tasks/216/Image/objectStructure.gif" alt="">


##Пример использования медиатора##
	
	// subscription
	mediator.subscribe('gallery:left', function () {
		console.log('Left sliding');
	});

	mediator.subscribe('gallery:left',
						updateProgressBar);


##Пример использования медиатора##
	
	// trigger
	Gallery.prototype.left = function () {
		// implementation ...
		mediator.trigger('gallery:left');
	};


##Реализация медиатора##
В [toolbox](https://github.com/podgorniy/javascript-toolbox/blob/master/mediator.js)



##observer##
Интерфейс для добавления обработчиков своих событий


##observer##
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/Observer.svg/500px-Observer.svg.png" alt="">


##пример observer##
	
	// subscription
	gallery.onSlide.add(function (sliderIndex) {
		console.log('Sliding to slide with index', sliderIndex);
	});

	gallery.onSlide.add(updateProgressBar);


##пример observer##

	// trigger
	Gallery.prototype.slideTo = function (sliderIndex) {
		// implementation ...

		this.onSlide.trigger(sliderIndex);
	};