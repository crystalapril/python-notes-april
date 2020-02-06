# Object & Class

- 对象概述 outline of object
- 类，对象和实例 class, object & instance
- 类的属性和方法 attribute & method 
- 自定义类
- 类的封装及私有化 encapsulation
- 类的多态 polymorphism
- 类的继承 inheritance
- 类的魔方方法

### 对象概述 outline of object

    一切皆对象 everything is object
    
    python有句话叫一切皆对象
    什么意思呢，就是你之前学过的，接触过的，都是对象
    
    举个栗子，第一篇里的整数 int 是 object，字符串 string 也是 object，同样 list 也是object 
    包括前天提到的，open 函数打开文档，返回的也是 file object
    
    那么，什么是对象？
    对象是python 里面一切事物的 基类（即基本类别）
    
    是不是到了这里，还是很困惑，一切都是对象，这有概念什么意义呢，我们接着往下看。
    

### 类，对象和实例 class, object & instance

    上面提到了，object 是python里面的最基础的类别
    
    那除了基类还有别的类别吗，当然有
    
    我们把 很相似（相似的属性、方法）的object 归为一类 （class）
    
    比如说，
    字符串 strings是一类，而 具体的'abc'是 str 类的 实例（instance）
    integer 整数是一类，具体的 123 是 int 类的 instance       
    
    这里有点类似生物界的分类
    我们人类是一个类别，每个具体的人呢，april是 Human 类中的 instance
    (python3里，class和type几乎同义，python2有所不同，这个不用深究)        
    

### 类的属性和方法 attribute & method 

    上面提到了我们把具有相似属性和方法object 归为一类
    
    那么，什么是属性 attribute ，什么是方法 method
     - 属性attribute 就是该对象的一些特有的性质，同一类的实例往往具有相同的属性
     - 方法就是该对象上绑定的函数
       之前我们见到了 len（）函数，strip（）方法，可能很困惑，这两个明明看起来差不多，为什么名称不同
       其实差别就在这里，函数可以单独使用，方法要对象的实例 instance 调用，是绑在实例上的
    
    我们还是以 字符串为例来说明：
    >>> a = '123 '
    >>> a.__class__
    <class 'str'>
    __class__ 字符串这个类的属性之一，告诉你 '123 '属于 str 这个类
    >>> a.strip()
    '123'
    strip() 是字符串可以调用的方法之一，经strip处理后，字符串 '123 '去掉了空格   
        
    我们再对比一下函数
    >>> len(a)
    4
    发现区别没有，方法的调用是 instance.method() ,函数是 function(instance)    
       函数                 方法
      id(a)              a.title() 
      min(a)             a.split()    
    

### 自定义类

    上面我们以字符串'123 '为例，简单的介绍了object的要素
    
    有同学可能不满足于此，如果我们想自己定义一个类，或者改进python原有的类怎么办
    
    这节我们尝试自定义一个简单的类
    
    class Person: #类名需要大写
        def __init__(self,age,name):  # 定义了年龄和姓名属性，__init__后面再说
            self.age = age            
            self.name = name

        def eat(self,times):  # 定义了 eat 方法
            print(f'I have {times} meals a day.')

        def sleep(self,hour):  # 定义了 sleep 方法
            print(f'I sleep for {hour} hours a day.')
            
     从上面可以看到，自定义类：
       - 要用class语句，后面跟类名，这里是Person，类名需首字母大写
       - 类名后面可以加(object),或其他类的(类名),括号里的类名为我们自定义类的父类（父类的概念后面再说）
       - 如果父类是object，也可以省略，如 Person(object) 等同于 Person
       - class 里面可以自定义方法和属性
       - 定义方法与定义函数类似，都是通过 def 语句，区别在于定义方法的第一个参数默认是self，
         self意味着 object 本身，方法也可以被看做成是绑定到 self 上的函数
            
     我们以 Person 为例来建立一个实例：
     
     >>> april = Person(25,'april')   # 建立了一个april的实例instance
     >>> april.age
     25
     >>> april.name
     'april'
     >>> april.eat(3)     # 还可以用 Person.eat(april,3)
     I have 3 meals a day.     
     >>> april.sleep(8)
     I sleep for 8 hours a day. 
     
     这里，april 是 Person 的实例
     april.age 跟 self.age 是不是很相似
     没错，这里的 april 就作为第一个参数 self 自动被传入进去了  
        

### 类的封装及私有化 encapsulation and privacy

    类的一个特点就是封装 encapsulation ，跟函数的封装类似
    
    我们在调用函数的时候，例如 
    >>> pow(2,4)
    16
    我们不需要知道pow函数里面是怎么写的，只需要知道pow可以用来进行幂运算，直接拿过来用就可以了
    
    同样，类也是如此，我们在调用方法时，也不需要知道方法是怎么写的
    >>> '123 '.strip()
    '123'
    >>> april.eat(3)     # 还可以用 Person.eat(april,3)
    I have 3 meals a day.   
    知道怎么用，能实现什么功能就好，这样让程序更简单
    
    
    Privacy
    
    但是有的同学说，这样还不够
    有些方法不希望别人使用，只有自己能用
    python为这种情况，提供了一个选项就是 私有化 privacy
    通过把想要隐藏的方法设为私有的（方法前加2个下划线 __method），让外面无法访问（其实是看起来无法访问）：
    
    我们通过下面的例子来说明：
    
    >>> class Person:
    ...:     def __init__(self,age,name):
    ...:         self.age = age
    ...:         self.name = name
    ...: 
    ...:     def __myweight(self):
    ...:         print("I won't tell you.")
    ...: 
    ...:     def weight(self):
    ...:         print("the weight is ...")
    ...:         self.__myweight()
    ...: 
    >>> april = Person(25,'april')
    >>> april.__myweight()
    Traceback (most recent call last):
      File "<ipython-input-17-b6512bc696d6>", line 1, in <module>
        april.__myweight()
    AttributeError: 'Person' object has no attribute '__myweight'
    >>> april.weight()
    the weight is ...
    I won't tell you.
    
    直接访问__weight 被拒绝，这时候__weight是私有的，程序显示没有这个属性
    通过weight方法进行内部访问，才可以访问到私有的内容
    
    但是事实上，python并不是绝对禁止访问私有的属性
    有一个办法可以让我们从外部访问私有属性：
    >>> april._Person__myweight()
    I won't tell you.
    
    在类名前加单下划线，后面跟着双下划线+私有方法名，就可以进入
    _Classname__privatemehtod
    
    尽管我们可以通过这个办法访问私有属性，但是还是尽量不要去这样做
    私有属性就类似一个提示，告诉大家没事不要去那里搞事情    
    

### 类的多态 polymorphism

### 类的继承 inheritance

### 类的魔方方法