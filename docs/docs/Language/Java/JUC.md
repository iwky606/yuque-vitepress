# 线程池
## 线程池的submit
线程池除了execute还有submit方法

```java
// 提交Runnable任务
Future<?> 
submit(Runnable task);
// 提交Callable任务
<T> Future<T> 
submit(Callable<T> task);
// 提交Runnable任务及结果引用  
<T> Future<T> 
submit(Runnable task, T result);
```



这个就解决了execute执行的任务不能join的问题。



# FutureTask类
FutureTask实现了Future接口和Runnable接口

> Runnable使得这个类的对象可以被创建线程任务  
Future接口定义了这个类返回值获取的方式
>

FutureTask的两个构造器

```java
public FutureTask(Callable<V> callable)
public FutureTask(Runnable runnable, V result)
```



实际上，线程池的submit的后两个方法就是通过这两个参数直接创建FutureTask的。



# CompletableFuture类
```java
//使用默认线程池
static CompletableFuture<Void> 
runAsync(Runnable runnable)
static <U> CompletableFuture<U> 
supplyAsync(Supplier<U> supplier)
//可以指定线程池  
static CompletableFuture<Void> 
runAsync(Runnable runnable, Executor executor)
static <U> CompletableFuture<U> 
supplyAsync(Supplier<U> supplier, Executor executor)  
```





# CompletionService如果
```java
// 创建线程池
ExecutorService executor =
Executors.newFixedThreadPool(3);
// 异步向电商S1询价
Future<Integer> f1 = 
executor.submit(
    ()->getPriceByS1());
// 异步向电商S2询价
Future<Integer> f2 = 
executor.submit(
    ()->getPriceByS2());
// 异步向电商S3询价
Future<Integer> f3 = 
executor.submit(
    ()->getPriceByS3());

// 获取电商S1报价并保存
r=f1.get();
executor.execute(()->save(r));

// 获取电商S2报价并保存
r=f2.get();
executor.execute(()->save(r));

// 获取电商S3报价并保存  
r=f3.get();
executor.execute(()->save(r));

```



这里就会有一个问题，三个Future在get的时候，都在主线程上，所以，是串行的，但是，如果f2任务先执行完，但是f1还在get那么就有时间浪费了。可以使用BlockingQueue优化。

推荐使用CompletionService

这里ExecutorCompletionService是CompletionService的实现类

```java
import java.util.concurrent.*;
import java.util.concurrent.atomic.AtomicInteger;

public class Main {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        // 创建线程池
        ExecutorService executor = Executors.newFixedThreadPool(3);
        // 创建CompletionService
        CompletionService<Integer> cs = new ExecutorCompletionService<>(executor,new LinkedBlockingQueue<>());
        // 异步向电商S1询价
        cs.submit(() -> getPriceByS1());
        // 异步向电商S2询价
        cs.submit(() -> getPriceByS2());
        // 异步向电商S3询价
        cs.submit(() -> getPriceByS3());
        // 将询价结果异步保存到数据库
        for (int i = 0; i < 3; i++) {
            Integer r = cs.take().get();
            executor.execute(() -> save(r));
        }
    }

    static int getPriceByS1() {
        return 1;
    }

    static int getPriceByS2() {
        return 2;
    }

    static int getPriceByS3() {
        return 3;
    }

    static void save(int r) {
        System.out.println("saved result:" + r);
    }
}
```

