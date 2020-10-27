# 查询以插入，删除数字的一次出现并打印最少和最频繁的元素

给定 Q 查询的类型为 1、2、3 和 4，如下所述。

*   **Type-1**：在列表中插入一个数字。
*   **Type-2**：仅删除一次出现的数字（如果存在）。
*   **Type-3**：打印最不频繁的元素，如果存在多个元素，则打印其中最频繁的元素。
*   **Type-4**：打印最频繁的元素，如果存在多个元素，则打印其中最小的元素。

任务是编写一个程序来执行上述所有查询。

**示例**：

> **输入**：
> Query1：1 6
> Query2：1 6
> Query3：1 7
> Query4：3
> Query5：1 7
> Query6：2 7
> Query7：1 7
> Query8：3
> Query9：4
> 
> **输出**：
> 7
> 7
> 6
> 
> 回答 Query4 时，频率 6 为 2，
> 7 的频率为 1，因此，最不频繁的元素为 7。
> 在 Query8 中，最不频繁的元素为 6 和 7，因此打印最大。
> 在 Query9 中，最频繁的元素是 6 和 7，因此打印最小的元素。

**天真的方法**是使用任何[数据结构（数组，向量等）](https://www.geeksforgeeks.org/data-structures/)并存储所有元素。 使用[哈希表](https://www.geeksforgeeks.org/hashing-data-structure/)，可以存储每个元素的频率。 在处理类型 2 的查询时，请从已存储元素的 DS 中删除该元素的一次出现。 类型 3 和类型 4 的查询可以通过遍历哈希表来回答。 每个查询的时间复杂度为 **O（N）**，其中 N 是 DS 中直到那时的元素数。

**有效方法**将使用[设置](http://www.geeksforgeeks.org/set-in-cpp-stl/)容器来回答每个查询。 使用两组哈希表，可以在每个查询的 **O（log n）**中解决上述问题。 使用两组 *s1* 和 *s2* ，一组存储 ***{num，frequency}*** ，而另一组存储 *[ **{frequency，number}*** 。 使用散列图来存储每个数字的频率。 使用运算符重载设计集合 s2，以使其按第一个元素的升序排序。 如果第一个元素看起来与一个或多个元素相同，则该集合将按第二个元素的降序排序。 用户定义的[操作重载](https://www.geeksforgeeks.org/operator-overloading-c/)功能将是：

```
bool operator b.second;          
 return a.first < b.first;
}
Note: Operator overloading only works with user-defined 
data-types. *pr* is a struct which has first and second as two integers. 
(pr>
```

以下是解决每种类型的查询的算法：

*   **Type1**：使用哈希表检查元素是否存在。 如果不存在，则在[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)中标记该数字。 使用 [insert（）](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)在集 s1 中插入 **{num，1}** 并在 set2 中插入 **{1，num}** 在 set2 中。 如果以前存在，则从哈希表中获取频率，然后使用 [find（）从 set1 中删除 **{num，frequency}** ，并从 set2 中删除 **{frequency，num}** [](https://www.geeksforgeeks.org/set-find-function-in-c-stl/) 和 [delete（）](https://www.geeksforgeeks.org/seterase-c-stl/)函数。 在[set1]中插入 **{num，frequency + 1}** ，在[set2]中插入 **{frequency + 1，num}** 。 另外，增加哈希表中的计数。
*   **Type2**：遵循与查询类型 1 相同的过程。 唯一的区别是减少哈希表中的计数，并在[set1]中插入 **{num，frequency-1}** ，在[set2]中插入 **{frequency-1，num}** 。
*   **Type3**：打印可​​以使用 begin（）函数获得的开始元素，因为该集合的设计方式是 [begin（）](https://www.geeksforgeeks.org/setbegin-setend-c-stl/)返回最不频繁的元素。 如果有多个，则返回最大的。
*   **Type4**：打印集合中的最后一个元素，可以使用集合中的 [rbegin（）](https://www.geeksforgeeks.org/setrbegin-and-setrend-in-c-stl/)函数获得该元素。

下面是上述方法的实现：

```
// C++ program for performing
// Queries of insert, delete one
//  occurrence of a number and
// print the least and most frequent element
#include <bits/stdc++.h>
using namespace std;
// user-defined data-types
struct pr {
int first;
int second;
};
// user-defined function to
// design a set
bool operator<(pr a, pr b)
{
if (a.first == b.first)
return a.second > b.second;
return a.first < b.first;
}
// declare a user-defined set
set<pr> s1, s2;
// hash map
unordered_map< int , int > m;
// Function to process the query
// of type-1
void type1( int num)
{
// if the element is already there
if (m[num]) {
// get the frequency of the element
int cnt = m[num];
// returns an iterator pointing to
// position where the pair is
auto it1 = s1.find({ num, cnt });
auto it2 = s2.find({ cnt, num });
// deletes the pair from sets
s1.erase(it1);
s2.erase(it2);
// re-insert the pair by increasing
// frequency
s1.insert({ num, m[num] + 1 });
s2.insert({ m[num] + 1, num });
}
[
[HTG9 4]
// if the element is not there in the list
else {
// insert the element with frequency 1
s1.insert({ num, 1 });
s2.insert({ 1, num });
}
]      // increase the count in hash-table
m[num] += 1;
}
[
// Function to process the query
// of type-2
void type2( int num)
{
// if the element exists
if (m[num]) {
// get the frequency of the element
int cnt = m[num];
]   [
// returns an iterator pointing to
// position where the pair is
auto it1 = s1.find({ num, cnt });
auto it2 = s2.find({ cnt, num });
// deletes the pair from sets
s1.erase(it1);
s2.erase(it2);
// re-insert the pair by increasing
// frequency
s1.insert({ num, m[num] - 1 });
s2.insert({ m[num] - 1, num });
// decrease the count
m[num] -= 1;
}
}
// Function to process the query
// of type-3
int type3()
{
// if the set is not empty
// return the first element
if (!s1.empty()) {
auto it = s2.begin();
return it->second;
}
else
return -1;
]
}
// Function to process the query
// of type-4
int type4()
{
// if the set is not empty
// return the last element
if (!s1.empty()) {
auto it = s2.rbegin();
return it->second;
}
[
else
return -1;
}
// Driver Code
int main()
{
[H TG232]
// inserts 6, 6 and 7
type1(6);
type1(6);
type1(7);
// print the answer to query of type3
cout << type3() << endl;
// inserts 7
type1(7);
// deletes one occurrence of 7
type2(7);
type1(7);
// print the answer to query of type3
cout << type3() << endl;
// print the answer to query of type4
]      cout << type4() << endl;
return 0;
}
```

**Output:**

```
7
7
6

```

**时间复杂度：每个查询** O（log N）。
**辅助空间**：O（N）



* * *

* * *



