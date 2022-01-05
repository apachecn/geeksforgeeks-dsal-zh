# 设置在 C++标准模板库(STL)

> 原文:[https://www.geeksforgeeks.org/set-in-cpp-stl/](https://www.geeksforgeeks.org/set-in-cpp-stl/)

集合是一种关联[容器](https://www.geeksforgeeks.org/containers-cpp-stl/)，其中每个元素必须是唯一的，因为元素的值标识了它。这些值以特定的顺序存储。

**语法:**

```
set<datatype> setname;
```

**数据类型**:集合可以根据值采用任何数据类型，例如 int、char、float 等。

**示例:**

```
set<int> val; // defining an empty set
set<int> val = {6, 10, 5, 1}; // defining a set with values
```

> **注意:**设置<数据类型，大于<数据类型>设置名称；用于以降序存储集合中的值。

**属性:**

1.  该集合按照排序后的顺序存储元素。
2.  一个集合中的所有元素都有**唯一值**。
3.  元素的值一旦被添加到集合中就不能被修改，尽管可以移除然后添加该元素的修改值。因此，值是**不可改变的**。
4.  设定遵循**二叉查找树**执行。
5.  集合中的值是**未索引的**。

> **注意:**要以未排序(随机)的顺序存储元素，可以使用 [**无序 _set()**](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/) 。

**与集合相关的一些基本功能:**

*   [begin()](https://www.geeksforgeeks.org/setbegin-setend-c-stl/)–返回集合中第一个元素的迭代器。
*   [end()](https://www.geeksforgeeks.org/setbegin-setend-c-stl/)–返回集合中最后一个元素之后的理论元素的迭代器。
*   [size()](https://www.geeksforgeeks.org/setsize-c-stl/)–返回集合中元素的数量。
*   [max _ size()](https://www.geeksforgeeks.org/set-max_size-function-in-c-stl/)–返回集合可以容纳的最大元素数。
*   [空()](https://www.geeksforgeeks.org/setempty-c-stl/)–返回集合是否为空。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to demonstrate various functions of
// Set in C++ STL
#include <iostream>
#include <iterator>
#include <set>

using namespace std;

int main()
{
    // empty set container
    set<int, greater<int> > s1;

    // insert elements in random order
    s1.insert(40);
    s1.insert(30);
    s1.insert(60);
    s1.insert(20);
    s1.insert(50);

    // only one 50 will be added to the set
    s1.insert(50);
    s1.insert(10);

    // printing set s1
    set<int, greater<int> >::iterator itr;
    cout << "\nThe set s1 is : \n";
    for (itr = s1.begin(); itr != s1.end(); itr++) {
        cout << *itr << " ";
    }
    cout << endl;

    // assigning the elements from s1 to s2
    set<int> s2(s1.begin(), s1.end());

    // print all elements of the set s2
    cout << "\nThe set s2 after assign from s1 is : \n";
    for (itr = s2.begin(); itr != s2.end(); itr++) {
        cout << *itr << " ";
    }
    cout << endl;

    // remove all elements up to 30 in s2
    cout << "\ns2 after removal of elements less than 30 "
            ":\n";
    s2.erase(s2.begin(), s2.find(30));
    for (itr = s2.begin(); itr != s2.end(); itr++) {
        cout << *itr << " ";
    }

    // remove element with value 50 in s2
    int num;
    num = s2.erase(50);
    cout << "\ns2.erase(50) : ";
    cout << num << " removed\n";
    for (itr = s2.begin(); itr != s2.end(); itr++) {
        cout << *itr << " ";
    }

    cout << endl;

    // lower bound and upper bound for set s1
    cout << "s1.lower_bound(40) : \n"
         << *s1.lower_bound(40) << endl;
    cout << "s1.upper_bound(40) : \n"
         << *s1.upper_bound(40) << endl;

    // lower bound and upper bound for set s2
    cout << "s2.lower_bound(40) :\n"
         << *s2.lower_bound(40) << endl;
    cout << "s2.upper_bound(40) : \n"
         << *s2.upper_bound(40) << endl;

    return 0;
}
```

**Output**

```
The set s1 is : 
60 50 40 30 20 10 

The set s2 after assign from s1 is : 
10 20 30 40 50 60 

s2 after removal of elements less than 30 :
30 40 50 60 
s2.erase(50) : 1 removed
30 40 60 
s1.lower_bound(40) : 
40
s1.upper_bound(40) : 
30
s2.lower_bound(40) :
40
s2.upper_bound(40) : 
60
```

### **c++ STL 中的集合方法**

<figure class="table">

| 方法 | 描述 |
| --- | --- |
| [begin()](https://www.geeksforgeeks.org/setbegin-setend-c-stl/) | 返回集合中第一个元素的迭代器。 |
| [end()](https://www.geeksforgeeks.org/setbegin-setend-c-stl/) | 返回集合中最后一个元素之后的理论元素的迭代器。 |
| [rbegin（）](https://www.geeksforgeeks.org/setrbegin-and-setrend-in-c-stl/) | 返回指向容器中最后一个元素的反向迭代器。 |
| [rend()](https://www.geeksforgeeks.org/setrbegin-and-setrend-in-c-stl/) | 返回一个反向迭代器，指向集合容器中第一个元素之前的理论元素。 |
| crbegin() | 返回指向容器中最后一个元素的常量迭代器。 |
| [信徒()](https://www.geeksforgeeks.org/set-crbegin-and-crend-function-in-c-stl/) | 返回一个常量迭代器，指向容器中第一个元素之前的位置。 |
| [cbegin（）](https://www.geeksforgeeks.org/set-cbegin-and-cend-function-in-c-stl/) | 返回指向容器中第一个元素的常量迭代器。 |
| [cend()](https://www.geeksforgeeks.org/set-cbegin-and-cend-function-in-c-stl/) | 返回指向容器中最后一个元素之后的位置的常量迭代器。 |
| [尺寸()](https://www.geeksforgeeks.org/setsize-c-stl/) | 返回集合中元素的数量。 |
| [max_size()](https://www.geeksforgeeks.org/set-max_size-function-in-c-stl/) | 返回集合可以容纳的最大元素数。 |
| [空()](https://www.geeksforgeeks.org/setempty-c-stl/) | 返回集合是否为空。 |
| [插入(常量 g)](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) | 向集合中添加新元素“g”。 |
| [迭代器插入(迭代器位置，常量 g)](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) | 在迭代器指向的位置添加一个新元素“g”。 |
| [擦除(迭代器位置)](https://www.geeksforgeeks.org/seterase-c-stl/) | 移除迭代器所指向位置的元素。 |
| [擦除(常量 g)](https://www.geeksforgeeks.org/seterase-c-stl/) | 从集合中移除值“g”。 |
| [晴()](https://www.geeksforgeeks.org/setclear-c-stl/) | 从集合中移除所有元素。 |
| [key _ comp()](https://www.geeksforgeeks.org/setkey_comp-in-c-stl/)/[value _ comp()](https://www.geeksforgeeks.org/set-value_comp-function-in-c-stl/) | 返回确定集合中元素排序方式的对象(默认情况下为“ |
| [查找(const g)](https://www.geeksforgeeks.org/set-find-function-in-c-stl/) | 如果找到集合中的元素“g”，返回一个迭代器，否则返回迭代器结束。 |
| [计数(常量 g)](https://www.geeksforgeeks.org/set-count-function-in-c-stl/) | 根据集合中是否存在元素“g”返回 1 或 0。 |
| [下限(常数 g)](https://www.geeksforgeeks.org/set-lower_bound-function-in-c-stl/) | 返回第一个元素的迭代器，它相当于“g ”,或者肯定不会在集合中的元素“g”之前。 |
| [上限(常数 g)](https://www.geeksforgeeks.org/set-upper_bound-function-in-c-stl/) | 返回集合中元素“g”之后的第一个元素的迭代器。 |
| [equal_range()](https://www.geeksforgeeks.org/set-equal_range-function-in-c-stl/) | 该函数返回一个对的迭代器。(key_comp)。该对指的是包含容器中所有元素的范围，这些元素的键等价于 k。 |
| [炮位()](https://www.geeksforgeeks.org/setemplace-c-stl/) | 仅当要插入的元素是唯一的并且不存在于集合中时，此函数用于将新元素插入集合容器。 |
| [location _ hint()](https://www.geeksforgeeks.org/set-emplace_hint-function-in-c-stl/) | 返回一个迭代器，指向完成插入的位置。如果参数中传递的元素已经存在，那么它会返回一个迭代器，指向现有元素所在的位置。 |
| [互换()](https://www.geeksforgeeks.org/setswap-c-stl/) | 此功能用于交换两个器械包的内容，但器械包必须是同一类型，尽管大小可能不同。 |
| [运算符=](https://www.geeksforgeeks.org/set-operator-in-c-stl/) | “=”是 C++ STL 中的一个运算符，它将一个集合复制(或移动)到另一个集合，而集合::运算符=是对应的运算符函数。 |
| [get _ 分配器()](https://www.geeksforgeeks.org/set-get_allocator-in-c-stl/) | 返回与集合关联的分配器对象的副本。 |

</figure>

**必读:** [集 vs 无序集](https://www.geeksforgeeks.org/set-vs-unordered_set-c-stl/)

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论