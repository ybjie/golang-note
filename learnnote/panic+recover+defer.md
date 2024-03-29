# panic
某个函数中的某行代码有意或无意地引发了一个 panic。这时，初始的 panic 详情会被建立起来，并且该程序的控制权会立即从此行代码转移至调用其所属函数的那行代码上，也就是调用栈中的上一级。
这也意味着，此行代码所属函数的执行随即终止。紧接着，控制权并不会在此有片刻的停留，它又会立即转移至再上一级的调用代码处。控制权如此一级一级地沿着调用栈的反方向传播至顶端，也就是我们编写的最外层函数那里。
这里的最外层函数指的是go函数，对于主 goroutine 来说就是main函数。但是控制权也不会停留在那里，而是被 Go 语言运行时系统收回。

# defer
defer语句就是被用来延迟执行代码的。延迟到什么时候呢？这要延迟到该语句所在的函数即将执行结束的那一刻，无论结束执行的原因是什么。
这与go语句有些类似，一个defer语句总是由一个defer关键字和一个调用表达式组成。
这里存在一些限制，有一些调用表达式是不能出现在这里的，包括：针对 Go 语言内建函数的调用表达式，以及针对unsafe包中的函数的调用表达式。
注意，被延迟执行的是defer函数，而不是defer语句。
至此，我向你展示了两个很典型的recover函数的错误用法，以及一个基本的正确用法。

# defer语句的执行原理
在defer语句每次执行的时候，Go 语言会把它携带的defer函数及其参数值另行存储到一个队列中。
这个队列与该defer语句所属的函数是对应的，并且，它是先进后出（FILO）的，相当于一个栈。

# defer
在同一个函数中，defer函数调用的执行顺序与它们分别所属的defer语句的出现顺序（更严谨地说，是执行顺序）完全相反。
它在被调用时会返回一个空接口类型的结果值。如果在调用它时并没有 panic 发生，那么这个结果值就会是nil。
如果被恢复的 panic 是我们通过调用panic函数引发的，那么它返回的结果值就会是我们传给panic函数参数值的副本。
