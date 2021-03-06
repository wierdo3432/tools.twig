## Тонкости битрикса

### twig для шаблона сайта

К сожалению, ядро устроено таким образом, что невозможно использовать twig при том подходе к разработке, который исповедует битрикс. Но если вдруг появится желание - это можно сделать, если оформить шаблон сайта в виде компонента. Правда в этом случае появятся недостатки, которые не позволят использовать стандартные возможности битрикс по работе с файлами.

### Языковые переменные

Языкозависимые переменные в шаблонах битрикса хранятся в директории /lang/<ID языка>/<имя файла шаблона>
Что очень странно, так это то, что расширение файла с языковыми константами должно совпадать с расширением файла шаблона. Т.е. если вы используете расширение twig для файла шаблона template.twig, то придется создать языковой файл /lang/ru/template.twig, в котором нужно будет держать php код, описывающий массив с языковыми параметрами ...
Для своих компонентов это ограничение можно обойти, если языкозависимые переменные шаблона хранить в языковом файле самого компонента, а не шаблона. 

### component_epilog.php

При использовании стороннего шаблонизатора битрикс не подключает данный файл. Внутри данной библиотеки данный файл подключается насильно. Однако никто не гарантирует, что битрикс со дня на день изменят обработку этого поведения в ядре, что может привести к двойному подключению файла component_epilog.php в шаблоне компонента.

### .php vs .twig

К сожалению, ядро битрикса так устроено, что при наличии двух файлов .php и .twig, будет использовать только .php, даже несмотря на то, что был определен сторонний шаблонизатор, поэтому для использования twig шаблона нужно позаботиться о том, чтобы php шаблон отсутствовал.