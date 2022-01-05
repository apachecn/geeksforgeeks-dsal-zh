# 如何在字符串的映射中插入数据？

> 原文:[https://www . geesforgeks . org/如何在字符串映射中插入数据/](https://www.geeksforgeeks.org/how-to-insert-data-in-the-map-of-strings/)

[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)是[关联容器](https://www.geeksforgeeks.org/sequence-vs-associative-containers-cpp/)，以特定顺序存储元素。它将元素存储在键值和映射值的组合中。

**语法:**

```
map<data type of key, data type of value> M
```

要在 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 中对地图使用上述语法，必须包含以下头文件:
**头文件:**

```
#include <map>
```

要在[地图中插入数据，使用地图中的插入()功能](https://www.geeksforgeeks.org/map-insert-in-c-stl/)。它用于在地图容器中插入具有特定键的元素。

**语法:**

```
iterator map_name.insert({key, element})
```

**参数:**它接受一个由要插入到地图容器中的键和元素组成的对，但它只插入唯一的键。这意味着，如果键已经存在于地图中，则该函数不会在地图中插入键和元素。

**返回值:**返回一个迭代器，指向地图中的新元素。

下面是同样的程序来说明:

## C++

```
// C++ program to store the string as
// the map value
#include <iostream>
#include <map>
using namespace std;

// Driver code
int main()
{
    // Get the Strings
    string s = "abc";
    string s1 = "bca";
    string s2 = "cba";

    // Declare map with both value
    // and key  having string data_type
    map<string, string> m;

    // Insert the string in the map
    m.insert(pair<string, string>(s1, s));
    m.insert(pair<string, string>(s, s2));

    // Print the elements stored
    // in the map
    for (auto itr = m.begin();
         itr != m.end(); ++itr) {
        cout << itr->first << '\t'
             << itr->second << '\n';
    }

    return 0;
}
```

**Output:**

```
abc    cba
bca    abc

```

还有一种方法[将数据存储在地图](https://www.geeksforgeeks.org/inserting-elements-in-stdmap-insert-emplace-and-operator/)中，下面是同样的语法:

**语法:**

```
iterator map_name.insert(iterator position, {key, element})
```

**参数:**该函数接受两个参数，如下所述:

1.  **{key，element}:** 这指定了一个由要插入到地图容器中的 key 和 element 组成的对。
2.  **位置:**它只指向开始插入的搜索操作的位置，以使过程更快。插入是根据容器遵循的顺序进行的。

**返回值:**函数返回一个迭代器，指向容器中的新元素。

下面是同样的程序来说明:

## C++

```
// C++ program to illustrate the map
// insert(iteratorposition, {key, element})
#include <iostream>
#include <map>
using namespace std;

// Driver Code
int main()
{
    // Initialize a Map mp
    map<string, int> mp;

    // Insert elements in random order
    mp.insert({ "abc", 30 });
    mp.insert({ "bcd", 40 });

    auto it = mp.find("bcd");

    // Insert {"dcd", 60} starting the
    // search from position where 2
    // is present
    mp.insert(it, { "dcd", 60 });

    // Print the element
    cout << "KEY\tELEMENT\n";

    for (auto itr = mp.begin();
         itr != mp.end(); ++itr) {
        cout << itr->first << '\t'
             << itr->second << '\n';
    }

    return 0;
}
```

**Output:**

```
KEY    ELEMENT
abc    30
bcd    40
dcd    60

```