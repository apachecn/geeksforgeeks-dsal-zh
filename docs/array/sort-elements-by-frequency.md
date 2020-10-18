# 按频率对元素排序 | 系列 1

> 原文： [https://www.geeksforgeeks.org/sort-elements-by-frequency/](https://www.geeksforgeeks.org/sort-elements-by-frequency/)

如果 2 个数字具有相同的频率，则以递减的频率打印数组的元素，然后打印第一个出现的频率。

 **示例**：

```
Input:  arr[] = {2, 5, 2, 8, 5, 6, 8, 8}
Output: arr[] = {8, 8, 8, 2, 2, 5, 5, 6}

Input: arr[] = {2, 5, 2, 6, -1, 9999999, 5, 8, 8, 8}
Output: arr[] = {8, 8, 8, 2, 2, 5, 5, 6, -1, 9999999}

```



**方法 1（使用排序）**：

*   使用排序算法对元素`O(nLogn)`进行排序。

*   扫描排序的数组，并构造一个 2D 元素数组，并计数`O(n)`。

*   根据计数`O(nLogn)`对 2D 数组排序。

**示例**：

```
  Input 2 5 2 8 5 6 8 8

  After sorting we get
  2 2 5 5 6 8 8 8

  Now construct the 2D array as
  2, 2
  5, 2
  6, 1
  8, 3

  Sort by count
  8, 3
  2, 2
  5, 2
  6, 1

```

**如果频率相同，如何保持元素顺序？**

如果频率相同，上述方法无法确定元素的顺序。 为了解决这个问题，我们应该在第 3 步中使用索引，如果两个计数相同，那么我们应该首先处理（或打印）具有较低索引的元素。 在步骤 1 中，我们应该存储索引而不是元素。

```
  Input 5  2  2  8  5  6  8  8

  After sorting we get
  Element 2 2 5 5 6 8 8 8
  Index   1 2 0 4 5 3 6 7

  Now construct the 2D array as
  Index, Count
  1,      2
  0,      2
  5,      1
  3,      3

  Sort by count (consider indexes in case of tie)
  3, 3
  0, 2
  1, 2
  5, 1

  Print the elements using indexes in the above 2D array.

```

下面是上述方法的实现。

```

// Sort elements by frequency. If two elements have same 
// count, then put the elements that appears first 
#include <bits/stdc++.h> 
using namespace std; 

// Used for sorting 
struct ele { 
    int count, index, val; 
}; 

// Used for sorting by value 
bool mycomp(struct ele a, struct ele b) 
{ 
    return (a.val < b.val); 
} 

// Used for sorting by frequency. And if frequency is same, 
// then by appearance 
bool mycomp2(struct ele a, struct ele b) 
{ 
    if (a.count != b.count) 
        return (a.count < b.count); 
    else
        return a.index > b.index; 
} 

void sortByFrequency(int arr[], int n) 
{ 
    struct ele element[n]; 
    for (int i = 0; i < n; i++) { 

        // Fill Indexes 
        element[i].index = i; 

        // Initialize counts as 0 
        element[i].count = 0; 

        // Fill values in structure 
        // elements 
        element[i].val = arr[i]; 
    } 

    /* Sort the structure elements according to value, 
       we used stable sort so relative order is maintained. */
    stable_sort(element, element + n, mycomp); 

    /* initialize count of first element as 1 */
    element[0].count = 1; 

    /* Count occurrences of remaining elements */
    for (int i = 1; i < n; i++) { 

        if (element[i].val == element[i - 1].val) { 
            element[i].count += element[i - 1].count + 1; 

            /* Set count of previous element as -1, we are 
               doing this because we'll again sort on the 
               basis of counts (if counts are equal than on 
               the basis of index)*/
            element[i - 1].count = -1; 

            /* Retain the first index (Remember first index 
               is always present in the first duplicate we 
               used stable sort. */
            element[i].index = element[i - 1].index; 
        } 

        /* Else If previous element is not equal to current 
          so set the count to 1 */
        else
            element[i].count = 1; 
    } 

    /* Now we have counts and first index for each element so now 
       sort on the basis of count and in case of tie use index 
       to sort.*/
    stable_sort(element, element + n, mycomp2); 
    for (int i = n - 1, index = 0; i >= 0; i--) 
        if (element[i].count != -1) 
            for (int j = 0; j < element[i].count; j++) 
                arr[index++] = element[i].val; 
} 

// Driver program 
int main() 
{ 
    int arr[] = { 2, 5, 2, 6, -1, 9999999, 5, 8, 8, 8 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    sortByFrequency(arr, n); 

    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    return 0; 
} 

```

**输出**：

```
8 8 8 2 2 5 5 6 -1 9999999 
```

感谢 Gaurav Ahirwar 提供了上述实现。

**方法 2（使用哈希和排序）**：

使用哈希机制，我们可以将元素（也包括第一个索引）及其计数存储在哈希中。 最后，根据哈希元素的计数对它们进行排序。

Below is the implementation of above approach.

```

#include <bits/stdc++.h> 
using namespace std; 

// Compare function 
bool fcompare(pair<int, pair<int, int> > p, 
                pair<int, pair<int, int> > p1) 
{ 
    if (p.second.second != p1.second.second) 
        return (p.second.second > p1.second.second); 
    else
        return (p.second.first < p1.second.first); 
} 

void sortByFrequency(int arr[], int n) 
{ 
    unordered_map<int, pair<int, int> > hash; // hash map 
    for (int i = 0; i < n; i++) { 
        if (hash.find(arr[i]) != hash.end()) 
            hash[arr[i]].second++; 
        else
            hash[arr[i]] = make_pair(i, 1); 
    } // store the count of all the elements in the hashmap 

    // Iterator to Traverse the Hashmap 
    auto it = hash.begin(); 

    // Vector to store the Final Sortted order 
    vector<pair<int, pair<int, int> > > b; 
    for (it; it != hash.end(); ++it) 
        b.push_back(make_pair(it->first, it->second)); 

    sort(b.begin(), b.end(), fcompare); 

    // Printing the Sorted sequence 
    for (int i = 0; i < b.size(); i++) { 
        int count = b[i].second.second; 
        while (count--) 
            cout << b[i].first << " "; 
    } 
} 

// Driver Function 
int main() 
{ 
    int arr[] = { 2, 5, 2, 6, -1, 9999999, 5, 8, 8, 8 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    sortByFrequency(arr, n); 

    return 0; 
} 

```

**输出**：

```
8 8 8 2 2 5 5 6 -1 9999999 
```

**方法 3（使用 BST 和排序）**：

*   在 BST 中一一插入元素，如果已经存在一个元素，则增加节点的计数。 二叉搜索树的节点（用于此方法）如下。

    ```

    struct tree { 
        int element; 
        int first_index /*To handle ties in counts*/
            int count; 
    } BST;</div> 

    ```

*   将第一个索引和相应的 BST 计数存储在 2D 数组中。

*   根据计数对 2D 数组进行排序（在平局的情况下使用索引）。

**时间复杂度**：如果使用[自平衡二分搜索树](http://en.wikipedia.org/wiki/Self-balancing_binary_search_tree)，则`O(nLogn)`。 这在[系列 2](https://www.geeksforgeeks.org/sort-elements-by-frequency-set-2/) 中实现。

[系列 2：按频率对元素进行排序](https://www.geeksforgeeks.org/sort-elements-by-frequency-set-2/)

