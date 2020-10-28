# 将数组的元素映射到另一个数组的元素

给定两个具有正整数的数组 *A* 和 *B* ，只有当两个数组 *A* 都可以映射到数组 *A* 的元素时， 元素具有相同的值。 任务是计算数组 *A* 中的位置，数组 *B* 的元素将映射到该位置。 如果无法完成特定元素的映射，则打印 NA。

**注意**：对于一个位置，只能映射一个整数。

**示例**：

> **输入**：A [] = {1、5、2、4、4、3}，B [] = {1、2、5、1}
> **输出**：0 2 1 NA
> B [0]，B [1]和 B [2]可以分别映射到 A [0]，A [2]和 A [1]，但 B [3]不能映射到任何 A 的元素，因为 A 中唯一的“ 1”已被映射
> 
> **输入**：A [] = {2，1，2，3，3，4，2，4，1}，B [] = {1,2,5,1,2,4,2 ，3，2，1}
> **输出**：1 0 NA 8 2 5 6 3 NA NA

想法是使用哈希表，其中键是 A []的元素，值是这些元素的索引。 由于一个元素可以出现多个，因此我们在哈希表中使用一列项目作为值。

下面是上述问题的实现：

```
// C++ program to map elements of an array
// to equal elements of another array
#include <bits/stdc++.h>
using namespace std;
[
// Function to print the mapping of elements
void printMapping( int A[], int B[], int N, int M)
{
[
// Create a hash table where all indexes are
// stored for a given value int , list< int >> m;
for ( int i=0; i<N; i++)
m[A[i]].push_back(i);
[
// Traverse through B[]
for ( int i=0; i<M; i++)
{
// If a mapping is found, print the mapping and
// remove the index from hash table so that the
// same element of A[] is not mapped again.
if (m.find(B[i]) != m.end() && m[B[i]].size() > 0)
{
cout << m[B[i]].front() << " " ;
m[B[i]].pop_front();
}
[
else // No mapping found
{
HTG172]
}
}
}
// Driver code
int main()
{
int A[] = {2, 1, 2, 3, 3, 4, 2, 4, 1};
int N = sizeof (A) / sizeof (A[0]);
int B[] = {1, 2, 5, 1, 2, 4, 2, 3, 2, 1};
int M = sizeof (B) / sizeof (B[0]);
printMapping(A, B, N, M);
return 0;
}
```

**Output:**

```
1 0 NA 8 2 5 6 3 NA NA

```



* * *

* * *



