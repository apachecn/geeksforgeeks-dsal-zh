# 根据给定条件从圆形容器打印给定字符串所需的最短时间

> 原文:[https://www . geesforgeks . org/基于给定条件从循环容器打印给定字符串所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-print-given-string-from-a-circular-container-based-on-given-conditions/)

给定一个由从“a”到“z”的小写字母组成的**圆形容器**，一个最初指向字母“a”的**指针**，以及一个字符串 **str** ，任务是根据可以对每个字符执行的以下操作，找到从圆形容器打印给定字符串 **str** 所需的最短时间:

*   在一个单位时间内逆时针或顺时针移动指针一个字符
*   在一个单位时间内打印字符，然后将指针移动到字符串的下一个索引处

**示例:**

> **输入** : str = "zcd"
> **输出:** 8
> **说明:**步骤如下:
> 
> *   在 1 秒钟内将指针逆时针移动到“z”
> *   在 1 秒内键入字符“z”
> *   在 3 秒钟内将指针顺时针移动到“c”
> *   在 1 秒内键入字符“c”
> *   在 1 秒钟内将指针顺时针移动到“d”
> *   在 1 秒内键入字符“d”。
> 
> **输入:**str = " zjcp "
> T3】输出:34
> T6】说明:步骤如下:
> 
> *   在 1 秒钟内将指针逆时针移动到“z”
> *   在 1 秒内键入字符“z”
> *   在 10 秒内将指针顺时针移动到“j”
> *   在 1 秒内键入字符“j”
> *   在 6 秒钟内将指针顺时针移动到“p”
> *   在 1 秒内键入字符“p”
> *   在 13 秒内将指针逆时针移动到“c”。

**方法:**可以按照以下步骤解决给定的问题:

*   计算从当前指针索引双向到达字符索引所需的时间:
    *   顺时针时间通过取两个指数的绝对差值来计算
    *   逆时针时间通过从 26 中减去顺时针时间来计算
*   将前一步中获得的两次的最小值添加到答案中
*   然后打印字符，一个单位时间也被添加到答案中

最后打印得到的答案作为最短所需时间。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum time to
// print all characters in the string
void minTime(string word)
{

    int ans = 0;

    // Current element where the
    // pointer is pointing
    int curr = 0;

    for (int i = 0; i < word.length(); i++) {

        // Find index of that element
        int k = word[i] - 'a';

        // Calculate absolute difference
        // between pointer index and character
        // index as clockwise distance
        int a = abs(curr - k);

        // Subtract clockwise time from
        // 26 to get anti-clockwise time
        int b = 26 - abs(curr - k);

        // Add minimum of both times to
        // the answer
        ans += min(a, b);

        // Add one unit time to print
        // the character
        ans++;

        curr = word[i] - 'a';
    }

    // Print the final answer
    cout << ans;
}

// Driver code
int main()
{
    // Given string word
    string str = "zjpc";

    // Function call
    minTime(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
class GFG{

// Function to calculate minimum time to
// print all characters in the string
static void minTime(String word)
{

    int ans = 0;

    // Current element where the
    // pointer is pointing
    int curr = 0;

    for (int i = 0; i < word.length(); i++) {

        // Find index of that element
        int k = (int)word.charAt(i) - 97;

        // Calculate absolute difference
        // between pointer index and character
        // index as clockwise distance
        int a = Math.abs(curr - k);

        // Subtract clockwise time from
        // 26 to get anti-clockwise time
        int b = 26 - Math.abs(curr - k);

        // Add minimum of both times to
        // the answer
        ans += Math.min(a, b);

        // Add one unit time to print
        // the character
        ans++;

        curr = (int)word.charAt(i) - 97;
    }

    // Print the final answer
    System.out.print(ans);
}

// Driver code
public static void main(String[] args)
{

    // Given string word
    String str = "zjpc";

    // Function call
    minTime(str);
}

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Function to calculate minimum time to
# print all characters in the string
def minTime(word):
    ans = 0

    # Current element where the
    # pointer is pointing
    curr = 0

    for i in range(len(word)):
        # Find index of that element
        k = ord(word[i]) - 97

        # Calculate absolute difference
        # between pointer index and character
        # index as clockwise distance
        a = abs(curr - k)

        # Subtract clockwise time from
        # 26 to get anti-clockwise time
        b = 26 - abs(curr - k)

        # Add minimum of both times to
        # the answer
        ans += min(a, b)

        # Add one unit time to print
        # the character
        ans += 1

        curr = ord(word[i]) - 97

    # Print the final answer
    print(ans)

# Driver code
if __name__ == '__main__':
    # Given string word
    str = "zjpc"

    # Function call
    minTime(str)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate minimum time to
// print all characters in the string
static void minTime(string word)
{

    int ans = 0;

    // Current element where the
    // pointer is pointing
    int curr = 0;

    for (int i = 0; i < word.Length; i++) {

        // Find index of that element
        int k = (int)word[i] - 97;

        // Calculate absolute difference
        // between pointer index and character
        // index as clockwise distance
        int a = Math.Abs(curr - k);

        // Subtract clockwise time from
        // 26 to get anti-clockwise time
        int b = 26 - Math.Abs(curr - k);

        // Add minimum of both times to
        // the answer
        ans += Math.Min(a, b);

        // Add one unit time to print
        // the character
        ans++;

        curr = (int)word[i] - 97;
    }

    // Print the final answer
    Console.Write(ans);
}

// Driver code
public static void Main()
{
    // Given string word
    string str = "zjpc";

    // Function call
    minTime(str);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

    // Function to calculate minimum time to
// print all characters in the string
funs minTime(string word)
{

    int ans = 0;

    // Current element where the
    // pointer is pointing
    let curr = 0;

    for (let i = 0; i < word.Length; i++) {

        // Find index of that element
        int k = word[i].charAt(0) - 'a'.charAt(0);

        // Calculate absolute difference
        // between pointer index and character
        // index as clockwise distance
        let a = Math.abs(curr - k);

        // Subtract clockwise time from
        // 26 to get anti-clockwise time
        let b = 26- Math.abs(curr - k);

        // Add minimum of both times to
        // the answer
        ans += Math.min(a, b);

        // Add one unit time to print
        // the character
        ans++;

        curr = word[i].charAt(0)- 'a'.charAt(0);
    }

    // Print the final answer
      document.write(ans);
}

        // Driver Code

        // Given Input
         let str="zjpc";

        // Function Call
        minTime(str);

// This code is contributed by dwivediyash
    </script>
```

**Output**

```
34
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度
T3】辅助空间: O(1)