# 在 C++中使用类模板实现堆栈

> 原文:[https://www . geesforgeks . org/implementing-stack-use-class-templates-in-CPP/](https://www.geeksforgeeks.org/implementing-stack-using-class-templates-in-cpp/)

任务是使用 C++中的类模板实现堆栈的一些重要功能，如 pop()、push()、display()、topElement()、isEmpty()、isFull()。[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)是一种线性数据结构，遵循执行操作的特定顺序。顺序可以是后进先出或后进先出。

简单的想法是将数据类型作为参数传递，这样我们就不需要为不同的数据类型编写相同的代码。例如，软件公司可能需要对不同的数据类型进行 sort()。我们可以编写一个 sort()并将数据类型作为参数传递，而不是编写和维护多个代码。

C++为支持模板增加了两个新关键词:*【模板】*和*【类型名】*。第二个关键字总是可以用关键字“*类*代替。

插图:

> 举个例子，食堂里的盘子叠在一起。位于顶部的板是第一个被移除的板，即已经放置在最底部位置的板在堆叠中保留最长的时间。因此，可以简单地看到它遵循后进先出/后进先出的顺序。

**示例:**

## c++ 14

```
// C++ Program to Implement stack using Class Templates

// Including input output libraries
#include <iostream>
// Header File including all string functions
#include <string>

using namespace std;

// Taking size of stack as 10
#define SIZE 5

// Class
// To represent stack using template by class
// taking class in template
template <class T> class Stack {
    // Pubic access modifier
public:
    // Empty constructor
    Stack();

    // Method 1
    // To add element to stack which can be any type
    // using stack push() operation
    void push(T k);

    // Method 2
    // To remove top element from stack
    // using pop() operation
    T pop();

    // Method 3
    // To print top element in stack
    // using peek() method
    T topElement();

    // Method 4
    // To check whether stack is full
    // using isFull() method
    bool isFull();

    // Method 5
    // To check whether stack is empty
    // using isEmpty() method
    bool isEmpty();

private:
    // Taking data member top
    int top;

    // Initialising stack(array) of given size
    T st[SIZE];
};

// Method 6
// To initialise top to
// -1(default constructor)
template <class T> Stack<T>::Stack() { top = -1; }

// Method 7
// To add element element k to stack
template <class T> void Stack<T>::push(T k)
{

    // Checking whether stack is completely filled
    if (isFull()) {
        // Display message when no elements can be pushed
        // into it
        cout << "Stack is full\n";
    }

    // Inserted element
    cout << "Inserted element " << k << endl;

    // Incrementing the top by unity as element
    // is to be inserted
    top = top + 1;

    // Now, adding element to stack
    st[top] = k;
}

// Method 8
// To check if the stack is empty
template <class T> bool Stack<T>::isEmpty()
{
    if (top == -1)
        return 1;
    else
        return 0;
}

// Utility methods

// Method 9
// To check if the stack is full or not
template <class T> bool Stack<T>::isFull()
{
    // Till top in inside the stack
    if (top == (SIZE - 1))
        return 1;
    else

        // As top can not exceeds th size
        return 0;
}

// Method 10
template <class T> T Stack<T>::pop()
{
    // Initialising a variable to store popped element
    T popped_element = st[top];

    // Decreasing the top as
    // element is getting out from the stack
    top--;

    // Returning the element/s that is/are popped
    return popped_element;
}

// Method 11
template <class T> T Stack<T>::topElement()
{
    // Initialising a variable to store top element
    T top_element = st[top];

    // Returning the top element
    return top_element;
}

// Method 12
// Main driver method
int main()
{

    // Creating object of Stack class in main() method
    // Declaring objects of type Integer and String
    Stack<int> integer_stack;
    Stack<string> string_stack;

    // Adding elements to integer stack object
    // Custom integer entries
    integer_stack.push(2);
    integer_stack.push(54);
    integer_stack.push(255);

    // Adding elements to string stack
    // Custom string entries
    string_stack.push("Welcome");
    string_stack.push("to");
    string_stack.push("GeeksforGeeks");

    // Now, removing element from integer stack
    cout << integer_stack.pop() << " is removed from stack"
         << endl;

    // Removing top element from string stack
    cout << string_stack.pop() << " is removed from stack "
         << endl;

    // Print and display the top element in integer stack
    cout << "Top element is " << integer_stack.topElement()
         << endl;

    // Print and display the top element in string stack
    cout << "Top element is " << string_stack.topElement()
         << endl;

    return 0;
}
```

**输出**

```
Inserted element 2
Inserted element 54
Inserted element 255
Inserted element Welcome
Inserted element to
Inserted element GeeksforGeeks
255 is removed from stack
GeeksforGeeks is removed from stack 
Top element is 54
Top element is to
```

**输出解释:**

这里，两种数据类型(整数和字符串)使用单个堆栈类实现。首先取两个对象，一个是整数类，第二个是字符串类，使用栈类的 *push()* 和 *isFull()* 方法在两个类中插入元素。使用堆栈类的 pop 和 *isEmpty()* 函数移除元素。最后，使用 top element()函数为每个类打印 top 元素。