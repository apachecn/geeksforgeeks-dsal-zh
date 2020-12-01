# 杀掉邻居的邻居后，在围成一个圈的`N`人中找到最后 2 个幸存者

> 原文：[https://www.geeksforgeeks.org/find-last-2-survivors-in-n-persons-standing-in-a-circle-after-killing-next-to-immediate-neighbour/](https://www.geeksforgeeks.org/find-last-2-survivors-in-n-persons-standing-in-a-circle-after-killing-next-to-immediate-neighbour/)

给定一个整数`N`代表一个圆圈中的`N`个人，任务是在每个人杀死顺时针方向上邻居的下一个时，找到剩下的最后 2 个人。

**示例**：

> **输入**：`N = 5`
>
> **输出**：`1 4`
>
> **说明**：
>
> 初始：`1 2 3 4 5`
>
> => 1 杀死 3
>
> 存活：`1 2 4 5`
>
> => 2 杀死 5
>
> 存活：`1 2 4`
>
> => 4 杀死 2
>
> 最终存活：`1 4`
>
> **输入**：`N = 2`
>
> **输出**：`1 2`

**朴素的方法**：一种简单的方法是保持大小为`N`的`bool`数组，以跟踪人是否还活着。

*   最初，布尔数组对所有人都是`true`。

*   保持[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)，一个指针位于当前活着的人，第二个指针用于存储它之前的人。

*   一旦找到当前人的第二个活着的邻居，请将其布尔值更改为`false`。

*   然后，当前指针再次从上一个更新为下一个。

*   这个过程将持续到最后两个人幸存。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`

**有效方法**：一种有效方法是从数据结构中删除该人（如果已死亡），以免再次遍历该人。

*   仅在完成一轮比赛后，最多只有`N / 2`人。

*   然后，在下一轮中将剩下`N / 4`人，依此类推，直到有很多活着的人变成 2 人为止。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 

#include <bits/stdc++.h> 
using namespace std; 

// Node for a Linked List 
struct Node { 
    int val; 
    struct Node* next; 

    Node(int _val) 
    { 
        val = _val; 
        next = NULL; 
    } 
}; 

// Function to find the last 2 survivors 
void getLastTwoPerson(int n) 
{ 
    // Total is the count 
    // of alive people 
    int total = n; 
    struct Node* head = new Node(1); 
    struct Node* temp = head; 

    // Initiating the list of n people 
    for (int i = 2; i <= n; i++) { 
        temp->next = new Node(i); 
        temp = temp->next; 
    } 

    temp->next = head; 
    temp = head; 

    struct Node* del; 

    // Total != 2 is terminating 
    // condition because 
    // at last only two-person 
    // will remain alive 
    while (total != 2) { 

        // Del represent next person 
        // to be deleted or killed 
        del = temp->next->next; 
        temp->next->next 
            = temp->next->next->next; 
        temp = temp->next; 
        free(del); 
        total -= 1; 
    } 

    // Last two person to 
    // survive (in any order) 
    cout << temp->val << " "
         << temp->next->val; 
} 

// Driver code 
int main() 
{ 
    int n = 2; 

    getLastTwoPerson(n); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG{ 

// Node for a Linked List 
static class Node  
{ 
    int val; 
    Node next; 

    Node(int _val) 
    { 
        val = _val; 
        next = null; 
    } 
}; 

// Function to find the last 2 survivors 
static void getLastTwoPerson(int n) 
{ 

    // Total is the count 
    // of alive people 
    int total = n; 
    Node head = new Node(1); 
    Node temp = head; 

    // Initiating the list of n people 
    for(int i = 2; i <= n; i++)  
    { 
        temp.next = new Node(i); 
        temp = temp.next; 
    } 

    temp.next = head; 
    temp = head; 

    Node del; 

    // Total != 2 is terminating 
    // condition because 
    // at last only two-person 
    // will remain alive 
    while (total != 2) 
    { 

        // Del represent next person 
        // to be deleted or killed 
        del = temp.next.next; 
        temp.next.next = temp.next.next.next; 
        temp = temp.next; 
        del = null; 

        System.gc(); 
        total -= 1; 
    } 

    // Last two person to 
    // survive (in any order) 
    System.out.print(temp.val + " " + 
                     temp.next.val); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int n = 2; 

    getLastTwoPerson(n); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG{ 

// Node for a Linked List 
class Node  
{ 
    public int val; 
    public Node next; 

    public Node(int _val) 
    { 
        val = _val; 
        next = null; 
    } 
}; 

// Function to find the last 2 survivors 
static void getLastTwoPerson(int n) 
{ 

    // Total is the count 
    // of alive people 
    int total = n; 
    Node head = new Node(1); 
    Node temp = head; 

    // Initiating the list of n people 
    for(int i = 2; i <= n; i++)  
    { 
        temp.next = new Node(i); 
        temp = temp.next; 
    } 

    temp.next = head; 
    temp = head; 

    Node del; 

    // Total != 2 is terminating 
    // condition because 
    // at last only two-person 
    // will remain alive 
    while (total != 2) 
    { 

        // Del represent next person 
        // to be deleted or killed 
        del = temp.next.next; 
        temp.next.next = temp.next.next.next; 
        temp = temp.next; 
        del = null; 

        total -= 1; 
    } 

    // Last two person to 
    // survive (in any order) 
    Console.Write(temp.val + " " + 
                  temp.next.val); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int n = 2; 

    getLastTwoPerson(n); 
} 
} 

// This code is contributed by Amit Katiyar

```

**输出**： 

```
1 2

```

**时间复杂度**：`O(N * log N)`

**辅助空间**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。