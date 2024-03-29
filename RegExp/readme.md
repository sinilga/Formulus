## RegExp
Набор функций для работы с регулярными выражениями

### [rexFindAll](rexFindAll.crf)
Поиск в строке с использованием регулярных выражений.
В отличие от стандартной функции REGEXPFIND эта функция возвращает все вхождения.
```
$rexFindAll(@str,@templ,@case)
```
**Параметры**  
`@str` - строка, в которой осуществляется поиск;  
`@rex` - шаблон поиска, обычная строка или регулярное выражедение;  
`@case` - флаг учета регистра при поиске: `1` - учитывать регистр, `0` - не учитывать. По умолчанию - 0.

**Возвращаемое значение**
- если подстроки, соответствующие шаблону найдены, функция возвращает массив:  
			[1] - число найденных подстрок;  
			[2] - номер символа, с которого начинается вхождение первой подстроки;  
			[3] - длина первой подстроки;  
			[4] - номер символа, с которого начинается вхождение 2-й подстроки;  
			[5] - длина 2-й подстроки;  
      и т. д.  
- если совпадений не найдено, функция возвращает `0`;  
- в случае ошибки (некорректный шаблон поиска), функция возвращает `-1` и описание ошибки.

**Пример использования**
```
@str:="When the going gets tough, the tough get going"
@t:="\bg\w+"	// слова, начинающиеся на `g`
@res:=$rexFindAll(@str, @t)
if @res > 0 then [
  @i:=2
  @text:=""
  while @i < valcount(@res) do [
    @text(-1):=substr(@str,@res[@i],@res[@i+1])
    @i:=@i+2
  ]
  Message(@res[1] << " matches: " << catval(@text,", "),@okcancel)
]
else if @res = 0 then [
  Message("No matches",@okcancel)
]	
else [
  Message("Error: " << @res[2])
]
```
В результате будет выведено сообщение: "4 matches: going, gets, get, going"

### [rexMatch](rexMatch.crf)
Функция выполняет поиск в строке первого вхождения, соответствующего регулярному выражению, и возвращает захваченные подстроки.
```
$rexMatch(@str, @tmpl, @case)
```
**Параметры**
- `@str` - строка, в которой осуществлется поиск; 
- `@tmpl` - шаблон поиска; 
- `@case` - флаг учета регистра, 1 - учитывать регистр при поиске, 0 - не учитывать;
		
**Возвращаемое значение**:
- если подстрока, соответствующая шаблону найдена, функция возвращает массив, состоящий из захваченных подстрок;      
- если совпадений не найдено, функция возвращает `0`;  
- в случае ошибки (некорректный шаблон поиска), функция возвращает `-1` и описание ошибки.

**Пример использования**
```
@str:="cronos.ru/cgi-bin/YaBB2/YaBB.cgi"
@res:=$rexMatch(@str,"(.+?)/(.+/)(.+)")
```
Переменной @res будет присвоен массив из трех строк: "cronos.ru", "cgi-bin/YaBB2/" и "YaBB.cgi"

### [rexReplace](rexReplace.crf)
Замена подстроки в строке с использованием регулярных выражений.
```
$rexReplace(@str, @tmpl, @sub, @case)
```
**Параметры**
- `@str` - строка, в которой осуществлется замена; 
- `@tmpl` - шаблон поиска; 
- `@sub` - подстрока для замены; 
- `@case` - флаг учета регистра, 1 - учитывать регистр при поиске, 0 - не учитывать;
		
**Возвращаемое значение**:

Функция возвращает новую строку, в которой произведена замена.

Если совпадений с шаблоном не найдено, возвращается исходная строка.

В случае ошибки (некорректное регулярное выражение), возвращается `-1` и описание ошибки.
