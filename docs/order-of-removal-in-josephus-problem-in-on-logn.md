# 约瑟夫斯问题在 O(N logN)

中的去除顺序

> 原文:[https://www . geeksforgeeks . org/约瑟夫斯移除顺序-日志中的问题/](https://www.geeksforgeeks.org/order-of-removal-in-josephus-problem-in-on-logn/)

给定 **N** 个站成一圈等待执行的孩子，以及一个数字 **K** ，表示顺时针方向跳过 **K-1** 个孩子， **K <sup>第</sup>个**个孩子在圈里被杀，然后开始执行 **(K+1) <sup>第</sup>** 个孩子，任务是打印将要在<sup>中被杀的孩子</sup>

**注:**默认最后一个孩子被认为是死在最后。

**示例:**

> **输入:** N = 5，K = 2
> **输出:** 3 1 5 2 4
> **说明:**
> 最初的排列是{1，2，3，4，5}，执行的操作是:
> 
> 1.  从 1 开始数，第 K<sup>个孩子是 3。所以第三个孩子被杀了。之后，剩下要执行的子级是{1，2，4，5}，然后开始执行子级 4。</sup>
> 2.  从 4 开始数，第 K<sup>个孩子是 1。所以第一个孩子被杀了。之后，剩下要执行的子级是{2，4，5}，然后开始执行子级 2。</sup>
> 3.  从 2 开始数，第 K<sup>个孩子是 5。所以第五个孩子被杀了。之后，剩下要执行的子级是{2，4}，然后开始执行子级 2。</sup>
> 4.  从 2 开始数，第 K<sup>个孩子是 2。所以第二个孩子被杀了。之后剩下要执行的孩子是 2，然后开始执行孩子 4。</sup>
> 5.  最后，孩子 4 是唯一剩下的孩子。所以孩子会被杀。
> 
> **输入:** N = 7，K = 2
> T3】输出: 3 6 2 7 5 1 4

**天真的做法:**最简单的想法就是用一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储剩余孩子的位置。然后当向量的[大小大于 **1** 时迭代，并且在每次迭代](https://www.geeksforgeeks.org/vectorempty-vectorsize-c-stl/)[中从向量](https://www.geeksforgeeks.org/vector-erase-and-clear-in-cpp/)中擦除期望的位置。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以使用[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)进行优化。按照以下步骤解决问题:

*   初始化一个[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)，说 **V** ，然后[将**【1，N】**范围内的元素插入 **V** 中。](https://www.geeksforgeeks.org/vector-insert-function-in-c-stl/)
*   初始化一个变量，将**位置**设为 **0** ，以存储被移除元素的索引。
*   迭代至集合、 **V** 的[尺寸大于 **1** ，执行以下步骤:](https://www.geeksforgeeks.org/setsize-c-stl/)
    *   将设置的[大小存储在一个变量中，比如 **X** 。](https://www.geeksforgeeks.org/setsize-c-stl/)
    *   将**位置**的值更新为**(位置+ K) % X** 。
    *   在 **V** 中打印 **pos** 指向的元素，然后[删除](https://www.geeksforgeeks.org/seterase-c-stl/)即可。
    *   将**位置**更新为**位置%V.size()。**
*   最后，完成上述步骤后，打印设置 **V** 开头存储的最后一个元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Header files, namespaces to use
// ordered set
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;

#define ordered_set                              \
    tree<int, null_type, less<int>, rb_tree_tag, \
         tree_order_statistics_node_update>

// Function to find the child who
// will get killed in the ith step
void orderOfExecution(int N, int K)
{

    // Create an ordered set
    ordered_set V;

    // Push elements in the range
    // [1, N] in the set
    for (int i = 1; i <= N; ++i)
        V.insert(i);

    // Stores the position to be removed
    int pos = 0;

    // Iterate until the size of the set
    // is greater than 1
    while (V.size() > 1) {

        // Update the position
        pos = (pos + K) % (int)V.size();

        // Print the removed element
        cout << *(V.find_by_order(pos)) << ' ';

        // Erase it from the ordered set
        V.erase(*(V.find_by_order(pos)));

        // Update position
        pos %= (int)V.size();
    }

    // Print the first element of the set
    cout << *(V.find_by_order(0));
}

// Driver Code
int main()
{
    // Given input
    int N = 5, K = 2;

    // Function Call
    orderOfExecution(N, K);

    return 0;
}
```

**Output**

```
3 1 5 2 4
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*