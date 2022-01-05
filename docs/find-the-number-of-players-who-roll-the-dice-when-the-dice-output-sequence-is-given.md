# 给出骰子输出顺序时，找出掷骰子的玩家数量

> 原文:[https://www . geeksforgeeks . org/find-掷骰子的玩家数量-当骰子输出序列被给出时/](https://www.geeksforgeeks.org/find-the-number-of-players-who-roll-the-dice-when-the-dice-output-sequence-is-given/)

给定一个字符串 **S** 和一个数字 **X** 。有 **M** 玩家掷骰子。玩家继续掷骰子，直到得到除 **X** 以外的数字。在字符串 S 中，S[i]代表骰子第 I 次滚动时的数字。任务是找到 **M** 。**注意****S**中的最后一个字符永远不会是 **X** 。
**例:**

> **输入:** s = "3662123 "，X = 6
> **输出:** 5
> 第一个玩家掷骰子得到 3。
> 第二个玩家掷出并获得 6、6 和 2。
> 第三名玩家掷骰子得到 1。
> 第四名玩家掷骰子得到 2。
> 第五名玩家掷出并获得 3。
> **输入:** s = "1234223 "，X = 2
> **输出:** 4

**方法:**迭代字符串，统计非 **X** 的字符。不是 **X** 的字符数就是玩家数。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of players
int findM(string s, int x)
{

    // Initialize cnt as 0
    int cnt = 0;

    // Iterate in the string
    for (int i = 0; i < s.size(); i++) {

        // Check for numbers other than x
        if (s[i] - '0' != x)
            cnt++;
    }
    return cnt;
}

// Driver code
int main()
{
    string s = "3662123";
    int x = 6;
    cout << findM(s, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the number of players
static int findM(String s, int x)
{

    // Initialize cnt as 0
    int cnt = 0;

    // Iterate in the string
    for (int i = 0; i < s.length(); i++)
    {

        // Check for numbers other than x
        if (s.charAt(i) - '0' != x)
            cnt++;
    }
    return cnt;
}

// Driver code
public static void main(String args[])
{
    String s = "3662123";
    int x = 6;
    System.out.println(findM(s, x));

}
}

//This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the number of players
def findM(s, x):

    # Initialize cnt as 0
    cnt = 0

    # Iterate in the string
    for i in range(len(s)):

        # Check for numbers other than x
        if (ord(s[i]) - ord('0') != x):
            cnt += 1

    return cnt

# Driver code
if __name__ == '__main__':
    s = "3662123"
    x = 6
    print(findM(s, x))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number of players
static int findM(String s, int x)
{

    // Initialize cnt as 0
    int cnt = 0;

    // Iterate in the string
    for (int i = 0; i < s.Length; i++)
    {

        // Check for numbers other than x
        if (s[i] - '0' != x)
            cnt++;
    }
    return cnt;
}

// Driver code
public static void Main()
{
    String s = "3662123";
    int x = 6;
    Console.Write(findM(s, x));
}
}

// This code is contributed by
// mohit kumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of players
function findM($s, $x)
{

    // Initialize cnt as 0
    $cnt = 0;

    // Iterate in the string
    for ($i = 0; $i < strlen($s); $i++)
    {

        // Check for numbers other than x
        if (ord($s[$i]) - ord('0') != $x)
            $cnt++;
    }
    return $cnt;
}

// Driver code
$s = "3662123";
$x = 6;

echo findM($s, $x);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the number of players
    function findM( s , x) {

        // Initialize cnt as 0
        var cnt = 0;

        // Iterate in the string
        for (i = 0; i < s.length; i++) {

            // Check for numbers other than x
            if (s.charCodeAt(i) - '0'.charCodeAt(0) != x)
                cnt++;
        }
        return cnt;
    }

    // Driver code

        var s = "3662123";
        var x = 6;
        document.write(findM(s, x));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
5
```