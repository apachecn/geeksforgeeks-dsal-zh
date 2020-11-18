# 在紧邻邻居的邻居中被杀后，在围成一个圈的N人中找到最后2个幸存者

给定一个整数 **N** 代表一个圆圈中的 **N** 个人，任务是找到一个人在顺时针方向上杀死紧邻的邻居时剩下的最后2个人。
**范例：** [

> **输入：** N = 5
> **输出：** 1 4
> **说明：**
> 初始：1 2 3 4 5
> = > 1杀死3
> 站立：1 2 4 5
> = > 2杀死5
> 站立：1 2 4
> = > 4杀死2
> 最终站立：1 4
> **输入：** N = 2
> **输出：** 1 2

**天真的方法：**一种简单的方法是保持大小为N的 **bool数组**，以跟踪人是否还活着。

*   最初，布尔数组对所有人都是正确的。
*   保持[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)，一个指针位于当前在世的人，第二个指针用于存储先前的当前人。
*   一旦找到当前人的第二个活着的邻居，请将其布尔值更改为false。
*   然后，当前电流再次从上一个更新为下一个。
*   这个过程将持续到最后两个人幸免。

***时间复杂度：** O（N <sup>2</sup> ）*Â
***辅助空间：** O（N）*

**有效方法：**一种有效方法是从数据结构中删除该人（如果已死亡），以免再次遍历该人。

*   仅在完成一轮比赛后，最多只有N / 2人。
*   然后，在下一轮中将剩下N / 4人，依此类推，直到有很多在世的人变成2人为止。

下面是上述方法的实现：

## C ++

```

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

## 爪哇

```

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

## C＃

```

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

**Output:** 

```
1 2

```

***时间复杂度：** O（N * log N）*
***辅助空间：** O（N）*

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。