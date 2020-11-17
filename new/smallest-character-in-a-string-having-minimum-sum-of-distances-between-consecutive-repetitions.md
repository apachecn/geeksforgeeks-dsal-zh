# 字符串中的最小字符，它的连续重复之间的距离之和最小

> 原文：[https://www.geeksforgeeks.org/smallest-character-in-a-string-having-minimum-sum-of-distances-between-consecutive-repetitions/](https://www.geeksforgeeks.org/smallest-character-in-a-string-having-minimum-sum-of-distances-between-consecutive-repetitions/)

给定仅由小写字母组成的大小为`N`的字符串`S`，任务是找到在其连续重复之间具有最小距离之和的最小字符。 如果字符串`S`仅包含不同的字符，则打印 -1。

**示例**：

> **输入**：`str = "aabbaadc"`
>
> **输出**：`b`
>
> **说明**：
>
> 对于给定字符串中的所有字符，所需距离的总和如下：
>
> `'a' = {0, 1, 4, 5}`
>
> 下一次重复的距离之和为`abs(0 – 1) + abs(4 – 1) + abs(5 – 4) = 5`。
>
> `b`的索引为`{2, 3}`。
>
> 下一次重复的距离之和为`abs(2 – 3) = 1`。
>
> `'c'，'d'`无重复。
>
> 对于字符`b`，从上述距离获得的最小距离总和为 1。
>
> 因此，所需的答案是`b`。
> 
> **输入**：`str = "abcdef"`
>
> **输出**：-1
>
> **说明**：
>
> 给定字符串中的所有字符都是不同的。

**朴素的方法**：最简单的方法是遍历给定的字符串，并针对每个字符分别找到最短距离的总和。 以最小的最短距离打印最小的字符。

**时间复杂度**：`O(N * 26)`，其中`N`是给定字符串的长度。

**辅助空间**：`O(n)`。

**高效方法**：想法是遍历字符串一次，并为每个字符找到第一个和最后一个索引，因为相同字符之间的索引之间的差之和就是第一个和最后一个字符之间的差 。 请按照以下步骤解决问题：

1.  创建长度为`26`的数组`last[]`和`first[]`，初始化两个数组均为`-1`。

2.  用一些大数目初始化`min`。

3.  如果它等于`-1`，则遍历字符串`S`并将当前字符的第一次出现更新为当前索引。

4.  [查找每个字符最后一次出现](https://www.geeksforgeeks.org/find-last-index-character-string/)的并将其存储在数组`last[]`中。

5.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果两个索引都具有非负值，则更新在每个对应的索引处具有最小差异的索引。

6.  如果在索引`x`处找到最小索引，则打印字符`x + 'a'`。

7.  否则，打印 -1。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the character
// repeats with minimum distance
char minDistChar(string s)
{
    int n = s.length();

    // Stores the first and last index
    int* first = new int[26];
    int* last = new int[26];

    // Initialize with -1
    for (int i = 0; i < 26; i++) {
        first[i] = -1;
        last[i] = -1;
    }

    // Get the values of last and
    // first occurence
    for (int i = 0; i < n; i++) {

        // Update the first index
        if (first[s[i] - 'a'] == -1) {
            first[s[i] - 'a'] = i;
        }

        // Update the last index
        last[s[i] - 'a'] = i;
    }

    // Initialize min
    int min = INT_MAX;
    char ans = '1';

    // Get the minimum
    for (int i = 0; i < 26; i++) {

        // Values must not be same
        if (last[i] == first[i])
            continue;

        // Update the minimum distance
        if (min > last[i] - first[i]) {
            min = last[i] - first[i];
            ans = i + 'a';
        }
    }

    // return ans
    return ans;
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";

    // Function Call
    cout << minDistChar(str);

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG{

// Function to find the character
// repeats with minimum distance
static char minDistChar(char []s)
{
int n = s.length;

// Stores the first and last index
int []first = new int[26];
int []last = new int[26];

// Initialize with -1
for (int i = 0; i < 26; i++) 
{
    first[i] = -1;
    last[i] = -1;
}

// Get the values of last and
// first occurence
for (int i = 0; i < n; i++) 
{
    // Update the first index
    if (first[s[i] - 'a'] == -1) 
    {
    first[s[i] - 'a'] = i;
    }

    // Update the last index
    last[s[i] - 'a'] = i;
}

// Initialize min
int min = Integer.MAX_VALUE;
char ans = '1';

// Get the minimum
for (int i = 0; i < 26; i++) 
{
    // Values must not be same
    if (last[i] == first[i])
    continue;

    // Update the minimum distance
    if (min > last[i] - first[i]) 
    {
    min = last[i] - first[i];
    ans = (char) (i + 'a');
    }
}

// return ans
return ans;
}

// Driver Code
public static void main(String[] args)
{
String str = "geeksforgeeks";

// Function Call
System.out.print(minDistChar(str.toCharArray()));
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program for the above approach
import sys

# Function to find the character
# repeats with minimum distance
def minDistChar(s):

    n = len(s)

    # Stores the first and last index
    first = []
    last = []

    # Intialize with -1
    for i in range(26):
        first.append(-1)
        last.append(-1)

    # Get the values of last and
    # first occurence
    for i in range(n):

        # Update the first index
        if (first[ord(s[i]) - ord('a')] == -1):
            first[ord(s[i]) - ord('a')] = i

        # Update the last index
        last[ord(s[i]) - ord('a')] = i

    # Intialize the min
    min = sys.maxsize
    ans = '1'

    # Get the minimum
    for i in range(26):

        # Values must not be same
        if (last[i] == first[i]):
            continue

        # Update the minimum distance
        if (min > last[i] - first[i]):
            min = last[i] - first[i]
            ans = i + ord('a')

    return chr(ans)

# Driver Code
if __name__ == "__main__":

    str = "geeksforgeeks"

    # Function call
    print(minDistChar(str))

# This code is contributed by dadi madhav

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic;  

class GFG{ 

// Function to find the character
// repeats with minimum distance
static char minDistChar(char []s)
{
    int n = s.Length;

    // Stores the first and last index
    int []first = new int[26];
    int []last = new int[26];

    // Initialize with -1
    for(int i = 0; i < 26; i++) 
    {
        first[i] = -1;
        last[i] = -1;
    }

    // Get the values of last and
    // first occurence
    for(int i = 0; i < n; i++) 
    {

        // Update the first index
        if (first[s[i] - 'a'] == -1) 
        {
              first[s[i] - 'a'] = i;
        }

        // Update the last index
        last[s[i] - 'a'] = i;
    }

    // Initialize min
    int min = int.MaxValue;
    char ans = '1';

    // Get the minimum
    for(int i = 0; i < 26; i++) 
    {
        // Values must not be same
        if (last[i] == first[i])
            continue;

        // Update the minimum distance
        if (min > last[i] - first[i]) 
        {
            min = last[i] - first[i];
            ans = (char)(i + 'a');
        }
    }

    // return ans
    return ans;
}

// Driver Code 
public static void Main(string[] args) 
{  
    String str = "geeksforgeeks";

    // Function call
    Console.Write(minDistChar(str.ToCharArray()));
} 
} 

// This code is contributed by rutvik_56

```

**输出**： 

```
g

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



