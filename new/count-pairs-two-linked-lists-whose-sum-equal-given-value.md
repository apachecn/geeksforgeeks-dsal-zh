# 来自两个链表的计数对，其总和等于给定值

给定两个链表（可以排序或不排序），它们的大小分别为 **n1** 和 **n2** 。 给定值 **x** 。 问题是要计算两个列表中总和等于给定值 **x** 的所有对。

**注意**：该对具有每个链接列表中的元素。

例子：

```
Input : list1 = 3->1->5->7
        list2 = 8->2->5->3
        x = 10
Output : 2
The pairs are:
(5, 5) and (7, 3)

Input : list1 = 4->3->5->7->11->2->1
        list2 = 2->3->4->5->6->8-12
        x = 9         
Output : 5

```

**方法 1（天真方法）**：使用两个循环从两个链表中选择元素，并检查该对的总和是否等于 **x** 。

## C / C++

```cpp

// C++ implementation to count pairs from both linked  
// lists  whose sum is equal to a given value 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node 
{ 
  int data; 
  struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
  /* allocate node */
  struct Node* new_node = 
          (struct Node*) malloc(sizeof(struct Node)); 

  /* put in the data  */
  new_node->data  = new_data; 

  /* link the old list to the new node */
  new_node->next = (*head_ref); 

  /* move the head to point to the new node */
  (*head_ref)    = new_node; 
} 

// function to count all pairs from both the linked lists 
// whose sum is equal to a given value 
int countPairs(struct Node* head1, struct Node* head2, int x) 
{ 
    int count = 0; 

    struct Node *p1, *p2; 

    // traverse the 1st linked list 
    for (p1 = head1; p1 != NULL; p1 = p1->next) 

        // for each node of 1st list 
        // traverse the 2nd list 

        for (p2 = head2; p2 != NULL; p2 = p2->next) 

            // if sum of pair is equal to 'x' 
            // increment count 
            if ((p1->data + p2->data) == x) 
                count++;             

    // required count of pairs      
    return count; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 

    // create linked list1 3->1->5->7 
    push(&head1, 7); 
    push(&head1, 5); 
    push(&head1, 1); 
    push(&head1, 3);     

    // create linked list2 8->2->5->3 
    push(&head2, 3); 
    push(&head2, 5); 
    push(&head2, 2); 
    push(&head2, 8); 

    int x = 10; 

    cout << "Count = "
         << countPairs(head1, head2, x); 
    return 0; 
}  

```

## Java

```java

// Java implementation to count pairs from both linked  
// lists  whose sum is equal to a given value 

// Note : here we use java.util.LinkedList for  
// linked list implementation 

import java.util.Arrays; 
import java.util.Iterator; 
import java.util.LinkedList; 

class GFG  
{ 
    // method to count all pairs from both the linked lists 
    // whose sum is equal to a given value 
    static int countPairs(LinkedList<Integer> head1, LinkedList<Integer> head2, int x) 
    { 
        int count = 0; 

        // traverse the 1st linked list 
        Iterator<Integer> itr1 = head1.iterator(); 
        while(itr1.hasNext()) 
        { 
            // for each node of 1st list 
            // traverse the 2nd list 
            Iterator<Integer> itr2 = head2.iterator(); 
            Integer t = itr1.next(); 
            while(itr2.hasNext()) 
            { 
                // if sum of pair is equal to 'x' 
                // increment count 
                if ((t + itr2.next()) == x) 
                    count++;  
            } 
        } 

        // required count of pairs      
        return count; 
    } 

    // Driver method 
    public static void main(String[] args)  
    { 
        Integer arr1[] = {3, 1, 5, 7}; 
        Integer arr2[] = {8, 2, 5, 3}; 

        // create linked list1 3->1->5->7 
        LinkedList<Integer> head1 = new LinkedList<>(Arrays.asList(arr1)); 

        // create linked list2 8->2->5->3 
        LinkedList<Integer> head2 = new LinkedList<>(Arrays.asList(arr2)); 

        int x = 10; 

        System.out.println("Count = " + countPairs(head1, head2, x)); 
    }     
} 

```

## Python3

```py

# Python3 implementation to count pairs from both linked  
# lists whose sum is equal to a given value 

# A Linked list node  
class Node:  
    def __init__(self,data):  
        self.data = data  
        self.next = None

# function to insert a node at the 
# beginning of the linked list 

def push(head_ref,new_data): 
    new_node=Node(new_data) 
    #new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# function to count all pairs from both the linked lists 
# whose sum is equal to a given value 
def countPairs(head1, head2, x): 
    count = 0

    #struct Node p1, p2 

    # traverse the 1st linked list 
    p1 = head1 
    while(p1 != None): 

        # for each node of 1st list 
        # traverse the 2nd list 
        p2 = head2 
        while(p2 != None): 

            # if sum of pair is equal to 'x' 
            # increment count 
            if ((p1.data + p2.data) == x): 
                count+=1
            p2 = p2.next

        p1 = p1.next
    # required count of pairs      
    return count 

# Driver program to test above 
if __name__=='__main__':  

    head1 = None
    head2 = None

    # create linked list1 3.1.5.7 
    head1=push(head1, 7) 
    head1=push(head1, 5) 
    head1=push(head1, 1) 
    head1=push(head1, 3)  

    # create linked list2 8.2.5.3 
    head2=push(head2, 3) 
    head2=push(head2, 5) 
    head2=push(head2, 2) 
    head2=push(head2, 8) 

    x = 10

    print("Count = ",countPairs(head1, head2, x)) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# implementation to count pairs from both linked  
// lists whose sum is equal to a given value 
using System; 
using System.Collections.Generic;  

// Note : here we use using System.Collections.Generic for  
// linked list implementation 
class GFG  
{ 
    // method to count all pairs from both the linked lists 
    // whose sum is equal to a given value 
    static int countPairs(List<int> head1, List<int> head2, int x) 
    { 
        int count = 0; 

        // traverse the 1st linked list 

        foreach(int itr1 in head1) 
        { 
            // for each node of 1st list 
            // traverse the 2nd list 
            int t = itr1; 
            foreach(int itr2 in head2) 
            { 
                // if sum of pair is equal to 'x' 
                // increment count 
                if ((t + itr2) == x) 
                    count++;  
            } 
        } 

        // required count of pairs      
        return count; 
    } 

    // Driver code 
    public static void Main(String []args)  
    { 
        int []arr1 = {3, 1, 5, 7}; 
        int []arr2 = {8, 2, 5, 3}; 

        // create linked list1 3->1->5->7 
        List<int> head1 = new List<int>(arr1); 

        // create linked list2 8->2->5->3 
        List<int> head2 = new List<int>(arr2); 

        int x = 10; 

    Console.WriteLine("Count = " + countPairs(head1, head2, x)); 
    }  
} 

// This code is contributed by 29AjayKumar  

```

**Output:**

```
Count = 2

```

**时间复杂度**：O（n1 * n2）

**辅助空间**：O（1）

**方法 2（排序）**：使用合并排序技术以升序对第一个链接列表和降序排列第二个[列表。 现在，按照以下方式从左到右遍历两个列表：](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

**算法**：

```
countPairs(list1, list2, x)
  Initialize count = 0
  while list != NULL and list2 != NULL
     if (list1->data + list2->data) == x
        list1 = list1->next    
        list2 = list2->next
        count++
    else if (list1->data + list2->data) > x
        list2 = list2->next
    else
        list1 = list1->next

  return count     

```

为简单起见，下面给出的实现假定 list1 以升序排序，list2 以降序排序。

## C / C++

```cpp

// C++ implementation to count pairs from both linked  
// lists  whose sum is equal to a given value 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node 
{ 
  int data; 
  struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
  /* allocate node */
  struct Node* new_node = 
          (struct Node*) malloc(sizeof(struct Node)); 

  /* put in the data  */
  new_node->data  = new_data; 

  /* link the old list to the new node */
  new_node->next = (*head_ref); 

  /* move the head to point to the new node */
  (*head_ref)    = new_node; 
} 

// function to count all pairs from both the linked  
// lists whose sum is equal to a given value 
int countPairs(struct Node* head1, struct Node* head2, 
                                              int x) 
{ 
    int count = 0; 

    // sort head1 in ascending order and 
    // head2 in descending order 
    // sort (head1), sort (head2) 
    // For simplicity both lists are considered to be  
    // sorted in the respective orders 

    // traverse both the lists from left to right 
    while (head1 != NULL && head2 != NULL) 
    { 
        // if this sum is equal to 'x', then move both  
        // the lists to next nodes and increment 'count' 
        if ((head1->data + head2->data) == x) 
        { 
            head1 = head1->next; 
            head2 = head2->next; 
            count++;     
        }     

        // if this sum is greater than x, then 
        // move head2 to next node 
        else if ((head1->data + head2->data) > x) 
            head2 = head2->next; 

        // else move head1 to next node     
        else
            head1 = head1->next; 
    }         

    // required count of pairs      
    return count; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 

    // create linked list1 1->3->5->7 
    // assumed to be in ascending order 
    push(&head1, 7); 
    push(&head1, 5); 
    push(&head1, 3); 
    push(&head1, 1);     

    // create linked list2 8->5->3->2 
    // assumed to be in descending order 
    push(&head2, 2); 
    push(&head2, 3); 
    push(&head2, 5); 
    push(&head2, 8); 

    int x = 10; 

    cout << "Count = "
         << countPairs(head1, head2, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count pairs from both linked  
// lists  whose sum is equal to a given value 

// Note : here we use java.util.LinkedList for  
// linked list implementation 

import java.util.Arrays; 
import java.util.Collections; 
import java.util.Iterator; 
import java.util.LinkedList; 

class GFG  
{ 
    // method to count all pairs from both the linked lists 
    // whose sum is equal to a given value 
    static int countPairs(LinkedList<Integer> head1, LinkedList<Integer> head2, int x) 
    { 
        int count = 0; 

        // sort head1 in ascending order and 
        // head2 in descending order 
        Collections.sort(head1); 
        Collections.sort(head2,Collections.reverseOrder()); 

        // traverse both the lists from left to right 
        Iterator<Integer> itr1 = head1.iterator(); 
        Iterator<Integer> itr2 = head2.iterator(); 

        Integer num1 = itr1.hasNext() ? itr1.next() : null; 
        Integer num2 = itr2.hasNext() ? itr2.next() : null; 

        while(num1 != null && num2 != null) 
        {      

            // if this sum is equal to 'x', then move both  
            // the lists to next nodes and increment 'count' 

            if ((num1 + num2) == x) 
            { 
                num1 = itr1.hasNext() ? itr1.next() : null; 
                num2 = itr2.hasNext() ? itr2.next() : null; 

                count++;  
            }  

            // if this sum is greater than x, then 
            // move itr2 to next node 
            else if ((num1 + num2) > x) 
                num2 = itr2.hasNext() ? itr2.next() : null; 

            // else move itr1 to next node  
            else
                num1 = itr1.hasNext() ? itr1.next() : null; 

        } 

        // required count of pairs      
        return count; 
    } 

    // Driver method 
    public static void main(String[] args)  
    { 
        Integer arr1[] = {3, 1, 5, 7}; 
        Integer arr2[] = {8, 2, 5, 3}; 

        // create linked list1 3->1->5->7 
        LinkedList<Integer> head1 = new LinkedList<>(Arrays.asList(arr1)); 

        // create linked list2 8->2->5->3 
        LinkedList<Integer> head2 = new LinkedList<>(Arrays.asList(arr2)); 

        int x = 10; 

        System.out.println("Count = " + countPairs(head1, head2, x)); 
    }     
} 

```

**Output:**

```
Count = 2

```

**时间复杂度**：O（n1 * logn1）+ O（n2 * logn2）

**辅助空间**：O（1）

排序将更改节点的顺序。 如果顺序很重要，则可以创建和使用链接列表的副本。

**方法 3（哈希）**：哈希表是使用 C++ 中的 [unordered_set 实现的。 我们将所有第一个链接列表元素存储在哈希表中。 对于第二个链表的元素，我们从 **x** 中减去每个元素，然后在哈希表中检查结果。 如果结果存在，我们将增加**计数**。](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)

## C++

```cpp

// C++ implementation to count pairs from both linked   
// lists whose sum is equal to a given value 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node 
{ 
  int data; 
  struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
  /* allocate node */
  struct Node* new_node = 
          (struct Node*) malloc(sizeof(struct Node)); 

  /* put in the data  */
  new_node->data  = new_data; 

  /* link the old list to the new node */
  new_node->next = (*head_ref); 

  /* move the head to point to the new node */
  (*head_ref)    = new_node; 
} 

// function to count all pairs from both the linked  
// lists whose sum is equal to a given value 
int countPairs(struct Node* head1, struct Node* head2,  
                                               int x) 
{ 
    int count = 0; 

    unordered_set<int> us; 

    // insert all the elements of 1st list 
    // in the hash table(unordered_set 'us') 
    while (head1 != NULL) 
    { 
        us.insert(head1->data);     

        // move to next node     
        head1 = head1->next; 
    } 

    // for each element of 2nd list 
    while (head2 != NULL)     
    { 
        // find (x - head2->data) in 'us' 
        if (us.find(x - head2->data) != us.end()) 
            count++; 

        // move to next node 
        head2 = head2->next;     
    } 
    // required count of pairs      
    return count; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 

    // create linked list1 3->1->5->7 
    push(&head1, 7); 
    push(&head1, 5); 
    push(&head1, 1); 
    push(&head1, 3);     

    // create linked list2 8->2->5->3 
    push(&head2, 3); 
    push(&head2, 5); 
    push(&head2, 2); 
    push(&head2, 8); 

    int x = 10; 

    cout << "Count = "
         << countPairs(head1, head2, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count pairs from both linked  
// lists  whose sum is equal to a given value 

// Note : here we use java.util.LinkedList for  
// linked list implementation 

import java.util.Arrays; 
import java.util.HashSet; 
import java.util.Iterator; 
import java.util.LinkedList; 

class GFG  
{ 
    // method to count all pairs from both the linked lists 
    // whose sum is equal to a given value 
    static int countPairs(LinkedList<Integer> head1, LinkedList<Integer> head2, int x) 
    { 
        int count = 0; 

        HashSet<Integer> us = new HashSet<Integer>(); 

        // insert all the elements of 1st list 
        // in the hash table(unordered_set 'us') 
        Iterator<Integer> itr1 = head1.iterator(); 
        while (itr1.hasNext()) 
        { 
            us.add(itr1.next());     

        } 

        Iterator<Integer> itr2 = head2.iterator(); 
        // for each element of 2nd list 
        while (itr2.hasNext())     
        { 
            // find (x - head2->data) in 'us' 
            if (!(us.add(x - itr2.next()))) 
                count++; 

        } 

        // required count of pairs      
        return count; 
    } 

    // Driver method 
    public static void main(String[] args)  
    { 
        Integer arr1[] = {3, 1, 5, 7}; 
        Integer arr2[] = {8, 2, 5, 3}; 

        // create linked list1 3->1->5->7 
        LinkedList<Integer> head1 = new LinkedList<>(Arrays.asList(arr1)); 

        // create linked list2 8->2->5->3 
        LinkedList<Integer> head2 = new LinkedList<>(Arrays.asList(arr2)); 

        int x = 10; 

        System.out.println("Count = " + countPairs(head1, head2, x)); 
    }     
} 

```

## C#

```cs

// C# implementation to count pairs from both linked  
// lists whose sum is equal to a given value 

// Note : here we use java.util.LinkedList for  
// linked list implementation 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    // method to count all pairs from both the linked lists 
    // whose sum is equal to a given value 
    static int countPairs(List<int> head1, List<int> head2, int x) 
    { 
        int count = 0; 

        HashSet<int> us = new HashSet<int>(); 

        // insert all the elements of 1st list 
        // in the hash table(unordered_set 'us') 
        foreach(int itr1 in head1) 
        { 
            us.Add(itr1);  

        } 

        // for each element of 2nd list 
        foreach(int itr2 in head2)  
        { 
            // find (x - head2->data) in 'us' 
            if (!(us.Contains(x - itr2))) 
                count++; 

        } 

        // required count of pairs      
        return count; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        int []arr1 = {3, 1, 5, 7}; 
        int []arr2 = {8, 2, 5, 3}; 

        // create linked list1 3->1->5->7 
        List<int> head1 = new List<int>(arr1); 

        // create linked list2 8->2->5->3 
        List<int> head2 = new List<int>(arr2); 

        int x = 10; 

        Console.WriteLine("Count = " + countPairs(head1, head2, x)); 
    }  
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
Count = 2

```

**时间复杂度**：O（n1 + n2）

**辅助空间**：O（n1），应为较小的数组创建哈希表，以降低空间复杂度 。

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

