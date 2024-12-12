[前景 · Go语言中文文档](https://www.topgoer.com/)

# 语法
## const以及iota
```go
const (
    a = iota   //0
    b          //1
    c          //2
    d = "ha"   //独立值，iota += 1
    e          //"ha"   iota += 1
    f = 100    //iota +=1
    g          //100  iota +=1
    h = iota*iota   //49,恢复计数
    i          //64
)
const j = iota //0
```



`iota`表示在下一个`const`关键字出现之前，每第一个常量就会值+1；再次出现`const`关键字就会使得`iota`变为0

`const()`这个形式如果没有给他声明表达式，就会继承上一个表达式，例如`i`就是继承了`h`的表达式`iota*iota`所以是64

