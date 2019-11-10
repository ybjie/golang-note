# 用户级线程
- go的运行时系统会自动创建和销毁系统级线程
- 用户级线程是架设在系统级线程之上的，完全由我们控制
- G(goroutine)、P(processor)、M(machine),经过P的连接，G和M是多对多的关系
- 与一个进程总有一个主线程类似，任何一个独立的go程序在运行的时候都有一个主goroutine
- 主goroutine的go函数就是那个做为程序入口的main函数

# go函数的执行
- 一定一直注意，go函数真正被执行的时间一定与其所属的go语句的执行时间是不同的，是明显滞后的
- 也与goroutine的创建顺序没有关系，都会被放到processor队列中，但是队列本身也可能有多个，不过单个队列是先进先出的顺序进行的

# 自旋
# time包、async包、runtime.GOMAXPROCS 
