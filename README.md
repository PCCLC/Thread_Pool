# Thread_Pool 基于可变参模板的线程池
## 1. 线程过多带来的消耗：

-   线程的创建和销毁都是非常"重"的操作
-   线程栈本身占用大量内存
-   线程的上下文切换要占用大量时间
-   大量线程同时唤醒会使系统经常出现锯齿状负载或者瞬间负载量很大导致宕机

## 2. **线程池的优势**：

操作系统上创建线程和销毁线程都是很"重"的操作，耗时耗性能都比较多，那么在服务执行的过程中，如果业务量比较大，实时的去创建线程、执行业务、业务完成后销毁线程，那么会导致系统的实时性能降低，业务的处理能力也会降低。

线程池的优势就是（每个池都有自己的优势），在服务进程启动之初，就事先创建好线程池里面的线程，当业务流量到来时需要分配线程，直接从线程池中获取一个空闲线程执行task任务即可，task执行完成后，也不用释放线程，而是把线程归还到线程池中继续给后续的task提供服务。

## **3. fixed**模式线程池

线程池里面的线程个数是固定不变的，一般是ThreadPool创建时根据当前机器的CPU核心数量进行指定。

## 4. **cached模式线程池**

线程池里面的线程个数是可动态增长的，根据任务的数量动态的增加线程的数量，但是会设置一个线程数量的阈值（线程过多的坏处上面已经讲过了），任务处理完成，如果动态增长的线程空闲了60s还没有处理其它任务，那么关闭线程，保持池中最初数量的线程即可。

## 5. **项目描述：**

-   基于可变参模板编程和引用折叠原理，实现线程池submitTask接口，支持任意任务函数和任意参数的传递
-   使用future类型定制submitTask提交任务的返回值
-   使用map和queue容器管理线程对象和任务
-   基于条件变量condition_variable和互斥锁mutex实现任务提交线程和任务执行线程间的通信机制
-   支持fifixed和cached模式的线程池定制
-   **平台工具**：vs2019开发，ubuntu cmake编译so库，gdb调试分析定位死锁问题
