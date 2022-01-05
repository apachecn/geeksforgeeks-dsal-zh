# 对循环链表元素进行排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-sort-the-elements-of-the-circular-link-list/](https://www.geeksforgeeks.org/java-program-to-sort-the-elements-of-the-circular-linked-list/)

在一个循环链表中，每个节点都指向序列中的下一个节点，但是最后一个节点指向列表中的第一个节点。这里，创建一个循环链表，并按升序对循环链表进行排序。

排序前循环链表:

![](img/7ec9508ba5da08fd1d1cffc1298bc856.png)

循环链表

排序后循环链表:

![](img/aea40cc4ad402a1bd90bb89f0b2e37bc.png)

排序循环链表

**进场:**

1.  取两个指针: **Current** 指向节点头部， **Temp** 指向 **Current 的下一个节点。**
2.  Now for each iteration compare **value of** **Current pointer** to the **value of Temp pointer**.
    Here two cases arise

    **情况 1:** 如果当前指针的值**大于**则临时指针的值
    交换当前指针和临时指针的值。
    将温度指针移动到下一个节点
    **情况 2:** 如果当前指针的值**小于或等于**温度指针的值
    将温度指针移动到下一个节点

3.  现在继续这样做，直到 **temp.next！=列表头**。
4.  完成第 3 步**后，将当前节点移动到下一个节点**，重复第 1、2、3 步。
5.  每次迭代都会将列表中最短的元素固定到正确的位置。
6.  重复以上步骤，直到当前。下一个！=列表头。

**让我们看看这对于给定循环链表的第一个节点**是如何工作的

![](img/ffd301780a7dab2e7dbbfbbc5fddc598.png)

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Sort the Elements
// of the Circular Linked List

import java.io.*;

public class GFG {
    // Stores Information about Node of List
    public class Node {
        int data;
        Node next;
        public Node(int data) { this.data = data; }
    }

    // Declaring Head of the Node
    public Node head_of_node = null;

    // A last pointer to help append values to our list
    public Node last = null;

    // Add method adds values to the end of the list
    public void add(int data)
    {
        Node newNode = new Node(data);
        if (head_of_node == null) {
            head_of_node = newNode;
            last = newNode;
            newNode.next = head_of_node;
        }
        else {
            last.next = newNode;
            last = newNode;
            last.next = head_of_node;
        }
    }
    // Sort_List method sorts the circular
    // linked list Using the algorithm
    public void Sort_List()
    {

        // current pointer pointing to the head of the list
        Node current = head_of_node;

        // a temp pointer
        Node temp = null;

        // variable value helps in swap of the values
        int value;

        // this is the Algorithm discussed above
        if (head_of_node == null) {
            System.out.println("Your list is empty");
        }
        else {
            while (current.next != head_of_node) {
                temp = current.next;
                while (temp != head_of_node) {
                    if (current.data > temp.data) {
                        value = current.data;
                        current.data = temp.data;
                        temp.data = value;
                    }
                    temp = temp.next;
                }
                current = current.next;
            }
        }
    }
    // Print_list method iterates through the list and
    // prints the values stored in the list
    public void Print_List()
    {
        Node current = head_of_node;
        if (head_of_node == null) {
            System.out.println("Your list is empty");
        }
        else {
            do {
                System.out.print(" " + current.data);
                current = current.next;
            } while (current != head_of_node);
            System.out.println();
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        GFG circular_list = new GFG();
        circular_list.add(10);
        circular_list.add(6);
        circular_list.add(3);
        circular_list.add(8);
        circular_list.add(4);

        System.out.print("Original List -->     ");
        circular_list.Print_List();
        circular_list.Sort_List();
        System.out.print("List after Sorting--> ");
        circular_list.Print_List();
    }
}
```

**Output**

```
Original List -->      10 6 3 8 4
List after Sorting-->  3 4 6 8 10
```

**时间复杂度:** O(N <sup>2</sup> )