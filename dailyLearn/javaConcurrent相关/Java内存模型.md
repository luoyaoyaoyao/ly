# Java内存模型

info:

1. 线程同步

2. 线程通信 -> 发送消息，共享内存

* 共享内存：全局变量 

* 发送消息：PipedInputStream, PipedOutputStream eg. ls | grep java <进程间通信>

3. 重排序

```java
public class ResortValue {
    boolean flag = false;
    int value = 0;
    public class Writer implements Runnable {
        @Override
        public void run() {
            flag = true;
            value =2;
        }
    }

    public class Reader implements Runnable {
        @Override
        public void run() {
            if (flag) {
                System.out.println(value * value);
            }
        }
    }
}
```

4. happens before

前一个操作的结果对于后一个操作是可见的

5. 数据竞争与顺序一致性

