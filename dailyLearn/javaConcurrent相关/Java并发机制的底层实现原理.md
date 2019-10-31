# Java并发机制的底层实现原理

## 线程安全

* 线程不安全

```java
public class UnsafeSequence implements Runnable {
    private int value;
    public static void main(String[] args) throws InterruptedException {
        UnsafeSequence unsafeSequence = new UnsafeSequence();
        Thread thread1 = new Thread(unsafeSequence);
        Thread thread2 = new Thread(unsafeSequence);
        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();
        System.out.println(unsafeSequence.value);
    }
    public void run() {
        for (int i = 0; i < 100000; i++) {
            this.value++;
        }
    }
}
```

* 线程安全

```java
import java.util.concurrent.atomic.AtomicInteger;

public class SafeSequence  implements Runnable {
    private AtomicInteger value = new AtomicInteger();

    public static void main(String[] args) throws InterruptedException {
        SafeSequence safeSequence = new SafeSequence();
        Thread thread1 = new Thread(safeSequence);
        Thread thread2 = new Thread(safeSequence);
        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();
        System.out.println(safeSequence.value.get());
    }

    public void run() {
        for (int i = 0; i < 100000; i++) {
            this.value.getAndIncrement();
        }
    }
}
```