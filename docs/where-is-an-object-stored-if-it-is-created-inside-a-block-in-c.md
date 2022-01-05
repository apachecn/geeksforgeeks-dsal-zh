# 如果一个对象是在 C++中的一个块内创建的，那么它存储在哪里？

> 原文:[https://www . geeksforgeeks . org/如果对象是在 c 块内部创建的，则该对象存储在哪里/](https://www.geeksforgeeks.org/where-is-an-object-stored-if-it-is-created-inside-a-block-in-c/)

内存中有两部分可以存储对象:

1.  **堆栈**–堆栈中的内存由块/函数内部声明的所有成员使用。注意，main 也是一个函数。
2.  **堆**–该内存未使用，可用于运行时动态分配内存。

在块或函数内部创建的对象的范围仅限于创建它的块。

*   块内创建的对象将存储在**堆栈**中，当函数/块退出时，对象将被销毁并从堆栈中移除。
*   但是如果我们在运行时创建对象，即通过**动态内存分配**，那么该对象将存储在**堆**上。这是在**新**操作员的帮助下完成的。在这种情况下，我们需要使用**删除**操作符显式销毁对象。

示例:

```
Output:
Inside Block1...
length of rectangle is : 2
width  of rectangle  is :3
Destructor of rectangle
with the exit of the block, destructor called
automatically for the object stored in stack.
*********************************************
Inside Block2
length of rectangle is : 5
width of rectangle  is :6
Destructor of rectangle
length of rectangle is : 0
width of rectangle is :0

```

下面是显示对象存储位置的程序:

```
// C++ program for required implementation
#include <iostream>
using namespace std;

class Rectangle {
    int width;
    int length;

public:
    Rectangle()
    {
        length = 0;
        width = 0;
    }

    Rectangle(int l, int w)
    {
        length = l;
        width = w;
    }

    ~Rectangle()
    {
        cout << "Destructor of rectangle" << endl;
    }

    int getLength()
    {
        return length;
    }

    int getWidth()
    {
        return width;
    }
};

int main()
{
    // Object creation inside block
    {

        Rectangle r(2, 3); // r is stored on stack
        cout << "Inside Block1..." << endl;
        cout << "length of rectangle is : " 
             << r.getLength() << endl;
        cout << "width  of rectangle  is :" 
             << r.getWidth() << endl;
    }

    cout << " with the exit of the block, destructor\n"
         << " called automatically for the object stored in stack." 
         << endl;

         /* 
          // uncomment  this code and run once you will get
         // the compilation error because the object is not in scope
         cout<<"length of rectangle is : "<< r.getLength();
         cout<< "width of rectangle is :" << r.getWidth();
        */

    Rectangle* ptr2;
    {
        // object will be stored in heap  
        // and pointer variable since its local
        // to block will be stored in the stack

        Rectangle* ptr3 = new Rectangle(5, 6);
        ptr2 = ptr3;
        cout << "********************************************"
             << endl;
        cout << "Inside Block2" << endl;
        cout << "length of rectangle is : " 
             << ptr3->getLength() << endl;
        cout << "width of rectangle  is :" 
             << ptr3->getWidth() << endl;

        // comment below line of code and 
        // uncomment *important line* 
        // and then check the object will remain
        // alive outside the block.

        // explicitly destroy object stored on the heap
        delete ptr3; 
    }

    cout << "length of rectangle is : " 
         << ptr2->getLength() << endl;

    cout << "width of rectangle is :" 
         << ptr2->getWidth() << endl;

     // delete ptr2;   /* important line*/

    return 0;
}
```

**Output:**

```
Inside Block1...
length of rectangle is : 2
width  of rectangle  is :3
Destructor of rectangle
 with the exit of the block, destructor
 called automatically for the object stored in stack.
********************************************
Inside Block2
length of rectangle is : 5
width of rectangle  is :6
Destructor of rectangle
length of rectangle is : 0
width of rectangle is :0

```