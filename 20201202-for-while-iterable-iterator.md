# for & while, iterable & iterator

### for & while

    for 循环的内在运行机制其实是while 循环的改写
    
    for variable... in expression:
        statement
        ...   
        
    == transform to ==>
    
    iterable = expression
    iterator = iter(iterable)
    try:
        while True:
            variable... = next(iterator)
            statement
            ...
    except StopIteration:
        pass
        
    上面for loop 的内部运行，实际上是下面的一整套 while 循环
    
    当 for in 语句，收到一个 表达式 expression 之后
    首先，对这个表达式用 iter() 函数，将该表达式，转换成 iterator
    然后再放到 while 循环下
    通过 next() 获取 variable
    一直到 iterator 取完，抛出 StopIteration
    用 try...except...语句接住
    
    那么有的同学可能会问了，如果 expression 本身就是 iterator 怎么办
    for 循环还会对其进行 iter()吗， iter(iterator) 会得到什么
    带着这个疑问，我们来看 2 个例子
    eg.1
    >>>next([1])  # [1] 是 list，list 是 iterable 
    TypeError: 'list' object is not an iterator  # 这句说明，next() 只能对 iterator 用，不能对 iterable 用
    eg.2
    for x in sorted(xs):
        statement
    把上面的 for 循环转换成 while 循环：
    i = iter(sorted(xs))   # 这里的 for 循环时没有 iter()的，转换成 while 里面就有一个 iter()
    try:
        while True:
            next(i)
    except StopIteration:
        pass
        
    当 expression 本来就有 iter()的时候, for转换还是会加一个 iter
    因为 for 循环不知道 expression 是不是 iterator，不能智能识别
    为了以防万一，都加上一个 iter()
    而 iter(iterator) == iterator
    
    eg.3
    for data in iter(lambda:file.read(1024),b''):
        statement
    转换后：
    iterator = iter(iter(lambda:fire.read(1024),b''))   # 被套了2个 iter()   
    
    
### iterable & iterator

    1.为什么 iter(iterator) == iterator 
    
    我们来看这2个例子：
    map(str,[1,2,3])， 返回一个 iterator
    sorted([1,2,3])， 返回一个 list
        
    for 要支持
    for x in sorted([1,2,3]):
        statement
    for 要调用 iter(sorted[1,2,3]) 来获得一个 iterator，然后 next()
    如果没有这个 iter，sorted([1,2,3]) 得到的 list 是没有办法用 next()的       
        
    而 for 又要支持
    for x in map(str,[1,2,3]):
        statement
    但是 for 没有那么智能，会根据 in 后面的结果来调整，它只能死板的调用 iter()
    所以上面的代码，也会经历 iter(map(str,[1,2,3])) 来获得一个 iterator，然后 next()
    因此这就要求 iter(iterator) 的结果依旧是 iterator
    而 for 只需要无脑的加 iter() 就可以了
    
    iter(iterable) -> iterator
    iter(iterator) -> iterator
    
    iterator 同时也是 iterable，因为把它传递给 iter()可以得到一个 iterator
    
    2.iterator 跟 iterable 的区别是什么
    
    为什么 next([1,2,3]) 不行，必须要 next(iter([1,2,3])) 先把list 边成 iterator 才行
    为什么 iterable 没有 __next__
    
    我们来看一个例子
    xs = [1,2,3]
    a = iter(xs)
    b = iter(xs)  # a 和 b 的位置是独立的
    next(a)
    next(b)
    next(b)
    next(a)
    
    如果让 list 直接成为 iterator，就没法有这么一个”趟“的概念
    iter(iterable) -> iterator， 这个 iterator 就可以逛一圈
    也只能逛一圈，逛到底了就 StopIteration，next 就一直抛异常
    
    如果 next 可以直接作用在 iterable 上，比如 list，那是不是也只能逛一圈？
    ys = sorted(xs)
    for y in ys:
        print(y)
    n = 0
    for y in ys:
        n += y
        
    sorted 返回 list，然后正常的 python里逛了两圈，一圈打印，一圈求和
    这是通过 iterator 这个概念来完成的， 一个 iterator 就是一圈
    如果是 iterable， 或者让 list 本身就是 iterator，该怎么逛 2 圈
    第二圈是不是就没了，n 的结果是初始值 0 
    
    我们再看 zip
    >>>list(zip([1,2],'ab'))
    [(1,'a'),(2,'b')]
    zip 需要同时看 2个 iterator，第一个用 next 取一下，第二个用next取一下，然后产生一个 tuple
    然后再来，交替的 next两个甚至多个 iterator
    
    xs = [1,2]
    ys = list(zip(xs,xs))
    zip 会交替的取，但是这又是同一个 xs
    如果让 list 自己可以 next 的话，那 zip 就会交替从一个 list 里取，那结果就一样了
    而真正的 python里，zip 会悄悄的对参数们都调用 iter
    来获得他们各自的独立一圈，不是这个参数的一圈完了之后，再下一个参数的一圈，而是让他们都交叉起来
    >>>xs = [1,2]
    >>>ys = list(zip(xs,xs))
    >>>ys
    [(1,1),(2,2)]
    
    >>>help(zip)
    zip(*iterables) --> a zip object yielding tuples until an input is exhausted.
    就是说，zip 会悄悄的对 iterable 调用 iter，然后交叉的 next 它们
    
    总结
    1.为什么要区分 iterable 和 iterator？
    因为 iterator 只能取一圈，取完了就 StopIteration 了
    而 iterable 可以取很多圈，每取一次，通过 iter() ，转变成独立的 iterator，通过 next(iterator) 来取出具体的数
    因此 next() 也不能直接用于 list，tuple 这些 iterable上面
    否则是取一圈之后抛 StopIteration，还是接着从头开始取，但是这样子就无法区分头尾，都不对
    
    2.这个区分使得 for 要加 iter()
    
    3.for 无脑加的这个 iter，使得 iter(iterator) 也是 iterator，同时 iterator 也是 iterable的
    
    
    
