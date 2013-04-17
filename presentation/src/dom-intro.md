#DOM#
<small>и BOM</small>



##DOM##
Document object model


##DOM##
* API для доступа и изменения элементов страницы
* Представление документа в виде js объектов



##Создание DOM##
Из текста - в объекты  
<small>парсинг html страницы</small>


##Структура html##
1. doctype
2. head
3. body


##doctype##
Объявление типа документа.
<small>ие ой как не любит комментарии перед DD</small>


##head##
Обычно содержит вспомогательную информацию о странице
Кодировка, заголовок, meta-информация, стили, скрипты...


##body##
Элементы для отображения на странице.



##Структура DOM##
дерево с корнем в &lt;html&gt;


##DOM Объекты##
* document
* htmlElement


##Свойства и методы DOM элементов##
* характерные для группы элементов (nodes)
* характерные для некоторых DOM элементов (table nodes)


##Свойства и методы document##
* links, styleSheets, scripts ...
* cookie
* querySelector, getElementsByTagName ...


##Нестандартные свойства и методы##
А также обратная совместимость - боль веб разработки



##Работа с DOM через консоль##
* исследование
* правка


##Работа с DOM через консоль##
* $
* console.dir(...)



##HTML → DOM##


##1 ли в 1?##
* doctype xhtml, html
* отсутствие закрывающих тегов
* no doctype


##Attr vs prop##
* аттрибуты !== свойства


##Загрузка документа##
* по порядку сверху, вниз
* асинхронные документы
* DOMReady
* window.onload


##Загрузка документа и динамическая вставка элементов##
document.write



##Стили##
* инлайновые
* внешние



##BOM##
* window
* location
* navigator
* name


##еще BOM##
* indexedDB, localStorage
* history
* requestAnimationFrame