# 数种方式将二进制字符串拆分为三个具有相等零计数的子字符串

> 原文：[https://www.geeksforgeeks.org/count-ways-to-split-a-binary-string-into-three-substrings-having-equal-count-of-zeros/](https://www.geeksforgeeks.org/count-ways-to-split-a-binary-string-into-three-substrings-having-equal-count-of-zeros/)

给定[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)`str`，任务是计算将给定字符串拆分为三个具有相同 **0** 数量的非重叠子字符串的方式总数`s`。

**示例**：

> **输入**：`str = "01010"`
>
> **输出**：4
>
> **说明**：
>
> 可能的分割为：`[0, 10, 10 ], [01, 01, 0], [01, 0, 10], [0, 101, 0]`
> 
> **输入**：`str = "11111"`
>
> **输出**：0

**方法**：解决该问题的方法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)的概念。 以下是解决问题的步骤：

1.  遍历字符串并计算零的总数并将其存储在变量中，例如`total_count`。

2.  使用[哈希映射](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)（例如**映射**）存储累计总和 0s 的频率。

3.  用`total_count / 3`初始化变量`k`，该变量表示每个分区所需的 **0** 的数量。

4.  初始化变量`res`和`sum`，以分别存储分割字符串的方式数目和 **0** 的累积和。

5.  如果当前字符为 **0** ，则遍历给定的字符串并增加`sum`。

6.  如果`sum = 2k`和`k`存在`map[k]`，则将`res`增加。

7.  更新映射中`sum`的频率。

8.  最后返回`res`。

9.  如果`total_count`无法被 **3** 整除，则返回 0。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return ways to split
// a string into three  parts
// with the equal number of 0
int count(string s)
{

    // Store total count of 0s
    int cnt = 0;

    // Count total no. of 0s
    // character in given string
    for(char c : s) 
    {
        cnt += c == '0' ? 1 : 0;
    }

    // If total count of 0
    // character is not
    // divisible by 3
    if (cnt % 3 != 0)
        return 0;

    int res = 0, k = cnt / 3, sum = 0;

    // Initialize mp to store
    // frequency of k
    map<int, int> mp;

    // Traverse string to find
    // ways to split string
    for(int i = 0; i < s.length(); i++)
    {

        // Increment count if 0 appears
        sum += s[i] == '0' ? 1 : 0;

        // Increment result if sum equal to
        // 2*k and k exists in mp
        if (sum == 2 * k && mp.find(k) != mp.end() && 
            i < s.length() - 1 && i > 0)
        {
            res += mp[k];
        }

        // Insert sum in mp
        mp[sum]++;
    }

    // Return result
    return res;
}

// Driver Code
int main()
{

    // Given string
    string str = "01010";

    // Function call
    cout << count(str);
}

// This code is contributed by rutvik_56

```

## Java

```java

// Java implementation for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to return ways to split
    // a string into three  parts
    // with the equal number of 0
    static int count(String s)
    {
        // Store total count of 0s
        int cnt = 0;

        // Count total no. of 0s
        // character in given string
        for (char c : s.toCharArray()) {
            cnt += c == '0' ? 1 : 0;
        }

        // If total count of 0
        // character is not
        // divisible by 3
        if (cnt % 3 != 0)
            return 0;

        int res = 0, k = cnt / 3, sum = 0;

        // Initialize map to store
        // frequency of k
        Map<Integer, Integer> map = new HashMap<>();

        // Traverse string to find
        // ways to split string
        for (int i = 0; i < s.length(); i++) {

            // Increment count if 0 appears
            sum += s.charAt(i) == '0' ? 1 : 0;

            // Increment result if sum equal to
            // 2*k and k exists in map
            if (sum == 2 * k && map.containsKey(k)
                && i < s.length() - 1 && i > 0) {
                res += map.get(k);
            }

            // Insert sum in map
            map.put(sum,
                    map.getOrDefault(sum, 0) + 1);
        }

        // Return result
        return res;
    }
    // Driver Code
    public static void main(String[] args)
    {
        // Given string
        String str = "01010";

        // Function call
        System.out.println(count(str));
    }
}

```

## Python3

```py

# Python3 implementation for 
# the above approach

# Function to return ways to split
# a string into three  parts
# with the equal number of 0
def count(s):

    # Store total count of 0s
    cnt = 0

    # Count total no. of 0s
    # character in given string
    for c in s:
        if c == '0':
            cnt += 1

    # If total count of 0
    # character is not
    # divisible by 3
    if (cnt % 3 != 0):
        return 0

    res = 0
    k = cnt // 3
    sum = 0

    # Initialize map to store
    # frequency of k
    mp = {}

    # Traverse string to find
    # ways to split string
    for i in range(len(s)):

        # Increment count if 0 appears
        if s[i] == '0':
            sum += 1

        # Increment result if sum equal to
        # 2*k and k exists in map
        if (sum == 2 * k and k in mp and
            i < len(s) - 1 and i > 0):
            res += mp[k]

        # Insert sum in map
        if sum in mp:
            mp[sum] += 1
        else:
            mp[sum] = 1

    # Return result
    return res

# Driver Code
if __name__ == "__main__":

    # Given string
    st = "01010"

    # Function call
    print(count(st))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return ways to split
// a string into three parts
// with the equal number of 0
static int count(String s)
{

    // Store total count of 0s
    int cnt = 0;

    // Count total no. of 0s
    // character in given string
    foreach(char c in s.ToCharArray())
    {
        cnt += c == '0' ? 1 : 0;
    }

    // If total count of 0
    // character is not
    // divisible by 3
    if (cnt % 3 != 0)
        return 0;

    int res = 0, k = cnt / 3, sum = 0;

    // Initialize map to store
    // frequency of k
    Dictionary<int, 
               int> map = new Dictionary<int, 
                                         int>();

    // Traverse string to find
    // ways to split string
    for(int i = 0; i < s.Length; i++)
    {

        // Increment count if 0 appears
        sum += s[i] == '0' ? 1 : 0;

        // Increment result if sum equal to
        // 2*k and k exists in map
        if (sum == 2 * k && map.ContainsKey(k) && 
            i < s.Length - 1 && i > 0) 
        {
            res += map[k];
        }

        // Insert sum in map
        if(map.ContainsKey(sum))
            map[sum] = map[sum] + 1;
        else
            map.Add(sum, 1);
    }

    // Return result
    return res;
}

// Driver Code
public static void Main(String[] args)
{

    // Given string
    String str = "01010";

    // Function call
    Console.WriteLine(count(str));
}
}

// This code is contributed by Amit Katiyar

```

**输出**：

```
4

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`

**有效方法**：

为了将输入字符串分成三部分，只需要两个剪切，这将给出三个子字符串`S1`，`S2`和`S3`。 每个子字符串将具有相等的 0，即`count(0) / 3`。 现在，从字符串开头开始跟踪 0 的计数。 一旦计数等于`count(0) / 3`，就进行第一次切割。 同样，一旦 0 的计数等于`2​​ * count(0) / 3`，就进行第二次切割。

**算法**

1.  计算 0 的数量。 如果不能被 3 整除，则答案为 0。

2.  如果计数为 0，则每个子字符串将具有相等的数字 0，即零个数字 0。 因此，分割给定字符串的方法总数为选择 2 个位置以从`n-1`个位置中分割字符串的组合数量。 对于第一个位置，我们有`n-1`个选择，对于第二个位置，我们有`n-2`个选择。 因此，组合的总数为`(n-1) * (n-2)`。 由于选择相同，因此将其除以 2。因此答案为`(n-1) * (n-2) / 2`。

3.  从头开始遍历给定的字符串，并再次保持 0 的计数，如果计数达到`count(0) / 3`，我们将开始累积第一次切割的方式； 当计数达到`2 * count(0) / 3`时，我们开始累积第二次切割的方式数。

4.  答案是第一次切割和第二次切割的方式数相乘。

下面是上述方法的实现：

## C++

```cpp

// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// the number of ways to split
int splitstring(string s)
{
    int n = s.length();

    // Calculating the total
    // number of zeros
    int zeros = 0;
    for (int i = 0; i < n; i++)
        if (s[i] == '0')
            zeros++;

    // Case1
    // If total count of zeros is not
    // divisible by 3
    if (zeros % 3 != 0)
        return 0;

    // Case2
    // if total count of zeros
    // is zero
    if (zeros == 0)
        return ((n - 1) * (n - 2)) / 2;

    // Case3
    // General case

    // Number of zeros in each substring
    int zerosInEachSubstring = zeros / 3;

    // Initialising zero to the number of ways
    // for first and second cut
    int waysOfFirstCut = 0, waysOfSecondCut = 0;

    // Initializing the count
    int count = 0;

    // Traversing from the begining
    for (int i = 0; i < n; i++) 
    {

        // Incrementing the count
        // if the element is '0'
        if (s[i] == '0')
            count++;

        // Incrementing the ways for the
        // 1st cut if count is equal to
        // zeros required in each substring
        if (count == zerosInEachSubstring)
            waysOfFirstCut++;

        // Incrementing the ways for the
        // 2nd cut if count is equal to
        // 2*(zeros required in each substring)
        else if (count == 2 * zerosInEachSubstring)
            waysOfSecondCut++;
    }

    // Total number of ways to split is 
    // multiplication of ways for the 1st 
    // and 2nd cut
    return waysOfFirstCut * waysOfSecondCut;
}

// Driver Code
int main()
{
    string s = "01010";

    // Function Call
    cout << "The number of ways to split is "
         << splitstring(s) << endl;
}

// this code is contributed by Arif

```

## Java

```java

// Java program for above approach
import java.util.*; 

class GFG{

// Function to calculate
// the number of ways to split
static int splitstring(String s)
{
    int n = s.length();

    // Calculating the total
    // number of zeros
    int zeros = 0;
    for(int i = 0; i < n; i++)
        if (s.charAt(i) == '0')
            zeros++;

    // Case1
    // If total count of zeros is not
    // divisible by 3
    if (zeros % 3 != 0)
        return 0;

    // Case2
    // if total count of zeros
    // is zero
    if (zeros == 0)
        return ((n - 1) * (n - 2)) / 2;

    // Case3
    // General case

    // Number of zeros in each substring
    int zerosInEachSubstring = zeros / 3;

    // Initialising zero to the number of ways
    // for first and second cut
    int waysOfFirstCut = 0;
    int waysOfSecondCut = 0;

    // Initializing the count
    int count = 0;

    // Traversing from the begining
    for(int i = 0; i < n; i++) 
    {

        // Incrementing the count
        // if the element is '0'
        if (s.charAt(i) == '0')
            count++;

        // Incrementing the ways for the
        // 1st cut if count is equal to
        // zeros required in each substring
        if (count == zerosInEachSubstring)
            waysOfFirstCut++;

        // Incrementing the ways for the
        // 2nd cut if count is equal to
        // 2*(zeros required in each substring)
        else if (count == 2 * zerosInEachSubstring)
            waysOfSecondCut++;
    }

    // Total number of ways to split is 
    // multiplication of ways for the 1st 
    // and 2nd cut
    return waysOfFirstCut * waysOfSecondCut;
}

// Driver Code
public static void main(String args[]) 
{
    String s = "01010";

    // Function Call
    System.out.println("The number of " + 
                       "ways to split is " +
                       splitstring(s));
}
}

// This code is contributed by Stream_Cipher

```

## Python3

```py

# Python3 program for above approach

# Function to calculate
# the number of ways to split
def splitstring(s):

    n = len(s)

    # Calculating the total
    # number of zeros
    zeros = 0
    for i in range(n):
        if s[i] == '0':
            zeros += 1

    # Case1
    # If total count of zeros is not
    # divisible by 3
    if zeros % 3 != 0:
        return 0

    # Case2
    # if total count of zeros
    # is zero
    if zeros == 0:
        return ((n - 1) *
                (n - 2)) // 2

    # Case3
    # General case

    # Number of zeros in each substring
    zerosInEachSubstring = zeros // 3

    # Initialising zero to the number of ways
    # for first and second cut
    waysOfFirstCut, waysOfSecondCut = 0, 0

    # Initializing the count
    count = 0

    # Traversing from the begining
    for i in range(n):

        # Incrementing the count
        # if the element is '0'
        if s[i] == '0':
            count += 1

        # Incrementing the ways for the
        # 1st cut if count is equal to
        # zeros required in each substring
        if (count == zerosInEachSubstring):
            waysOfFirstCut += 1

        # Incrementing the ways for the
        # 2nd cut if count is equal to
        # 2*(zeros required in each substring)
        elif (count == 2 * zerosInEachSubstring):
            waysOfSecondCut += 1

    # Total number of ways to split is 
    # multiplication of ways for the 1st 
    # and 2nd cut
    return waysOfFirstCut * waysOfSecondCut

# Driver code
s = "01010"

# Function call
print("The number of ways to split is", splitstring(s))

# This code is contributed by divyeshrabadiya07

```

## C#

```cs

// C# program for above approach
using System.Collections.Generic; 
using System; 

class GFG{

// Function to calculate
// the number of ways to split
static int splitstring(string s)
{
    int n = s.Length;

    // Calculating the total
    // number of zeros
    int zeros = 0;
    for(int i = 0; i < n; i++)
        if (s[i] == '0')
            zeros++;

    // Case1
    // If total count of zeros is not
    // divisible by 3
    if (zeros % 3 != 0)
        return 0;

    // Case2
    // if total count of zeros
    // is zero
    if (zeros == 0)
        return ((n - 1) * (n - 2)) / 2;

    // Case3
    // General case

    // Number of zeros in each substring
    int zerosInEachSubstring = zeros / 3;

    // Initialising zero to the number of ways
    // for first and second cut
    int waysOfFirstCut = 0;
    int waysOfSecondCut = 0;

    // Initializing the count
    int count = 0;

    // Traversing from the begining
    for(int i = 0; i < n; i++) 
    {

        // Incrementing the count
        // if the element is '0'
        if (s[i] == '0')
            count++;

        // Incrementing the ways for the
        // 1st cut if count is equal to
        // zeros required in each substring
        if (count == zerosInEachSubstring)
            waysOfFirstCut++;

        // Incrementing the ways for the
        // 2nd cut if count is equal to
        // 2*(zeros required in each substring)
        else if (count == 2 * zerosInEachSubstring)
            waysOfSecondCut++;
    }

    // Total number of ways to split is 
    // multiplication of ways for the 1st 
    // and 2nd cut
    return waysOfFirstCut * waysOfSecondCut;
}

// Driver Code
public static void Main() 
{
    string s = "01010";

    // Function call
    Console.WriteLine("The number of ways " + 
                      "to split is " + 
                      splitstring(s));
}
}

// This code is contributed by Stream_Cipher

```

**输出**：

```
The number of ways to split is 4

```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`



* * *

* * *



