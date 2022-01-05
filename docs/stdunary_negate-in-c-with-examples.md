# 标准::C++中的一元 _ 求反()，示例

> 原文:[https://www . geeksforgeeks . org/stdunary _ notify-in-c-with-examples/](https://www.geeksforgeeks.org/stdunary_negate-in-c-with-examples/)

**std::一元 _ 求反()**是一个包装函数对象，返回它持有的一元谓词的补码。包装函数是软件库或计算机程序中的子例程，其主要目的是调用第二个子例程或系统调用，几乎不需要或不需要额外的计算。一元否定类型的对象通常使用函数 [**std::not1()**](https://www.geeksforgeeks.org/not1-and-not2-function-templates-in-c-stl-with-examples/) 来构造。
**头文件:**

```
#include <functional>
```

**语法:**

```
std::unary_negate<class T>
    variable_name(Object of class T);
```

**参数:**函数 **std::一元 _ 求反()**接受谓词函数对象作为参数，并返回调用谓词函数生成的结果的逻辑补数。
**返回值:**通过调用谓词函数返回结果的逻辑补数。
下面是说明功能的程序 **std::一元 _ 求反()** :
**程序 1:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to illustrate
// std::unary_negate to find number
// greater than equals 4 in arr[]

#include <algorithm>
#include <functional>
#include <iostream>
#include <vector>
using namespace std;

// Predicate function to find the
// count of number greater than or
// equals to 4 in array arr[]
struct gfg : unary_function<int, bool> {

    // Function returns true if any
    // element is less than 4
    bool operator()(int i)
        const
    {
        return i < 4;
    }
};

// Driver Code
int main()
{
    // Declare vector
    vector<int> arr;

    // Insert value from 1-10 in arr
    for (int i = 1; i <= 10; ++i) {
        arr.push_back(i);
    }

    // Use unary_negate() to find the
    // count of number greater than 4
    unary_negate<gfg> func((gfg()));

    // Print the count of number using
    // function count_if()
    cout << count_if(arr.begin(),
                     arr.end(), func);
    return 0;
}
```

**Output:** 

```
7
```