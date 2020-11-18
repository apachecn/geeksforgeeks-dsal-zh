# 运算符在链接列表类

中重载了'< >运算符

**先决条件：C++中的** [运算符重载](https://www.geeksforgeeks.org/operator-overloading-c/)和[在 C++中的链接列表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)

C++附带的库提供了执行[输入和输出](https://www.geeksforgeeks.org/basic-input-output-c/)的方法。 在 C++中，输入和输出以字节序列（也称为流）的形式执行。 [输入和输出流](https://www.geeksforgeeks.org/basic-input-output-c/)由 iostream 库管理。 **cin** 和 **cout** 是输入流和输出流的标准对象。

我们可以重载**'> >'**和**'< <'**运算符，以在[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)中输入 并在 C++中打印[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)中的元素。 它具有为运算符提供针对数据类型的特殊含义的能力，此功能称为[运算符重载](http://www.geeksforgeeks.org/operator-overloading-c/)。

重载运算符的语法为：

```
returnType operator symbol (arguments)
{
   Operations...
} 

```

**<u>重载 istream 运算符“ > >”：</u>**

```

istream& operator>>(istream& is, node*& head) 
{ 
    // Function call to overload the ">>" 
    // operator 
    takeInput(head); 
} 

```

**说明**：

上面函数的返回类型是对 istream 对象的引用。 在陈述中：[ **cin > >头；** “，cin 是该功能的第一个参数，对头部的引用是第二个参数。 当执行任何这样的语句时，将调用上述函数。

**<u>重载了 ostream 运算符'< <'：</u>**

```

ostream& operator<<(ostream& os, node* head) 
{ 
    // Function call to overload the "<<" 
    // operator 
    print(head); 
} 

```

**说明**：

上面函数的返回类型是对 ostream 对象的引用。 在陈述中 **cout < <头；** “，cout 是该功能的第一个参数，对 head 的引用是第二个参数。 当执行任何这样的语句时，将调用上述函数。

**<u>用于重载“ < >”运算符的代码：</u>**

以下是**'> >'**和**'< <'**运算符的重载代码，其使用数字 **N** 作为 连续输入并在链接列表中插入数字 **N** ，直到 **N** = -1。

```

// C++ program to demonstrate the 
// overloading of '<<' and '>>' 
// operators 
#include <iostream> 
using namespace std; 

// Class for each node object 
// of the linked list 
class node { 
public: 
    // Node of the linked list 
    int data; 
    node* next; 

    // Constructor of node class 
    node(int d) 
    { 
        data = d; 
        next = NULL; 
    } 
}; 

// Insert a node at head of linked 
// list 
void insertAtHead(node*& head, int d) 
{ 
    node* n = new node(d); 
    n->next = head; 
    head = n; 
} 

// Insert a node at tail of linked 
// list 
void insertAtTail(node* head, int data) 
{ 
    // Make new node using 
    // constructor 
    node* n = new node(data); 
    node* temp = head; 

    // Traverse till we get to end of 
    // the linked list 
    while (temp->next != NULL) 
        temp = temp->next; 

    // Append the new node n at the end 
    // of the linked list 
    temp->next = n; 
} 

// Print the node at the linked list 
void print(node* head) 
{ 
    // Print the first Node 
    if (head != NULL) { 
        cout << head->data; 
        head = head->next; 
    } 

    // Traverse till head traverse 
    // till end 
    while (head != NULL) { 
        cout << "->" << head->data; 
        head = head->next; 
    } 
} 

// Function that takes continuous input 
// until user enter -1 while initializing 
// the linked list. 
void takeInput(node*& head) 
{ 
    int n; 
    cin >> n; 

    // If n is not equals to -1 insert 
    // the node in the linked list 
    while (n != -1) { 

        // If head is NULL, insert at 
        // the beginning of list 
        if (head == NULL) 
            insertAtHead(head, n); 
        else
            insertAtTail(head, n); 
        cin >> n; 
    } 
} 

// Overloading the ostream operator '<<' 
// to print the complete linked list from 
// beginning 
ostream& operator<<(ostream& os, node* head) 
{ 
    print(head); 
} 

// Overloading the istream operator '>>' 
// to take continuous input into the linked 
// list until user inputs -1 
istream& operator>>(istream& is, node*& head) 
{ 
    takeInput(head); 
} 

// Driver Code 
int main() 
{ 
    // initialise head to NULL 
    node* head = NULL; 

    // Overloading of '>>' for inserting 
    // element in the linked list 
    cin >> head; 

    // Overloading of '<<' for printing 
    // element in the linked list 
    cout << head; 
    return 0; 
} 

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。