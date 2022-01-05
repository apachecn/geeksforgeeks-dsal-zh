# 检查一个字符串是否可以通过附加另一个字符串的子序列获得

> 原文:[https://www . geesforgeks . org/check-if-a-string-可以通过追加另一个字符串的子序列来获得/](https://www.geeksforgeeks.org/check-if-a-string-can-be-obtained-by-appending-subsequences-of-another-string/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **str1** 和 **str2** ，任务是检查 **str2** 是否可以通过多次追加 **str1** 的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)形成。如果可能，打印所需的最小追加操作数。否则，打印 **-1** 。

**示例:**

> **输入:**str 1 =“abb”，str2 =“ababbb”
> T3】输出: 4
> **说明:**
> 字符串 str 2 可以通过追加 str 1 =“ab”+“abb”+“bb”+“b”=“ababbb”的子序列形成。因为至少需要 4 个操作，所以打印 4 个。
> 
> **输入:**str1 =“mt”，str2 =“atttm”
> **输出:** -1
> **解释:**
> 由于字符串 str1 中不存在‘a’，因此无法从 str 1 生成 str 2。因此，打印-1。

**方法:**想法是基于以下观察使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)的概念:

*   考虑字符串**str 1 =“abb”**和**str 2 =“ABA”**。在 **str1** 中找到索引大于等于 **0** 的字符**str 2【0】**的位置，即 **str1** 的索引 **0** 。
*   再次在 **str1** 中找到**str 2【1】**，使其指数大于或等于 **1** ，即 **str1** 的指数 **1** 。
*   然后在 **str1** 中找到**str 2【2】**，使其指数大于等于不存在的 **2** 。
*   因此，从索引 **0** 重新开始，在 **str1** 中找到索引大于或等于索引 **0** 的**str 2【2】**，即 **str1** 的索引 **0** 。
*   因此，两个子序列**“ab”**和**“a”**可以被附加以形成**“ABA”**。

按照以下步骤解决问题:

*   初始化一个长度为 **26** 的[向量阵列](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/) **向量[]** 。
*   在**vec【0】**中推送所有字符为**‘a’**的指标 **str1** 。同样，在**vec【1】**中推送所有具有字符**【b】**的索引。从 **'a'** 到 **'z'** 的每个字符都要这样做。
*   用 **1** 初始化一个变量结果，用 **0** 定位，存储 **str1** 的最小操作和当前位置。
*   在范围**【0，M】**内遍历字符串 **str2** ，并对每个字符执行以下操作:
    *   如果**vec[str 2[I]–‘a’]**为空，则字符 **str2[i]** 在 **str1** 中不存在。因此，答案是不可能的。因此，打印 **-1** 。
    *   否则，在**vec【str 2[I]–‘a’】**中找到位置的[下限](https://www.geeksforgeeks.org/lower_bound-in-cpp/)。顺其自然 **p** 。如果 **p** 等于**vec【str 2[I]–‘a’】**的大小，那么将结果增加 **1** 并将 **i** 减少 **1** ，因为尚未找到字符 **str2[i]** 的答案，并将位置设置为 **0** 。
    *   否则，将位置设置为 **(vec[p] + 1)** 。
*   遍历后，将结果打印为所需的最少操作。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>

using namespace std;

// Function to find minimum operations
// required to form str2 by adding
// subsequences of str1
void find(string str1, string str2)
{

    // Initialize vector of length 26
    vector<int> vec1[26];

    // Push indices of characters of str1
    for (int i = 0; i < str1.size(); i++)
        vec1[str1[i] - 'a'].push_back(i);

    // Initialize the result & position
    int result = 1, position = 0;

    // Traverse the string str2
    for (int i = 0; i < str2.size(); i++)
    {

        char c = str2[i];

        // Return if no answer exist
        if (vec1.empty())
        {
            result = -1;
            break;
        }

        // Pointer of vec1[c-'a']
        vector<int>& vec2 = vec1;

        // Lower bound of position
        int p = lower_bound(vec2.begin(),
                            vec2.end(),
                            position)
                - vec2.begin();

        // If no index found
        if (p == vec2.size())
        {
            // Increment result
            result++;
            i--;
            position = 0;
            continue;
        }

        // Update the position
        else {
            position = vec2[p] + 1;
        }
    }

    // Print the result
    cout << result << '\n';
}

// Driver Code
int main()
{
    // Given string str1 & str2
    string str1 = "abb", str2 = "ababbbbb";

    // Function Call
    find(str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    static void find(String str1, String str2)
    {

        List<List<Integer> > vec1
            = new ArrayList<List<Integer> >();

        // Initialize vector of length 26
        for (int i = 0; i < 26; i++) {
            vec1.add(new ArrayList<Integer>());
        }

        // Push indices of characters of str1
        for (int i = 0; i < str1.length(); i++)
            vec1.get(str1.charAt(i) - 'a').add(i);

        // Initialize the result & position
        int result = 1, position = 0;

        // Traverse the string str2
        for (int i = 0; i < str2.length(); i++)
        {
            char c = str2.charAt(i);

            // Return if no answer exist
            if (vec1.get(c - 'a').size() == 0)
            {
                result = -1;
                break;
            }

            List<Integer> vec2 = vec1.get(c - 'a');

            // Lower bound of position
            int p = lower_bound(vec2, position);

            // If no index found
            if (p == vec2.size())
            {

                // Increment result
                result++;
                i--;
                position = 0;
                continue;
            }

            // Update the position
            else {
                position = vec2.get(p) + 1;
            }
        }

        // Print the result
        System.out.println(result);
    }

    // Driver Code
    static int lower_bound(List<Integer> vec2, int position)
    {
        int low = 0, high = vec2.size() - 1;

        while (low < high) {
            int mid = (low + high) / 2;
            if (vec2.get(mid) < position)
                low = mid + 1;
            else
                high = mid;
        }
        return (vec2.get(low) < position) ? low + 1 : low;
    }

    public static void main(String[] args)
    {
        // Given string str1 & str2
        String str1 = "abb", str2 = "ababbbbb";

        // Function Call
        find(str1, str2);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left

# Function to find minimum operations
# required to form str2 by adding
# subsequences of str1
def find(str1, str2):

    # Initialize vector of length 26
    vec1 = [[] for i in range(26)]

    # Push indices of characters of str1
    for i in range(len(str1)):
        vec1[ord(str1[i]) - ord('a')].append(i)

    # Initialize the result & position
    result = 1
    position = 0

    # Traverse the str2
    i = 0
    while i < len(str2):
        c = str2[i]

        # Return if no answer exist
        if (len(vec1[ord(c) - ord('a')]) == 0):
            result = -1
            break

        # Pointer of vec1[c-'a']
        vec2 = vec1[ord(c) - ord('a')]

        # Lower bound of position
        p = bisect_left(vec2, position)

        #print(c)

        # If no index found
        if (p == len(vec2)):

            # Increment result
            result += 1

            #i-=1
            position = 0
            continue

        # Update the position
        else:
            i += 1
            position = vec2[p] + 1

    # Print the result
    print(result)

# Driver Code
if __name__ == '__main__':

    # Given str1 & str2
    str1 = "abb"
    str2 = "ababbbbb"

    # Function Call
    find(str1, str2)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum operations
// required to form str2 by adding
// subsequences of str1   
static void find(string str1, string str2)
{
    List<List<int>> vec1 = new List<List<int>>();

    // Initialize vector of length 26
    for(int i = 0; i < 26; i++)
    {
        vec1.Add(new List<int>());
    }

    // Push indices of characters of str1
    for(int i = 0; i < str1.Length; i++)
    {
        vec1[str1[i] - 'a'].Add(i);
    }

    // Initialize the result & position
    int result = 1, position = 0;

    // Traverse the string str2
    for(int i = 0; i < str2.Length; i++)
    {
        char c = str2[i];

        // Return if no answer exist
        if (vec1.Count == 0)
        {
            result = -1;
            break;
        }
        List<int> vec2 = vec1;

        // Lower bound of position
        int p = lower_bound(vec2, position);

        // If no index found
        if (p == vec2.Count)
        {

            // Increment result
            result++;
            i--;
            position = 0;
            continue;
        }

        // Update the position
        else
        {
            position = vec2[p] + 1;
        }
    }

    // Print the result
    Console.WriteLine(result);
}

static int lower_bound(List<int> vec2,
                       int position)
{
    int low = 0, high = vec2.Count - 1;

    while (low < high)
    {
        int mid = (low + high) / 2;

        if (vec2[mid] < position)
        {
            low = mid + 1;
        }
        else
        {
            high = mid;
        }
    }
    return (vec2[low] < position) ?
                  low + 1 : low;
}

// Driver Code
static public void Main()
{

    // Given string str1 & str2
    string str1 = "abb", str2 = "ababbbbb";

    // Function Call
    find(str1, str2);
}
}

// This code is contributed by avanitrachhadiya2155
```

**Output**

```
4
```

**时间复杂度:**O(N+M log N)
T3】辅助空间: O(M + N)