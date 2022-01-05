# 计算一个字符串中相等对的数量

> 原文:[https://www.geeksforgeeks.org/number-equal-pairs-string/](https://www.geeksforgeeks.org/number-equal-pairs-string/)

给定一个字符串 s，找出相同字符对的数量。对(s[i]、s[j])、(s[j]、s[i])、(s[i]、s[i])、(s[j]、s[j])应被视为不同。

**示例:**

```
Input: air
Output: 3
Explanation :
3 pairs that are equal are (a, a), (i, i) and (r, r)

Input : geeksforgeeks
Output : 31

```

**天真的方法**将是你运行两个嵌套的 for 循环，找出所有的对，并保留所有对的计数。但是这对于更长的字符串来说不够有效。

对于一个**有效的方法**，我们需要计算**线性时间**中相等对的数量。因为对(x，y)和对(y，x)被认为是不同的。我们需要使用哈希表来存储一个字符的所有出现次数。所以我们知道如果一个字符出现两次，那么它将有 4 对–**(I，I)，(j，j)，(I，j)，(j，i)** 。所以使用散列函数，存储每个字符的出现，那么对于每个字符，对的数量将是 occurrence^2.哈希表的长度将是 256，因为我们有 256 个字符。

以下是上述方法的实现:

## C++

```
// CPP program to count the number of pairs
#include <bits/stdc++.h>
using namespace std;
#define MAX 256

// Function to count the number of equal pairs
int countPairs(string s)
{
    // Hash table
    int cnt[MAX] = { 0 };

    // Traverse the string and count occurrence
    for (int i = 0; i < s.length(); i++)
        cnt[s[i]]++;

    // Stores the answer
    int ans = 0;

    // Traverse and check the occurrence of every character
    for (int i = 0; i < MAX; i++)
        ans += cnt[i] * cnt[i];

    return ans;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";
    cout << countPairs(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of pairs
import java.io.*;

class GFG {

    static int MAX = 256;

    // Function to count the number of equal pairs
    static int countPairs(String s)
    {
        // Hash table
        int cnt[] = new int[MAX];

        // Traverse the string and count occurrence
        for (int i = 0; i < s.length(); i++)
            cnt[s.charAt(i)]++;

        // Stores the answer
        int ans = 0;

        // Traverse and check the occurrence
        // of every character
        for (int i = 0; i < MAX; i++)
            ans += cnt[i] * cnt[i];

        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String s = "geeksforgeeks";
        System.out.println(countPairs(s));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to count the 
# number of pairs 
MAX = 256

# Function to count the number 
# of equal pairs
def countPairs(s):

    # Hash table 
    cnt = [0 for i in range(0, MAX)]

    # Traverse the string and count 
    # occurrence 
    for i in range(len(s)):
        cnt[ord(s[i]) - 97] += 1

    # Stores the answer 
    ans = 0

    # Traverse and check the occurrence 
    # of every character 
    for i in range(0, MAX):
        ans += cnt[i] * cnt[i]

    return ans

# Driver code 
if __name__=="__main__":
    s = "geeksforgeeks"
    print(countPairs(s))

# This code is contributed 
# by Sairahul099         
```

## C#

```
// C# program to count the number of pairs
using System;

class GFG {

    static int MAX = 256;

    // Function to count the number of equal pairs
    static int countPairs(string s)
    {
        // Hash table
        int []cnt = new int[MAX];

        // Traverse the string and count occurrence
        for (int i = 0; i < s.Length; i++)
            cnt[s[i]]++;

        // Stores the answer
        int ans = 0;

        // Traverse and check the occurrence
        // of every character
        for (int i = 0; i < MAX; i++)
            ans += cnt[i] * cnt[i];

        return ans;
    }

    // Driver Code
    public static void Main ()
    {
        string s = "geeksforgeeks";
        Console.WriteLine(countPairs(s));
    }
}

// This code is contributed by vt_m
```

**Output :**

```
31

```