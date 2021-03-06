二进制、八进制、十六进制

定义：

    二进制：  缩写Bin，二进制数据是用0和1两个数码来表示的数。它的基数为2，进位规则是从右向左“逢二进一”

    四进制:   缩写Qua，以4为基数，用0，1，2，3表示的一种计算实数的一种进制。因其具体算法为逢四进一（四进制不常用）

    八进制：  Octal，缩写OCT或O，一种以8为基数的计数法，采用0，1，2，3，4，5，6，7八个数字，逢八进1

    十六进制：缩写hex或下标16，逢16进1。一般用数字0到9和字母A到F（或a-f）表示，其中:A-F表示10-15，这些称作十六进制数字

详解：

1.二进制：

1.1 概述
二进制，是计算技术中广泛采用的一种数制。二进制数据是用0和1两个数码来表示的数。它的基数为2，进位规则是“逢二进一”，借位规则是“借一当二”，由18世纪德国数理哲学大师莱布尼兹发现。计算机中的二进制则是一个非常微小的开关，用“开”来表示1，“关”来表示0。

回顾十进制计数规则：

    基数为10。
    有10个数字，0、1、2、3、4、5、6、7、8、9。
    逢10进1，借1当10。

那么类似，二进制计数规则就是：

    基数为2。
    有2个数字，即0和1。
    逢2进1，借1当2。
    
因此，二进制数据也是采用位置计数法，其位权是以2为底的幂。

    例如二进制数据110.11，逢2进1，其权的大小顺序为2²、2¹、2º、2﹣¹、2﹣²

    将二进制数据写成加权系数的形式为：
    
    (110.11)₂ = (1*2²)+(1*2¹)+(0*2º)+(1*2﹣¹)+(1*2﹣²)

1.2 二进制的运算

1.2.1 加减乘除

加法

    0+0=0    0+1=1    1+0=1   1+1=10（0 进位为1）
    
乘法

    0×0=0    1×0=0    0×1=0   1×1=1
    
减法

    0－0=0   1－0=1   1－1=0   0－1=1
       
除法

    0÷1=0    1÷1=1


1.2.2 二进制的位运算

程序中的所有数在计算机内存中都是以二进制的形式储存的。位运算实质是将参与运算的数字转换为二进制，而后逐位对应进行运算。

1.2.2.1 按位与 and（&）

    and运算通常用于二进制的取位操作，例如一个数 and 1的结果就是取二进制的最末位。
    这可以用来判断一个整数的奇偶，二进制的最末位为0表示该数为偶数，最末位为1表示该数为奇数。
    
    两位都为1，则为1；若有一个不为1，则为0, 即1&1=1，1&0=0，0&1=0，0&0=0。
    例如51 & 5 -> 00110011 & 00000101 = 00000001 -> 51 & 5 = 1
  
    特殊用法：
    （1）与0相与可清零。
    （2）与1相与可保留原值，可从一个数中取某些位。例如需要取10101110中的低四位，10101110 & 00001111 = 00001110，即得到所需结果。

1.2.2.2 按位或 or（|）

    or运算通常用于二进制特定位上的无条件赋值，例如一个数or 1的结果就是把二进制最末位强行变成1。如果需要把二进制最末位变成0，对这个数or 1之后再减一就可以了，其实际意义就是把这个数强行变成最接近的偶数。

    两位只要有一位为1，结果则为1，即1|1=1，1|0=1，0|1=1，0|0=0。
    
    特殊用法：
    （1）与0相或可保留原值。
    （2）与1相或可将对应位置1。例如，将X=10100000的低四位置1，使X | 00001111 = 10101111即可。


1.2.2.3  异或运算  xor（^）

    两位相“异”，即一位为1一位为0，则结果为1，否则为0。即1^1=1，1^0=0，0^1=0，0^0=1。 
         
    特殊用法：
    （1）使指定位翻转：找一个数，对应X要翻转的各位为1，其余为0，使其与X进行异或运算即可。例如，X=10101110，使低四位翻转，X ^ 00001111 = 10100001。
    （2）恒等律，与0相异或保留原值：X ^ 0 = X。例如 X ^ 00000000 = 10101110。
    （3）归零律：X ^ X = 0
    （4）xor运算的逆运算是它本身，也就是说，一个数对同一个数连续两次进行异或运算，结果与这个数相等。即（a xor b) xor b = a
     因此，交换方法为：A = A ^ B，B = A ^ B，A = A ^ B。
    （5）交换律：A ^ B = B ^ A
    （6）结合律： (A ^ B) · C = A ^ (B ^  C)
    （7）分配率： A ^ (B + C)= A ^ B + A ^  C

1.2.2.4 取反 not（~）

    把内存中的0和1全部取反，即 ~ 0 = 1，~ 1 = 0
    例如： 00110101 ~ 0 = 11001010
    需要注意整数类型有没有符号，如果not的对象是有符号的整数，情况有所不同。    

1.2.2.5 左移 shl（<<）

    将一个数左移x位，即左边丢弃x位，右边用0补x位。例：11100111 << 2 = 10011100
    若左移时舍弃的高位全为0，则每左移1位，相当于该数十进制时乘一次2。
    例：11(1011) << 2 = 44（11表示为1011时实际上不完整，若计算机中规定整型的大小为32bit，则11的完整二进制形式为00000000 00000000 0000000 00001011）

1.2.2.6 右移 shr（>>）

    将一个数右移若干位，右边舍弃，正数左边补0，负数左边补1。每右移一位，相当于除以一次2。
    例：4 >> 2 = 1，-14 >> 2 = -4。

1.2.2.7 无符号右移（>>>）

    将一个数右移若干位，左边补0，右边舍弃。
    例：-14 >>> 2 = (11111111 11111111 11111111 11110010) >>> 2 = (00111111 11111111 11111111 11111100) = 1073741820

1.2.2.8 拓展：

    ==原码==： 一个整数按照绝对值大小转换为二进制即为原码；
    ==反码==： 将二进制数按位取反，得到的即为反码；
    ==补码==： 反码加1即为补码。
    == 由于计算机底层硬件的限制，负数均使用补码表示。 ==


1.3 十进制与二进制之间的转换

1.3.1 二进制转换成十进制

    方法：“按权展开求和”，如：

    (110.11)₂ = (1*2²)+(1*2¹)+(0*2⁰)+(1*2⁻¹)+(1*2⁻²)
    
    (1011)₂ = (1*2³)+(0*2²)+(1*2¹)+(1*2⁰) = (11)₁₀

    规律：个位上的数字的次数是0，十位上的数字的次数是1，......，依次递增，而十分位的数字的次数是-1，百分位上数字的次数是-2，......，依次递减


1.3.2 十进制正整数转二进制

    十进制整数转二进制数：“除以2取余，逆序排列”（除二取余法）   （从右到左）

    比如十进制89换算成二进制就是：
    89÷2 ……1
    44÷2 ……0
    22÷2 ……0
    11÷2 ……1
    5÷2 ……1
    2÷2 ……0
    1
    (89)₁₀ =(1011001)₂ 

注：在计算机中存储字节是定长的，即我们8、16、32位等等，6的二进制位为110，但如果在8位计算机中是00000110，高位补零

1.3.3 十进制负整数转二进制

    在计算机中，除了十进制是有符号（正、负号）的外，其它如二进制、八进制、16进制都是无符号的

    十进制负数转二进制：“先取正数的二进制值（原码），再取反（反码），加1（补码）”
    
    例：(-32)₁₀转化成二进制数
    1. (32)₁₀ = (00100000)₂                   (原码)
    2. (00100000)₂ 逐位取反为：(11011111)₂      (反码)
    3. (11011111)₂  +1  = (11100000)₂          (补码)

    例：(-5)₁₀转化成二进制数
    1. (5)₁₀ = (00000101)₂
    2. (00000101)₂ 逐位取反为：(11111010)₂
    3. (11111010)₂ + 1 = (11111011)₂

1.3.4 十进制小数转二进制

    十进制小数转用二进制，通常是用乘以2取整，顺序排列（乘2取整法）  （从左到右）

    比如0.65换算成二进制就是：
    0.65 × 2 = 1.3 取1，留下0.3继续乘二取整
    0.3 × 2 = 0.6 取0， 留下0.6继续乘二取整
    0.6 × 2 = 1.2 取1，留下0.2继续乘二取整
    0.2 × 2 = 0.4 取0， 留下0.4继续乘二取整
    0.4 × 2 = 0.8 取0， 留下0.8继续乘二取整
    0.8 × 2 = 1.6 取1， 留下0.6继续乘二取整
    0.6 × 2 = 1.2 取1，留下0.2继续乘二取整

    一直循环，直到达到精度限制才停止（所以，计算机保存的小数一般会有误差，所以在编程中，要想比较两个小数是否相等，只能比较某个精度范围内是否相等）。这时，十进制的0.65，用二进制就可以表示为：0.1010011

注意：不是任何一个十进制小数都能转换成有限位的二进制数。
    
 
 
2 八进制

八进制的计数规则为：

    基数为8。
    由16个数字符号组成，分别是0、1、2、3、4、5、6、7。
    逢8进1，借1当8。
    
    
    二进制和十进制相互转换的方法——“按权展开”，同样适用于八进制的数转换为十进制，例如： 

    （7654.345）₈ = 7*8³ + 6*8²+ 5*8¹ + 4*8⁰ + 3*8⁻¹  +4*8⁻² + 5*8⁻³ 

    
    二进制转换为八进制，采用“3位并1位”，按从右向左方向，每3位二进制位一组，最高位不足3位，添0补足3位，然后将各组3位二进制数加权展开，得到八进制数。
   
                                           001  101  001  101  110  011
    (1101001101110011)₂ = （151563）₈        1    5    1    5    6    3


    将八进制转换为二进制，可以采用相反的操作“1位拆3位”。



3 十六进制

十六进制的计数规则为：

    基数为16。
    由16个数字符号组成，分别是0、1、2、3、4、5、6、7、8、9、A、B、C、D、E、F。
    逢16进1，借1当16。


    “按权展开”，同样适用于十六进制的数转换为十进制，例如BC0D：

    (BC0D)₁₆ = (11*16⁴⁻¹)+(12*16³⁻¹)+(0*16²⁻¹)+(13*16¹⁻¹) = (48141)₁₀


    类似八进制十六进制和二进制转换为“4位并1位”，“1位拆4位”的方法。





参考附录

https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6/361457?fr=aladdin

https://baike.baidu.com/item/%E4%BD%8D%E8%BF%90%E7%AE%97/6888804?fr=aladdin

二进制/八进制/十进制/十六进制  怎么学会？是怎么算的方式？ - yukirock的回答 - 知乎  （二进制权位的意义）
https://www.zhihu.com/question/23131605/answer/23713736

二进制/八进制/十进制/十六进制  怎么学会？是怎么算的方式？ - 涂小图的回答 - 知乎  
https://www.zhihu.com/question/23131605/answer/142989017

二进制有什么好处，为何电脑都采用二进制？ - Jeffersli的回答 - 知乎
https://www.zhihu.com/question/20830886/answer/48079392



 





