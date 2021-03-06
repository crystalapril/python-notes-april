# 数字

  - 整数类型
  - 浮点数类型
  - 复数类型
  - 数字类型转换
  - 数值运算操作符
  - 数值运算函数
  - math模块及函数

  
  
### 整数类型

    与数学中整数的概念一致
    
    - 可正可负，没有取值范围限制
    
    - pow(x,y)函数，计算xʸ，想算多大算多大
    
    例 1.1：
    >> pow(2,100)                        >> pow(2,pow(2,15))
    1267650600228229401496703205376      14154610310449547890015530277449516013481......
    
    整数类型的四种表现形式
    - 十进制：405,326,-217
    - 二进制，以0b或0B开头：0b010,-0B101
    - 八进制，以0o或0O开头：0o123,-0O456
    - 十六进制，以0x或0X开头：0x9a,-0X89


### 浮点数类型

    与数学中实数的概念一致
    
    - 带有小数点及小数的数字
    - 浮点数取值范围和小数精度都存在限制，但常规计算可忽略
    - 取值范围数量级约-10³⁰⁷ 至 10³⁰⁸ ，精度数量级10⁻¹⁶
    
    浮点数间运算存在不确定尾数，不是bug
    
    例 2.1：
    >> 0.1 + 0.3 
    0.4 
    >> 0.1 + 0.2
    0.30000000000000004
       ----------------
          不确定尾数
          
    0.1        53位二进制表示小数部分，约10⁻¹⁶
    0.0001100110011001100110011001100110011001100110011001101 （二进制表示）
    0.1000000000000000055511151231257827021181583404541015625 （十进制表示）
          二进制表示小数，可以无限接近，但不完全相同
    0.1 + 0.2 
          结果无限接近0.3，但可能存在尾数
          
    例 2.2：      
    >> 0.1 +0.2 == 0.3
    False
    >> round(0.1+0.2, 1) == 0.3
    True
    
    - round(x,d): 对x四舍五入，d是小数截取位数
    - 浮点数间运算与比较用round() 函数辅助
    - 不确定尾数一般发生在 10⁻¹⁶ 左右，round()十分有效
    
     浮点数可以采用科学计数法表示
     
     - 使用字母e 或E作为幂的符号，以10为基数，格式如下：
     
          <a>e<b>   表示a*10ᵇ
          
     例 2.3： 4.3e-3 值为 0.0043     9.6E5 值为 960000.0
     

### 复数类型

    与数学中复数的概念一致 
    
    如果 x² = -1 ，那么x的值是什么
    
    - 定义 j = √-1 ，以此为基础，构建数学体系
    - a + bj 被称为复数，或者complex(a,b)表示，a是实部，b是虚部，a，b都是浮点型
     
    例 3.1：
    z = 1.23e-4 + 5.6e+89j
    z.real获得实部    z.imag获得虚部
    0.000123          5.6e+89j
    
    不同数字类型之间可以进行混合运算，生成结果为“最宽”类型
    
    整数----> 浮点数 -----> 复数
    
    例 3.2：
    123 + 4.0 =127.0 （整数 + 浮点数 = 浮点数）
    

### 数字类型转换

|数字类型转换函数|                                描述                                  |
|---------------|---------------------------------------------------------------------|
| int(x)        | 将x转换为一个整数                                                     |
| float(x)      | 将x转换到一个浮点数                                                   |
| complex(x)    | 将x转换到一个复数，实数部分为 x，虚数部分为 0                           |
| complex(x, y) | 将 x 和 y 转换到一个复数，实数部分为 x，虚数部分为 y。x 和 y 是数字表达式 |

    例 4.1：
    # int(x, base=10)  base-进制数，默认十进制
    >> int()   # 不传入参数时，得到0    
    0                                    
    >> int(3.6)
    3
    >> int('12',16)   如果是带参数base的话，12要以字符串的形式进行输入，12 为 16进制
    18
    >> int('10',8)
    8
    
    # float()
    >> float(1)     >> float(-123.6)     >> float(123)
    1.0             -123.6               123.0
    
    # complex([real[, imag]])
    >> complex(1)
    (1+0j)
    >> complex("1+2j")  # 注：在"+"号两边不能有空格，也就是不能写成"1 + 2j"，应该是"1+2j"，否则会报错
    (1+2j)
    >> complex(1,2)
    (1+2j)

    
### 数值运算操作符

|操作符及使用|                                描述                                     |
|-----------|------------------------------------------------------------------------|
| x + y     | 加，x与y之和                                                            |
| x - y     | 减，x与y之差                                                            |
| x * y     | 乘，x与y之积                                                            |
| x / y     | 除，x与y之商                                                            |
| x // y    | 整数除，x与y之整数商                                                     |
| + x       | x本身                                                                   |
| - x       | x的负数                                                                 |
| x % y     | 余数，模运算                                                             |
| x ** y    | 幂运算，x的y次幂，xʸ；当y是小数时，为开方运算                               |
| x op= y   | 即 x = x op y,其中op为二元操作符，例如 x+=y,x-=y,x*=y,x/=y,x//=y,x%=y,x**=y|

    例 5.1：
    >> 21 + 10
    31
    >> 21 - 10
    11
    >> 21 * 10
    210
    >> 21 / 10
    2.1
    >> 10 // 3  # 取商  
    3
    >> 10 % 3   # 取余数
    1
    >> 2 ** 3
    8
    >> 2 ** 0.5
    1.4142135623730951

    >> x=3
    >> x +=5
    >> x
    8
    
    >> x=3
    >> x *=5
    >> x
    15

    >> x= 75
    >> x //=5.0  # 等价于 x = x // 5.0
    >> x
    15.0
    注意： // 得到的并不一定是整数类型的数，它与分母分子的数据类型有关系
    
    >> x=14
    >> x %=6
    >> x
    2
        
    >> x=3    
    >> x **=2   # 等价于 x = x **2
    >> x 
    9
    

### 数值运算函数

|      函数      |	                             描述                                |
|----------------|------------------------------------------------------------------|
| abs(x)         | 返回数字的绝对值                                                   |
| divmod(a, b)   | 把除数和余数运算结果结合起来，返回一个包含商和余数的元组(a // b, a % b)|
| max(seq)       | 返回给定参数的最大值，参数可以为序列                                 |
| min(seq)       | 返回给定参数的最小值，参数可以为序列                                 |
| pow(x, y[, z]) | 返回x的y次方，如果z在存在，再对结果取模，返回 pow(x,y) %z             |
| round(x [,n])  | 返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数         |
| sum(seq)       | 返回给定参数的和，参数可以为序列                                     |

    例 6.1：
    # abs 
    >> abs(-10)               >> abs(10)
    10                        10
    
    # divmod(a, b)
    >> divmod(7,2)      >> divmod(8,2)     >> divmod(1+2j,1+0.5j)
    (3,1)               (4,0)              ((1+0j), 1.5j)
    
    # max(seq) 
    >> max(80, 100, 1000)     >> max(-20, 100, 400)
    1000                      400
    
    # min(seq)
    >> min(80, 100, 1000)     >> min(-20, 100, 400) 
    80                        -20
    
    # pow(x, y[, z])   返回 pow(x,y) %z 
    # 区别于math.pow(),pow() 通过内置的方法直接调用，内置方法会把参数作为整型，而 math 模块则会把参数转换为 float
    >> pow(100,2)      >> math.pow(100,2)
    10000              10000.0
    >> pow(3,3,5)
    2
    
    # round(x [,n])
    >> round(4.05326)     >> round(4.05326,1)    >> round(-4.05326)
    4                     4.1                    -4.05
    
    # sum(iterable[, start])
    >> sum([4,0,5])       >> sum((4,0,5),1)
    9                     10
    
    
### math模块及函数
    
    math模块提供了对C标准定义的数学函数的访问。
    这些函数不适用于复数；如果需要计算复数，使用 cmath 模块中的同名函数。
    
    math模块，包含有：
    数论与表示函数、幂函数与对数函数、三角函数、角度转换函数、双曲函数、特殊函数、常数
    
    这里仅描述常用的数学函数、幂函数及对数函数
    
|  数论与表示函数  |                          描述                                 |
|----------------|---------------------------------------------------------------|
| ceil(x)        | 返回 x 的上限，即大于或者等于 x 的最小整数                         |
| copysign(x,y)  | 返回一个基于 x 的绝对值和 y 的符号的浮点数                         |
| fabs(x)        | 返回 x 的绝对值                                                 |
| factorial(x)   | 以一个整数返回 x 的阶乘。 如果 x 不是整数或为负数时则将引发 ValueError|
| floor(x)       | 返回 x 的向下取整，小于或等于 x 的最大整数                          |
| fmod(x,y)      | 取模运算                                                          |
| frexp(x)       | 返回 x 的尾数和指数作为对``(m, e)``                                |
| fsum(iterable) | 返回迭代中的精确浮点值                                             |
| gcd(a,b)       | 返回整数 a 和 b 的最大公约数                                       |
| hypot(x, y)    | 欧几里德范数 sqrt(x*x + y*y)                                      |
| isclose(a, b)  | 若 a 和 b 的值比较接近则返回 True，否则返回 False                   |
| isfinite(x)    | 如果 x 既不是无穷大也不是NaN，则返回 True ，否则返回 False           |
| isinf(x)       | 如果 x 是正或负无穷大，则返回 True ，否则返回 False                  |
| isnan(x)       | 如果 x 是 NaN（不是数字），则返回 True ，否则返回 False              |
| ldexp(x,i)     | 返回 x * (2**i)                                                   |
| modf(x)        | 返回 x 的小数和整数部分。两个结果都带有 x 的符号并且是浮点数           |
| remainder(x,y) | 返回 IEEE 754 风格的 x 相对于 y 的余数                              |
| trunc(x)       | 返回 Real 值 x 截断为 Integral （通常是整数）                       |

    例 7.1：
    import math
    
    # math.ceil(x)    向上取整
    >> math.ceil(405.326)      >> math.ceil(-40.5)      >> math.ceil(math.pi)
    406                        -40                      4
        
    # math.copysign()   返回一个基于 x 的绝对值和 y 的符号的浮点数
    >> math.copysign(3,-2)     >> math.copysign(-3,2)
    -3.0                       3.0
        
    # math.fabs(x) 
    # 区别于内置函数abs()：fabs() 函数只对浮点型跟整型数值有效， abs() 还可以运用在复数中
    >> math.fabs(-40.5)         >> math.fabs(32.6)
    40.5                        32.6
    
    # math.factorial(x)   阶乘
    >> math.factorial(3)        >> math.factorial(4)
    6                           24    
    
    # math.floor(x)   向下取整
    >> math.floor(-40.5)        >> math.floor(32.6) 
    -41                         32
    
    # math.fmod(x,y)  
    # 模运算, 与运算符号%的区别：
      - fmod默认返回浮点数，fmod() 在使用浮点数时通常是首选，而x % y 在使用整数时是首选
      - 对于x、y符号一致时，%与fmod结果一致
      - 但x、y符号不一致时，结果不同      
    >> math.fmod(3.1,2)       >> math.fmod(-3,-2)     >> math.fmod(-3,2)      >> math.fmod(3,-2)
    1.1                       -1.0                    -1.0                    1.0             
    >> 3.1 % 2                >> -3 % -2              >> -3 % 2               >> 3 % -2
    1.1                       -1                      1                       -1
    
    # math.frexp(x)  将x分解为尾数与指数  x = 尾数 * 2^指数
    >> math.frexp(3)       >> math.frexp(-32)
    (0.75, 2)              (-0.5, 6)
    >> 0.75*2**2           >> -0.5*2**6
    3.0                    -32
    
    # math.fsum(iterable)    功能同内置函数sum()，但精度更高
    >> math.fsum((1,2,3,4))
    10.0
    
    # math.gcd(a,b)  返回最大公约数
    >> math.gcd(8,6)          >> math.gcd(27,36)
    2                         9
    
    # math.hypot(x, y)  返回欧几里德范数 sqrt(x*x + y*y)
    >> math.hypot(1,2)        >> math.hypot(0,2)
    2.23606797749979          2.0
    
    # math.isclose(a, b, *, rel_tol=1e-09, abs_tol=0.0)   
    # a与b “接近” 的判定条件是： 
      - a与b的差距是否小于ab较大的那个乘以rel_tol
      - 或a、b差距小于abs_tol
      - 也即 abs(a-b) <= max(rel_tol * max(abs(a), abs(b)), abs_tol)
    >> math.isclose(1,1.01)  >> math.isclose(1,1.01,rel_tol=0.1)  >> math.isclose(1,1.0000000001)  
    False                    True                                 True
    
    # math.isfinite()   如果 x 既不是无穷大也不是NaN，则返回 True ，否则返回 False
    >> math.isfinite(0.1)     >> math.isfinite(3)
    True                      True
    
    # math.isinf()   如果 x 是正或负无穷大，则返回 True ，否则返回 False  
    >> math.isinf(405)
    False
    
    # math.isnan(x)   如果 x 是 NaN（不是数字），则返回 True ，否则返回 False   
    >> math.isnan(405)
    False
    
    # math.ldexp(x,i)     返回 x * (2**i)  ，math.frexp(x)的逆运算
    >> math.ldexp(5,2)
    20.0
    
    # math.modf(x)   返回 x 的小数和整数部分组成的元祖
    >> math.modf(math.pi)
    (0.14159265358979312, 3.0)
    
    # math.remainder(x,y)   返回 IEEE 754 风格的 x 相对于 y 的余数  
    >> math.remainder(4,3)
    1.0
    
    # math.trunc(x)   返回 Real 值 x 截断为 Integral （通常是整数）    
    >> math.trunc(4.05)
    4    
    
    
|幂函数与对数函数|                                描述                                     |
|--------------|-------------------------------------------------------------------------|
| exp(x)       | 返回 e 次 x 幂，其中 e = 2.718281... 是自然对数的基数                      |
| expm1(x)     | 返回 e 的 x 次幂，减1                                                     |
| log(x[,base])| 使用两个参数，返回给定的 base 的对数 x ，计算为 log(x)/log(base)，默认base为e |
| log1p(x)     | 返回 1+x (base e) 的自然对数,以对于接近零的 x 精确的方式计算结果              |
| log2(x)      | 返回 x 以2为底的对数                                                       |
| log10(x)     | 返回 x 底为10的对数                                                        |
| pow(x,y)     | 返回 x 的 y 次幂                                                           |
| sqrt(x)      | 返回 x 的平方根                                                            |

    例 7.2：
    
    import math
    
    # math.exp(x)   返回e为底的指数,eˣ
    >> math.exp(2)              >> math.exp(-4.05)
    7.38905609893065            0.017422374639493515
    
    # math.expm1(x) 返回x的指数,eˣ -1
    >> math.exp(2)              >> math.exp(-4.05)
    6.38905609893065            -0.9825776253605065
    
    # math.log(x[,base])  返回 log(x)/log(base)，默认base为e 
    >> math.log(10)             >> math.log(10,2)
    2.302585092994046c          3.3219280948873626    
    
    # math.log1p(x)  返回 1+x (base e) 的自然对数，math.log1p(x)=math.log(x+1,math.e)
    >> math.log1p(10)
    2.3978952727983707
    
    # math.log2(x)   返回 x 以2为底的对数。这通常比 log(x, 2) 更准确
    >> math.log2(10)
    3.321928094887362    
    
    # math.log10(x)  返回 x 底为10的对数。这通常比 log(x, 10) 更准确
    >> math.log10(2)
    0.3010299956639812
    
    # math.pow(x,y)  返回 x 的 y 次幂。如果 x 是负数，会引发 ValueError 
    >> math.pow(2,3)        >> math.pow(2,-3)       >> math.pow(2,2.5)  
    8                       0.125                   5.656854249492381
    
    # math.sqrt( x )    返回 x 的平方根   
    >> math.sqrt(4)         >> math.sqrt(5)
    2.0                     2.23606797749979


|常量 |              描述              |
|----|--------------------------------|
| pi | 数学常量 pi（圆周率，一般以π来表示）|
| e  | 数学常量 e，e即自然常数（自然常数） |
    

### 附录

https://docs.python.org/3/library/math.html

https://www.runoob.com/python3/python3-number.html


    
