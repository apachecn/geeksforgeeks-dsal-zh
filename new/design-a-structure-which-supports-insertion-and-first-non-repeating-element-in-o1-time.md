# 设计一种在`O(1)`时间内支持插入和第一个非重复元素的结构

设计一个[数据结构](https://www.geeksforgeeks.org/data-structures/)，该数据结构支持`O(1)`时间中的插入和第一个非重复元素。 数据结构支持的操作：

*   **插入**：将元素插入数据结构。

*   **第一个非重复元素**：数组中的第一个非重复元素。

**注意：**如果数组中没有非重复元素，则打印-1。

考虑以下自定义数据结构：

> **插入（4）：** [4]
> **插入（1）：** [4，1]
> **插入（4）：** [4， 1，4]
> 
> **第一个非重复元素：** 1

这个想法是使用[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)和[哈希图](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)来维护数组元素的频率。 以下是此数据结构中的哈希映射和双链表的用例：

*   **双链表：**跟踪阵列中的非重复元素。

*   **哈希图**跟踪双链表中元素的出现以及非重复元素的地址

以下是操作说明：

*   **插入：**将元素插入到数组中，然后将元素的频率检查到映射中。 如果以前发生过，请借助哈希映射中存储的地址从双向链接列表中删除该元素。 最后，将元素的出现增加到哈希图中。

*   **第一个非重复元素：**数组的第一个非重复元素将是双链表的第一个元素。

**此数据结构的优点：**

*  `O(1)`时间中的插入和第一个非重复元素。

**此数据结构的缺点：**

*   无法跟踪元素的顺序。

*   自定义数据结构将需要自定义 Hasp 映射，以将元素存储到映射中。

*   内存不足

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of a structure 
// which supports insertion, deletion 
// and first non-repeating element  
// in constant time 

#include <bits/stdc++.h> 

using namespace std; 

// Node for doubly  
// linked list 
struct node { 

    // Next pointer 
    struct node* next; 

    // Previous pointer 
    struct node* prev;  

    // Value of node 
    int data;  
}; 

// Head and tail pointer  
// for doubly linked list 
struct node *head = NULL, *tail = NULL; 

// Occurences map container  
// to count for occurence  
// of the element 
map<int, int> occurrences; 

// Address map container  
// to store nodes of the  
// list which are unique 
map<int, node*> address; 

// Function to insert the element 
// into the given data-structure 
void insert(int value) 
{ 
    // Increasing count of  
    // value to be inserted 
    occurrences[value]++; 

    // If count of element is  
    // exactly 1 and is yet 
    // not inserted in the list, 
    // we insert value in list 
    if (occurrences[value] == 1 &&  
        address.find(value) == address.end()) { 
        struct node* temp =  
            (struct node*)malloc(sizeof(struct node)); 
        temp->next = NULL; 
        temp->prev = NULL; 
        temp->data = value; 

        // Storing node mapped  
        // to its value in  
        // address map container 
        address[value] = temp; 

        // Inserting first element 
        if (head == NULL) 
        { 
            head = temp; 
            tail = temp; 
        } 
        else
        { 
            // Appending  
            // element at last 
            tail->next = temp; 
            temp->prev = tail; 
            tail = temp; 
        } 
    } 

    // if occurrence of particular  
    // value becomes >1 and, 
    // it is present in address  
    // container(which means 
    // it is not yet deleted) 
    else if (occurrences[value] > 1 &&  
        address.find(value) != address.end()) { 

        // Taking node to be deleted 
        struct node* temp = address[value]; 

        // Erasing its value from  
        // map to keep track that  
        // this element is deleted 
        address.erase(value); 

        // Deleting node in  
        // doubly linked list 
        if (temp == head) { 
            temp = head; 
            head = head->next; 
            free(temp); 
        } 
        else if (temp == tail) { 
            temp = tail; 
            tail->prev->next = NULL; 
            free(temp); 
        } 
        else { 
            temp->next->prev = temp->prev; 
            temp->prev->next = temp->next; 
            free(temp); 
        } 
    } 
} 

// Function to find the first 
// unique element from list 
void findUniqueNumber() 
{ 
    // No element in list 
    if (head == NULL) 
        cout << "-1\n"; 

    // Head node contains  
    // unique number 
    else
        cout << head->data << "\n"; 
} 

// Driver Code 
int main() 
{ 
    // Inserting element in list 
    insert(4); 
    insert(1); 
    insert(4); 

    // Finding the first  
    // unique number 
    findUniqueNumber(); 
    cout << "\n"; 
    return 0; 
} 

```

**Output:**

```
1

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。