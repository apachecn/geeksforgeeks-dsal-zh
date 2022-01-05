# 如何在 C++ STL 中使用列表实现堆栈

> 原文:[https://www . geesforgeks . org/如何使用 c-stl 中的列表实现堆栈/](https://www.geeksforgeeks.org/how-to-implement-a-stack-using-list-in-c-stl/)

在本文中，我们将讨论如何使用 [C++ STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 中的[列表](https://www.geeksforgeeks.org/list-cpp-stl/)来实现堆栈。

[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)是一个线性数据结构，如下所示。[后进先出法或后进先出法。](https://www.geeksforgeeks.org/lifo-last-in-first-out-approach-in-programming/)主要支持 4 大操作:
1。[推](https://www.geeksforgeeks.org/scala-stack-push-method-with-example/) : [将](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)一个元素推入堆栈。
2。[弹出](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/):按照后进先出顺序删除元素。
3。Top:返回堆栈顶部的元素。
4。空:返回堆栈是否为空。

下面是上述方法的实现:

## C++

```
// C++ implementation of stack
// using list STL
#include <bits/stdc++.h>
using namespace std;

template <typename T>
// templating it so that any data type can be used

class Stack {
public:
    list<T> l;
    int cs = 0;
    // current size of the stack

    // pushing an element into the stack
    void push(T d)
    {
        cs++;
        // increasing the current size of the stack
        l.push_front(d);
    }

    // popping an element from the stack
    void pop()
    {
        if (cs <= 0) {
            // cannot pop us stack does not contain an
            // elements
            cout << "Stack empty" << endl;
        }
        else {
            // decreasing the current size of the stack
            cs--;
            l.pop_front();
        }
    }

    // if current size is 0 then stack is empty
    bool empty() { return cs == 0; }

    // getting the element present at the top of the stack
    T top() { return l.front(); }
    int size()
    {
        // getting the size of the stack
        return cs;
    }

    // printing the elements of the stack
    void print()
    {
        for (auto x: l) {
            cout << x << endl;
        }
    }
};
int main()
{
    Stack<int> s;
    s.push(10); // pushing into the stack
    s.push(20);
    s.push(30);
    s.push(40);
    cout << "Current size of the stack is " << s.size()
         << endl;
    cout << "The top element of the stack is " << s.top()
         << endl;
    s.pop(); // popping from the stack
    cout << "The top element after 1 pop operation is "
         << s.top()
         << endl; // printing the top of the stack
    s.pop(); // popping
    cout << "The top element after 2 pop operations is "
         << s.top() << endl;
    cout << "Size of the stack after 2 pop operations is "
         << s.size() << endl;
    return 0;
}
```

**Output**

```
Current size of the stack is 4
The top element of the stack is 40
The top element after 1 pop operation is 30
The top element after 2 pop operations is 20
Size of the stack after 2 pop operations is 2

```

***时间复杂度:** O(1)适用于堆栈中的推送和弹出操作。*
***辅助空间:** O(N)*