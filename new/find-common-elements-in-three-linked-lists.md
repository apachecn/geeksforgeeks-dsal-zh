# 在三个链接列表中查找公共元素

给定三个链表，在三个链表中找到所有共同的元素。

**示例：**

```
Input :  
   10 15 20 25 12
   10 12 13 15 
   10 12 15 24 25 26
Output : 10 12 15 

Input :
   1 2 3 4 5
   1 2 3 4 6 9 8
   1 2 4 5 10
Output : 1 2 4

```

**方法1 ：（简单）**
使用三指针迭代给定的三个链表，如果有公共元素，则打印该元素。
上述解决方案的时间复杂度为O（N * N * N）

**方法2 ：（使用合并排序）**
在此方法中，我们首先对三个列表进行排序，然后遍历排序后的列表以获取交集。

以下是获取三个列表的交集要遵循的步骤：

1）使用合并排序对第一个链表进行排序。 此步骤需要O（mLogm）时间。 有关此步骤的详细信息，请参见此帖子的[。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

2）使用合并排序对第二个链接列表进行排序。 此步骤需要O（nLogn）时间。 有关此步骤的详细信息，请参见此帖子的[。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

3）使用合并排序对第三个链表进行排序。 此步骤需要O（pLogp）时间。 有关此步骤的详细信息，请参见此帖子的[。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

3）线性扫描三个排序的列表以获得交集。 此步骤需要O（m + n + p）时间。 可以使用与此处中讨论的排序数组算法相同的算法来实现此步骤。

此方法的时间复杂度为O（mLogm + nLogn + plogp），优于方法1的时间复杂度。

**方法3 ：（散列）**
以下是使用散列获得三个列表的交点的步骤：
1）创建一个空散列表。 遍历第一个链表，并在哈希表中将所有元素频率标记为1。 此步骤需要O（m）时间。
2）遍历第二个链表，如果当前元素频率在哈希表中为1，则将其标记为2。此步骤需要O（n）时间。
3）迭代第三个链表，如果当前元素频率在哈希表中为2，则将其标记为3。此步骤需要O（p）时间。
4）现在再次迭代第一个链表以检查元素的频率。 如果哈希表中存在频率为3的元素，则它将出现在三个链表的交集中。 此步骤需要O（m）时间。

该方法的时间复杂度为O（m + n + p），优于方法1和2的时间复杂度。

以下是上述想法的实现。

## C++

```cpp

// C++ program to find common element 
// in three unsorted linked list 
#include <bits/stdc++.h> 
#define max 1000000 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* A utility function to insert a node at the  
beginning of a linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node =  
            (struct Node *)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* print the common element in between 
given three linked list*/
void Common(struct Node* head1,  
            struct Node* head2, struct Node* head3) 
{ 

    // Creating empty hash table; 
    unordered_map<int, int> hash; 

    struct Node* p = head1; 
    while (p != NULL) { 

        // set frequency by 1 
        hash[p->data] = 1; 
        p = p->next; 
    } 

    struct Node* q = head2; 
    while (q != NULL) { 

        // if the element is already exist in the 
        // linked list set its frequency 2 
        if (hash.find(q->data) != hash.end())  
            hash[q->data] = 2; 
        q = q->next; 
    } 

    struct Node* r = head3; 
    while (r != NULL) { 
        if (hash.find(r->data) != hash.end() &&  
            hash[r->data] == 2)  

        // if the element frquancy is 2 it means 
        // its present in both the first and second 
        // linked list set its frquancy 3 
        hash[r->data] = 3; 
        r = r->next; 
    } 

    for (auto x : hash) { 

        // if current frequency is 3 its means  
        // element is common in all the given  
        // linked list 
        if (x.second == 3)  
            cout << x.first << " "; 
    } 
} 

// Driver code 
int main() 
{ 

    // first list 
    struct Node* head1 = NULL; 
    push(&head1, 20); 
    push(&head1, 5); 
    push(&head1, 15); 
    push(&head1, 10); 

    // second list 
    struct Node* head2 = NULL; 
    push(&head2, 10); 
    push(&head2, 20); 
    push(&head2, 15); 
    push(&head2, 8); 

    // third list 
    struct Node* head3 = NULL; 
    push(&head3, 10); 
    push(&head3, 2); 
    push(&head3, 15); 
    push(&head3, 20); 

    Common(head1, head2, head3); 

    return 0; 
} 

```

## Java

```java

// Java program to find common element 
// in three unsorted linked list 
import java.util.*; 

class GFG  
{ 
static int max = 1000000; 

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

/* A utility function to insert a node  
at the beginning of a linked list */
static Node push(Node head_ref, 
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

/* print the common element in between 
given three linked list*/
static void Common(Node head1,  
                   Node head2,  
                   Node head3) 
{ 

    // Creating empty hash table; 
    HashMap<Integer,  
            Integer> hash = new HashMap<Integer,  
                                        Integer>(); 

    Node p = head1; 
    while (p != null)  
    { 

        // set frequency by 1 
        hash. put(p.data, 1); 
        p = p.next; 
    } 

    Node q = head2; 
    while (q != null)  
    { 

        // if the element is already exist in the 
        // linked list set its frequency 2 
        if (hash.containsKey(q.data))  
            hash. put(q.data, 2); 
        q = q.next; 
    } 

    Node r = head3; 
    while (r != null) 
    { 
        if (hash.containsKey(r.data)&&  
            hash.get(r.data) == 2)  

        // if the element frquancy is 2 it means 
        // its present in both the first and second 
        // linked list set its frquancy 3 
        hash. put(r.data, 3); 
        r = r.next; 
    } 

    for (Map.Entry<Integer, 
                   Integer> x : hash.entrySet())  
    { 

        // if current frequency is 3 its means  
        // element is common in all the given  
        // linked list 
        if (x.getValue() == 3)  
            System.out.println(x.getKey() + " "); 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 

    // first list 
    Node head1 = null; 
    head1 = push(head1, 20); 
    head1 = push(head1, 5); 
    head1 = push(head1, 15); 
    head1 = push(head1, 10); 

    // second list 
    Node head2 = null; 
    head2 = push(head2, 10); 
    head2 = push(head2, 20); 
    head2 = push(head2, 15); 
    head2 = push(head2, 8); 

    // third list 
    Node head3 = null; 
    head3 = push(head3, 10); 
    head3 = push(head3, 2); 
    head3 = push(head3, 15); 
    head3 = push(head3, 20); 

    Common(head1, head2, head3); 
} 
}  

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# program to find common element 
// in three unsorted linked list 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
static int max = 1000000; 

/* Link list node */
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

/* A utility function to insert a node  
at the beginning of a linked list */
static Node push(Node head_ref, 
                int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

/* print the common element in between 
given three linked list*/
static void Common(Node head1,  
                Node head2,  
                Node head3) 
{ 

    // Creating empty hash table; 
    Dictionary<int,      
               int> hash = new Dictionary<int,  
                                          int>(); 

    Node p = head1; 
    while (p != null)  
    { 

        // set frequency by 1 
        hash.Add(p.data, 1); 
        p = p.next; 
    } 

    Node q = head2; 
    while (q != null)  
    { 

        // if the element is already exist in the 
        // linked list set its frequency 2 
        if (hash.ContainsKey(q.data))  
            hash[q.data] = 2; 
        q = q.next; 
    } 

    Node r = head3; 
    while (r != null) 
    { 
        if (hash.ContainsKey(r.data)&&  
            hash[r.data] == 2)  

        // if the element frquancy is 2 it means 
        // its present in both the first and  
        // second linked list set its frquancy 3 
        hash[r.data] = 3; 
        r = r.next; 
    } 

    foreach(KeyValuePair<int, int> x in hash) 
    { 

        // if current frequency is 3 its means  
        // element is common in all the given  
        // linked list 
        if (x.Value == 3)  
            Console.Write(x.Key + " "); 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    // first list 
    Node head1 = null; 
    head1 = push(head1, 20); 
    head1 = push(head1, 5); 
    head1 = push(head1, 15); 
    head1 = push(head1, 10); 

    // second list 
    Node head2 = null; 
    head2 = push(head2, 10); 
    head2 = push(head2, 20); 
    head2 = push(head2, 15); 
    head2 = push(head2, 8); 

    // third list 
    Node head3 = null; 
    head3 = push(head3, 10); 
    head3 = push(head3, 2); 
    head3 = push(head3, 15); 
    head3 = push(head3, 20); 

    Common(head1, head2, head3); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
10 15 20

```

时间复杂度：O（m + n + p）



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。