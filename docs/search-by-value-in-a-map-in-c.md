# 在 C++的地图中按值搜索

> 原文:[https://www . geesforgeks . org/按 c 中值搜索地图/](https://www.geeksforgeeks.org/search-by-value-in-a-map-in-c/)

给定一组 **N 对**作为一个**(键，值)** [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)在一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和一个整数 **K** 中，任务是找到所有映射到给定值 **K** 的键。如果没有映射到 **K** 的键值，则打印**-1”**。
**示例:**

> **输入:** Map[] = { {1，3}、{2，3}、{4，-1}、{7，2}、{10，3} }，K = 3
> **输出:**1 2 10
> T6】解释:
> 映射到值 3 的 3 个键值为 1、2、10。
> **输入:** Map[] = { {1，3}，{2，3}，{4，-1}，{7，2}，{10，3} }，K = 10
> **输出:** -1
> **说明:**
> 没有任何键值映射到值 10。

**方法:**思路是遍历给定的[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，打印所有映射到给定值 **K** 的键值。下面是用于查找所有键值的循环:

> 对于(auto & it:Map){
> if(it . second = = K){
> print(it . first)
> }
> }

如果没有用 **K** 映射的值，则打印**-1”**。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to find the key values
// according to given mapped value K
void printKey(map<int, int>& Map,
              int K)
{

    // If a is true, then we have
    // not key-value mapped to K
    bool a = true;

    // Traverse the map
    for (auto& it : Map) {

        // If mapped value is K,
        // then print the key value
        if (it.second == K) {
            cout << it.first << ' ';
            a = false;
        }
    }

    // If there is not key mapped with K,
    // then print -1
    if (a) {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    map<int, int> Map;

    // Given map
    Map[1] = 3;
    Map[2] = 3;
    Map[4] = -1;
    Map[7] = 2;
    Map[10] = 3;

    // Given value K
    int K = 3;

    // Function call
    printKey(Map, K);
    return 0;
}
```

**Output:** 

```
1 2 10
```

**时间复杂度:** *O(N)* ，其中 N 为地图中存储的对数。这是因为我们要遍历所有的对一次。
**辅助空间:** *O(1)*