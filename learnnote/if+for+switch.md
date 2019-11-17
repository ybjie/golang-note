# if
- 被range的迭代对象是副本
- 当只有一个接收值的时候智能接收到索引而非元素本身

# for、switch
- case的书写顺序很重要，一旦一个case被选中，其余的都会被忽略
- switch和case的结果是要用来做判等操作的，因此必须类型相同
- case是可以有多个表达式的，之间用逗号分隔
- 只要switch表达式的结果值与某个case表达式中的任意一个子表达式的结果值相等，该case表达式所属的case子句就会被选中
- 不允许多个case的表达式中存在相等的情况，当然这个限制只针对于值为常量的子表达式