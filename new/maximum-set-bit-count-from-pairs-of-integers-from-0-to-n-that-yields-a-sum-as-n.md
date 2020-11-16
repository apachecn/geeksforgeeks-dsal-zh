# 从 0 到`N`的整数偶对的总和为`N`的最大设置位数量

> 原文：[https://www.geeksforgeeks.org/maximum-set-bit-count-from-pairs-of-integers-from-0-to-n-that-yields-a-sum-as-n/](https://www.geeksforgeeks.org/maximum-set-bit-count-from-pairs-of-integers-from-0-to-n-that-yields-a-sum-as-n/)

给定整数`N`，任务是在从 0 到`N`的所有整数对中找到设置位的最大频率，该总和产生为`N`。

**示例**：

> **输入**：`N = 5`
>
> **输出**：3
>
> **说明**：
>
> 所有对是`{0, 5}, {1, 4}, {2, 3}`，其总和为 5。
>
> 0（0000）和 5（0101），设置的位数为 2
>
> 1（0001）和 4（0100），设置的位数为 2
>
> 2（0010）和 3（0011），设置的位数为 3，因此 3 是最大值。
> 
> **输入**：`N = 11`
>
> **输出**：4
>
> **说明**：
>
> 所有对是`{0, 11}, {1,  10}, {2, 9}, {3, 8}, {4, 7}, {5, 6}`，并且最大答案是`{4, 7}`对。
>
> `4 = 1000`和`7 = 0111`，设置的位数总数为`1 + 3 = 4`。

**朴素的方法**：解决此问题的最简单方法是生成所有总和为`N`的可能对，并计算所有此类对的设置位的最大和，并打印最大设置位总和。

**时间复杂度**：`O(N * log N)`。

**辅助空间**：`O(1)`。

**高效方法**：可以通过以下步骤优化上述方法：

*   找出一个小于等于`N`的数字，该数字中从最低有效位到最高有效位的所有位均为置位位。 该数字将是该对中的第一个数字。

*   计算对`{first, N-first}`的设置位数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the first number
int create_first_no(int n)
{
    // Length of the binary from
    int length = 0;

    // Number of set bits
    int freq_set_bits = 0;
    int ans = 0;
    while (n) {

        // Update the first number
        ans = ans << 1;
        ans = ans + 1;

        // Increment length
        length++;

        // Update the frequency
        if ((n & 1))
            freq_set_bits += 1;

        n = n >> 1;
    }
    // Check if n does not have all the
    // bits as set bits then make
    // the first as less than n
    if (length != freq_set_bits)
        ans = (ans >> 1);

    // Return the first value
    return ans;
}

// Function to calculate maximum
// set bit frequency sum
int maxSetBits(int n)
{
    // First value of pair
    int first = create_first_no(n);

    // Second value of pair
    int second = n - first;

    // __builtin_popcount() is inbuilt
    // function to count the number of set bits
    int freq_first
        = __builtin_popcount(first);
    int freq_second
        = __builtin_popcount(second);

    // Return the sum of freq of setbits
    return freq_first + freq_second;
}

// Driver Code
int main()
{
    int N = 5;

    // Function call
    cout << maxSetBits(N);
    return 0;
}

```

## Java

```java

// Java program to implement the
// above approach
import java.util.*;

class GFG {

// Function to find the first number
static int create_first_no(int n)
{

    // Length of the binary from
    int length = 0;

    // Number of set bits
    int freq_set_bits = 0;
    int ans = 0;

    while (n != 0) 
    {

        // Update the first number
        ans = ans << 1;
        ans = ans + 1;

        // Increment length
        length++;

        // Update the frequency
        if ((n & 1) == 1)
            freq_set_bits += 1;

        n = n >> 1;
    }

    // Check if n does not have all the
    // bits as set bits then make
    // the first as less than n
    if (length != freq_set_bits)
        ans = (ans >> 1);

    // Return the first value
    return ans;
}

// Function to calculate maximum
// set bit frequency sum
static int maxSetBits(int n)
{

    // First value of pair
    int first = create_first_no(n);

    // Second value of pair
    int second = n - first;

    // Integer.bitCount() is inbuilt
    // function to count the number of set bits
    int freq_first = Integer.bitCount(first);
    int freq_second = Integer.bitCount(second);

    // Return the sum of freq of setbits
    return freq_first + freq_second;
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    // Function call
    System.out.println(maxSetBits(N));
}
}

// This code is contributed by offbeat

```

## C#

```cs

// C# program to implement the
// above approach
using System;
using System.Linq; 
class GFG {

// Function to find the first number
static int create_first_no(int n)
{

    // Length of the binary from
    int length = 0;

    // Number of set bits
    int freq_set_bits = 0;
    int ans = 0;

    while (n != 0) 
    {

        // Update the first number
        ans = ans << 1;
        ans = ans + 1;

        // Increment length
        length++;

        // Update the frequency
        if ((n & 1) == 1)
            freq_set_bits += 1;

        n = n >> 1;
    }

    // Check if n does not have all the
    // bits as set bits then make
    // the first as less than n
    if (length != freq_set_bits)
        ans = (ans >> 1);

    // Return the first value
    return ans;
}
public static int countSetBits(int n) 
{ 

  // base case 
  if (n == 0) 
    return 0; 

  else

    // if last bit set 
    // add 1 else add 0 
    return (n & 1) + countSetBits(n >> 1); 
} 

// Function to calculate maximum
// set bit frequency sum
static int maxSetBits(int n)
{

    // First value of pair
    int first = create_first_no(n);

    // Second value of pair
    int second = n - first;

    //countSetBits function to 
    //count the number of set bits
    int freq_first = countSetBits(first);
    int freq_second = countSetBits(second);

    // Return the sum of freq of setbits
    return freq_first + freq_second;
}

// Driver code
public static void Main(string[] args)
{
    int N = 5;

    // Function call
    Console.Write(maxSetBits(N));
}
}

// This code is contributed by Ritik Bansal

```

**输出**： 

```
3

```

**时间复杂度**：`O(logN)`。

**辅助空间**：`O(1)`。



* * *

* * *



