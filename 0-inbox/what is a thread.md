---
created: 2024-07-31T11:24
updated: 2024-07-31T11:52
---
A **thread** in computing is the smallest unit of execution within a process. It is a sequence of instructions that can be executed independently of other threads within the same process. Every Java application has at least one thread, known as the **main thread** which is created automatically by the Java Virtual Machine (JVM) when the program starts. 

**Threading** refers to the concept of running multiple threads at the same time within a program. 

Programs can be *single-thread* or *multi-thread*. JavaScript is a single-thread programming language. Everything happens on the same thread. 
[[Benefits of threading]]

##### Example: Creating a Simple Thread

Here’s how you might create and start a thread in Java by implementing `Runnable`:
```java
class MyTask implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Running in MyTask thread: " + i);
        }
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyTask task = new MyTask();
        Thread thread = new Thread(task); // Creating a new thread with MyTask
        thread.start(); // Starting the thread

        // Main thread continues to run concurrently
        for (int i = 0; i < 5; i++) {
            System.out.println("Running in the main thread: " + i);
        }
    }
}
// returns any combination of the following with main 0 always first
/* Running in the main thread: 0
Running in the main thread: 1
Running in the main thread: 2
Running in MyTask thread: 0
Running in the main thread: 3
Running in the main thread: 4
Running in MyTask thread: 1
Running in MyTask thread: 2
Running in MyTask thread: 3
Running in MyTask thread: 4 */
```

