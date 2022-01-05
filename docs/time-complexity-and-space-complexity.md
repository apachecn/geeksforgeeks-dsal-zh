# 时间复杂度和空间复杂度

> 原文:[https://www . geeksforgeeks . org/时间复杂性和空间复杂性/](https://www.geeksforgeeks.org/time-complexity-and-space-complexity/)

一般来说，在计算机科学中，用不同的算法解决一个问题的方法总是不止一种。因此，非常需要使用一种方法来比较解决方案，以判断哪一个更优。方法必须是:

*   独立于运行算法的机器及其配置。
*   显示了与输入数量的直接相关性。
*   可以清晰的区分两种算法，没有歧义。

这样的方法有两种， [**时间复杂度**](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/) 和 [**空间复杂度**](https://www.geeksforgeeks.org/g-fact-86/) 下面讨论:

**时间复杂度:**算法的时间复杂度将算法运行所花费的时间量量化为输入长度的函数。请注意，运行时间是输入长度的函数，而不是运行算法的机器的实际执行时间。

为了计算算法的时间复杂度，假设取一个**时间常数 c** 执行一个运算，然后计算一个输入长度在 **N** 上的总运算。举个例子来理解计算的过程:假设一个问题是[发现一个数组中是否存在一对 **(X，Y)** ，一对 **N** 元素，其和为 **Z**](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/) 。最简单的想法是考虑每一对，检查它是否满足给定的条件。

伪代码如下:

```
int a[n];
for(int i = 0;i < n;i++)
  cin >> a[i]

for(int i = 0;i < n;i++)
  for(int j = 0;j < n;j++)
    if(i!=j && a[i]+a[j] == z)
       return true

return false
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a pair in the given
// array whose sum is equal to z
bool findPair(int a[], int n, int z)
{
    // Iterate through all the pairs
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)

            // Check if the sum of the pair
            // (a[i], a[j]) is equal to z
            if (i != j && a[i] + a[j] == z)
                return true;

    return false;
}

// Driver Code
int main()
{
    // Given Input
    int a[] = { 1, -2, 1, 0, 5 };
    int z = 0;
    int n = sizeof(a) / sizeof(a[0]);

    // Function Call
    if (findPair(a, n, z))
        cout << "True";
    else
        cout << "False";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find a pair in the given
// array whose sum is equal to z
static boolean findPair(int a[], int n, int z)
{

    // Iterate through all the pairs
    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)

            // Check if the sum of the pair
            // (a[i], a[j]) is equal to z
            if (i != j && a[i] + a[j] == z)
                return true;

    return false;
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int a[] = { 1, -2, 1, 0, 5 };
    int z = 0;
    int n = a.length;

    // Function Call
    if (findPair(a, n, z))
        System.out.println("True");
    else
        System.out.println("False");
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a pair in the given
# array whose sum is equal to z
def findPair(a, n, z) :

    # Iterate through all the pairs
    for i in range(n) :
        for j in range(n) :

            # Check if the sum of the pair
            # (a[i], a[j]) is equal to z
            if (i != j and a[i] + a[j] == z) :
                return True

    return False

# Driver Code

# Given Input
a = [ 1, -2, 1, 0, 5 ]
z = 0
n = len(a)

# Function Call
if (findPair(a, n, z)) :
    print("True")
else :
    print("False")

    # This code is contributed by splevel62.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to find a pair in the given
// array whose sum is equal to z
static bool findPair(int[] a, int n, int z)
{

    // Iterate through all the pairs
    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)

            // Check if the sum of the pair
            // (a[i], a[j]) is equal to z
            if (i != j && a[i] + a[j] == z)
                return true;

    return false;
}

// Driver Code
static void Main()
{
     // Given Input
    int[] a = { 1, -2, 1, 0, 5 };
    int z = 0;
    int n = a.Length;

    // Function Call
    if (findPair(a, n, z))
        Console.WriteLine("True");
    else
        Console.WriteLine("False");
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find a pair in the given
// array whose sum is equal to z
function findPair(a, n, z)
{

    // Iterate through all the pairs
    for(let i = 0; i < n; i++)
        for(let j = 0; j < n; j++)

            // Check if the sum of the pair
            // (a[i], a[j]) is equal to z
            if (i != j && a[i] + a[j] == z)
                return true;

    return false;
}

// Driver Code

// Given Input
let a = [ 1, -2, 1, 0, 5 ];
let z = 0;
let n = a.length;

// Function Call
if (findPair(a, n, z))
    document.write("True");
else
    document.write("False");

// This code is contributed by code_hunt

</script>
```

**Output**

```
False
```

假设计算机中的每一个操作都需要大约恒定的时间，让它成为 **c** 。执行的代码行数实际上取决于 **Z** 的值。在算法分析过程中，主要考虑最坏的情况，即没有和等于 **Z** 的元素对。在最坏的情况下，

*   输入需要 **N*c** 操作。
*   外环 **i** 环运行 **N** 次。
*   对于每个 **i** ，内环 **j** 循环运行 **N** 次。

所以总执行时间为 **N*c + N*N*c + c** 。现在忽略低阶项，因为低阶项对于大输入来说相对不重要，因此只取最高阶项(没有常数)，在这种情况下是 **N*N** 。不同的符号被用来描述函数的极限行为，但是由于采用了最坏的情况，所以[大 0 符号](https://www.geeksforgeeks.org/analysis-algorithms-big-o-analysis/)将被用来表示时间复杂度。

因此，对于上述算法，时间复杂度为 **O(N <sup>2</sup> )** 。请注意，时间复杂度仅基于数组 **A** 中的元素数量，即输入长度，因此如果数组的长度增加，执行时间也会增加。

**增长顺序**是执行的时间如何取决于输入的长度。在上面的例子中，很明显，执行时间二次取决于数组的长度。增长顺序将有助于轻松计算运行时间。

**另一个例子:**我们来计算一下下面算法的时间复杂度:

## C++

```
count = 0
for (int i = N; i > 0; i /= 2)
  for (int j = 0; j < i; j++)
    count++;
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
int count = 0 ;
for (int i = N; i > 0; i /= 2)
    for (int j = 0; j < i; j++)
        count++;

//This code is contributed by Shubham Singh
```

## C#

```
int count = 0 ;
for (int i = N; i > 0; i /= 2)
    for (int j = 0; j < i; j++)
        count++;

// This code is contributed by Shubham Singh
```

## java 描述语言

```
let count = 0
for(let i = N; i > 0; i /= 2)
    for(let j = 0; j < i; j++)
        count += 1;

// This code is contributed by Shubham Singh
```

这是一个棘手的案件。第一眼看上去好像复杂度是 **O(N * log N)** 。 **N** 代表 **j 的**弧线， **log(N)** 代表 **i 的**弧线。但这是错误的。让我们看看为什么。

想想**计数++** 会跑多少次。

*   当 **i = N** 时，它将运行 **N** 次。
*   当 **i = N / 2** 时，它将运行 **N / 2** 次。
*   当 **i = N / 4** 时，它将运行 **N / 4** 次。
*   等等。

**计数++** 运行的总次数为 **N + N/2 + N/4+…+1= 2 * N** 。所以时间复杂度会是 **O(N)** 。

下面列出了一些一般的时间复杂性，以及它们在竞争性编程中被接受的输入范围:

<figure class="table">

| **输入长度** | **最差接受时间复杂度** | **通常的解决方案类型** |
| 10 -12 | O(N！) | [递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/) |
| 15-18

 | O(2 <sup>N</sup> * N) | 递归、回溯和[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/) |
| 18-22 | O(2 <sup>N</sup> * N) | 递归、回溯和位操作 |
| 30-40 | O(2 <sup>N/2</sup> * N) | [中段相遇](https://www.geeksforgeeks.org/meet-in-the-middle/)[分而治之](https://www.geeksforgeeks.org/divide-and-conquer-introduction/) |
| One hundred | O(N <sup>4</sup> ) | [动态编程](https://www.geeksforgeeks.org/dynamic-programming/)[建设性](https://www.geeksforgeeks.org/basic/constructive-algorithms/) |
| four hundred | O(N <sup>3</sup> ) | 动态规划，建设性 |
| 2K | O(N <sup>2</sup> * log N) | 动态规划，[二分搜索法](https://www.geeksforgeeks.org/binary-search/)[排序](https://www.geeksforgeeks.org/sorting-algorithms/)
分而治之 |
| 10K | O(N <sup>2</sup> ) | 动态编程，[图形](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，[树木](https://www.geeksforgeeks.org/binary-tree-data-structure/)，建设性 |
| 1M

 | O(N*对数 N) | 排序，二分搜索法，分而治之 |
| 100 米 | 氧(氮)、氧(对数氮)、氧(1) | 建设性，[数学，](https://www.geeksforgeeks.org/mathematical-algorithms/)T2】贪婪算法 |

**空间复杂度:**算法的**空间复杂度**将算法运行所占用的空间量量化为输入长度的函数。举个例子:假设一个问题求数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

伪代码如下:

```
int freq[n];
int a[n];

for(int i = 0; i<n; i++)
{
   cin>>a[i];
   freq[a[i]]++;
}  
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count frequencies of array items
void countFreq(int arr[], int n)
{
    unordered_map<int, int> freq;

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Traverse through map and print frequencies
    for (auto x : freq)
        cout << x.first << " " << x.second << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countFreq(arr, n);
    return 0;
}
```

**Output**

```
5 1
10 3
20 4
```

这里算法中使用了两个长度为 **N** 的数组和变量 **i** ，因此使用的总空间为 **N * c + N * c + 1 * c = 2N * c + c** ，其中 **c** 为单位空间。对于很多输入，常量 **c** 微不足道，可以说空间复杂度为 **O(N)** 。

还有**辅助空间，**不同于空间复杂度。主要区别在于空间复杂度量化了算法使用的总空间，辅助空间量化了算法中除给定输入之外使用的额外空间。在上面的例子中，辅助空间是 freq[]数组使用的空间，因为它不是给定输入的一部分。所以总辅助空间是 **N * c + c** ，也就是 **O(N)** 而已。

</figure>