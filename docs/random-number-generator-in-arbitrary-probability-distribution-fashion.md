# 任意概率分布方式的随机数发生器

> 原文:[https://www . geesforgeks . org/随机数生成器-任意概率分布-时尚/](https://www.geeksforgeeks.org/random-number-generator-in-arbitrary-probability-distribution-fashion/)

给定 n 个数字，每个数字都有一定的出现频率。返回一个概率与其出现频率成正比的随机数。

示例:

```
Let following be the given numbers.
  arr[] = {10, 30, 20, 40}  

Let following be the frequencies of given numbers.
  freq[] = {1, 6, 2, 1}  

The output should be
  10 with probability 1/10
  30 with probability 6/10
  20 with probability 2/10
  40 with probability 1/10
```

很明显，简单的随机数发生器在这里不起作用，因为它不记录出现的频率。

我们需要以某种方式把这个问题转化成一个我们知道其解决方案的问题。

一个简单的方法是取一个辅助数组(比如 aux[])并根据数字出现的频率复制它们。生成一个介于 0 到 Sum-1(包括两者)之间的随机数(比如 r)，其中 Sum 表示频率数组的总和(上例中为 freq[])。返回随机数 aux[r](这个方法的实现留给读者练习)。

上面讨论的上述方法的局限性是当出现频率高时会消耗大量内存。如果输入是 997、8761 和 1，这种方法显然效率不高。

如何才能降低内存消耗？下面是使用 O(n)个额外空间的详细算法，其中 n 是输入数组中的元素数量。
**1。**取一个大小为 n.
**2 的辅助阵(比如前缀[])。**用前缀和填充它，使得前缀[i]表示从 0 到 I 的数字的和。
**3。**生成 1 到 Sum(包括两者)之间的随机数(比如 r)，其中 Sum 表示输入频率阵列的总和。
**4。**在前缀数组中找到步骤#3 生成的随机数 Ceil 的索引。让指数为指数 **c** 。
**5。**返回随机数 arr[indexc]，其中 arr[]包含输入的 n 个数字。
在进入实现部分之前，我们先用一个例子快速看一下算法:
arr[]: {10，20，30}
freq[]: {2，3，1}
前缀[]: {2，5，6}
由于前缀中的最后一个条目是 6，所以 r 的所有可能值都是[1，2，3，4，5，6]
1: Ceil 是 2。生成的随机数是 10。
2:Cell 为 2。生成的随机数是 10。
3:Cell 为 5。生成的随机数是 20。
4:Cell 为 5。生成的随机数是 20。
5:Cell 为 5。生成的随机数是 20。
6。天花板是 6 层。生成的随机数是 30。
在上面的例子中
10 以 2/6 的概率生成。
20 生成概率 3/6。
30 以概率 1/6 生成。

**这是如何工作的？**
任何数字输入[i]的生成次数与其出现频率相同，因为范围内存在整数计数(前缀[I–1]，前缀[i]]为输入[i]。像上面的例子一样，3 被生成三次，因为存在 3 个整数 3、4 和 5，它们的上限是 5。

## C++

```
// C++ program to generate random numbers
// according to given frequency distribution
#include <bits/stdc++.h>
using namespace std;

// Utility function to find ceiling of r in arr[l..h]
int findCeil(int arr[], int r, int l, int h)
{
    int mid;
    while (l < h)
    {
        mid = l + ((h - l) >> 1); // Same as mid = (l+h)/2
        (r > arr[mid]) ? (l = mid + 1) : (h = mid);
    }
    return (arr[l] >= r) ? l : -1;
}

// The main function that returns a random number
// from arr[] according to distribution array
// defined by freq[]. n is size of arrays.
int myRand(int arr[], int freq[], int n)
{
    // Create and fill prefix array
    int prefix[n], i;
    prefix[0] = freq[0];
    for (i = 1; i < n; ++i)
        prefix[i] = prefix[i - 1] + freq[i];

    // prefix[n-1] is sum of all frequencies.
    // Generate a random number with
    // value from 1 to this sum
    int r = (rand() % prefix[n - 1]) + 1;

    // Find index of ceiling of r in prefix array
    int indexc = findCeil(prefix, r, 0, n - 1);
    return arr[indexc];
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4};
    int freq[] = {10, 5, 20, 100};
    int i, n = sizeof(arr) / sizeof(arr[0]);

    // Use a different seed value for every run.
    srand(time(NULL));

    // Let us generate 10 random numbers according to
    // given distribution
    for (i = 0; i < 5; i++)
    cout << myRand(arr, freq, n) << endl;

    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
//C program to generate random numbers according to given frequency distribution
#include <stdio.h>
#include <stdlib.h>

// Utility function to find ceiling of r in arr[l..h]
int findCeil(int arr[], int r, int l, int h)
{
    int mid;
    while (l < h)
    {
         mid = l + ((h - l) >> 1);  // Same as mid = (l+h)/2
        (r > arr[mid]) ? (l = mid + 1) : (h = mid);
    }
    return (arr[l] >= r) ? l : -1;
}

// The main function that returns a random number from arr[] according to
// distribution array defined by freq[]. n is size of arrays.
int myRand(int arr[], int freq[], int n)
{
    // Create and fill prefix array
    int prefix[n], i;
    prefix[0] = freq[0];
    for (i = 1; i < n; ++i)
        prefix[i] = prefix[i - 1] + freq[i];

    // prefix[n-1] is sum of all frequencies. Generate a random number
    // with value from 1 to this sum
    int r = (rand() % prefix[n - 1]) + 1;

    // Find index of ceiling of r in prefix array
    int indexc = findCeil(prefix, r, 0, n - 1);
    return arr[indexc];
}

// Driver program to test above functions
int main()
{
    int arr[]  = {1, 2, 3, 4};
    int freq[] = {10, 5, 20, 100};
    int i, n = sizeof(arr) / sizeof(arr[0]);

    // Use a different seed value for every run.
    srand(time(NULL));

    // Let us generate 10 random numbers according to
    // given distribution
    for (i = 0; i < 5; i++)
      printf("%d\n", myRand(arr, freq, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate random numbers
// according to given frequency distribution
class GFG
{

// Utility function to find ceiling of r in arr[l..h]
static int findCeil(int arr[], int r, int l, int h)
{
    int mid;
    while (l < h)
    {
        mid = l + ((h - l) >> 1); // Same as mid = (l+h)/2
        if(r > arr[mid])
            l = mid + 1;
        else
            h = mid;
    }
    return (arr[l] >= r) ? l : -1;
}

// The main function that returns a random number
// from arr[] according to distribution array
// defined by freq[]. n is size of arrays.
static int myRand(int arr[], int freq[], int n)
{
    // Create and fill prefix array
    int prefix[] = new int[n], i;
    prefix[0] = freq[0];
    for (i = 1; i < n; ++i)
        prefix[i] = prefix[i - 1] + freq[i];

    // prefix[n-1] is sum of all frequencies.
    // Generate a random number with
    // value from 1 to this sum
    int r = ((int)(Math.random()*(323567)) % prefix[n - 1]) + 1;

    // Find index of ceiling of r in prefix array
    int indexc = findCeil(prefix, r, 0, n - 1);
    return arr[indexc];
}

// Driver code
public static void main(String args[])
{
    int arr[] = {1, 2, 3, 4};
    int freq[] = {10, 5, 20, 100};
    int i, n = arr.length;

    // Let us generate 10 random numbers according to
    // given distribution
    for (i = 0; i < 5; i++)
    System.out.println( myRand(arr, freq, n) );
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to generate random numbers
# according to given frequency distribution
import random

# Utility function to find ceiling of r in arr[l..h]
def findCeil(arr, r, l, h) :

    while (l < h) :   
        mid = l + ((h - l) >> 1); # Same as mid = (l+h)/2
        if r > arr[mid] :
            l = mid + 1
        else :
            h = mid

    if arr[l] >= r :
        return l
    else :
        return -1

# The main function that returns a random number
# from arr[] according to distribution array
# defined by freq[]. n is size of arrays.
def myRand(arr, freq, n) :

    # Create and fill prefix array
    prefix = [0] * n
    prefix[0] = freq[0]
    for i in range(n) :
        prefix[i] = prefix[i - 1] + freq[i]

    # prefix[n-1] is sum of all frequencies.
    # Generate a random number with
    # value from 1 to this sum
    r = random.randint(0, prefix[n - 1]) + 1

    # Find index of ceiling of r in prefix array
    indexc = findCeil(prefix, r, 0, n - 1)
    return arr[indexc]

# Driver code
arr = [1, 2, 3, 4]
freq = [10, 5, 20, 100]
n = len(arr)

# Let us generate 10 random numbers according to
# given distribution
for i in range(5) :
    print(myRand(arr, freq, n))

    # This code is contributed by divyesh072019
```

## C#

```
// C# program to generate random numbers
// according to given frequency distribution
using System;

class GFG{

// Utility function to find ceiling
// of r in arr[l..h] 
static int findCeil(int[] arr, int r,
                    int l, int h) 
{ 
    int mid;
    while (l < h) 
    { 

        // Same as mid = (l+h)/2 
        mid = l + ((h - l) >> 1);

        if (r > arr[mid]) 
            l = mid + 1;
        else
            h = mid; 
    } 
    return (arr[l] >= r) ? l : -1; 
}

// The main function that returns a random number
// from arr[] according to distribution array 
// defined by freq[]. n is size of arrays. 
static int myRand(int[] arr, int[] freq, int n) 
{ 

    // Create and fill prefix array 
    int[] prefix = new int[n];
    int i; 
    prefix[0] = freq[0]; 

    for(i = 1; i < n; ++i) 
        prefix[i] = prefix[i - 1] + freq[i]; 

    // prefix[n-1] is sum of all frequencies.
    // Generate a random number with 
    // value from 1 to this sum
    Random rand = new Random();
    int r = ((int)(rand.Next() * (323567)) %
                      prefix[n - 1]) + 1; 

    // Find index of ceiling of r in prefix array 
    int indexc = findCeil(prefix, r, 0, n - 1); 
    return arr[indexc]; 
}

// Driver Code
static void Main()
{
    int[] arr = { 1, 2, 3, 4 }; 
    int[] freq = { 10, 5, 20, 100 }; 
    int i, n = arr.Length; 

    // Let us generate 10 random numbers
    // according to given distribution 
    for(i = 0; i < 5; i++) 
        Console.WriteLine(myRand(arr, freq, n)); 
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program to generate random numbers
// according to given frequency distribution

    // Utility function to find ceiling of r in arr[l..h]
    function findCeil(arr, r, l, h)
    {
        let mid;
        while (l < h)
        {
            mid = l + ((h - l) >> 1); // Same as mid = (l+h)/2
            (r > arr[mid]) ? (l = mid + 1) : (h = mid);
        }
        return (arr[l] >= r) ? l : -1;
    }

    // The main function that returns a random number
    // from arr[] according to distribution array
    // defined by freq[]. n is size of arrays.
    function myRand(arr, freq,  n) {
        // Create and fill prefix array
        let prefix= [];
        let i;
        prefix[0] = freq[0];
        for (i = 1; i < n; ++i)
            prefix[i] = prefix[i - 1] + freq[i];

        // prefix[n-1] is sum of all frequencies.
        // Generate a random number with
        // value from 1 to this sum
        let r = Math.floor((Math.random()* prefix[n - 1])) + 1;

        // Find index of ceiling of r in prefix array
        let indexc = findCeil(prefix, r, 0, n - 1);
        return arr[indexc];
    }

    // Driver code
    let arr = [1, 2, 3, 4];
    let freq = [10, 5, 20, 100];
    let i;
    let n = arr.length;

    // Use a different seed value for every run.

    // Let us generate 10 random numbers according to
    // given distribution
    for (i = 0; i < 5; i++)
      document.write(myRand(arr, freq, n));

      // This code is contributed by rohitsingh07052.
</script>
```

**输出:**对于不同的运行可能不同

```
4
3
4
4
4
```

***时间复杂度:** O(n)*

本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish)编辑。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。