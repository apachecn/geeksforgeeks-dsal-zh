# 数组

> 原文：[https://www.geeksforgeeks.org/sum-and-product-of-k-smallest-and-largest-fibonacci-numbers-in-the-array/](https://www.geeksforgeeks.org/sum-and-product-of-k-smallest-and-largest-fibonacci-numbers-in-the-array/)

中 K 个最小和最大斐波纳契数的总和与乘积

给定一个整数 **K** 和一个包含 **N** 个整数的数组 **arr []** ，任务是找到最小的 **K** 的和和乘积 数组中最大的 **K** 斐波那契数。

**注意**：假设数组中至少有 **K** 个斐波那契数。

**示例**：

> **输入**：arr [] = {2，5，6，8，10，11}，K = 2
> **输出**：
> K 个最小斐波那契数的总和 是 7
> K-最小斐波那契数的乘积是 10
> K-最大斐波那契数的总和是 13
> K-最大斐波那契数的乘积是 40
> **说明**：
> {2，5，8}是数组中唯一的斐波那契数。
> {2，5}是其中的 2 个最小值，{5，8}是其中的 2 个最大值。
> 
> **输入**：arr [] = {3，2，12，13，5，19}，K = 3
> **输出**：
> K 个最小斐波那契数之和 是 10
> K-最小斐波那契数的乘积是 30
> K-最大斐波那契数的总和是 21
> K-最小斐波那契数的乘积是 195

**方法**：的想法是使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储[斐波纳契结点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)到最大值，并将其存储在[设置](https://www.geeksforgeeks.org/set-in-java/)中，以 使检查变得容易和高效（在 O（1）时间内）。

1.  遍历整个数组并获得列表中的最大值。

2.  现在，构建一个[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中包含所有小于或等于数组最大值的 Fibonacci 节点。

完成上述预计算后，遍历数组并将所有斐波那契数都插入两个[堆](https://www.geeksforgeeks.org/binary-heap/)，*最小堆和最大堆*中。

现在，从最小堆和最大堆中弹出顶部的 **K** 元素，以计算 **K** 斐波那契数的*和*和*乘积*。

下面是上述方法的实现：

```
// C++ program to find the sum and
// product of K smallest and K
// largest Fibonacci numbers in an array
#include <bits/stdc++.h>
using namespace std;
// Function to create the hash table
// to check Fibonacci numbers
void createHash(set< int >& hash,
int maxElement)
{
// Inserting the first two elements
// into the hash
int prev = 0, curr = 1;
hash.insert(prev);
hash.insert(curr);
[HTG30
// Computing the remaining
// elements using
// the previous two elements
while (curr <= maxElement) {
int temp = curr + prev;
hash.insert(temp);
prev = curr;
curr = temp;
[H TG309]      }
}
// Function that calculates the sum
// and the product of K smallest and
// K largest Fibonacci numbers in an array
void fibSumAndProduct( int arr[],
int n, int k)
{
// Find the maximum value in the array
int max_val = *max_element(arr, arr + n);
// Creating a hash containing
// all the Fibonacci numbers
// upto the maximum data value
// in the array
set< int > hash;
createHash(hash, max_val);
// Max Heap to store all the
// Fibonacci numbers
priority_queue< int > maxHeap;
[
// Min Heap to store all the
// Fibonacci numbers [
priority_queue< int ,
vector< int >,
greater< int > >
minHeap;
// Push all the fibonacci numbers
// from the array to the heaps
for ( int i = 0; i < n; i++)
if (hash.find(arr[i])
!= hash.end()) {
minHeap.push(arr[i]);
maxHeap.push(arr[i]);
}
long long int minProduct = 1,
maxProduct = 1,
minSum = 0,
maxSum = 0;
// Finding the K minimum
// and the K maximum
// elements from the heaps
while (k--) {
// Calculate the products
minProduct *= minHeap.top();
maxProduct *= maxHeap.top();
// Calculate the sum
minSum += minHeap.top();
maxSum += maxHeap.top();
// Pop the current
// minimum element
]          minHeap.pop();
// Pop the current
// maximum element
maxHeap.pop();
}
cout << "Sum of K-minimum "
<< "fibonacci numbers is "
<< minSum << "\n" ;
cout << "Product of K-minimum "
<< "fibonacci numbers is "
<< minProduct << "\n" ;
cout << "Sum of K-maximum "
<< "fibonacci numbers is "
<< maxSum << "\n" ;
cout << "Product of K-maximum "
<< "fibonacci numbers is "
<< maxProduct;
}
// Driver code
int main()
{
int arr[] = { 2, 5, 6, 8, 10, 11 };
int N = sizeof (arr) / sizeof (arr[0]);
int K = 2;
fibSumAndProduct(arr, N, K);
return 0;
[HTG4 95] }
```

**Output:**

```
Sum of K-minimum fibonacci numbers is 7
Product of K-minimum fibonacci numbers is 10
Sum of K-maximum fibonacci numbers is 13
Product of K-maximum fibonacci numbers is 40

```



* * *

* * *



