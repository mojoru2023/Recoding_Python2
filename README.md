# Recoding_Python2


2020.2.26 

python协程的逻辑



对比生成器版的协程，使用asyncio库后变化很大：

没有了yield 或 yield from，而是async/await
没有了自造的loop()，取而代之的是asyncio.get_event_loop()
无需自己在socket上做异步操作，不用显式地注册和注销事件，aiohttp库已经代劳
没有了显式的** Future** 和** Task，asyncio**已封装
更少量的代码，更优雅的设计

协程的逻辑:
定义协程---创建loop---创建task(asyncio.create_task将协程打包成task)-task接入loop---用await(挂起当前任务,切换用的,类似生成器里yield切换函数的作用) 等待task



使用async可以定义协程,协程用于耗时的IO操作,也可以封装更多的IO操作过程,在一个协程中await另外一个协程实现洗成的其那套

可等待对象:如果一个对象可以在await语句中使用,那么它就是可等待对象呢
许多asyncio API都被设计为接收可等待对象


可等待对象有三种类型:协程,任务和Future

协程:python中的协程属于可等待对象,所有可以在其他协程中被等待
任务是用来设置日程以便并发执行协程

当一个协程通过asyncio.create_task()等函数被打包成一个任务,该协程
将自动排入日程准备立即执行


尝试使用协程写一个爬虫(协程还是函数维度的编程)

以后就多玩协程,线程.协程更好,值切换上下文;线程还要缓存,会有性能消耗


io密集用协程
CPU密集用多进程