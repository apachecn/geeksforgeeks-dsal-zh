# 幸存者围成一圈 | 剑谜题的代码解决方案

> 原文：[https://www.geeksforgeeks.org/lucky-alive-person-circle/](https://www.geeksforgeeks.org/lucky-alive-person-circle/)

给定`n`个人站在第一个持剑的圈子中，找到圈子中最幸运的人，如果从第一个持剑的士兵中每个都必须杀死下一个士兵并将剑移交给下一个士兵，那么该士兵将 杀死相邻的士兵，并将剑移交给下一位士兵，以使一名士兵仍在这场战争中被任何人杀死。

先决条件：[谜题 81 | 一圈有 100 人的枪谜游戏](https://www.geeksforgeeks.org/puzzle-100-people-in-a-circle-with-gun-puzzle/)

例子 ：

> 输入：5
>
> 输出：3
>
> 说明：
>
> `N = 5`
>
> 士兵`1 2 3 4 5`（5 名士兵）
>
> 首先是`1 3 5`（剩余）因为 2 和 4 分别被 1 和 3 杀死。
>
> 第二步中，3 和 5 杀死了 1，3 杀死了 5，士兵 3 活着。
> 
> 输入：100
>
> 输出：73
>
> 说明：
>
> `N = 10`
>
> 士兵`1 2 3 4 5 6 7 8 9 10`（10 名士兵）
>
> 首先是`1 3 5 7 9`，因为`2 4 6 8 10`被`1 3 5 7`和 9 杀死。
>
> 第二步是`1 5 9`，因为 9 杀死 1，然后 5 杀死士兵 9。
>
> 第三步中，士兵 5 还活着。

**方法**：想法是使用[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)。 根据士兵的数量`N`创建一个循环链表。根据规则，您必须杀死相邻的士兵并将剑移交给下一个士兵，而后者又会杀死其相邻​​的士兵并将剑移交给下一个士兵。 因此，在循环链表中，相邻的士兵被杀死，其余的士兵以循环的方式互相对抗，只有一名士兵被任何人杀害而幸存。

## C++

```cpp

// CPP code to find the luckiest person 
#include <bits/stdc++.h> 
using namespace std; 

// Node structure 
struct Node { 
    int data; 
    struct Node* next; 
}; 

Node *newNode(int data) 
{ 
   Node *node = new Node; 
   node->data = data; 
   node->next = NULL; 
   return node; 
} 

// Function to find the luckiest person 
int alivesol(int Num) 
{ 
    if (Num == 1) 
        return 1; 

    // Create a single node circular 
    // linked list. 
    Node *last = newNode(1); 
    last->next = last; 

    for (int i = 2; i <= Num; i++) { 
        Node *temp = newNode(i); 
        temp->next = last->next;         
        last->next = temp; 
        last = temp;      
    } 

    // Starting from first soldier. 
    Node *curr = last->next; 

    // condition for evaluating the existence 
    // of single soldier who is not killed. 
    Node *temp; 
    while (curr->next != curr) { 
        temp = curr; 
        curr = curr->next; 
        temp->next = curr->next; 

        // deleting soldier from the circular 
        // list who is killed in the fight. 
        delete curr; 
        temp = temp->next; 
        curr = temp; 
    } 

    // Returning the Luckiest soldier who 
    // remains alive. 
    int res = temp->data; 
    delete temp; 

    return res; 
} 

// Driver code 
int main() 
{ 
    int N = 100; 
    cout << alivesol(N) << endl; 
    return 0; 
} 

```

## Java

```java

// Java code to find the luckiest person  
class GFG 
{ 

// Node structure  
static class Node  
{  
    int data;  
    Node next;  
};  

static Node newNode(int data)  
{  
    Node node = new Node();  
    node.data = data;  
    node.next = null;  
    return node;  
}  

// Function to find the luckiest person  
static int alivesol(int Num)  
{  
    if (Num == 1)  
        return 1;  

    // Create a single node circular  
    // linked list.  
    Node last = newNode(1);  
    last.next = last;  

    for (int i = 2; i <= Num; i++)  
    {  
        Node temp = newNode(i);  
        temp.next = last.next;      
        last.next = temp;  
        last = temp;      
    }  

    // Starting from first soldier.  
    Node curr = last.next;  

    // condition for evaluating the existence  
    // of single soldier who is not killed.  
    Node temp = new Node();  
    while (curr.next != curr)  
    {  
        temp = curr;  
        curr = curr.next;  
        temp.next = curr.next;  

        // deleting soldier from the circular  
        // list who is killed in the fight.  
        temp = temp.next;  
        curr = temp;  
    }  

    // Returning the Luckiest soldier who  
    // remains alive.  
    int res = temp.data;  

    return res;  
}  

// Driver code  
public static void main(String args[])  
{  
    int N = 100;  
    System.out.println( alivesol(N) );  
}  
} 

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# code to find the luckiest person  
using System; 

class GFG  
{  

// Node structure  
public class Node  
{  
    public int data;  
    public Node next;  
};  

static Node newNode(int data)  
{  
    Node node = new Node();  
    node.data = data;  
    node.next = null;  
    return node;  
}  

// Function to find the luckiest person  
static int alivesol(int Num)  
{  
    if (Num == 1)  
        return 1;  

    // Create a single node circular  
    // linked list.  
    Node last = newNode(1);  
    last.next = last;  

    for (int i = 2; i <= Num; i++)  
    {  
        Node tem = newNode(i);  
        tem.next = last.next;  
        last.next = tem;  
        last = tem;  
    }  

    // Starting from first soldier.  
    Node curr = last.next;  

    // condition for evaluating the existence  
    // of single soldier who is not killed.  
    Node tem1 = new Node();  
    while (curr.next != curr)  
    {  
        tem1 = curr;  
        curr = curr.next;  
        tem1.next = curr.next;  

        // deleting soldier from the circular  
        // list who is killed in the fight.  
        tem1 = tem1.next;  
        curr = tem1;  
    }  

    // Returning the Luckiest soldier who  
    // remains alive.  
    int res = tem1.data;  

    return res;  
}  

// Driver code  
public static void Main(String []args)  
{  
    int N = 100;  
    Console.WriteLine( alivesol(N) );  
}  
}  

// This code is contributed by Arnab Kundu  

```

**输出**：

```
73

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。