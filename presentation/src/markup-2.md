#Верстка#



##CSS каскад##
[педеефка](https://www.dropbox.com/s/wyfeqyn7spay0l2/CSS-cascade.pdf)



##Типы элементов##
* блочные
* инлайновые
* инлайн-блоки
* табличные


##Как определяется тип элемента##
Примененным свойством
	
	display: /* тип элемента */;



##Поток##
Порядок в котором выстраивается последовательность блоков


##Блочные элементы##
* занимают всю доступную ширину родителя
* выстраиваются в потоке один за другим
* границы следующего элемента потока начинаются там, где кончается граница предыдущего
* на размеры блока можно повлиять padding-ами, margin-ами


##Инлайновые элементы##
* ведут себя как текст, заполняющий блок
* выравниваются по базовой линии шрифта ([baseline](http://en.wikipedia.org/wiki/Baseline_%28typography%29))
* стремно видут себя с вертикальными margin и padding


##Инлайн-блоки##
* В потоке выстраиваются как инлайновые
* margin и padding ожидаемо влияет на размер блока
* пробелы между инлайн-блоками считаются