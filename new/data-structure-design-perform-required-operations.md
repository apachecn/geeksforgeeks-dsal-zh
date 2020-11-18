# 执行所需操作的数据结构设计

设计可以执行以下操作的数据结构

1.  O（n）中的add（）
2.  getMinimum（）到O（1）
3.  O（1）中的deleteMinimum（）

**来源：** [MakeMyTrip访谈。](https://www.geeksforgeeks.org/makemytrip-interview-experience-set-16/)

1.  维护一个链表，其中的元素按升序排列。
2.  删除最小操作时，将磁头移至下一个位置。
3.  如果进行最小操作，则返回First元素。

```

// Java code for linked list to 
// perform required operations 
import java.util.*; 

// Node class 
class Node 
{ 
    int data; 
    Node next; 

    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

// main class 
class MinDS 
{ 
    Node start; 

    public MinDS() 
    { 
        start = null; 
    } 

    // Function to add element 
    void addElement(int d) 
    { 
        Node tmp = new Node(d); 

        // If linked list is empty 
        if (start == null) 
        { 
            start = tmp; 
            return; 
        } 

        // If head itself is greater 
        if (d < start.data) 
        { 
            tmp.next = start; 
            start = tmp; 
            return; 
        } 

        // If need to insert somewhere in middle 
        Node prev = start; 
        Node ptr = start.next; 
        while (ptr != null) 
        { 
            if (d < ptr.data) 
            { 
                tmp.next = ptr; 
                prev.next = tmp; 
                return; 
            } 
            else
            { 
                prev = ptr; 
                ptr = ptr.next; 
            } 
        } 
        prev.next = tmp; 
    } 

    // Function to get minimum 
    int getMin() 
    { 
        return start.data; 
    } 

    // Function to delete minimum 
    int delMin() 
    { 
        int min = start.data; 
        start = start.next; 
        return min; 
    } 

    // Function to print elements 
    void print() 
    { 
        Node ptr = start; 
        System.out.print("Elements: "); 
        while (ptr != null) 
        { 
            System.out.print(ptr.data + ", "); 
            ptr = ptr.next; 
        } 
        System.out.println("\n"); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        MinDS x = new MinDS(); 
        x.addElement(10); 
        x.addElement(20); 
        x.addElement(5); 
        x.addElement(15); 
        x.print(); 

        System.out.println("Get Min: " + x.getMin()); 
        System.out.println("Del Min: " + x.delMin()); 
        x.print(); 

        System.out.println("Min: " + x.getMin()); 
    } 
} 

```

**Output:**

```
Elements: 5, 10, 15, 20, 

Get Min: 5
Del Min: 5
Elements: 10, 15, 20, 

Min: 10

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。