# 找到四个元素的总和为给定值| 组合 3（哈希图）

给定一个整数数组，请检查数组中不同索引处是否存在四个元素的总和等于给定值 k。

例如，如果给定的数组为{1 5 1 0 6 0}且 k = 7，则您的函数应将“是”打印为（1 + 5 + 1 + 0 = 7）。

例子：

```
Input  : arr[] = {1 5 1 0 6 0} 
             k = 7
Output : YES

Input :  arr[] = {38 7 44 42 28 16 10 37 
                  33 2 38 29 26 8 25} 
            k = 22
Output : NO

```

我们在以下两组中讨论了不同的解决方案。

[找出四个总和为给定值的元素| 设置 1（n ^ 3 个解）](https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/)

[找出四个总和为给定值的元素| 集合 2（O（n ^ 2Logn）解决方案）](https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-set-2/)

在这篇文章中，讨论了一种优化的解决方案，该解决方案平均可以在 O（n <sup>2</sup> ）中工作。

这个想法是创建一个散列图来存储对和。

```
Loop i = 0 to n-1 :
 Loop j = i + 1 to n-1  
   calculate sum = arr[i] + arr[j]
     If (k-sum) exist in hash 
      a) Check in hash table for all
         pairs of indexes which form
         (k-sum).
      b) If there is any pair with no 
         no common indexes.
           return true 
    Else  update hash table
    EndLoop;
EndLoop;

```

```
// C++ program to find if there exist 4 elements
// with given sum
#include <bits/stdc++.h>
using namespace std;
[
// function to check if there exist four
// elements whose sum is equal to k
bool findfour( int arr[], int n, int k)
{
// map to store sum and indexes for
// a pair sum
unordered_map< int , vector<pair< int , int > > > hash;
for ( int i = 0; i < n; i++) {
] for ( int j = i + 1; j < n; j++) {
// calculate the sum of each pair
int sum = arr[i] + arr[j];
// if k-sum exist in map
if (hash.find(k - sum) != hash.end()) {
auto num = hash.find(k - sum);
vector<pair< int , int > > v = num->second;
// check for index coincidence as if
// there is a common that means all
// the four numbers are not from
// different indexes and one of the
// index is repeated
for ( int k = 0; k < num->second.size(); k++) {
pair< int , int > it = v[k];
]
// if all indexes are different then
// it means four number exist
// set the flag and break the loop
if (it.first != i && it.first != j &&
it.second != i && it.second != j)
return true ;
}
}
// store the sum and index pair in hashmap
hash[sum].push_back(make_pair(i, j));
}
]
}
hash.clear();
return false ;
}
[
// Driver code
int main()
{
int k = 7;
int arr[] = { 1, 5, 1, 0, 6, 0 };
int n = sizeof (arr) / sizeof (arr[0]);
if (findfour(arr, n, k))
cout
<< "YES" << endl;
else ]
cout << "NO" << endl;
return 0;
}
```

输出：

```
YES

```

本文由 **Niteesh Kumar** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

