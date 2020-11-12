# 在给定字符串中连续出现的不同子字符串的计数

> 原文：[https://www.geeksforgeeks.org/count-of-distinct-substrings-occurring-consecutively-in-a-given-string/](https://www.geeksforgeeks.org/count-of-distinct-substrings-occurring-consecutively-in-a-given-string/)

给定字符串`str`，任务是查找在给定字符串中连续放置的**不同的子字符串**的数量。

**示例**：

> **输入**：`str = "geeksgeeksforgeeks"`
>
> **输出**：2
>
> **说明**：
>
> `geeksgeeksforgeeks -> {"geeks"}`
>
> `geeksgeeksforgeeks -> {"e"}`
>
> `"e"`仅连续出现一次。
>
> 因此，两个不同的子字符串`{"geeks", " e"}`在字符串中连续出现。
>
> 因此，答案是 2。
> 
> **输入**：`s =" geeksforgeeks"`
>
> **输出**：1
>
> **说明**：
>
> `geeksgeeksforgeeks -> {"e", "e"}`
>
> 字符串中仅连续出现一个子字符串`{"e"}`。

**朴素的方法**：

最简单的方法是[生成给定字符串的所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并为每个子字符串找到在字符串中连续出现的给定子字符串**计数** 。 最后，打印**计数**。

**时间复杂度**：`O(N ^ 3)`

**辅助空间**：`O(n)`

**有效方法**：

为了优化上述方法，其想法是使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)。

请按照以下步骤解决问题：

1.  如果字符串的长度确实**不超过 1**，则不可能找到任何这样连续放置的相似子字符串。 因此**返回 0** 作为**计数**。

2.  否则，初始化尺寸为`(N + 1) * (N + 1)`的备注表`dp[]`，该表被初始化为`0`。

3.  初始化[`unordered_set`](http://www.geeksforgeeks.org/unorderd_set-stl-uses/)，以存储连续放置的不同子字符串。

4.  从字符串末尾进行迭代。

5.  在遍历字符串时，如果发现任何**重复字符**，则将根据先前计算的`dp`值来确定`dp[i][j]`，即直到`dp[i+1][j+1]`字符的相同子字符串的数量，包括当前字符。

6.  如果字符不相似，则`dp[i][j]`将填充 0。

7.  相似的子字符串连续放置在一起，没有任何其他字符，并且最多`j – i`个字符相同。 因此，对于有效的子字符串， `dp[i][j]`值必须大于`j – i`。 将那些子字符串存储在`unordered_set`中，它代表连续出现最大次数。

8.  最后，返回`unordered_set`的[大小](https://www.geeksforgeeks.org/setsize-c-stl/)作为连续放置的不同子字符串的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the distinct substrings
// placed consecutively in the given string
int distinctSimilarSubstrings(string str)
{
    // Length of the string
    int n = str.size();

    // If length of the string
    // does not exceed 1
    if (n <= 1) {
        return 0;
    }

    // Initialize a DP-table
    vector<vector<int> > dp(
        n + 1, vector<int>(n + 1, 0));

    // Stores the distinct substring
    unordered_set<string> substrings;

    // Iterate from end of the string
    for (int j = n - 1; j >= 0; j--) {

        // Iterate backward until
        // dp table is all computed
        for (int i = j - 1; i >= 0; i--) {

            // If character at i-th index is
            // same as character at j-th index
            if (str[i] == str[j]) {

                // Update dp[i][j] based on
                // previously computed value
                dp[i][j] = dp[i + 1][j + 1] + 1;
            }

            // Otherwise
            else {

                dp[i][j] = 0;
            }

            // Condition for consecutively
            // placed similar substring
            if (dp[i][j] >= j - i) {

                substrings.insert(
                    str.substr(i, j - i));
            }
        }
    }

    // Return the count
    return substrings.size();
}

// Driver Code
int main()
{
    string str = "geeksgeeksforgeeks";

    cout << distinctSimilarSubstrings(str);
    return 0;
}

```

## Java

```java

// Java program to implement 
// the above approach 
import java.io.*;
import java.util.ArrayList;

class GFG{

// Function to count the distinct substrings 
// placed consecutively in the given string     
static int distinctSimilarSubstrings(String str)
{

    // Length of the string 
    int n = str.length();

    // If length of the string 
    // does not exceed 1 
    if (n <= 1)
        return 0;

    // Initialize a DP-table 
    long dp[][] = new long[n + 1][n + 1];

    // Declaring ArrayList to store strings
    ArrayList<String> list = new ArrayList<String>();

    // Iterate from end of the string 
    for(int j = n - 1; j >= 0; j--) 
    {

        // Iterate backward until
        // dp table is all computed
        for(int i = j - 1; i >= 0; i--) 
        {

            // If character at i-th index is
            // same as character at j-th index
            if (str.charAt(i) == str.charAt(j)) 
            {

                // Update dp[i][j] based on
                // previously computed value
                dp[i][j] = dp[i + 1][j + 1] + 1;
            }

            // Otherwise
            else
            {
                dp[i][j] = 0;
            }

            // Condition for consecutively
            // placed similar substring
            if (dp[i][j] >= j - i)
            {
                list.add(str.substring(j - i, i));
            }
        }
    }

    // Return the count
    return list.size();
}

// Driver Code
public static void main(String[] args)
{
    String str = "geeksforgeeks";

    System.out.println(distinctSimilarSubstrings(str));
}
}

// This code is contributed by user_00

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to count the distinct substrings
# placed consecutively in the given string
def distinctSimilarSubstrings(str):

    # Length of the string
    n = len(str)

    # If length of the string
    # does not exceed 1
    if(n <= 1):
        return 0

    # Initialize a DP-table
    dp = [[0 for x in range(n + 1)]
             for y in range(n + 1)]

    # Stores the distinct substring
    substrings = set()

    # Iterate from end of the string
    for j in range(n - 1, -1, -1):

        # Iterate backward until
        # dp table is all computed
        for i in range(j - 1, -1, -1):

            # If character at i-th index is
            # same as character at j-th index
            if(str[i] == str[j]):

                # Update dp[i][j] based on
                # previously computed value
                dp[i][j] = dp[i + 1][j + 1] + 1

            # Otherwise
            else:
                dp[i][j] = 0

            # Condition for consecutively
            # placed similar substring
            if(dp[i][j] >= j - i):
                substrings.add(str[i : j - i])

    # Return the count 
    return len(substrings)

# Driver Code
str = "geeksgeeksforgeeks"

# Function call
print(distinctSimilarSubstrings(str))

# This code is contributed by Shivam Singh

```

**输出**： 

```
2

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



