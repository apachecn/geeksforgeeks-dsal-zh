# c++中元组向量的排序(升序)

> 原文:[https://www . geesforgeks . org/sorting-vector-tuple-c-升序/](https://www.geeksforgeeks.org/sorting-vector-tuple-c-ascending-order/)

**什么是元组向量？**
一个[元组](https://www.geeksforgeeks.org/tuples-in-c/)是一个可以容纳多个元素的对象，一个包含多个这样的元组的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)被称为元组向量。元素可以是不同的数据类型。元组的元素按照被访问的顺序被初始化为参数。

```
// C++ program to demonstrate vector of tuple
#include <bits/stdc++.h>
using namespace std;
int main()
{
    vector<tuple<int, int, int> > v;
    v.push_back(make_tuple(10, 20, 30));
    v.push_back(make_tuple(15, 5, 25));
    v.push_back(make_tuple(3, 2, 1));

    // Printing vector tuples
    for (int i = 0; i < v.size(); i++) 
        cout << get<0>(v[i]) << " " 
             << get<1>(v[i]) << " " 
             << get<2>(v[i]) << "\n";

    return 0;
}
```

**Output:**

```
10 20 30
15 5 25
3 2 1

```

**元组向量排序的不同方式**
**案例一:在元组**第一个元素**的基础上，按升序对向量元素进行排序。**
这种类型的排序可以使用简单的“ **sort()** ”功能来实现。默认情况下，排序函数根据元组的第一个元素对向量元素进行排序。

```
// C++ program to demonstrate sorting in
// vector of tuple according to 1st element
// of tuple
#include <bits/stdc++.h>
using namespace std;
int main()
{
    vector<tuple<int, int, int> > v;
    v.push_back(make_tuple(10, 20, 30));
    v.push_back(make_tuple(15, 5, 25));
    v.push_back(make_tuple(3, 2, 1));

    // Using sort() function to sort by 1st 
    // element of tuple
    sort(v.begin(), v.end());
    cout << "Sorted Vector of Tuple on basis"
           " of first element of tuple:\n";
    for (int i = 0; i < v.size(); i++) 
        cout << get<0>(v[i]) << " " 
             << get<1>(v[i]) << " "
             << get<2>(v[i]) << "\n";

    return 0;
}
```

**Output:**

```
Sorted Vector of Tuple on basis of first element of tuple:
3 2 1
10 20 30
15 5 25

```

**情况 2:基于元组**的**第二元素，按升序对向量元素进行排序。**
有时我们需要根据元组的第二个元素对向量的元素进行排序。为此，我们修改了 sort()函数，并传递了第三个参数，即对 sort()函数中用户定义的显式函数的调用。

```
// C++ program to demonstrate sorting in vector
// of tuple according to 2nd element of tuples
#include <bits/stdc++.h>
using namespace std;

// Comparison function to sort the vector elements
// by second element of tuples
bool sortbysec(const tuple<int, int, int>& a, 
               const tuple<int, int, int>& b)
{
    return (get<1>(a) < get<1>(b));
}

int main()
{
    vector<tuple<int, int, int> > v;
    v.push_back(make_tuple(10, 20, 30));
    v.push_back(make_tuple(15, 5, 25));
    v.push_back(make_tuple(3, 2, 1));

    // Using sort() function to sort by 2nd element
    // of tuple
    sort(v.begin(), v.end(), sortbysec);
    cout << "Sorted Vector of Tuple on basis"
           " of Second element of tuple:\n";

    for (int i = 0; i < v.size(); i++) 
        cout << get<0>(v[i]) << " " 
             << get<1>(v[i]) << " " 
             << get<2>(v[i]) << "\n";
    return 0;
}
```

**Output:**

```
Sorted Vector of Tuple on basis of Second element of tuple:
3 2 1
15 5 25
10 20 30

```

**案例三:基于元组**的**第三元素，按照升序对向量元素进行排序。**
有时我们需要根据元组的第三个元素对向量的元素进行排序。为此，我们修改了 sort()函数，并传递了第三个参数，即对 sort()函数中用户定义的显式函数的调用。

```
// C++ program to demonstrate sorting in vector
// of tuple according to 3rd element of tuple
#include <bits/stdc++.h>
using namespace std;
// Driver function to sort the vector elements
// by third element of tuple
bool sortbyth(const tuple<int, int, int>& a, 
              const tuple<int, int, int>& b)
{
    return (get<2>(a) < get<2>(b));
}

int main()
{
    vector<tuple<int, int, int> > v;
    v.push_back(make_tuple(10, 20, 30));
    v.push_back(make_tuple(15, 5, 25));
    v.push_back(make_tuple(3, 2, 1));

    // Using sort() function to sort by 3rd element
    // of tuple
    sort(v.begin(), v.end(), sortbyth);
    cout << "Sorted Vector of Tuple on basis"
            " of Third element of tuple:\n";
    for (int i = 0; i < v.size(); i++) 
        cout << get<0>(v[i]) << " " 
             << get<1>(v[i]) << " " 
             << get<2>(v[i]) << "\n";

    return 0;
}
```

**Output:**

```
Sorted Vector of Tuple on basis of Third element of tuple:
3 2 1
15 5 25
10 20 30

```