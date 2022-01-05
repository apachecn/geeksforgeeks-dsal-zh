# 如何用数组和泛型在 Java 中实现队列？

> 原文:[https://www . geesforgeks . org/如何使用数组和泛型实现 java 中的队列/](https://www.geeksforgeeks.org/how-to-implement-queue-in-java-using-array-and-generics/)

队列是遵循先进先出规则的线性数据结构。我们不仅可以为整数实现队列，还可以为字符串、浮点或字符实现队列。队列中有 5 个主要操作:

1.  *入队()* 将元素 x 添加到队列的前面
2.  *出列()* 移除队列的最后一个元素
3.  *前置()***T3】返回前置元素**
4.  *后方()*T2 返回后方元素
5.  *空()* 返回队列是否为空

> **注意:**所有操作的时间复杂度为 1

**实施:**

**例**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Implement Queue using Array and Generics

// Importing input output classes
import java.io.*;
// Importing all utility classes
import java.util.*;

// Class 1
// Helper Class(user defined - generic queue class)
class queue<T> {
    // front and rear variables are initially initiated to
    // -1 pointing to no element that control queue
    int front = -1, rear = -1;

    // Creating an object of ArrayList class of T type
    ArrayList<T> A = new ArrayList<>();

    // Method 1
    // Returns value of element at front
    T front()
    {
        // If it is not pointing to any element in queue
        if (front == -1)

            return null;

        // else return the front element
        return A.get(front);
    }
    // Method 2
    // Returns value of element at rear
    T rear()
    {
        // If it is not pointing to any element in queue
        if (rear == -1)
            return null;
        return A.get(rear);
    }
    // Method 3
    // Inserts element at the front of queue
    void enqueue(T X)
    {
        // If queue is empty
        if (this.empty()) {
            front = 0;
            rear = 0;
            A.add(X);
        }

        // If queue is not empty
        else {
            front++;
            if (A.size() > front) {

                // Mov front pointer to next
                A.set(front, X);
            }
            else

                // Add element to the queue
                A.add(X);
        }
    }
    // Method 4
    // Deletes elements from the rear from queue
    void dequeue()
    {
        // if queue doesn't have any elements
        if (this.empty())

            // Display message when queue is already empty
            System.out.println("Queue is already empty");

        // If queue has only one element
        else if (front == rear) {

            // Both are pointing to same element
            front = rear = -1;
        }

        // If queue has more than one element
        else {

            // Increment the rear
            rear++;
        }
    }

    // Method 5
    // Checks whether the queue is empty
    boolean empty()
    {
        // Both are initialized to same value
        // as assigned at declaration means no queue made
        if (front == -1 && rear == -1)
            return true;
        return false;
    }
    // Method 6
    // Print the queue

    // @Override
    public String toString()
    {
        if (this.empty())
            return "";

        String Ans = "";

        for (int i = rear; i < front; i++) {
            Ans += String.valueOf(A.get(i)) + "->";
        }

        Ans += String.valueOf(A.get(front));

        return Ans;
    }
}

// Class 2
// Main class
class GFG {

    // Main driver method
    public static void main(String args[])
    {
        // Case 1 : Integer Queue

        // Creating object of queue Class (user defined)
        // Declaring object of integer type
        queue<Integer> q1 = new queue<>();

        // Pushing elements to the integer object created
        // Custom input integer entries
        q1.enqueue(5);
        q1.enqueue(10);
        q1.enqueue(20);

        // Print the queue after inserting integer elements
        System.out.println(
            "q1 after enqueue of 3 elements:\n" + q1);
        q1.dequeue();
        System.out.println("q1 after dequeue :\n" + q1);

        // Case 2 : String Queue

        // Creating object of queue Class (user defined)
        // Declaring object of string type
        queue<String> q2 = new queue<>();

        // Pushing elements to the String object created
        // Custom input string entries
        q2.enqueue("hello");
        q2.enqueue("world");
        q2.enqueue("GFG");

        // Print the queue after inserting string elements
        System.out.println(
            "\nq2 after enqueue of 3 elements:\n" + q2);

        // Printing front and rear of the above queue
        System.out.println("q2 front = " + q2.front()
                           + ", q2 rear = " + q2.rear());

        // Case 3 : Float Queue

        // Creating object of queue Class (user defined)
        // Declaring object of float type
        queue<Float> q3 = new queue<>();

        // Display message only
        System.out.println(
            "\nCreated new Float type queue q3...");

        // Display whether queue is empty or not
        // using the empty() method
        System.out.println(
            "Checking if queue is empty or not :\n"
            + q3.empty());
    }
}
```

**Output**

```
q1 after enqueue of 3 elements:
5->10->20
q1 after dequeue :
10->20

q2 after enqueue of 3 elements:
hello->world->GFG
q2 front = GFG, q2 rear = hello

Created new Float type queue q3...
Checking if queue is empty or not :
true
```