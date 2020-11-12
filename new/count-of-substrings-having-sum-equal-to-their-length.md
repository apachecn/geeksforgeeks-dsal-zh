# 总和等于其长度的子串的计数

> 原文：[https://www.geeksforgeeks.org/count-of-substrings-having-sum-equal-to-their-length/](https://www.geeksforgeeks.org/count-of-substrings-having-sum-equal-to-their-length/)

给定数字字符串`str`，任务是计算数字总和等于其长度的子字符串的数量。

**示例**：

> **输入**：`str = "112112"`
>
> **输出**：6
>
> **解释**：
>
> 子串`"1", "1", "11"`满足给定条件。
>
> **输入**：`str = "1101112"`
>
> **输出**：12

**朴素的方法**：最简单的解决方案是[生成给定字符串的所有子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并为每个子字符串检查其总和是否等于其长度。 对于发现为真的每个子字符串，增加计数。

**时间复杂度**：`O(N ^ 3)`。

**辅助空间**：`O(1)`。

**高效方法**：可以使用[`Hashmap`](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)优化上述方法，并不断更新`Hashmap`中的子字符串计数，并在最后打印所需的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// substrings with sum equal to length
int countSubstrings(string s, int n)
{

    int count = 0, sum = 0;

    // Stores the count of substrings
    unordered_map<int, int> mp;
    mp[0]++;

    for (int i = 0; i < n; ++i) {

        // Add character to sum
        sum += (s[i] - '0');

        // Add count of substrings to result
        count += mp[sum - (i + 1)];

        // Increase count of subarrays
        ++mp[sum - (i + 1)];
    }

    // Return count
    return count;
}

// Driver Code
int main()
{
    string str = "112112";
    int n = str.length();
    cout << countSubstrings(str, n) << endl;

    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count the number of
// subStrings with sum equal to length
static int countSubStrings(String s, int n)
{
    int count = 0, sum = 0;

    // Stores the count of subStrings
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();
    mp.put(0, 1);

    for(int i = 0; i < n; ++i)
    {

        // Add character to sum
        sum += (s.charAt(i)- '0');

        // Add count of subStrings to result
        count += mp.containsKey(sum - (i + 1)) == true ?
                         mp.get(sum - (i + 1)) : 0;

        // Increase count of subarrays
        if(!mp.containsKey(sum - (i + 1)))
                    mp.put(sum - (i + 1), 1);
        else
            mp.put(sum - (i + 1), 
            mp.get(sum - (i + 1)) + 1);
    }

    // Return count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    String str = "112112";
    int n = str.length();

    System.out.print(countSubStrings(str, n) + "\n");
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program to implement 
# the above approach
from collections import defaultdict

# Function to count the number of 
# substrings with sum equal to length
def countSubstrings(s, n):

    count, sum = 0, 0

    # Stores the count of substrings
    mp = defaultdict(lambda : 0)
    mp[0] += 1

    for i in range(n):

        # Add character to sum
        sum += ord(s[i]) - ord('0')

        # Add count of substrings to result
        count += mp[sum - (i + 1)]

        # Increase count of subarrays
        mp[sum - (i + 1)] += 1

    # Return count
    return count

# Driver code
str = '112112'
n = len(str)

print(countSubstrings(str, n))

# This code is contributed by Stuti Pathak

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to count the number of
// subStrings with sum equal to length
static int countSubStrings(String s, int n)
{
    int count = 0, sum = 0;

    // Stores the count of subStrings
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    mp.Add(0, 1);

    for(int i = 0; i < n; ++i)
    {

        // Add character to sum
        sum += (s[i]- '0');

        // Add count of subStrings to result
        count += mp.ContainsKey(sum - (i + 1)) == true ?
                             mp[sum - (i + 1)] : 0;

        // Increase count of subarrays
        if(!mp.ContainsKey(sum - (i + 1)))
                    mp.Add(sum - (i + 1), 1);
        else
            mp[sum - (i + 1)] = mp[sum - (i + 1)] + 1;
    }

    // Return count
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "112112";
    int n = str.Length;

    Console.Write(countSubStrings(str, n) + "\n");
}
}

// This code is contributed by Rohit_ranjan

```

**输出**： 

```
6

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



