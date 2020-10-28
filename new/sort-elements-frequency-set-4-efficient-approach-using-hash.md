# 按频率对元素进行排序| 第 4 组（使用哈希的有效方法）

如果 2 个数字具有相同的频率，则以递减的频率打印数组的元素，然后打印第一个出现的频率。

**示例**：[

```
Input : arr[] = {2, 5, 2, 8, 5, 6, 8, 8}
Output : arr[] = {8, 8, 8, 2, 2, 5, 5, 6}

Input : arr[] = {2, 5, 2, 6, -1, 9999999, 5, 8, 8, 8}
Output : arr[] = {8, 8, 8, 2, 2, 5, 5, 6, -1, 9999999}

```

我们在以下帖子中讨论了不同的方法：

[按频率对元素进行排序| 设置 1](https://www.geeksforgeeks.org/sort-elements-by-frequency/)

[按频率对元素进行排序| 集 2](https://www.geeksforgeeks.org/sort-elements-by-frequency-set-2/)

[按频率对数组元素进行排序| 集合 3（使用 STL）](http://Sorting Array Elements By Frequency | Set 3 (Using STL))

以上所有方法均在 O（n Log n）时间内工作，其中 n 是元素总数。 在这篇文章中，讨论了一种在 **O（n + m Log m）**时间中工作的新方法，其中 n 是元素总数，m 是不同元素总数。

这个想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)。

1.  我们将所有元素及其计数插入哈希中。 此步骤花费 O（n）时间，其中 n 是元素数。

2.  我们将哈希的内容复制到数组（或向量）中，并按计数对其进行排序。 此步骤花费 O（m Log m）时间，其中 m 是不同元素的总数。

3.  为了在频率相同的情况下保持元素的顺序，我们使用另一个散列，该散列的键为数组的元素，而值为索引。 如果两个元素的频率相同，则根据索引对元素进行排序。

下图是上述方法的模拟：

![](img/8216aa935ae2833360ce5c42a0c8a7d5.png)

我们不需要声明另一个映射 m2，因为它没有为问题提供适当的预期结果。

相反，我们只需要检查 sortByVal 函数中作为参数发送的对的第一个值即可。

下面是上述方法的实现：

## C++

```cpp

//     CPP program for the above approach 
#include <bits/stdc++.h>
using namespace std;

// Used for sorting by frequency. And if frequency is same,
// then by appearance
bool sortByVal(const pair<int, int>& a, 
                      const pair<int, int>& b)
{

   // If frequency is same then sort by index
   if (a.second == b.second)  
       return a.first < b.first;

   return a.second > b.second;
}

// function to sort elements by frequency
vector<int>sortByFreq(int a[], int n)
{

   vector<int>res;

   unordered_map<int, int> m;

   vector<pair<int, int> > v;

   for (int i = 0; i < n; ++i) {

       // Map m is used to keep track of count  
       // of elements in array
       m[a[i]]++;      
   }

   // Copy map to vector
   copy(m.begin(), m.end(), back_inserter(v));

   // Sort the element of array by frequency
   sort(v.begin(), v.end(), sortByVal);

   for (int i = 0; i < v.size(); ++i)  
      while(v[i].second--)
      {
              res.push_back(v[i].first);
      }

   return res;
}

// Driver program
int main()
{

   int a[] = { 2, 5, 2, 6, -1, 9999999, 5, 8, 8, 8 };
   int n = sizeof(a) / sizeof(a[0]);
   vector<int>res;
   res = sortByFreq(a, n);

   for(int i = 0;i < res.size(); i++)
         cout<<res[i]<<" ";

   return 0;

}

```

输出：

```
8 8 8 2 2 5 5 6 -1 9999999 

```

时间复杂度：O（n）+ O（m Log m）其中，n 是元素总数，m 是不同元素的总数。

本文由贡献。 ]和**被** [**Ankur Goel**](https://auth.geeksforgeeks.org/user/AnkurGoel) 改进。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

