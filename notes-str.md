# 文本字符串 STR

  - 字符串类型的表示  
  - 字符串的转义字符
  - 字符串操作符  
  - 字符串处理函数
  - 字符串处理方法
  - 字符串类型的格式化
  
 ###  字符串类型的表示
 
     字符串定义：由0个或多个字符组成的有序字符序号
     - 字符串由一对单引号或一对双引号表示单行字符串
       例 1.1：
       >> 'C' 
       >> "请输入带有符号的温度值："
     - 字符串是字符的有序序号，可以对其中的字符进行索引
       例 1.2：
       "请"是"请输入带有符号的温度值："的第0个字符
     - 字符串还可以由一对三单引号或三双引号表示，多行字符串
       例 1.3：
       '''Pyhton 
                  语言 '''
       Q：如果希望在字符串中包含双引号或单引号呢？
       A：'这里有个双引号(")'  或者  "这里有个单引号(')"
       Q：如果希望在字符串中既包括单引号又包括双引号呢？
       A：''' 这里既有打引号(')又有双引号(") ''' 
     
     字符串的使用
     - 正向递增序号 和 反向递减序号
     
                          反向递减序号
                 <-------------------------------
     -12  -11  -10  -9   -8   -7   -6  -5   -4   -3   -2  -1
     请    输   入   带   有   符   号   的   温   度   值   ：
      0    1    2    3    4    5    6   7    8    9   10   11
                --------------------------------->
                           正向递增序号
     使用[]获取字符串中一个或多个字符串
     -索引：返回字符串中单个字符     <str>[m]
      例 1.4：
      >> "请输入带有符号的温度值："[0]
      >> TempStr[-1]
     -切片：返回字符串中一段字符子串  <str>[m:n]
      例 1.5：
      >> "请输入带有符号的温度值："[1:3]
      >> TempStr[0:-1]
      
      字符串切片高级用法：
      [m:n:k]，根据步长对字符串切片
      - <str>[m:n]，m缺失[:n]表示至开头，n缺失[m:]表示至结尾
      例 1.6：
      >> "〇一二三四五六七八九十"[:3]
      〇一二
      - <str>[m:n:k]，根据步长k对字符串切片
      例 1.7：
      >> "〇一二三四五六七八九十"[1:8:2]
      "一三五七"
      >> "〇一二三四五六七八九十"[::-1]
      "十九八七六五四三二一〇"
 
 
 ###  字符串的转义字符      
      
    如果字符串内部既包含'又包含"怎么处理，可以用转义字符\来标识。
     
    例 2.1：
    >> 'I\'m \"OK\"!'
    I'm "OK"!
      
    转义字符\可以转义很多字符，比如\n表示换行，\t表示制表符，字符\本身也要转义，\\表示的字符就是\:
      
    使用\n换行，例 2.2 :  
     >> print('duo \nduo')      
     "duo
           duo"
      
    使用转义字符"\t"制表符，可以看到打印结果中间隔了一个制表符，例 2.3 ：
    >> print('duo \tduo')      
    duo  duo

    使用转义字符"\""引号，例 2.4：
    >> print('duo \"duo')      
    duo "duo

    使用转义字符"\\"引号，例 2.5 ：
    >> print('duo \\duo')
    duo \duo
    >> print('\\\n\\')
    \
    \
    
    原始字符串
    如果字符串里面有很多\，为了简化，Python允许用r''表示''内部的字符串默认不转义
    例 2.6：
    >> print(r'duo \\duo')
    duo \\duo
    >> print('\\\t\\')
    \       \
    >> print(r'\\\t\\')
    \\\t\\

转义字符表

|   转义字符  |                 描述            	   |
| ---------- | ------------------------------------ |
| \(在行尾时) | 续行符                                |
| \\         | 反斜杠符号                            |
| \’	       | 单引号                                |
| \”         | 双引号                                |
| \a	       | 响铃                                  |
| \b         | 退格(Backspace)                       |
| \e	       | 转义                                  |
| \000       | 空                                    |
| \n         | 换行                                  |
| \v         | 纵向制表符                            |
| \t         | 横向制表符                            |
| \r         | 回车                                  |
| \f	       | 换页                                  |
| \oyy       | 八进制数yy代表的字符，例如：\o12代表换行 |
| \xyy       | 十进制数yy代表的字符，例如：\x0a代表换行 |
| \other     | 其它的字符以普通格式输出                |

 
 ###  字符串操作符
 
|  操作符及使用   |                   描述                 |
| -------------- | ------------------------------------- |
| x + y          | 连接两个字符串x和y                      |
| n * x 或 x * n | 赋值n次字符串x                          |
| x in s         | 如果x是s的子串，返回True，否则返回False   |
| x not in x     | 如果x不是s的子串，返回True，否则返回False |

    例 3.1：
    >> 'a' + 'b'          >> 'b' + 'a'
    'ab'                  'ba'
    >> 3 * 'ab'           >> 'ab' * 3
    'ababab'              'ababab'
    >> 'a' in 'ab'        >> 'c' in 'ab'
    True                  False
    >> 'a' not in 'ab'    >> 'c' not in 'ab'
    False                 True 
 
 ###  字符串处理函数
      
|     函数及使用    |                 描述              |
| ---------------- | -------------------------------- |
| len(x)           | 返回字符串的长度                   |
| str(x)           | 任意类型x所对应的字符串形           |
| max(x)           | 返回字符串 x 中最大的字母           |
| min(x)           | 返回字符串 x 中最小的字母           |
| hex(x) 或 oct(x) | 整数x的十六进制或八进制小写形式字符串 |
| chr(x)           | x为Unicode编码，返回其对应的字符    |
| ord(x)           | x为字符，返回其对应的Unicode编码    |

    例 4.1：
    >> len('ab')      >> len('一二三456')
    2                 6
    >> str(12)        >> str([1,2])
    '12'              '[1,2]' 
    
    >> max('ab')
    'b'
    >> min('ab')
    'a'
    
    >> hex(425)
    '0x1a9'
    >> oct(425)
    '0o651' 
    
    
    chr(x),ord(x)
    
                chr(u)
              --------->
    Unicode                 单字符
              <---------
                 ord(x)         
    例 3.1：
    >> ord('A')
    65
    >> ord('中')
    20013
    >> chr(66)
    'B'
    >> chr(25991)
    '文'    
   

 ###  字符串处理方法   

    “方法”特指<a>.<b>()风格中的函数<b>()
    
    -方法本身也是函数，但是与<a>有关，<a>.<b>()风格使用    
    -字符串或字符串变量是<a>，存在一些可用方法    
    
|                     |                     |      字符串的方法     |                     |                     | 
| --------------------|-------------------- | --------------------|---------------------|-------------------- |
| string.capitalize() | string.center()     | string.count()      | string.docode()     | string.encode()     | 
| string.endswith()   | string.expandtabs() | string.find()       | string.format()     | string.index()      |   
| string.isalnum()    | string.isalpha()    | string.isdecimal()  | string.isdigit()    | string.islower()    |
| string.isnumeric()  | string.isspace()    | string.istitle()    | string.isupper()    | string.join(seq)    |	
| string.ljust()      | string.lower()      | string.lstrip()     | string.maketrans()  | string.partition()  | 
| string.replace()    | string.rfind()      | string.rindex()     | string.rjust()      | string.rpartition() |
| string.rstrip()     | string.split()      | string.splitlines() | string.startswith() | string.strip()      |
| string.swapcase()   | string.title()      | string.translate()  | string.upper()      | string.zfill()      |
	
常见用法详见：

https://github.com/crystalapril/python-notes-april/blob/master/notes-str-functions-method.md



 ###  字符串格式化

 字符串格式化可以用 % 运算符，也可以使用.format()方法，或f-string。     
    
    5.1 % (取模) 运算符 ： 
    
    有时需要输出类似'亲爱的xxx你好！你的地址是xx，电话是xx'的字符串，xxx的内容是变化的，所以需要简便的格式化字符串的方式。
    
    % 运算符就是用来格式化字符串的。
    
    %s表示用字符串替换，%d表示用整数替换，%f表示浮点数替换，%x表示十六进制整数替换。
    有几个%?占位符，后面就跟几个变量或者值，顺序一一对应。如果只有一个%?，括号可以省略。 
    
    例： 
    # %s 可以把任何类型转换为字符串
    >> 'my name is %s.' % ('april')      
    'my name is april.'
    
    # %d 整数
    >> 'april is %d years old.' % (18)   
    'april is 18 years old.'
    
    # %f 浮点数
    >> 'her weight is %f kg.' % (37.5)  
    'her weight is 37.500000 kg.'
    
    # %.2f 浮点数，指定保留2位小数点
    >> 'her weight is %.2f kg.' % (37.262)  
    'her weight is 37.26 kg.'
    
    #  %10s %10d %10.2f 指定占位符宽度  默认空格
    >> 'name:%10s age:%10d weight:%10.2f' % ('april',18,37.2666)  
    'name:     april age:        18 weight:     37.27'
    
    #  %-10s %-10d %-10.2f 指定占位符宽度  左对齐
    >> 'name:%-10s age:%-10d weight:%-10.2f' % ('april',18,37.2666)  
    'name:april      age:18         weight:37.27     '
    
    # 指定0为占位符
    >> 'name:%-10s age:%08d weight:%08.2f' % ('april',18,37.2666) 
    'name:april      age:00000018 weight:00037.27'
    
    # 科学计数法，默认保留小数点后6位 
    >> '%e' % (3.2666666)    
    '3.266667e+00'
    
    # 科学计数法，指定保留小数点后3位 
    >> '%.3e' % (3.2666666) 
    '3.267e+00'
    
    # %g  保证6位有效数字的前提下用 %f表示，否则用 %e  
    >> '%g' % (3266.666666)           
    '3266.67'
    
    >> '%g' % (32666666.66)  
    '3.26667e+07'
    
    # %g  此时7是有效数字的个数  
    >> '%.7g' % (3266.666666)         
    '3266.667'
    
    >> '%.3g' % (3266.666666)     
    '3.27e+03'
    
    # %% 表示一个%(转义)
    >> 'growth rate: %d %%' % 7    
    'growth rate: 7 %'
    

python字符串格式化符号

|  符号  |                描述             |
| ----- | ------------------------------- |
| %c    | 格式化字符及其ASCII码             |
| %s    | 格式化字符串                     |
| %d    | 格式化整数                       |
| %u    | 格式化无符号整型                  |
| %o    | 格式化无符号八进制数              |
| %x    | 格式化无符号十六进制数             |
| %X    | 格式化无符号十六进制数（大写）      |
| %f    | 格式化浮点数字，可指定小数点后的精度 |
| %e    | 用科学计数法格式化浮点数           |
| %E    | 作用同%e，用科学计数法格式化浮点数  |
| %g    | %f和%e的简写                     |
| %G    | %f 和 %E 的简写                  |
| %p    | 用十六进制数格式化变量的地址        |    
    

格式化操作符辅助指令

|  符号  |	                          功能                                   |
| ----- | ----------------------------------------------------------------------- |
| *     | 定义宽度或者小数点精度                                                     |
| -     | 用做左对齐                                                                |
| +     | 在正数前面显示加号( + )                                                    |
| <sp>  | 在正数前面显示空格                                                         |
| #     | 在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X')|
| 0     | 显示的数字前面填充'0'而不是默认的空格                                        |
| %     | '%%'输出一个单一的'%'                                                      |
| (var) | 映射变量(字典参数)                                                         |
| m.n.  | m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)                          |    
    

    5.2 format()方法 ： 
    
    基本语法是通过 {} 和 : 来代替以前的 % 
    format 函数可以接受不限个参数，位置可以不按顺序。
     
         <模板字符串>.format(<逗号分隔的参数>)
	 
	                            槽
	 
	 "{ }:计算机{ }的CPU占用率为{ }%".format("2018-10-10","C",10)
	   |        |              |                |        |  |
	   0        1              2                0        1  2
	   ------------------------>           ------------------->
	     字符串中槽{ }的默认顺序                 format()中参数的顺序
	     
	                       
	                            槽
	   --------------------------------------------------  
	   |        --------------------------------        |
	   |        |                              |        |
	 "{1}:计算机{0}的CPU占用率为{2}%".format("2018-10-10","C",10) 
	                          |                             |
				  -------------------------------
    例：
    
    >> "{} {}".format("hello","april")   #  不设置指定位置，按默认顺序
    'hello april'
    >> "{0} {1}".format("hello","april")  # 设置指定位置
    'hello april'
    >> "{1} {0} {1}".format("hello","april")  # 设置指定位置
    'april hello april'
    
    也可以设置参数：
    # 通过字典设置参数
    >> student = {'name':'april','age':18}
    >> '姓名:{name},年龄:{age}'.format(**student)
    '姓名:april,年龄:18'
    
    #通过列表索引设置参数
    >> my_list = ['april',18]
    >> '姓名：{0[0]},年龄：{0[1]}'.format(my_list)
    '姓名：april,年龄：18'
    
    >> 'hello, {0}, 成绩提升了 {1:.2f}%'.format('april',4.05326)
    'hello, april, 成绩提升了 4.05%'


    槽内部对格式化的配置方式
    
    { <参数序号> : <格式控制标记> }

|   ：   |     <填充>     |           <对齐>         |    <宽度>     |      <,>     |           <.精度>            |             <类型>              |
|--------|---------------|--------------------------|--------------|--------------|------------------------------|---------------------------------|
| 引导符号|用于填充的单个字符| < 左对齐 > 右对齐 ^ 居中对齐|槽设定的输出宽度|数字的千位分隔符|浮点数小数精度 或字符串最大输出长度|整数类型:b,c,d,o,x,X，浮点数类型:e,E,f,%|

    例：
    # = 填充 ^ 居中对齐 
    >> '{0:=^20}'.format('april')
    '=======april========'
    
    # * 填充 > 右对齐
    >> '{0:*>20}'.format('april')
    '***************april'
    
    # 指定宽度 10
    >> '{:10}'.format('april')
    'april     '
    
    # .2f 浮点数，保留2位小数点
    >> '{0:.2f}'.format(326.666666)
    '326.67'
    
    # 整数类型
    >> '{0:b},{0:c},{0:d},{0:o},{0:x},{0:X}'.format(326)
    '101000110,ņ,326,506,146,146'
    
    # 浮点数
    >> '{0:e},{0:E},{0:f},{0:%}'.format(3.26)
    '3.260000e+00,3.260000E+00,3.260000,326.000000%'
    
    >> format(0.0026,'.2e')
	#输出效果：
    '2.60e-03'
    


format数字格式化表


|数字	   |    格式   |	  输出   |       	   描述          |
|-----------|-----------|----------|-------------------------|
|3.1415926  | {:.2f}    |3.14      |保留小数点后两位           |
|3.1415926  |{:+.2f}    |+3.14     |带符号保留小数点后两位      |
|-1 	    |{:+.2f}  	|-1.00     |带符号保留小数点后两位      |
|2.71828    |{:.0f} 	|3 	   |不带小数                  |
|5 	    |{:0>2d} 	|05 	   |数字补零 (填充左边, 宽度为2)|
|5 	    |{:x<4d} 	|5xxx 	   |数字补x (填充右边, 宽度为4) |
|10 	    |{:x<4d} 	|10xx 	   |数字补x (填充右边, 宽度为4) |
|1000000    |{:,} 	|1,000,000 |以逗号分隔的数字格式        |
|0.25 	    |{:.2%} 	|25.00%    |百分比格式                 |
|1000000000 |{:.2e} 	|1.00e+09  |指数记法                   |
|13 	    |{:10d}     |13 	   |右对齐 (默认, 宽度为10)     |
|13 	    |{:<10d} 	|13 	   |左对齐 (宽度为10)           |
|13 	    |{:^10d} 	|13        |中间对齐 (宽度为10)         |
|11         |'{:b}'.format(11) , '{:d}'.format(11) , '{:o}'.format(11) , '{:x}'.format(11) , '{:#x}'.format(11) , '{:#X}'.format(11)| 1011 , 11 , 13 , b , 0xb , 0XB    | 进制 |

	
    5.3 f-string
    
    f-string，亦称为格式化字符串常量（formatted string literals），是Python3.6新引入的一种字符串格式化方法。
    
    f-string在形式上是以 f 或 F 修饰符引领的字符串（f'xxx' 或 F'xxx'），以大括号 {} 标明被替换的字段，例如：
    >> name = 'april'
    >> f'Hello, my name is {name}'
    'Hello, my name is april'
    
    f-string在本质上并不是字符串常量，而是一个在运行时运算求值的表达式：
    While other string literals always have a constant value, formatted strings are really expressions evaluated at run time.
    （与具有恒定值的其它字符串常量不同，格式化字符串实际上是运行时运算求值的表达式。）
    —— Python Documentation

    f-string在功能方面不逊于传统的%-formatting语句和str.format()函数，同时性能又优于二者，用法举例：
    
    5.3.1 简单例子

	>> name = 'april'
	>> age = 18
	>> f"Hello, {name}. you are {age}" 
	'Hello, april. you are 18'

    5.3.2 任意表达式及函数调用

	f字符串是在运行时进行渲染，因此可以将任何有效的Python表达式或函数放入其中；
	>> f"{2*26}"
	'52'

	>> f"{name.lower()} is funny."
	'april is funny.'
	
	>> import math
	>> f'The answer is {math.log(math.pi)}'
	'The answer is 1.1447298858494002'

	可以使用带有f字符串的类创建对象。
	class f_str:
	    def __init__(self, name, age, sex):
		self.name = name
		self.age = age
		self.sex = sex
	    def __repr__(self):
		return f"your name is {self.name}, and age is {self.age}, but you are {self.sex}, Surprise!"

	you_self = f_str("april", 18, "female") 
	you_self
	--> Your name is april, and age is 18, but you are female, Surprise!

    5.3.3 多行 f-string

	每一行开头放一个 f；
	>> profession = "comedian"
	>> affiliation = "Monty Python"
	>> message = (f"Hi {name}. "
		      f"You are a {profession}. "
		      f"You were in {affiliation}.")
	>> message
	'Hi april. You are a comedian. You were in Monty Python.'

	某一行放个 f ，仅该行进行匹配，其它行不变；
	>> message = (f"Hi {name}. "
	  	      "You are a {profession}. "
		      "You were in {affiliation}.")
	>> message
	'Hi april. You are a {profession}. You were in {affiliation}.'

	多行一个f且使用三个引号时，返回时有换行符。
	>> message = f"""
	  	     Hi {name}. 
		     You are a {profession}. 
		     You were in {affiliation}.
		     """
	>> message
	'\n    Hi april. \n    You are a comedian. \n    You were in Monty Python.\n 
	


      
 ### 附录



https://www.icourse163.org/learn/BIT-268001?tid=1206073223#/learn/content?type=detail&id=1210530417&cid=1212669817 北京理工大学 嵩天 python语言程序设计
 
https://blog.csdn.net/sunxb10/article/details/81036693  f-string简介 
https://www.jianshu.com/p/d0aa54e497ba                  f-string
 
 
 


