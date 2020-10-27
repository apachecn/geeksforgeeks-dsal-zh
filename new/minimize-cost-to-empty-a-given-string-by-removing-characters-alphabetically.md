# 通过按字母顺序删除字符来最大程度地减少清空给定字符串的成本。

给定字符串 **str** ，任务是最小化以[字母顺序](https://www.geeksforgeeks.org/check-if-the-characters-of-a-given-string-are-in-alphabetical-order/)从字符串中删除所有字符的总成本。

> 从字符串中删除第<sup>个第</sup>个索引处的任何字符的成本为 **i** 。 索引基于 1。

**示例：**

> **输入：** str =“ abcab”
> **输出：** 8
> **说明：**
> 删除索引 1 的第一个字符'a'， str []变为“ bcab”，
> 然后删除索引为 3 的 char'a'，str []变为“ bcb”。
> 在删除索引为 1 的 char'b'之后，str []变为“ cb ”，
> 然后删除索引为 2 的 char'b'，str []变为“ c”，
> 最后，删除 char'c'。
> 总分= 1 + 3 +1 + 2 + 1 =8。
> **输入：** str =“ def”
> **输出：** 3

**天真的方法：**最简单的方法是在每一步中删除字符串中具有较小索引的最小字符，并继续将成本添加到总成本中。 执行此操作后，打印最终成本。

***时间复杂度：** O（N <sup>2</sup> ）*
***辅助空间：** O（1）*

**高效方法：**通过为每个字符预先计算给定字符串中位于其前面的较小字符的数量，可以优化上述方法。 步骤如下：

1.  将总成本初始化为 **0** 。
2.  遍历给定的字符串，并为每个字符计算小于当前字符且在其之前出现的字符数。
3.  如果此计数为 0，则表示将在当前索引处删除当前字符，因此将字符的索引添加到结果成本中。
4.  否则，从当前索引中减去该计数，然后将其添加到总费用中。
5.  完成上述所有步骤后，打印总费用。

下面是上述方法的实现：

## C ++

```

// C++ program for the above approach
#include <bits/stdc++.h>
#include <vector>
using namespace std;

// Function to find the minimum cost
// required to remove each character
// of the string in alphabetical order
int minSteps(string str, int N)
{
    int smaller, cost = 0;

    // Stores the frequency of
    // characters of the string
    int f[26] = { 0 };

    // Iterate through the string
    for (int i = 0; i < N; i++) {
        int curr_ele = str[i] - 'a';
        smaller = 0;

        // Count the number of characters
        // smaller than the present character
        for (int j = 0; j <= curr_ele; j++) {
            if (f[j])
                smaller += f[j];
        }

        // If no smaller character
        // preceeds current character
        if (smaller == 0)
            cost += (i + 1);
        else
            cost += (i - smaller + 1);

        // Increase the frequency of
        // the current character
        f[str[i] - 'a']++;
    }

    // Return the
    // total cost
    return cost;
}

// Driver Code
int main()
{
    // Given string str
    string str = "abcab";
    int N = str.size();

    // Function call
    cout << minSteps(str, N);
    return 0;
}

```

## 爪哇

```

// Java program for 
// the above approach
import java.io.*;
class GFG{

    // Function to find the minimum cost
    // required to remove each character
    // of the string in alphabetical order
    static int minSteps(String str, int N)
    {
        int smaller, cost = 0;

        // Stores the frequency of
        // characters of the string
        int f[] = new int[26];

        // Iterate through the string
        for (int i = 0; i < N; i++) 
        {
            int curr_ele = str.charAt(i) - 'a';
            smaller = 0;

            // Count the number of characters
            // smaller than the present character
            for (int j = 0; j <= curr_ele; j++) 
            {
                if (f[j] != 0)
                    smaller += f[j];
            }

            // If no smaller character
            // preceeds current character
            if (smaller == 0)
                cost += (i + 1);
            else
                cost += (i - smaller + 1);

            // Increase the frequency of
            // the current character
            f[str.charAt(i) - 'a']++;
        }

        // Return the
        // total cost
        return cost;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string str
        String str = "abcab";

        int N = str.length();

        // Function call
        System.out.println(minSteps(str, N));
    }
}

// This code is contributed by AnkitRai01

```

## Python3

```

# Python3 program for the above approach 

# Function to find the minimum cost
# required to remove each character
# of the string in alphabetical order 
def minSteps(str, N):

    cost = 0

    # Stores the frequency of
    # characters of the string
    f = [0] * 26

    # Iterate through the string
    for i in range(N):
        curr_ele = ord(str[i]) - ord('a')
        smaller = 0

        # Count the number of characters
        # smaller than the present character
        for j in range(curr_ele + 1):
            if (f[j]):
                smaller += f[j]

        # If no smaller character
        # preceeds current character
        if (smaller == 0):
            cost += (i + 1)
        else:
            cost += (i - smaller + 1)

        # Increase the frequency of
        # the current character
        f[ord(str[i]) - ord('a')] += 1

    # Return the total cost
    return cost

# Driver Code

# Given string str
str = "abcab"

N = len(str)

# Function call
print(minSteps(str, N))

# This code is contributed by Shivam Singh

```

## C＃

```

// C# program for 
// the above approach
using System;
class GFG{

// Function to find the minimum cost
// required to remove each character
// of the string in alphabetical order
static int minSteps(string str, int N)
{
    int smaller, cost = 0;

    // Stores the frequency of
    // characters of the string
    int[] f = new int[26];

    // Iterate through the string
    for (int i = 0; i < N; i++) 
    {
        int curr_ele = str[i] - 'a';
        smaller = 0;

        // Count the number of characters
        // smaller than the present character
        for (int j = 0; j <= curr_ele; j++) 
        {
            if (f[j] != 0)
            smaller += f[j];
        }

        // If no smaller character
        // preceeds current character
        if (smaller == 0)
            cost += (i + 1);
        else
            cost += (i - smaller + 1);

        // Increase the frequency of
        // the current character
        f[str[i] - 'a']++;
    }

    // Return the
    // total cost
    return cost;
}

// Driver Code
public static void Main()
{

    // Given string str
    string str = "abcab";

    int N = str.Length;

    // Function call
    Console.Write(minSteps(str, N));
}
}

// This code is contributed by Chitranayal

```

**Output:** 

```
8

```

**时间复杂度：** O（N）
**辅助空间：** O（26）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。