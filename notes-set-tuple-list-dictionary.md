集合、元祖、列表、字典

1 集合

1.1 集合类型定义

    集合类型与数学中的集合概念一致
    
    -集合元素之间无序，每个元素唯一，不存在相同元素
    -集合元素不可更改，不能是可变数据类型
    
    -集合用大括号{}表示，元素间用逗号分隔
    -建立集合类型用{}或set()
    -建立空集合类型，必须使用set()  （不同于tuple,list可以直接用(),[]来创建，因为{}表示空的字典）
    
    >>> A = {"python",123,("python",123)}  #使用{}建立集合
    {"python",123,("python",123)} 
    
    >>> B = set("pypy123")   #使用set()建立集合
    {'1','p','2','3','y'}    
    #注意，新建集合的顺序与原字符串的顺序有所不同了
    
    >>> C = {"python",123,"python",123} 
    {"python",123}
    #相当于去重了 

1.2 集合操作符（6个操作符， 4个增强操作符）
    
|  集合操作符及应用 |                   描述                     |
|-----------------|------------------------------------------ |
|      S | T      |  并，返回一个新集合，包括在集合S和T中的所有元素 |    
|      S - T      |  差，返回一个新集合，包括在集合S但不在T中的元素 |   
|      S & T      |  交，返回一个新集合，包括同时在集合S和T中的元素 |
|      S ^ T      |  补，返回一个新集合，包括集合S和T中的非相同元素 |
| S <= T 或 S < T |  返回True/False，判断S和T的子集关系           |
| S >= T 或 S > T |  返回True/False，判断S和T的包含关系           |
|    S |= T       |  并，更新集合S，包括在集合S和T中的所有元素     |
|    S -= T       |  差，更新集合S，包括在集合S但不在T中的元素     |
|    S &= T       |  交，更新集合S，包括同时在集合S和T中的元素     |
|    S ^= T       |  补，更新集合S，包括集合S和T中的非相同元素     |
    
    例 1.2：
    >>> A = {"p","y",123}
    >>> B = set("pypy123")
    {'1','p','2','3','y'}   
    
    >>> A - B   # 差
    {123}
    >>> B - A
    {'3','1','2'}
    >>> A & B   # 交
    {'p','y'}
    >>> A | B   # 并
    {'1','p','2','y','3',123}
    >>> A ^ B   # 补
    {'2',123,'3','1'}

1.3 集合处理方法

| 集合操作函数或方法 |                      描述                       |
|------------------|-------------------------------------------------|
| S.add(x)         | 如果x不在集合S中，将x增加到S                      |
| S.discard(x)     | 移除S中元素x，如果x不在集合S中，不报错             |
| S.remove(s)      | 移除S中元素x，如果x不在集合S中，产生KeyError异常   |
| S.clear()        | 移除S中所有的元素                                |
| S.pop()          | 随机返回S的一个元素，更新S，若S为空产生KeyError异常 |
| S.copy()         | 返回集合S的一个副本                               |
| len(S)           | 返回集合S的元素个数                               |
| x in S           | 判断S中元素x，x在集合S中，返回True，否则返回False   |
| x not in S       | 判断S中元素x，x不在集合S中，返回True，否则返回False |
| set(x)           | 将其他类型变量x转变为集合类型                      |
    
    例 1.3：
    >>> A = {"p","y",123}
    >>> for item in A:
            print(item,end="")
    p123y    
    
    >>> A
    {"p",123,"y"}
    
    >>> try:
            while True:
                print(A.pop(),end="")
            except:
                pass
    p123y
    
    >>> A
    set()   
    
1.4 集合类型应用场景

    1.4.1 包含关系的比较
    >>> "p" in {"p","y",123}
    True
    >>> {"p","y"} >= {"p","y",123}
    False
    
    1.4.2 数据去重：集合类型所有元素无重复
    >>> ls = ["p","y","p","y",123]
    >>> s = set(ls)    # 利用了集合无重复元素的特点
    {"p","y",123}
    >>> lt = list(s)   # 还可以将集合转换为列表
    ["p","y",123]
 
 
2 序列类型及操作

2.1 序列类型定义

    序列是具有先后关系的一组元素
    
    -序列是一维元素向量，元素类型可以不同
    -类似数学元素序列：s₀,s₁,...,sₙ₋₁
    -元素间由序号引导，通过下标访问序列的特定元素   
    
    序列是一个基类类型，包含:    
    字符串类型 、元祖类型、列表类型
    
    序号的定义
     
                      反向递减序号
            <--------------------------------                    
     -5         -4         -3       -2           -1   
     
    "BIT"     3.1415      1024     (2,3)     ["中国",9]
    
      0          1          2        3            4
            -------------------------------->
                      正向递增序号
        

2.2 序列通用处理函数及方法

| 序列通用操作符及应用 |                   描述                          |
|--------------------|-------------------------------------------------|
| x in s             | 如果 x 是序列 s 的元素，返回True，否则返回Fasle    |
| x not in s         | 如果 x 是序列 s 的元素，返回Fasle，否则返回True    |
| s + t              | 连接两个序列 s 和 t                               |
| s*n 或 n*s         | 将序列 s 复制 n 次                                |
| s[i]               | 索引，返回 s 中的第 i 个元素，i是序列的序号         |
| s[i:j] 或 s[i:j:k] | 切片，返回序列 s 中第 i 到 j 以 k 为步长的元素子序列 |
    
    例 2.2.1：
    >>> ls = ["python" ,123,".io"]
    >>> ls[::-1]
    ['.io',123,'python']
    >>> s = "python123.io"
    >>> s[::-1]
    'oi.321nohtyp'
    
    >>> ls[0]
    'python'
    >>> ls[2]
    '.io'
    >>> ls[3]
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    IndexError: list index out of range
    当索引超出了范围时，Python会报IndexError错误，所以要确保索引不要越界，最后一个元素的索引是len(ls) - 1

   
|      序列通用函数或方法      |                    描述                     |
|-----------------------------|--------------------------------------------|
| len(s)                      | 返回序列s的长度，即元素个数                   |
| min(s)                      | 返回序列s的最小元素，s中元素需要可比较         |
| max(s)                      | 返回序列s的最大元素，s中元素需要可比较         |
| sum(iterable[,start=0])     | 对可迭代对象求和，如果start不为0，则加上strat  |
| sorted()                    | 对可迭代对象排序                             |
| reversed()                  | 对序列进行翻转                               |
| enumerate()                 | 返回序列索引和值的元祖                        |
| zip()                       | 两个参数，返回两个序列组成的元祖               |
| list()                      | 把一个可迭代对象变成一个列表                   |
| tuple()                     | 把一个可迭代对象变成一个元祖                   |
| str()                       | 把对象转化为字符串                            |
| s.index(x) 或 s.index(x,i,j) | 返回序列s从i开始到j位置中第一次出现元素x的位置 |
| ls.count(x)                 | 返回序列s中出现x的总次数                      |
       
    例 2.2.2：
    >>> s = "python123.io"
    >>> max(s)
    'y'
    
    >>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
    >>> list(enumerate(seasons))
    [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
    
    >>> a = [1,2,3]
    >>> b = [4,5,6]
    >>> zipped = zip(a,b)     # 打包为元组的列表
    [(1, 4), (2, 5), (3, 6)]   
    

2.3 元祖类型及操作

    2.3.1 定义
    
    元祖是序列类型的一种扩展
    
    -元祖是一种序列类型，一旦创建就不能被修改
    -使用小括号()或tuple()创建，元素间用逗号,分隔
    -可以使用或不使用小括号，如：
        def func():
            return 1,2
    
    例 2.3.1.1：
    >>> creature = "cat","dog","tiger","human"   
    >>> creature
    ("cat","dog","tiger","human")
    >>> color = (0x001100,"blue",creature)
    >>> color
    (4352,'blue',('cat','dog','tiger','human'))
    这里color可以看成是一个二维数组，类似的还有三维、四维……数组，不过很少用到。
    
    2.3.2 元祖类型操作
    
    元祖继承序列类型的全部通用操作
    
    注意事项1：    
    -元祖因为创建后不能修改，因此没有特殊操作
    -使用或者不使用小括号均可

    例 2.3.2.1：
    >>> creature = "cat","dog","tiger","human"   
    >>> creature[::-1]
    ("human","tiger","dog","cat")
    >>> color = (0x001100,"blue",creature)
    >>> color[-1][2]
    'tiger'  
    
    注意事项2：
    要定义一个只有1个元素的tuple，如果这么定义：
    >>> t = (1)
    >>> t
    1
    定义的不是tuple，是1这个数！
    因为括号()既可以表示tuple，又可以表示数学公式中的小括号。Python规定，该情况下，按数学公式小括号进行计算，结果是1。
    因此，只有1个元素的tuple定义时必须加一个逗号,：
    >>> t = (1,)
    >>> t
    (1,)
    Python在显示只有1个元素的tuple时，也会加一个逗号,以免被误解成数学计算意义上的括号。
    
    
    一个“可变的”tuple:
    
    >>> t = ('a', 'b', ['A', 'B'])
    >>> t[2][0] = 'X'
    >>> t[2][1] = 'Y'
    >>> t
    ('a', 'b', ['X', 'Y'])
    
    这个tuple定义的时候有3个元素，分别是'a'，'b'和一个list。
    表面上看，tuple的元素变了，但其实没变。tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向'a'，就不能改成指向'b'，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！
    因此，要创建一个内容也不变的tuple，就必须保证tuple的每一个元素本身也不能变。


2.4 列表类型及操作

    列表是序列类型的一种扩展，十分常用
    
    -列表是一种序列类型，创建后可以随意被修改
    -使用方括号[] 或 list()创建，元素之间用逗号，分隔
    -列表中各元素类型可以不同，无长度限制
    
    例 2.4.1：
    >>> ls = ["cat","dog","tiger",1024]
    >>> ls
    ["cat","dog","tiger",1024]
    >>> lt = ls
    >>> lt
    ["cat","dog","tiger",1024]
    注意： 这里ls和lt都指向了["cat","dog","tiger",1024]，这是个赋值的过程，并没有创建新的list
          方括号[]真正创建一个列表，而赋值仅传递引用
    
|  列表操作符     |              描述                  |
|----------------|------------------------------------|
| ls[i] = x      | 替换列表ls第i元素为x                 |
| ls[i:j:k] = lt | 用列表lt替换ls切片后对应元素子列表    |
| del ls[i]      | 删除列表ls第i元素                    |
| del ls[i:j:k]  | 删除列表ls中第i到第j以k为步长的元素    |
| ls + = lt      | 更新列表ls，将列表lt元素增加到列表ls中 |
| ls * = n       | 更新列表ls，其元素重复n次             |
    
    例 2.4.2：
    >>> ls = ["cat","dog","tiger",1024]
    >>> ls[1:2] = [1,2,3,4]
    ['cat',1,2,3,4,'tiger',1024]
    >>> del ls[::3]
    [1,2,4,'tiger']
    >>> ls *2
    [1,2,4,'tiger',1,2,4,'tiger']
    
    
|  列表函数  |                 描述             |
|-----------|-----------------------------------|
| len(list) | 返回序列s的长度，即元素个数         |
| min(list) | 返回序列s的最小值，s中元素需要可比较 |
| max(list) | 返回序列s的最大值，s中元素需要可比较 |
| list(seq) | 将元组转换为列表                   |
    
    例 2.2.2：
    >>> ls = ["python" ,123,".io"]
    >>> len(s)
    3
    >>> s = "python123.io"
    >>> max(s)
    'y'       
    
|            列表方法              |                           描述                            |
|---------------------------------|----------------------------------------------------------|
| l.append(obj)                   | 在列表末尾添加新的对象                                      |
| l.count(obj)                    | 统计某个元素在列表中出现的次数                               |
| l.extend(seq)                   | 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）|
| l.index(x)或l.index(x,i,j)      | 返回序列s从i开始到j位置中第一次出现元素x的位置                 |
| l.insert(index, obj)            | 将对象插入列表                                             |
| l.pop([index=-1])               | 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值     |
| l.remove(obj)                   | 移除列表中某个值的第一个匹配项                               |
| l.reverse()                     | 反向列表中元素                                             |
| l.sort(key=None, reverse=False) | 对原列表进行排序                                           |
| l.clear()                       | 清空列表                                                  |
| l.copy()                        | 复制列表                                                  |
       
    例 2.2.3：
    #count
    >> aList = [123, 'april', 'duoduo', 'crystal', 123]
    >> aList.count(123)
    2    
       
    #extend
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list1.extend([0,1,2,3,4]) 
    >> list1
    ['april', 'duoduo', 'crystal', 0, 1, 2, 3, 4]
    
    #index
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list1.index('duoduo')
    1
    
    #insert
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list1.insert(1, 'pengpeng')
    >> list1
    ['april', 'pengpeng','duoduo', 'crystal']
    
    #remove
    >> list1 = ['april','pengpeng', 'duoduo', 'crystal']
    >> list1.remove('april')
    >> list1
    ['pengpeng', 'duoduo', 'crystal']
    
    #pop
    >> list1 = ['april','pengpeng', 'duoduo', 'crystal']
    >> list1.pop()
    >> list1
    ['april','pengpeng', 'duoduo']
    
    #reverse
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list1.reverse()
    >> list1
    ['crystal', 'duoduo', 'april']    
    
    #sort
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list1.sort()
    >> list1
    ['april', 'crystal', 'duoduo']
    
    #clear
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list1.clear()
    >> list1
    []
    
    #copy
    >> list1 = ['april', 'duoduo', 'crystal']
    >> list2 = list1.copy()
    >> list2
    ['april', 'duoduo', 'crystal']    
    
2.5 序列类型应用场景

    数据表示： 
    -元祖用于元素不改变的应用场景，更多用于固定搭配场景
    -列表更加灵活，更为常见
    -最主要作用：表示一组有序数据，进而操作
    
    元素遍历：
    for item in ls:         for item in tp:
        <语句块>                 <语句块>
    
    数据保护：
    -如果不希望数据被程序改变，转换成元祖类型
    >>> lt = tuple(ls)

3 字典

3.1 字典类型定义

    映射：是一种键（索引）和值（数据）的对应
    
    例 3.1.1
                红色
    内部颜色                                  内部颜色：蓝色
                黑色       --------->   
    外部颜色                                  外部颜色：红色
                蓝色
    
    例 3.1.2：
    "streetAddr" : "中关村南大街5号"
    "city"       : "北京市"
    "zipcode"    : "100081"
    
    区别于序列类型（列表、元祖）：       
    ["python",123,".io"]
        |      |     |         ------>       内部颜色：蓝色
        0      1     2                       外部颜色：红色
    序列类型由0...N整数作为数据的默认索引        映射类型则由用户为数据定义索引
    
    
    字典类型是“映射”的体现
    
    -键值对：键是数据索引的扩展
    -字典是键值对的集合，键值对之间无序
    -采用大括号{}和dict()创建，键值对用冒号:表示   （回顾set，用{}表示，但是不能用{}创建空集合）
    {<键1>:<值1>,<键2>:<值2>,...,<键n>:<值n>}  
    
    
    在字典变量中，通过键获得值
    
    <字典变量> = {<键1>:<值1>,<键2>:<值2>,...,<键n>:<值n>}     
    <值> = <字典变量>[<键>]     <字典变量>[<键>] = <值>    
    []用来向字典变量中索引或者增加元素  （d[key]方法既可以索引，也可以赋值，增改）
    
    例 3.1.2
    >>> d = {"中国":"北京","美国":"华盛顿","法国":"巴黎"}
    >>> d
    {'中国':'北京','美国':'华盛顿','法国':'巴黎'}
    >>> d["中国"]
    '北京'
    >>> d["英国"] = "伦敦"
    >>> d["英国"]
    '伦敦'    
    把数据放入dict的方法，除了初始化时指定外，还可以通过key放入
    
    >>> d['美国'] = '纽约'
    >>> d['美国']
    '纽约'
    一个key只能对应一个value，多次对一个key放入value，后面的值会把前面的值覆盖掉，这也是修改值的方法：
    
    >>> d['土耳其']
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    KeyError: '土耳其'
    如果key不存在，dict就会报错
    判断key是否存在，可以用 '土耳其' in d的方法，或是 d.gets()，后面会提到
    
    >>> de = {};type(de)
    <class 'dict'>    
    type(x)
    返回变量x的类型 
    
    注意事项：
    dict的key必须是不可变对象！
    因为dict根据key来计算value的存储位置，如果每次计算相同的key得出的结果不同，那dict内部就完全混乱了。这个通过key计算位置的算法称为哈希算法（Hash）。
    要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key：

    >>> key = [1, 2, 3]
    >>> d[key] = 'a list'
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: unhashable type: 'list'   
    
    
3.2 字典处理函数及方法

|    字典函数     |                    描述                    |
|----------------|-------------------------------------------|
| len(d)         | 返回字典d中元素的个数                        |
| str(dict)      | 输出字典，以可打印的字符串表示                |
| type(variable) | 返回输入的变量类型，如果变量是字典就返回字典类型 |
| del d[k]       | 删除字典d中键k对应的数据值                    |

    
    例 3.2.1
    # len(d)
    >>> dict1 = {'Name': 'april', 'Age': 18, 'Class': 'First'}
    >>> len(dict1)
    3
    
    # str(d)
    >>> dict1 = {'Name': 'april', 'Age': 18, 'Class': 'First'}
    >>> str(dict1)
    "{'Name': 'april', 'Class': 'First', 'Age': 18}"
    
    # type(d)
    >>> dict1 = {'Name': 'april', 'Age': 18, 'Class': 'First'}
    >>> type(dict1)
    <class 'dict'>  
    
    # del d[k] , del d
    >>> dict1 = {'Name': 'april', 'Age': 18, 'Class': 'First'}
    >>> del dict1['Class']
    >>> dict1
    {'Name': 'april', 'Age': 18}
    >>> del dict1
    >>> dict1
    NameError                                 Traceback (most recent call last)
    <ipython-input-138-e36219336d90> in <module>
    ----> 1 dict1
    NameError: name 'dict1' is not defined

    
|            字典方法             |                             描述                                |
|--------------------------------|----------------------------------------------------------------|
| d.clear()                      | 删除字典内所有元素                                                |
| d.copy()                       | 返回一个字典的浅复制                                              |    
| d.fromkeys()                   | 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值   |
| d.get(key,default=None)        | 返回指定键的值，如果值不在字典中返回default值                        |
| k in d                         | 如果键在字典dict里返回true，否则返回false                           |
| d.items()                      | 以列表返回可遍历的(键, 值) 元组数组                                 |
| d.keys()                       | 返回一个迭代器，可以使用 list() 来转换为列表                         |
| d.setdefault(key,default=None) | 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default       |
| d.update(dict2)                | 把字典dict2的键/值对更新到dict里                                   |
| d.values()                     | 返回一个迭代器，可以使用 list() 来转换为列表                         |
| d.pop(key,<default>)      |字典给定键key所对应的值，返回值为被删除的值。key值必须给出。否则，返回default值|
| d.popitem()                    | 随机返回并删除字典中的一对键和值(一般删除末尾对)                      |
  
    
    例 3.2.2
    
    # d.clear()
    >> dict1 = {'Name': 'april', 'Age': 18}
    >> dict1.clear()
    >> dict1
    {}
    
    # d.copy() 浅复制（区别于直接赋值，以及copy模块里的深拷贝deepcopy）
    >> dict1 = {'Name': 'april', 'Age': 18, 'Class': 'First'}
    >> dict2 = dict1.copy()
    >> dict2
    {'Age': 7, 'Name': 'Runoob', 'Class': 'First'}    
   
    直接赋值、浅拷贝和深度拷贝区别
    >> import copy
    >> a = {'Name': 'april', 'Age': 18, 'location': ['beijing','jingzhou']}  #原始对象
       b = a                        #赋值，传对象的引用
       c = dict1.copy(a)            #对象拷贝，浅拷贝
       d = copy.deepcopy(a)         #对象拷贝，深拷贝
       
    >> a['condidant']='duoduo'      #修改对象a，添加元素
       a['Age']=20    
       a['location'].remove('jingzhou')  #修改对象a中的['beijing','jingzhou']数组对象  
            
    >> print(a,b,c,d )
    ({'Name': 'april', 'Age': 20, 'location': ['beijing'], 'condidant': 'duoduo'},
     {'Name': 'april', 'Age': 20, 'location': ['beijing'], 'condidant': 'duoduo'},
     {'Name': 'april', 'Age': 18, 'location': ['beijing']},
     {'Name': 'april', 'Age': 18, 'location': ['beijing', 'jingzhou']})
     
    b 其实是 a 的引用（别名），所以输出结果都是一致的
    c 父对象进行了深拷贝，不会随 a 修改而修改，‘Age’ 的值不变，子对象['beijing','jingzhou']是浅拷贝所以随 a 的修改而修改
    d 完全拷贝了 a 的父对象及其子对象，两者是完全独立的，所以不随 a 的修改而修改
     
    详细讨论见：https://www.runoob.com/w3cnote/python-understanding-dict-copy-shallow-or-deep.html 

    # d.fromkeys()  创建一个新字典，以序列 seq 中元素做字典的键，value 为字典所有键对应的初始值
    >> seq = ('name', 'age', 'sex')    
    
    >> dict2 = dict1.fromkeys(seq)
    >> dict2
    {'name': None, 'age': None, 'sex': None}
    
    >> dict3 = dict1.fromkeys(seq,10)
    >> dict3
    {'name': 10, 'age': 10, 'sex': 10}    
    
    # d.get(key,default=None)  函数返回指定键的值，如果值不在字典中返回默认值 
    >>> d = {"name":"april","age":18,"location":"beijing"}
    >>> d.get("name","condidant") 
    'april'
    >>> d.get("condidant","duoduo")
    'duoduo'
    
    # key in dict    
    >>> d = {"name":"april","age":18,"location":"beijing"}
    >>> "name" in d
    True
    
    # d.items()  以列表返回可遍历的(键, 值) 元组数组
    >>> d = {"name":"april","age":18,"location":"beijing"}
    >>> d.items()
    dict_items([('name', 'april'), ('age', 18), ('location', 'beijing')])
    
    # d.keys()   返回一个可迭代对象，可以使用 list() 来转换为列表 
    >>> d = {"name":"april","age":18,"location":"beijing"}
    >>> d.keys()
    dict_keys(['name', 'age', 'location'])
    
    # d.setdefault(key, default=None)  和 get()类似, 如果键不已经存在于字典中，将添加键并将值设为默认值
    >> d = {"name":"april","age":18}
    >> d.setdefault('age',None)
    >> d.setdefault('location',None)
    >> d
    {'name': 'april', 'age': 18, 'location': None}
    
    # d.update(dict2)   把字典参数 dict2 的 key/value(键/值) 对更新到字典 dict 里
    >> dict1 = {'Name': 'name', 'Age': 18}
    >> dict2 = {'Sex': 'female' }
    >> dict1.update(dict2)
    >> dict1
    {'Name': 'name', 'Age': 18, 'Sex': 'female'}
    
    # d.values()  返回一个迭代器，可以使用 list() 来转换为列表，列表为字典中的所有值
    >>> d = {"name":"april","age":18,"location":"beijing"}
    >>> d.values()
    dict_values(['april', 18, 'beijing'])    
    
    # pop(key[,default])  删除给定键 key 对应的值，返回值为被删除的值。key值必须给出。否则，返回default值
    >> d = {"name":"april","age":18,"location":"beijing"}
    >> a=d.pop('location')
    >> print(d,a)
    {'name': 'april', 'age': 18},
    'beijing'
    
    # popitem()  随机返回并删除字典中的一对键和值(一般删除末尾对)
    >> d = {"name":"april","age":18,"location":"beijing"}
    >> a = d.popitem()
    >> print(d,a)
    {'name': 'april', 'age': 18}, ('location', 'beijing')
    
3.3 字典类型应用场景
    
    映射的表达：
    -映射无处不在，键值对无处不在
    -例如：统计数据出现的次数，数据是键，次数是值
    -最主要作用：表达键值对数据，进而操作

    元素遍历：
    for k in d :
        <语句块>
        
    快速查找：
    -字典相较于列表，查找和插入速度更快
    -dict的实现原理和查字典是一样的。假设字典包含了1万个汉字，我们要查某一个字，一个办法是把字典从第一页往后翻，直到找到我们想要的字为止，这种方法就是在list中查找元素的方法，list越大，查找越慢。
    -第二种方法是先在字典的索引表里（比如部首表）查这个字对应的页码，然后直接翻到该页，找到这个字。无论找哪个字，这种查找速度都非常快，不会随着字典大小的增加而变慢。
    （但是，相对于list，dict也更占用内存，所以dict是用空间来换取时间的一种方法）
    

4 补充：
    不可变对象str
    
    3.1字典的定义注意事项里，我们提到了，str是不变对象，而list是可变对象。

    对于可变对象，比如list，对list进行操作，list内部的内容是会变化的，比如：

    >>> a = ['c', 'b', 'a']
    >>> a.sort()
    >>> a
    ['a', 'b', 'c']

    而对于不可变对象，比如str，对str进行操作呢：

    >>> a = 'abc'
    >>> a.replace('a', 'A')
    'Abc'
    >>> a
    'abc'

    虽然字符串有个replace()方法，也确实变出了'Abc'，但变量a最后仍是'abc'，应该怎么理解呢？

    我们先把代码改成下面这样：

    >>> a = 'abc'
    >>> b = a.replace('a', 'A')
    >>> b
    'Abc'
    >>> a
    'abc'

    要始终牢记的是，a是变量，而'abc'才是字符串对象！有些时候，我们经常说，对象a的内容是'abc'，但其实是指，a本身是一个变量，它指向的对象的内容才是'abc'：

    ┌───┐                  ┌───────┐
    │ a │─────────────────>│ 'abc' │
    └───┘                  └───────┘

    当我们调用a.replace('a', 'A')时，实际上调用方法replace是作用在字符串对象'abc'上的，而这个方法虽然名字叫replace，但却没有改变字符串'abc'的内容。相反，replace方法创建了一个新字符串'Abc'并返回，如果我们用变量b指向该新字符串，就容易理解了，变量a仍指向原有的字符串'abc'，但变量b却指向新字符串'Abc'了：

    ┌───┐                  ┌───────┐
    │ a │─────────────────>│ 'abc' │
    └───┘                  └───────┘
    ┌───┐                  ┌───────┐
    │ b │─────────────────>│ 'Abc' │
    └───┘                  └───────┘

    所以，对于不变对象来说，调用对象自身的任意方法，也不会改变该对象自身的内容。相反，这些方法会创建新的对象并返回，这样，就保证了不可变对象本身永远是不可变的。


附录：

https://www.icourse163.org/learn/BIT-268001?tid=1206073223#/learn/content?type=detail&id=1210530417&cid=1212669817
北京理工大学 嵩天 python语言程序设计

https://www.liaoxuefeng.com/wiki/1016959663602400/1017104324028448 廖雪峰python教程

https://www.runoob.com/python3/python3-dictionary.html

