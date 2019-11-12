# volatile & synchronized

## background

java -> (编译器) -> 字节码 -> (类加载器) -> 加载到jvm里 -> (执行引擎) -> 转变成汇编指令在CPU上执行。  
Java种使用的并发机制依赖于jvm的实现和cpu指令。

## volatile保证“可见性”

* 数据可见性

在不使用volatile

```java
package com.ly.concurrency.demo;

public class VolatileTest {
    private static volatile int MY_INT = 0;
    public static void main(String[] args) {
        new ChangeListener().start();
        new ChangeMaker().start();
    }

    static class ChangeListener extends Thread {
        @Override
        public void run() {
            int local_value = MY_INT;
            while (local_value < 5) {
                if (local_value != MY_INT) {
                    System.out.println("Got Change for MY_INT :" + MY_INT);
                    local_value = MY_INT;
                }
            }
        }
    }

    static class ChangeMaker extends Thread {
        @Override
        public void run() {

            int local_value = MY_INT;
            while (MY_INT < 5) {
                System.out.println("Incrementing MY_INT to " + (local_value + 1));
                MY_INT = ++local_value;
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```