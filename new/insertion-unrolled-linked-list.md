# 插入展开的链表

> 原文：[https://www.geeksforgeeks.org/insertion-unrolled-linked-list/](https://www.geeksforgeeks.org/insertion-unrolled-linked-list/)

展开的链表是小数组的链表，它们的大小都相同，但每个数组的大小都很小，以至于插入或删除都很快，但又足够大以填充高速缓存行。 指向列表的迭代器既包含指向节点的指针，又包含指向包含数组的节点的索引。 它也是一种数据结构，是链表的另一种形式。 它与 B 树有关。 它可以在节点上存储元素数组，而不像普通链表在节点上存储单个元素。 它是数组和链表融合在一起的组合。 它提高了缓存性能，并减少了与存储元数据引用相关的内存开销。 其他主要优点和缺点已在上一篇文章中提到。

**先决条件**：[展开的链表简介](https://www.geeksforgeeks.org/unrolled-linked-list-set-1-introduction/)

以下是展开的链表的插入和显示操作。

```
Input : 72 76 80 94 90 70
        capacity = 3
Output : Unrolled Linked List : 
72 76 
80 94 
90 70 
Explanation : The working is well shown in the
algorithm below. The nodes get broken at the 
mentioned capacity i.e., 3 here, when 3rd element 
is entered, the flow moves to another newly created 
node. Every node contains an array of size 
(int)[(capacity / 2) + 1]. Here it is 2\. 

Input : 49 47 62 51 77 17 71 71 35 76 36 54
        capacity = 5
Output :
Unrolled Linked List : 
49 47 62 
51 77 17 
71 71 35 
76 36 54 
Explanation : The working is well shown in the
algorithm below. The nodes get broken at the
mentioned capacity i.e., 5 here, when 5th element
is entered, the flow moves to another newly 
created node. Every node contains an array of 
size (int)[(capacity / 2) + 1]. Here it is 3\. 

```

**算法**：

```
Insert (ElementToBeInserted)
    if start_pos == NULL
        Insert the first element into the first node
        start_pos.numElement ++
        end_pos = start_pos
    If end_pos.numElements + 1 <  node_size
        end_pos.numElements.push(newElement)
        end_pos.numElements ++
    else
        create a new Node new_node
        move final half of end_pos.data into new_node.data
        new_node.data.push(newElement)
        end_pos.numElements = end_pos.data.size / 2 + 1
        end_pos.next = new_node
        end_pos = new_node

```

以下是插入和显示操作的 Java 实现。 在下面的代码中，容量为 5，并输入随机数。

## Java

```java

/* Java program to show the insertion operation 
* of Unrolled Linked List */
import java.util.Scanner; 
import java.util.Random; 

// class for each node 
class UnrollNode { 
    UnrollNode next; 
    int num_elements; 
    int array[]; 

    // Constructor 
    public UnrollNode(int n) 
    { 
        next = null; 
        num_elements = 0; 
        array = new int[n]; 
    } 
} 

// Operation of Unrolled Function 
class UnrollLinkList { 

    private UnrollNode start_pos; 
    private UnrollNode end_pos; 

    int size_node; 
    int nNode; 

    // Parameterized Constructor 
    UnrollLinkList(int capacity) 
    { 
        start_pos = null; 
        end_pos = null; 
        nNode = 0; 
        size_node = capacity + 1; 
    } 

    // Insertion operation 
    void Insert(int num) 
    { 
        nNode++; 

        // Check if the list starts from NULL 
        if (start_pos == null) { 
            start_pos = new UnrollNode(size_node); 
            start_pos.array[0] = num; 
            start_pos.num_elements++; 
            end_pos = start_pos; 
            return; 
        } 

        // Attaching the elements into nodes 
        if (end_pos.num_elements + 1 < size_node) { 
            end_pos.array[end_pos.num_elements] = num; 
            end_pos.num_elements++; 
        } 

        // Creation of new Node 
        else { 
            UnrollNode node_pointer = new UnrollNode(size_node); 
            int j = 0; 
            for (int i = end_pos.num_elements / 2 + 1; 
                 i < end_pos.num_elements; i++) 
                node_pointer.array[j++] = end_pos.array[i]; 

            node_pointer.array[j++] = num; 
            node_pointer.num_elements = j; 
            end_pos.num_elements = end_pos.num_elements / 2 + 1; 
            end_pos.next = node_pointer; 
            end_pos = node_pointer; 
        } 
    } 

    // Display the Linked List 
    void display() 
    { 
        System.out.print("\nUnrolled Linked List = "); 
        System.out.println(); 
        UnrollNode pointer = start_pos; 
        while (pointer != null) { 
            for (int i = 0; i < pointer.num_elements; i++) 
                System.out.print(pointer.array[i] + " "); 
            System.out.println(); 
            pointer = pointer.next; 
        } 
        System.out.println(); 
    } 
} 

/* Main Class */
class UnrolledLinkedList_Check { 

    // Driver code 
    public static void main(String args[]) 
    { 
        Scanner sc = new Scanner(System.in); 

        // create instance of Random class 
        Random rand = new Random(); 

        UnrollLinkList ull = new UnrollLinkList(5); 

        // Perform Insertion Operation 
        for (int i = 0; i < 12; i++) { 

            // Generate random integers in range 0 to 99 
            int rand_int1 = rand.nextInt(100); 
            System.out.println("Entered Element is " + rand_int1); 
            ull.Insert(rand_int1); 
            ull.display(); 
        } 
    } 
} 

```

## C#

```cs

/* C# program to show the insertion operation 
* of Unrolled Linked List */
using System; 

// class for each node 
public class UnrollNode { 
    public UnrollNode next; 
    public int num_elements; 
    public int[] array; 

    // Constructor 
    public UnrollNode(int n) 
    { 
        next = null; 
        num_elements = 0; 
        array = new int[n]; 
    } 
} 

// Operation of Unrolled Function 
public class UnrollLinkList { 

    private UnrollNode start_pos; 
    private UnrollNode end_pos; 

    int size_node; 
    int nNode; 

    // Parameterized Constructor 
    public UnrollLinkList(int capacity) 
    { 
        start_pos = null; 
        end_pos = null; 
        nNode = 0; 
        size_node = capacity + 1; 
    } 

    // Insertion operation 
    public void Insert(int num) 
    { 
        nNode++; 

        // Check if the list starts from NULL 
        if (start_pos == null) { 
            start_pos = new UnrollNode(size_node); 
            start_pos.array[0] = num; 
            start_pos.num_elements++; 
            end_pos = start_pos; 
            return; 
        } 

        // Attaching the elements into nodes 
        if (end_pos.num_elements + 1 < size_node) { 
            end_pos.array[end_pos.num_elements] = num; 
            end_pos.num_elements++; 
        } 

        // Creation of new Node 
        else { 
            UnrollNode node_pointer = new UnrollNode(size_node); 
            int j = 0; 
            for (int i = end_pos.num_elements / 2 + 1; 
                 i < end_pos.num_elements; i++) 
                node_pointer.array[j++] = end_pos.array[i]; 

            node_pointer.array[j++] = num; 
            node_pointer.num_elements = j; 
            end_pos.num_elements = end_pos.num_elements / 2 + 1; 
            end_pos.next = node_pointer; 
            end_pos = node_pointer; 
        } 
    } 

    // Display the Linked List 
    public void display() 
    { 
        Console.Write("\nUnrolled Linked List = "); 
        Console.WriteLine(); 
        UnrollNode pointer = start_pos; 
        while (pointer != null) { 
            for (int i = 0; i < pointer.num_elements; i++) 
                Console.Write(pointer.array[i] + " "); 
            Console.WriteLine(); 
            pointer = pointer.next; 
        } 
        Console.WriteLine(); 
    } 
} 

/* Main Class */
public class UnrolledLinkedList_Check { 

    // Driver code 
    public static void Main(String[] args) 
    { 
        // create instance of Random class 
        Random rand = new Random(); 

        UnrollLinkList ull = new UnrollLinkList(5); 

        // Perform Insertion Operation 
        for (int i = 0; i < 12; i++) { 

            // Generate random integers in range 0 to 99 
            int rand_int1 = rand.Next(100); 
            Console.WriteLine("Entered Element is " + rand_int1); 
            ull.Insert(rand_int1); 
            ull.display(); 
        } 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
Entered Element is 90

Unrolled Linked List = 
90 

Entered Element is 3

Unrolled Linked List = 
90 3 

Entered Element is 12

Unrolled Linked List = 
90 3 12 

Entered Element is 43

Unrolled Linked List = 
90 3 12 43 

Entered Element is 88

Unrolled Linked List = 
90 3 12 43 88 

Entered Element is 94

Unrolled Linked List = 
90 3 12 
43 88 94 

Entered Element is 15

Unrolled Linked List = 
90 3 12 
43 88 94 15 

Entered Element is 7

Unrolled Linked List = 
90 3 12 
43 88 94 15 7 

Entered Element is 67

Unrolled Linked List = 
90 3 12 
43 88 94 
15 7 67 

Entered Element is 74

Unrolled Linked List = 
90 3 12 
43 88 94 
15 7 67 74 

Entered Element is 85

Unrolled Linked List = 
90 3 12 
43 88 94 
15 7 67 74 85 

Entered Element is 48

Unrolled Linked List = 
90 3 12 
43 88 94 
15 7 67 
74 85 48

```

时间复杂度： `O(n)`

另外，实际应用很少：

*   它用于 B 树和 T 树

*   用于哈希数组树

*   在跳表中使用

*   用于 CDR 编码



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。