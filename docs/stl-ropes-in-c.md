# c++中的 STL 绳索

> 原文:[https://www.geeksforgeeks.org/stl-ropes-in-c/](https://www.geeksforgeeks.org/stl-ropes-in-c/)

[**绳索**T3】均可伸缩](https://www.geeksforgeeks.org/ropes-data-structure-fast-string-concatenation/)[串](https://www.geeksforgeeks.org/string-data-structure/)实现。它们是为整个管柱的高效操作而设计的。赋值、连接和子字符串等操作花费的时间几乎与字符串的长度无关。

一根绳子是一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，其中每片叶子(末端节点)持有一个字符串和一个长度(也称为“**权重**”)，而树的更上游的每个节点持有其左子树中所有叶子的长度之和。因此，具有两个子节点的节点将整个字符串分为两部分:左边的子树存储字符串的第一部分，右边的子树存储字符串的第二部分，节点的权重是第一部分的长度。

对于绳索操作，在典型的非破坏性情况下，存储在节点中的字符串被假设为常数[不可变对象](https://www.geeksforgeeks.org/c-mutable-keyword/)，允许一些写时复制行为。叶节点通常被实现为基本的固定长度字符串，当不再需要时附加一个引用计数用于释放，尽管也可以使用其他垃圾收集方法。

**注:**绳类和绳头为 **SGI 分机**；它们不是 C++标准库的一部分。

**声明:**
绳索的定义方式与[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)相同为**“矢量<int>”**。但是对于人物绳，我们可以用 **crope** 作为**“绳<char>”**。

下面是同样的程序:

**程序 1:**

## C++

```
// C++ program to illustrate the use
// of ropes using Rope header file
#include <ext/rope>
#include <iostream>

// SGI extension
using namespace __gnu_cxx;

using namespace std;

// Driver Code
int main()
{
    // rope<char> r = "abcdef"
    crope r = "abcdef";

    cout << r << "\n";

    return 0;
}
```

**Output:** 

```
abcdef
```

**<u>绳索上允许的操作</u> :**

*   **push_back():** 此功能用于输入绳子末端的一个字符。 ***时间复杂度:*** O(对数 N)。
*   **pop_back():** 从 C++11 引入(针对字符串)，这个函数用来删除绳子上的最后一个字符。 ***时间复杂度:*** O(对数 N)。
*   **插入(int x，crope r1):** 在 **x <sup>th</sup>** 元素之前插入 **r1** 的内容。 ***时间复杂度:**对于**最佳情况:*** O(log N)而对于**最坏情况:** O(N)。
*   **擦除(int x，int l):** 擦除 l 个元素，从 **x <sup>第</sup>个**元素开始。 ***时间复杂度:*** O(log N)。
*   **substr(int x，int l):** 返回一个新的绳子，其元素是从位置 **x** 开始的 **l** 字符。 ***时间复杂度:*** O(log N)。
*   **替换(int x，int l，crope r1):** 用 **r1** 中的元素替换以**x<sup>th</sup>T7】开头的 **l** 元素。 ***时间复杂度:*** O(log N)。**
*   **连接(+):** 使用“+”符号连接两条绳子。 ***时间复杂度:*** O(1)。

下面是同样的程序:

**程序 2:**

## C++

```
// C++ program to illustrate the use
// of ropes using Rope header file
#include <ext/rope>
#include <iostream>

// SGI extension
using namespace __gnu_cxx;
using namespace std;

// Driver Code
int main()
{
    // rope<char> r = "abcdef"
    crope r = "geeksforgeeks";

    cout << "Initial rope: "
         << r << endl;

    // 'g' is added at the
    // end of the rope
    r.push_back('g');
    r.push_back('f');
    r.push_back('g');

    cout << "Rope after pushing f: "
         << r << endl;

    int pos = 2;

    // gfg will be inserted
    // before position 2
    r.insert(pos - 1, "gfg");

    cout << "Rope after inserting "
         << "gfg at position 2: " << r
         << endl;

    // gfg will be deleted
    r.erase(pos - 1, 3);

    cout << "Rope after removing gfg"
         << " inserted just before: "
         << r << endl;

    // Replace "ee" with "00"
    r.replace(pos - 1, 2, "00");

    cout << "Rope after replacing "
         << "characters: " << r
         << endl;

    // Slice the rope
    crope r1 = r.substr(pos - 1, 2);

    cout << "Subrope at position 2: "
         << r << endl;

    // Removes the last element
    r.pop_back();
    r.pop_back();
    r.pop_back();

    cout << "Final rope after poping"
         << " out 3 elements: " << r;

    return 0;
}
```

**Output**

```
Initial rope: geeksforgeeks
Rope after pushing f: geeksforgeeksgfg
Rope after inserting gfg at position 2: ggfgeeksforgeeksgfg
Rope after removing gfg inserted just before: geeksforgeeksgfg
Rope after replacing characters: g00ksforgeeksgfg
Subrope at position 2: g00ksforgeeksgfg
Final rope after poping out 3 elements: g00ksforgeeks
```

**<u>容量功能</u> :**

*   **size():** 返回绳子的长度。
*   **max_size():** 保证可表示的最长绳索的尺寸。

下面是同样的程序:

**程序 3:**

## C++

```
// C++ program to illustrate the use
// of ropes using Rope header file
#include <ext/rope>
#include <iostream>

// SGI extension
using namespace __gnu_cxx;
using namespace std;

// Driver Code
int main()
{
    // rope<char> r = "abcdef"
    crope r = "abcdef";

    cout << r.size() << endl;
    cout << r.max_size() << endl;
    return 0;
}
```

**Output:** 

```
6
1836311902
```

**<u>迭代器</u> :**

*   **可变 _begin():** 返回一个指向绳子开头的迭代器。
*   **可变 _end():** 返回一个指向绳子末端的迭代器。

下面是同样的程序:

**程序 4:**

## C++

```
// C++ program to illustrate the use
// of ropes using Rope header file
#include <ext/rope>
#include <iostream>

// SGI extension
using namespace __gnu_cxx;
using namespace std;

// Driver Code
int main()
{
    // rope<char> r = "abcdef"
    crope r = "abcdef";

    rope<char>::iterator it;
    for (it = r.mutable_begin();
         it != r.mutable_end(); it++) {

        // Print the value
        cout << char((*it) + 2)
             << "";
    }

    return 0;
}
```

**Output:** 

```
cdefgh
```