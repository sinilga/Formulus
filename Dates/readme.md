# Dates
набор пользовательских функций для работы с датами

### Dates_CurMonthBounds
Возвращает границы указанного месяца

**Параметры**
		`@Month` - номер месяца (1..12)      
		`@Year` - номер года
    
		Если первым параметром в функцию передана дата (т.е. строка формата ДД.ММ.ГГГГ), то месяц и год берутся из этой даты, а второй параметр игнорируется.
    
		Если первый парамер не задан - он принимается равным текущей дате.	
		
**Возвращаемое значение**
		Функция возвращает массив из двух значений, определяющих даты первого и последнего дня месяца. 
			
**Примеры использования**
`@n := $Dates_CurMonth(Bounds(2,2020)
@ret := catval(@n," - ")
`
Переменной `@ret` будет присвоено значение  "01.02.2020 - 29.02.2020".

`@n := $Dates_CurMonth(Bounds()
@ret:=@n[2]
`
В переменной `@ret` будет содержаться дата последнего дня текущего месяца