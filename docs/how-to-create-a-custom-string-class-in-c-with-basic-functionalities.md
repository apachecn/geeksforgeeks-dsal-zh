# 如何使用基本功能在 C++中创建自定义字符串类

> 原文:[https://www . geesforgeks . org/如何使用基本功能创建自定义字符串类/](https://www.geeksforgeeks.org/how-to-create-a-custom-string-class-in-c-with-basic-functionalities/)

在本文中，我们将创建我们的自定义字符串类，它将具有与现有的[字符串类](https://www.geeksforgeeks.org/c-string-class-and-its-applications/)相同的功能。
字符串类具有以下基本功能:

1.  **不带参数的构造函数:**这将为堆中的字符串对象分配存储空间，并将该值指定为[空字符](https://www.geeksforgeeks.org/difference-between-null-pointer-null-character-0-and-0-in-c-with-examples/)。
2.  **只有一个参数的构造函数:**它接受一个指向一个字符的指针，或者我们可以说，如果我们传递一个字符数组，接受指向数组中第一个字符的指针，那么 String 类的构造函数会在[堆内存](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)上分配与传递的数组大小相同的存储空间，并将数组的内容复制到堆中[分配的内存](https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/)上。它使用在 cstring 库中声明的 [strcpy()](https://www.geeksforgeeks.org/strcpy-in-c-cpp/) 函数复制内容。
    在执行上述操作之前，它会检查传递的参数是否是[空指针](https://www.geeksforgeeks.org/few-bytes-on-null-pointer-in-c/)，然后它会表现为没有参数的构造函数。
3.  **复制构造器:**当从已经创建的对象创建的相同类型的任何对象时调用它，然后它执行**深度复制**。它在堆上为要创建的对象分配新的空间，并复制传递的对象的内容(作为引用传递)。
4.  **移动构造函数:**通常在从同一类型的右值初始化对象(通过直接初始化或复制初始化)时调用。它接受对自定义字符串类类型的对象的[值的引用。](https://www.geeksforgeeks.org/lvalue-and-rvalue-in-c-language/)

下面是使用自定义字符串类 **Mystring** :
实现上述方法

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate the
// above discussed functionality
#include <cstring>
#include <iostream>
using namespace std;

// Custom string class
class Mystring {

    // Initialise the char array
    char* str;

public:
    // No arguments Constructor
    Mystring();

    // Constructor with 1 arguments
    Mystring(char* val);

    // Copy Constructor
    Mystring(const Mystring& source);

    // Move Constructor
    Mystring(Mystring&& source);

    // Destructor
    ~Mystring() { delete str; }
};

// Function to illustrate Constructor
// with no arguments
Mystring::Mystring()
    : str{ nullptr }
{
    str = new char[1];
    str[0] = '\0';
}

// Function to illustrate Constructor
// with one arguments
Mystring::Mystring(char* val)
{
    if (val == nullptr) {
        str = new char[1];
        str[0] = '\0';
    }

    else {

        str = new char[strlen(val) + 1];

        // Copy character of val[]
        // using strcpy
        strcpy(str, val);
        str[strlen(val)] = '\0';

        cout << "The string passed is: "
             << str << endl;
    }
}

// Function to illustrate
// Copy Constructor
Mystring::Mystring(const Mystring& source)
{
    str = new char[strlen(source.str) + 1];
    strcpy(str, source.str);
    str[strlen(source.str)] = '\0';
}

// Function to illustrate
// Move Constructor
Mystring::Mystring(Mystring&& source)
{
    str = source.str;
    source.str = nullptr;
}

// Driver Code
int main()
{
    // Constructor with no arguments
    Mystring a;

    // Convert string literal to
    // char array
    char temp[] = "Hello";

    // Constructor with one argument
    Mystring b{ temp };

    // Copy constructor
    Mystring c{ a };

    char temp1[] = "World";

    // One arg constructor called,
    // then the move constructor
    Mystring d{ Mystring{ temp } };
    return 0;
}
```

**Output:** 

```
The string passed is: Hello
The string passed is: Hello
```

字符串类的更多功能:

1.  **pop_back():** 从 Mystring 对象中移除最后一个元素。
2.  **push_back(char ch):** 接受一个字符作为参数，并将其添加到 Mystring 对象的末尾。
3.  **长度():**返回 mystring 的长度。
4.  **copy():** 它从给定的位置(pos)和特定的长度(len)将 mystring 对象复制到字符数组中。
5.  **swap():** 它交换两个 Mystring 对象。
6.  使用重载“+”运算符连接两个字符串:允许我们连接两个字符串。

下面是说明上述功能的程序:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate the
// above functionalities
#include <cstring>
#include <iostream>
using namespace std;

// Class Mystring
class Mystring {

    // Prototype for stream insertion
    friend ostream&
    operator<<(
        ostream& os,
        const Mystring& obj);

    // Prototype for stream extraction
    friend istream& operator>>(
        istream& is,
        Mystring& obj);

    // Prototype for '+'
    // operator overloading
    friend Mystring operator+(
        const Mystring& lhs,
        const Mystring& rhs);
    char* str;

public:
    // No arguments constructor
    Mystring();

    // pop_back() function
    void pop_bk();

    // push_back() function
    void push_bk(char a);

    // To get the length
    int get_length();

    // Function to copy the string
    // of length len from position pos
    void cpy(char s[], int len, int pos);

    // Swap strings function
    void swp(Mystring& rhs);

    // Constructor with 1 arguments
    Mystring(char* val);

    // Copy Constructor
    Mystring(const Mystring& source);

    // Move Constructor
    Mystring(Mystring&& source);

    // Overloading the assignment
    // operator
    Mystring& operator=(
        const Mystring& rhs);

    // Destructor
    ~Mystring() { delete str; }
};

// Overloading the assignment operator
Mystring& Mystring::operator=(
    const Mystring& rhs)
{
    if (this == &rhs)
        return *this;
    delete[] str;
    str = new char[strlen(rhs.str) + 1];
    strcpy(str, rhs.str);
    return *this;
}

// Overloading the plus operator
Mystring operator+(const Mystring& lhs,
                   const Mystring& rhs)
{
    int length = strlen(lhs.str)
                 + strlen(rhs.str);

    char* buff = new char[length + 1];

    // Copy the strings to buff[]
    strcpy(buff, lhs.str);
    strcat(buff, rhs.str);
    buff[length] = '\0';

    // String temp
    Mystring temp{ buff };

    // delete the buff[]
    delete[] buff;

    // Return the concatenated string
    return temp;
}
// Overloading the stream
// extraction operator
istream& operator>>(istream& is,
                    Mystring& obj)
{
    char* buff = new char[1000];
    memset(&buff[0], 0, sizeof(buff));
    is >> buff;
    obj = Mystring{ buff };
    delete[] buff;
    return is;
}

// Overloading the stream
// insertion operator
ostream& operator<<(ostream& os,
                    const Mystring& obj)
{
    os << obj.str;
    return os;
}

// Function for swapping string
void Mystring::swp(Mystring& rhs)
{
    Mystring temp{ rhs };
    rhs = *this;
    *this = temp;
}

// Function to copy the string
void Mystring::cpy(char s[], int len,
                   int pos)
{
    for (int i = 0; i < len; i++) {
        s[i] = str[pos + i];
    }
    s[len] = '\0';
}

// Function to implement push_bk
void Mystring::push_bk(char a)
{
    // Find length of string
    int length = strlen(str);

    char* buff = new char[length + 2];

    // Copy character from str
    // to buff[]
    for (int i = 0; i < length; i++) {
        buff[i] = str[i];
    }
    buff[length] = a;
    buff[length + 1] = '\0';

    // Assign the new string with
    // char a to string str
    *this = Mystring{ buff };

    // Delete the temp buff[]
    delete[] buff;
}

// Function to implement pop_bk
void Mystring::pop_bk()
{
    int length = strlen(str);
    char* buff = new char[length];

    // Copy character from str
    // to buff[]
    for (int i = 0; i < length - 1; i++)
        buff[i] = str[i];
    buff[length-1] = '\0';

    // Assign the new string with
    // char a to string str
    *this = Mystring{ buff };

    // delete the buff[]
    delete[] buff;
}

// Function to implement get_length
int Mystring::get_length()
{
    return strlen(str);
}

// Function to illustrate Constructor
// with no arguments
Mystring::Mystring()
    : str{ nullptr }
{
    str = new char[1];
    str[0] = '\0';
}

// Function to illustrate Constructor
// with one arguments
Mystring::Mystring(char* val)
{
    if (val == nullptr) {
        str = new char[1];
        str[0] = '\0';
    }

    else {

        str = new char[strlen(val) + 1];

        // Copy character of val[]
        // using strcpy
        strcpy(str, val);
        str[strlen(val)] = '\0';
    }
}

// Function to illustrate
// Copy Constructor
Mystring::Mystring(const Mystring& source)
{
    str = new char[strlen(source.str) + 1];
    strcpy(str, source.str);
}

// Function to illustrate
// Move Constructor
Mystring::Mystring(Mystring&& source)
{
    str = source.str;
    source.str = nullptr;
}

// Driver Code
int main()
{
    // Constructor with no arguments
    Mystring a;

    // Convert string literal to
    // char array
    char temp[] = "Hello";

    // Constructor with one argument
    Mystring b{ temp };

    // Copy constructor
    Mystring c{ a };

    char temp1[] = "World";

    // One arg constructor called,
    // then the move constructor
    Mystring d{ Mystring{ temp } };

    // Remove last character from
    // Mystring b
    b.pop_bk();

    // Print string b
    cout << "Mystring b: "
         << b << endl;

    // Append last character from
    // Mystring b
    b.push_bk('o');

    // Print string b
    cout << "Mystring b: "
         << b << endl;

    // Print length of string b
    cout << "Length of Mystring b: "
         << b << endl;

    char arr[80];

    // Copy string b chars from
    // length 0 to 3
    b.cpy(arr, 3, 0);

    // Print string arr
    cout << "arr is: "
         << arr << endl;

    // Swap d and b
    d.swp(b);

    // Print d and b
    cout << d << " "
         << b << endl;

    // Concatenate b and b with
    // overloading '+' operator
    d = b + b;

    // Print string d
    cout << "string d: "
         << d << endl;

    return 0;
}
```

**Output:** 

```
Mystring b: Hell
Mystring b: Hello
Length of Mystring b: Hello
arr is: Hel
Hello Hello
string d: HelloHello
```