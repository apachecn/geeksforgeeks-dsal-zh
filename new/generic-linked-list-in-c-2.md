# C

中的通用链接列表

与 [C ++](https://www.geeksforgeeks.org/c-plus-plus/) 和 [Java](https://www.geeksforgeeks.org/java/) 不同， [C](https://www.geeksforgeeks.org/c/) 不支持泛型。 如何在C中创建可用于任何数据类型的链表？ 在C语言中，我们可以使用[无效指针](http://geeksquiz.com/void-pointer-c/)和函数指针来实现相同的功能。 关于void指针的伟大之处在于它可以用于指向任何数据类型。 另外，所有类型的指针的大小始终是相同的，因此我们总是可以分配一个链表节点。 需要使用函数指针来处理存储在void指针指向的地址中的实际内容。

以下是示例C代码，以演示通用链表的工作。

```

// C program for generic linked list 
#include<stdio.h> 
#include<stdlib.h> 

/* A linked list node */
struct Node 
{ 
    // Any data type can be stored in this node 
    void  *data; 

    struct Node *next; 
}; 

/* Function to add a node at the beginning of Linked List. 
   This function expects a pointer to the data to be added 
   and size of the data type */
void push(struct Node** head_ref, void *new_data, size_t data_size) 
{ 
    // Allocate memory for node 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    new_node->data  = malloc(data_size); 
    new_node->next = (*head_ref); 

    // Copy contents of new_data to newly allocated memory. 
    // Assumption: char takes 1 byte. 
    int i; 
    for (i=0; i<data_size; i++) 
        *(char *)(new_node->data + i) = *(char *)(new_data + i); 

    // Change head pointer as new node is added at the beginning 
    (*head_ref)    = new_node; 
} 

/* Function to print nodes in a given linked list. fpitr is used 
   to access the function to be used for printing current node data. 
   Note that different data types need different specifier in printf() */
void printList(struct Node *node, void (*fptr)(void *)) 
{ 
    while (node != NULL) 
    { 
        (*fptr)(node->data); 
        node = node->next; 
    } 
} 

// Function to print an integer 
void printInt(void *n) 
{ 
   printf(" %d", *(int *)n); 
} 

// Function to print a float 
void printFloat(void *f) 
{ 
   printf(" %f", *(float *)f); 
} 

/* Driver program to test above function */
int main() 
{ 
    struct Node *start = NULL; 

    // Create and print an int linked list 
    unsigned int_size = sizeof(int); 
    int arr[] = {10, 20, 30, 40, 50}, i; 
    for (i=4; i>=0; i--) 
       push(&start, &arr[i], int_size); 
    printf("Created integer linked list is \n"); 
    printList(start, printInt); 

    // Create and print a float linked list 
    unsigned float_size = sizeof(float); 
    start = NULL; 
    float arr2[] = {10.1, 20.2, 30.3, 40.4, 50.5}; 
    for (i=4; i>=0; i--) 
       push(&start, &arr2[i], float_size); 
    printf("\n\nCreated float linked list is \n"); 
    printList(start, printFloat); 

    return 0; 
} 

```

输出：

```
Created integer linked list is
 10 20 30 40 50

Created float linked list is
 10.100000 20.200001 30.299999 40.400002 50.500000
```

本文由 **Himanshu Gupta** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。