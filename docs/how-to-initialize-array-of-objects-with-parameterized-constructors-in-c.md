# 如何在 C++中用参数化构造函数初始化对象数组

> 原文:[https://www . geeksforgeeks . org/如何使用参数化构造函数初始化对象数组/](https://www.geeksforgeeks.org/how-to-initialize-array-of-objects-with-parameterized-constructors-in-c/)

**<u>对象数组:</u>**
定义类时，只定义对象的规范；没有分配内存或存储空间。要使用类中定义的数据和访问函数，需要创建对象。

**语法:**

```
ClassName ObjectName[number of objects];
```

**<u>初始化对象数组的不同方法</u>** [**<u>参数化构造函数</u>**](https://www.geeksforgeeks.org/constructors-c/)**<u>:</u>**

1.**使用** **<u>一堆函数调用</u>** 作为数组的**元素:**就像普通的数组声明一样，但是这里我们用构造函数的函数调用作为该数组的元素来初始化数组。

## C++

```
#include <iostream>
using namespace std;

class Test {
    // private variables.
private:
    int x, y;

public:
    // parameterized constructor
    Test(int cx, int cy)
    {
        x = cx;
        y = cy;
    }
    // method to add two numbers
    void add() { cout << x + y << endl; }
};
int main()
{
    // Initializing 3 array Objects with function calls of
  // parameterized constructor as elements of that array
    Test obj[] = { Test(1, 1), Test(2, 2), Test(3, 3) };

    // using add method for each of three elements.
    for (int i = 0; i < 3; i++) {
        obj[i].add();
    }

    return 0;
}
```

2.**使用**[**malloc()**](https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/)**:**要避免调用非参数化的构造函数，请使用 malloc()方法。C++中的“malloc”或“内存分配”方法用于动态分配指定大小的单个大内存块。它返回一个 void 类型的指针，该指针可以转换成任何形式的指针。

## C++

```
#include <iostream>
#define N 5

using namespace std;

class Test {
    // private variables
    int x, y;

public:
    // parameterized constructor
    Test(int x, int y)
    {
        this->x = x;
        this->y = y;
    }

    // function to print
    void print() { cout << x << " " << y << endl; }
};

int main()
{
    // allocating dynamic array
    // of Size N using malloc()
    Test* arr = (Test*)malloc(sizeof(Test) * N);

    // calling constructor
    // for each index of array
    for (int i = 0; i < N; i++) {
        arr[i] = Test(i, i + 1);
    }

    // printing contents of array
    for (int i = 0; i < N; i++) {
        arr[i].print();
    }

    return 0;
}
```

**Output:** 

```
0 1
1 2
2 3
3 4
4 5
```

3.**使用** [**新关键字**](https://www.geeksforgeeks.org/new-vs-operator-new-in-cpp/) **:** 新运算符表示对堆内存分配的请求。如果有足够的内存可用，新操作符初始化内存，并将新分配和初始化的内存的地址返回给指针变量。这里，指针变量是数据类型的指针。数据类型可以是任何内置的数据类型，包括数组，也可以是任何用户定义的数据类型，包括结构和类。

对于动态初始化，如果我们添加参数化构造函数，新关键字需要非参数化构造函数。所以我们将为它使用一个伪构造函数。

## C++

```
#include <iostream>
#define N 5

using namespace std;

class Test {
    // private variables
    int x, y;

public:
    // dummy constructor
    Test() {}

    // parameterised constructor

    Test(int x, int y)
    {
        this->x = x;
        this->y = y;
    }

    // function to print
    void print() { cout << x << " " << y << endl; }
};

int main()
{
    // allocating dynamic array
    // of Size N using new keyword
    Test* arr = new Test[N];

    // calling constructor
    // for each index of array
    for (int i = 0; i < N; i++) {
        arr[i] = Test(i, i + 1);
    }

    // printing contents of array
    for (int i = 0; i < N; i++) {
        arr[i].print();
    }

    return 0;
}
```

**Output:** 

```
0 1
1 2
2 3
3 4
4 5
```

如果我们不使用虚拟构造函数，编译器会显示下面给出的错误

**编译器错误:**

```
error: no matching function for call to ‘Test::Test()’
     Test *arr=new Test[N];
```

4.**使用** [**双指针(指针指向指针概念)**](https://www.geeksforgeeks.org/double-pointer-pointer-pointer-c/) **:** 指向一个指针的指针是多个间接指向的一种形式，或者是一个指针链。通常，指针包含变量的地址。当我们定义一个指向指针的指针时，第一个指针包含第二个指针的地址，它指向包含实际值的位置，如下所示。
这里我们可以分配一些要分配的块，因此对于每个索引，我们必须使用 new 关键字调用参数化构造函数来初始化。

## C++

```
#include <iostream>
#define N 5

using namespace std;

class Test {
    // private variables
    int x, y;

public:
    // parameterized constructor

    Test(int x, int y)
        : x(x)
        , y(y)
    {
    }

    // function to print
    void print() { cout << x << " " << y << endl; }
};

int main()
{
    // allocating array using
    // pointer to pointer concept
    Test** arr = new Test*[N];

    // calling constructor for each index
    // of array using new keyword
    for (int i = 0; i < N; i++) {
        arr[i] = new Test(i, i + 1);
    }

    // printing contents of array
    for (int i = 0; i < N; i++) {
        arr[i]->print();
    }

    return 0;
}
```

**Output:** 

```
0 1
1 2
2 3
3 4
4 5
```

5.**使用类型类的**[**Vector**](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**:**Vector 是[标准模板库](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)最强大的元素之一，可以轻松高效地编写任何与静态或动态数组相关的复杂代码。它接受一个可以是任何类型的参数，因此我们使用我们的类作为向量类型，并在循环的每次迭代中推送对象。
向量与动态数组相同，能够在插入或删除元素时自动调整自身大小，其存储由容器自动处理。向量元素被放在连续的存储中，这样就可以使用迭代器访问和遍历它们。在向量中，数据被插入到末尾。

## C++

```
#include <iostream>
#include <vector>
#define N 5

using namespace std;

class Test {
    // private variables
    int x, y;

public:
    // parameterized constructor

    Test(int x, int y)
        : x(x)
        , y(y)
    {
    }

    // function to print
    void print() { cout << x << " " << y << endl; }
};

int main()
{
    // vector of type Test class
    vector<Test> v;

    // inserting object at the end of vector
    for (int i = 0; i < N; i++)
        v.push_back(Test(i, i + 1));

    // printing object content
    for (int i = 0; i < N; i++)
        v[i].print();

    return 0;
}
```

**Output:** 

```
0 1
1 2
2 3
3 4
4 5
```