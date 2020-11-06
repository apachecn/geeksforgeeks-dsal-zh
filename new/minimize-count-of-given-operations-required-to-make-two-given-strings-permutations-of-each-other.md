# 最小化使两个给定字符串彼此置换所需的给定操作数

> 原文：[https://www.geeksforgeeks.org/minimize-count-of-given-operations-required-to-make-two-given-strings-permutations-of-each-other/](https://www.geeksforgeeks.org/minimize-count-of-given-operations-required-to-make-two-given-strings-permutations-of-each-other/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/)`str1`和`str2`，任务是对两个字符串之一进行以下三种类型的最小操作数计数，使`str1`和`str2`彼此置换：

1.  在字符串中插入一个字符。

2.  从字符串中删除一个字符。

3.  用字符串中的另一个字符替换一个字符。

**注意**：所有上述操作费用相同。

**示例**：

> **输入**：`str1 = "geeksforgeeks", str2 = "geeksforcoder"`
>
> **输出**：4
>
> **说明**：将字符串`str2`重新排列为`"geeksforcedor"`
>
> 将`str1[8]`的值替换为`c`。
>
> 将`str1[10]`的值替换为`d`。
>
> 将`str1[11]`的值替换为`o`。
>
> 将`str1[12]`的值替换为`r`。
>
> 因此，所需的输出为 4。
> 
> **输入**：`str1 = "geek", str2 = "keeg"`
>
> **输出**：1

**方法**：可以使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)存储两个字符串的每个字符的频率来解决该问题。 以下是解决该问题的观察结果：

> `X`为字符串`str1`和`str2`中都存在的字符数。
>
> `N1 – X`为仅出现在`str1`中的字符数。
>
> `N2 – X`为仅在`str2`中存在的字符数。
>
> 替换操作总数为`min(N1 - X, N2 - X)`
>
> 插入/删除总数为 `max(N1 - X, N2-X) - min(N1 - X, N2 - X)`。
>
> 因此，操作总数为`max(N1 - X, N2 - X)`，

请按照以下步骤解决问题：

1.  初始化两个数组，例如`freq1[]`和`freq2[]`，以存储`str1`和`str2`的所有字符的[频率](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)。

2.  [遍历两个字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，并将两个字符串的每个字符的频率分别存储在数组`freq1[]`和`freq2[]`中。

3.  [遍历两个数组](https://www.geeksforgeeks.org/iterating-arrays-java/)`freq1[]`和`freq2[]`。

4.  对于第`i`个字符，如果`freq1[i]`超过`freq2[i]`，则将`freq1[i]`替换为`freq1[i] – freq2[i]`并设置`freq2[i] = 0`，反之亦然。

5.  最后，计算数组`freq1[]`和`freq2[]`的[总和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)，并打印它们之间的[最大值](https://www.geeksforgeeks.org/maximum-of-two-numbers-in-python/)作为答案。

下面是实现上述方法的方法：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize the count of
// operations to make str1 and str2
// permutations of each other
int ctMinEdits(string str1, string str2)
{
    int N1 = str1.length();
    int N2 = str2.length();

    // Store the frequency of
    // each character of str1
    int freq1[256] = { 0 };
    for (int i = 0; i < N1; i++) {
        freq1[str1[i]]++;
    }

    // Store the frequency of
    // each character of str2
    int freq2[256] = { 0 };
    for (int i = 0; i < N2; i++) {
        freq2[str2[i]]++;
    }

    // Traverse the freq1[] and freq2[]
    for (int i = 0; i < 256; i++) {

        // If frequency of character in
        // str1 is greater than str2
        if (freq1[i] > freq2[i]) {
            freq1[i] = freq1[i]
                       - freq2[i];
            freq2[i] = 0;
        }

        // Otherwise
        else {
            freq2[i] = freq2[i]
                       - freq1[i];
            freq1[i] = 0;
        }
    }

    // Store sum of freq1[]
    int sum1 = 0;

    // Store sum of freq2[]
    int sum2 = 0;

    for (int i = 0; i < 256; i++) {
        sum1 += freq1[i];
        sum2 += freq2[i];
    }

    return max(sum1, sum2);
}

// Driver Code
int main()
{
    string str1 = "geeksforgeeks";
    string str2 = "geeksforcoder";
    cout << ctMinEdits(str1, str2);
}

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*;
import java.io.*;
import java.lang.Math;

class GFG{

// Function to minimize the count of 
// operations to make str1 and str2 
// permutations of each other 
static int ctMinEdits(String str1, String str2) 
{ 
    int N1 = str1.length(); 
    int N2 = str2.length(); 

    // Store the frequency of 
    // each character of str1 
    int freq1[] = new int[256];
    Arrays.fill(freq1, 0);

    for(int i = 0; i < N1; i++)
    { 
        freq1[str1.charAt(i)]++; 
    } 

    // Store the frequency of 
    // each character of str2 
    int freq2[] = new int[256];
    Arrays.fill(freq2, 0);

    for(int i = 0; i < N2; i++)
    { 
        freq2[str2.charAt(i)]++; 
    } 

    // Traverse the freq1[] and freq2[] 
    for(int i = 0; i < 256; i++)
    { 

        // If frequency of character in 
        // str1 is greater than str2 
        if (freq1[i] > freq2[i]) 
        { 
            freq1[i] = freq1[i] - freq2[i]; 
            freq2[i] = 0; 
        } 

        // Otherwise 
        else
        { 
            freq2[i] = freq2[i] - freq1[i]; 
            freq1[i] = 0; 
        } 
    } 

    // Store sum of freq1[] 
    int sum1 = 0; 

    // Store sum of freq2[] 
    int sum2 = 0; 

    for(int i = 0; i < 256; i++)
    { 
        sum1 += freq1[i]; 
        sum2 += freq2[i]; 
    } 

    return Math.max(sum1, sum2); 
} 

// Driver Code
public static void main(final String[] args) 
{
    String str1 = "geeksforgeeks"; 
    String str2 = "geeksforcoder"; 

    System.out.println(ctMinEdits(str1, str2)); 
}
}

// This code is contributed by bikram2001jha

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to minimize the count of
# operations to make str1 and str2
# permutations of each other
def ctMinEdits(str1, str2):

    N1 = len(str1)
    N2 = len(str2)

    # Store the frequency of
    # each character of str1
    freq1 =  [0] * 256
    for i in range(N1):
        freq1[ord(str1[i])] += 1

    # Store the frequency of
    # each character of str2
    freq2 = [0] * 256
    for i in range(N2):
        freq2[ord(str2[i])] += 1

    # Traverse the freq1[] and freq2[]
    for i in range(256):

        # If frequency of character in
        # str1 is greater than str2
        if (freq1[i] > freq2[i]):
            freq1[i] = freq1[i] - freq2[i]
            freq2[i] = 0

        # Otherwise
        else:
            freq2[i] = freq2[i] - freq1[i]
            freq1[i] = 0

    # Store sum of freq1[]
    sum1 = 0

    # Store sum of freq2[]
    sum2 = 0

    for i in range(256):
        sum1 += freq1[i]
        sum2 += freq2[i]

    return max(sum1, sum2)

# Driver Code
str1 = "geeksforgeeks"
str2 = "geeksforcoder"

print(ctMinEdits(str1, str2))

# This code is contributed by code_hunt

```

## C#

```cs

// C# program to implement
// the above approach
using System;

class GFG{

// Function to minimize the count of 
// operations to make str1 and str2 
// permutations of each other 
static int ctMinEdits(string str1, string str2) 
{ 
    int N1 = str1.Length; 
    int N2 = str2.Length; 

    // Store the frequency of 
    // each character of str1 
    int[] freq1 = new int[256];
    freq1[0] = str1[0]; 

    for(int i = 0; i < N1; i++)
    { 
        freq1[str1[i]]++; 
    } 

    // Store the frequency of 
    // each character of str2 
    int[] freq2 = new int[256];
    freq2[0] = str2[0]; 

    for(int i = 0; i < N2; i++)
    { 
        freq2[str2[i]]++; 
    } 

    // Traverse the freq1[] and freq2[] 
    for(int i = 0; i < 256; i++)
    { 

        // If frequency of character in 
        // str1 is greater than str2 
        if (freq1[i] > freq2[i]) 
        { 
            freq1[i] = freq1[i] - freq2[i]; 
            freq2[i] = 0; 
        } 

        // Otherwise 
        else
        { 
            freq2[i] = freq2[i] - freq1[i]; 
            freq1[i] = 0; 
        } 
    } 

    // Store sum of freq1[] 
    int sum1 = 0; 

    // Store sum of freq2[] 
    int sum2 = 0; 

    for(int i = 0; i < 256; i++)
    { 
        sum1 += freq1[i]; 
        sum2 += freq2[i]; 
    } 
    return Math.Max(sum1, sum2); 
} 

// Driver Code
public static void Main() 
{
    string str1 = "geeksforgeeks"; 
    string str2 = "geeksforcoder"; 

    Console.WriteLine(ctMinEdits(str1, str2)); 
}
}

// This code is contributed by code_hunt

```

**Output:** 

```
4

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *



