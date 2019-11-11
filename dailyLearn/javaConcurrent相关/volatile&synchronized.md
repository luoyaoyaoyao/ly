# volatile & synchronized

## background

java -> (编译器) -> 字节码 -> (类加载器) -> 加载到jvm里 -> (执行引擎) -> 转变成汇编指令在CPU上执行。  
Java种使用的并发机制依赖于jvm的实现和cpu指令。

## volatile保证“可见性”

* 数据可见性

在不使用volatile

```java
public class VolatileDemo {
    static int i = 0;
    static int j;
    public static class ThreadOne implements Runnable {
        @Override
        public void run() {
            i = 10;
        }
    }

    public static class ThreadTwo implements Runnable {
        @Override
        public void run() {
            Thread.sleep(100);
            j = i;
        }
    }

    public static void main(String args[]) {
        Thread threadOne = new Thread(new ThreadOne());
        Thread threadTwo = new Thread(new ThreadTwo());
        threadOne.start();
        //Thread.sleep(500);
        threadTwo.start();
        System.out.println(i);
        SYstem.out.println(j);
    }
}
```