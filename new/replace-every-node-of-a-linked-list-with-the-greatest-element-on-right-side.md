# 将链接列表的每个节点替换为右侧的最大元素

给定[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)，任务是为链表的每个节点查找[下一更大元素](https://www.geeksforgeeks.org/next-greater-element-in-same-order-as-input/)。
**注意：**对于没有下一个更大元素的节点，将-1存储在结果中。
**范例：**

> **输入：**链表= [2，1，5]
> **输出：** [5，5，-1]
> **输入：**链表 = [2，7，4，4，3，5]
> **输出：** [7，-1，5，5，-1]

**方法：**
要解决上述问题，主要思想是使用 [**堆栈数据结构**](https://www.geeksforgeeks.org/stack-data-structure/) 。

*   遍历链表，并将链表元素的值和位置插入堆栈。
*   为每个节点使用-1初始化结果向量。
*   当当前节点的值大于先前节点的值时，更新先前节点的值，并在更新后从堆栈中弹出该值。

下面是上述方法的实现：

## C ++

```

// C++ Program to find the
// Next Greater Element for
// a Linked List

#include <bits/stdc++.h>
using namespace std;

// Linked List Node
struct Node {
    int val;
    struct Node* next;
};

// Function to print
// next greater element
vector<int> nextLargerNodes(
    struct Node* head)
{
    int cur_pos = 0;

    stack<pair<int, int> > arr;

    vector<int> res;

    // Iterate for all
    // element in linked list
    while (head) {

        // Initialize every
        // position with 0
        res.push_back(-1);

        // Check if current value is
        // greater then update previous
        while (
            !arr.empty()
            && arr.top().second
                   < head->val) {

            res[arr.top().first]
                = head->val;
            arr.pop();
        }

        arr.push(make_pair(
            cur_pos,
            head->val));

        cur_pos++;

        // Increment the head pointer
        head = head->next;
    }

    // Return the final result
    return res;
}

// Utility function to
// create a new node
Node* newNode(int val)
{
    struct Node* temp = new Node;
    temp->val = val;
    temp->next = NULL;
    return temp;
}

// Driver Program
int main()
{
    struct Node* head = newNode(2);
    head->next = newNode(7);
    head->next->next = newNode(4);
    head->next->next->next = newNode(3);
    head->next->next->next->next = newNode(5);

    vector<int> ans;

    ans = nextLargerNodes(head);

    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << ", ";
    }
}

```

## 爪哇

```

// Java Program to find the
// Next Greater Element for
// a Linked List
import java.util.*;
class GFG{

// Linked List Node
static class Node 
{
  int val;
  Node next;
};

static class pair
{ 
  int first, second; 
  public pair(int first, 
              int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
} ;

// Function to print
// next greater element
static Vector<Integer> 
       nextLargerNodes(Node head)
{
  int cur_pos = 0;
  Stack<pair > arr = new Stack<>();
  Vector<Integer> res = new Vector<>();

  // Iterate for all
  // element in linked list
  while (head != null) 
  {
    // Initialize every
    // position with 0
    res.add(-1);

    // Check if current value is
    // greater then update previous
    while (!arr.isEmpty() && 
           arr.peek().second < 
           head.val) 
    {
      res.set(arr.peek().first,
              head.val);
      arr.pop();
    }

    arr.add(new pair(cur_pos, 
                     head.val));
    cur_pos++;

    // Increment the head 
    // pointer
    head = head.next;
  }

  // Return the final result
  return res;
}

// Utility function to
// create a new node
static Node newNode(int val)
{
  Node temp = new Node();
  temp.val = val;
  temp.next = null;
  return temp;
}

// Driver code
public static void main(String[] args)
{
  Node head = newNode(2);
  head.next = newNode(7);
  head.next.next = newNode(4);
  head.next.next.next = newNode(3);
  head.next.next.next.next = newNode(5);

  Vector<Integer> ans = new Vector<>();
  ans = nextLargerNodes(head);

  for (int i = 0; i < ans.size(); i++) 
  {
    System.out.print(ans.elementAt(i) + ", ");
  }
}
}

// This code is contributed by Princi Singh

```

## C＃

```

// C# Program to find the
// Next Greater Element for
// a Linked List
using System;
using System.Collections.Generic;
class GFG{

// Linked List Node
class Node 
{
  public int val;
  public Node next;
};

class pair
{ 
  public int first, second; 
  public pair(int first, 
              int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
} ;

// Function to print
// next greater element
static List<int> 
       nextLargerNodes(Node head)
{
  int cur_pos = 0;
  Stack<pair > arr = new Stack<pair>();
  List<int> res = new List<int>();

  // Iterate for all
  // element in linked list
  while (head != null) 
  {
    // Initialize every
    // position with 0
    res.Add(-1);

    // Check if current value is
    // greater then update previous
    while (arr.Count !=0  && 
           arr.Peek().second < 
           head.val) 
    {
      res[arr.Peek().first] = 
          head.val;
      arr.Pop();
    }

    arr.Push(new pair(cur_pos,  
                      head.val));
    cur_pos++;

    // Increment the head 
    // pointer
    head = head.next;
  }

  // Return the readonly result
  return res;
}

// Utility function to
// create a new node
static Node newNode(int val)
{
  Node temp = new Node();
  temp.val = val;
  temp.next = null;
  return temp;
}

// Driver code
public static void Main(String[] args)
{
  Node head = newNode(2);
  head.next = newNode(7);
  head.next.next = newNode(4);
  head.next.next.next = newNode(3);
  head.next.next.next.next = newNode(5);

  List<int> ans = new List<int>();
  ans = nextLargerNodes(head);

  for (int i = 0; i < ans.Count; i++) 
  {
    Console.Write(ans[i] + ", ");
  }
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
7, -1, 5, 5, -1,

```

***时间复杂度：** O（N）*
***辅助空间复杂度：** O（N）*

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。