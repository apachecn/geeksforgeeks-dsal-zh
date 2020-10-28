# 以给定字符串

> 原文：[https://www.geeksforgeeks.org/generate-a-number-in-decreasing-order-of-frequencies-of-characters-of-a-given-string/](https://www.geeksforgeeks.org/generate-a-number-in-decreasing-order-of-frequencies-of-characters-of-a-given-string/)

的字符频率降序生成数字

给定长度为 **N** 的字符串 **Str** ，由小写字母组成，任务是按照给定字符串中字符频率的降序生成数字。 如果两个字符具有相同的频率，则首先显示具有较小 ASCII 值的字符。 分配给字符{a，b，…。，y，z}的数字分别为{1,2，…。，25，26}。

**注意**：对于分配了大于 **9** 值的字符，取其模数 10。

**示例**：

> **输入**：N = 6，Str =“ aaabbd” ：
> 
> *   a = 3
> *   b = 2
> *   d = 1
> 
> 由于需要以频率增加的顺序生成数字，因此最终生成的数字是 **124** 。
> **输入**：N = 6，Str =“ akkzzz”
> **输出**：611
> **说明**：
> 给定的字符及其字符 各自的频率是：
> 
> *   a = 1
> *   k = 2
> *   z = 3
> 
> 对于 **z** ，分配给的值= **26**
> 因此，分配给相应的数字= **26％10 = 6**
> 对于 **k** 的值，分配给的值= **11** 。 频率，最终生成的数字是 **611** 。

**方法**：[

]请按照以下步骤解决问题：

*   初始化[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)并存储每个字符的频率。

*   遍历**映射**并将所有{**字符，频率**}对插入向量对中。

*   对向量进行排序，以使频率较高的*对首先出现*，而频率相同的对中，ASCII 值较小的对首先出现。

*   遍历此向量并找到与每个字符相对应的数字。

*   打印生成的最终号码。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Custom comparator for sorting
bool comp(pair<char, int>& p1,
          pair<char, int>& p2)
{

    // If frequency is same
    if (p1.second == p2.second)

        // Character with lower ASCII
        // value appears first
        return p1.first < p2.first;

    // Otherwise character with higher
    // frequency appears first
    return p1.second > p2.second;
}

// Function to sort map accordingly
string sort(map<char, int>& m)
{

    // Declaring vector of pairs
    vector<pair<char, int> > a;

    // Output string to store the result
    string out;

    // Traversing map and pushing
    // pairs to vector
    for (auto x : m) {

        a.push_back({ x.first, x.second });
    }

    // Using custom comparator
    sort(a.begin(), a.end(), comp);

    // Traversing the Vector
    for (auto x : a) {

        // Get the possible digit
        // from assigned value
        int k = x.first - 'a' + 1;

        // Ensures k does not exceed 9
        k = k % 10;

        // Apppend each digit
        out = out + to_string(k);
    }

    // Returning final result
    return out;
}

// Function to generate and return
// the required number
string formString(string s)
{
    // Stores the frequencies
    map<char, int> mp;

    for (int i = 0; i < s.length(); i++)
        mp[s[i]]++;

    // Sort map in required order
    string res = sort(mp);

    // Return the final result
    return res;
}

// Driver Code
int main()
{
    int N = 4;

    string Str = "akkzzz";

    cout << formString(Str);

    return 0;
}

```

## Python3

```py

# Python3 Program to implement 
# the above approach

# Function to sort map 
# accordingly
def sort(m):

    # Declaring vector 
    # of pairs
    a = {}

    # Output string to 
    # store the result
    out = ""

    # Traversing map and
    # pushing pairs to vector
    for x in m:
        a[x] = []

        a[x].append(m[x])

    # Character with lower ASCII 
    # value appears first
    a = dict(sorted(a.items(), 
                  key = lambda x : x[0]))

    # Character with higher 
    # frequency appears first 
    a = dict(sorted(a.items(), 
                    reverse = True, 
                    key = lambda x : x[1]))

    # Traversing the Vector
    for x in a:

        # Get the possible digit 
        # from assigned value
        k = ord(x[0]) - ord('a') + 1

        # Ensures k does 
        # not exceed 9
        k = k % 10

        # Apppend each digit
        out = out + str(k)

    # Returning final result
    return out

# Function to generate and return 
# the required number
def formString(s):

    # Stores the frequencies
    mp = {}
    for i in range(len(s)):
        if s[i] in mp:
            mp[s[i]] += 1
        else:
            mp[s[i]] = 1

    # Sort map in 
    # required order
    res = sort(mp)

    # Return the 
    # final result
    return res

# Driver Code 
N = 4
Str = "akkzzz"
print(formString(Str))

# This code is contributed by avanitrachhadiya2155

```

**Output:** 

```
611

```

***时间复杂度**：O（NlogN）*

***辅助空间**：O（N）*



* * *

* * *



