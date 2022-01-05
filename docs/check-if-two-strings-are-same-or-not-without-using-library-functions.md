# 不使用库函数检查两个字符串是否相同

> 原文:[https://www . geeksforgeeks . org/check-如果两个字符串相同或不相同，则不使用库函数/](https://www.geeksforgeeks.org/check-if-two-strings-are-same-or-not-without-using-library-functions/)

给定两个[字符串](https://www.geeksforgeeks.org/python-strings/) **S1** 和 **S2** ，任务是在不使用[字符串库函数](https://www.geeksforgeeks.org/commonly-used-string-functions-in-c-c-with-examples/)的情况下检查它们是否相同。

**示例:**

> **输入:**S1 =“geesforgeks”，S2 =“geesforgeks”
> T3】输出:T5】真
> T7】说明:T9】S1 和 S2 是同一个字符串
> 
> **输入:** S1 =【极客 ForGeeks】，S2 =【极客 forgeeks】
> T3】输出:T5】假

**方法:**按照以下步骤解决问题:

*   创建一个函数**comparistrings()**，该函数将两个字符串 **S1** 和 **S2** 作为输入参数，并执行以下操作:
    *   如果 **S1** 和 **S2** 的[长度](https://www.geeksforgeeks.org/python-string-length-len/)不同，则返回**假**。
    *   将 **S1** 的长度存储在一个变量中，比如 **N** 。
    *   使用变量 **i** 从 **0** 遍历到 **N-1** ，并执行以下操作:
        *   如果**S1【I】**不等于**S2【I】**，则返回**假**。
    *   遍历结束时返回**真**。

下面是上述方法的实现:

## C

```
#include <stdbool.h>
#include <stdio.h>

// Function to calculate length of string
int len(char* S)
{
    // Variable for traversal
    int i = 0;

    // Traverse till null is reached
    while (S[i])
        i++;

    return i;
}

// Function to check whether
// two strings are same or not
bool compareStrings(char S1[], char S2[])
{
    // If lengths of the two
      // strings are different
    if (len(S1) != len(S2))
        return false;

    // Variable for traversal
    int i = 0;

    // Traverse till null is reached
    while (S1[i]) {

        if (S1[i] != S2[i])
            return false;

          // Increment i
        i++;
    }
    return true;
}

// Driver Code
int main()
{
    // Input
    char S1[] = "GeeksForGeeks";
    char S2[] = "GeeksForGeeks";

    // Function Call
    bool ans = compareStrings(S1, S2);

    printf("%s", ans ? "True" : "False");

    return 0;
}
```

## 蟒蛇 3

```
# Function to check whether
# two strings are same or not
def compareStrings(S1, S2):

    # If lengths of the two
    # strings are different
    if (len(S1) != len(S2)):
        return False

    # Variable for traversal
    i = 0

    # Traverse till null is reached
    while (i < len(S1)):
        if (S1[i] != S2[i]):
            return False

        # Increment i
        i += 1

    return True

# Driver Code
if __name__ == '__main__':

    # Input
    S1 = "GeeksForGeeks"
    S2 = "GeeksForGeeks"

    # Function Call
    ans = compareStrings(S1, S2)

    print("True" if ans else "False")

# This code is contributed by mohit kumar 29
```

## C#

```
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate length of string
static int len(string S)
{
    // Variable for traversal
    int i = 0;

    // Traverse till null is reached
    while (i < S.Length)
        i++;

    return i;
}

// Function to check whether
// two strings are same or not
static bool compareStrings(string S1, string S2)
{

    // If lengths of the two
    // strings are different
    if (len(S1) != len(S2))
        return false;

    // Variable for traversal
    int i = 0;

    // Traverse till null is reached
    while (i < S1.Length)
    {
        if (S1[i] != S2[i])
            return false;

        // Increment i
        i++;
    }
    return true;
}

// Driver Code
public static void Main()
{

    // Input
    string S1 = "GeeksForGeeks";
    string S2 = "GeeksForGeeks";

    // Function Call
    bool ans = compareStrings(S1, S2);

    Console.Write(ans ? "True" : "False");
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

function len(S)
{
    // Variable for traversal
    let i = 0;

    // Traverse till null is reached
    while (i < S.length)
        i++;

    return i;
}

function compareStrings(S1,S2)
{
    // If lengths of the two
    // strings are different
    if (len(S1) != len(S2))
        return false;

    // Variable for traversal
    let i = 0;

    // Traverse till null is reached
    while (i < S1.length)
    {
        if (S1[i] != S2[i])
            return false;

        // Increment i
        i++;
    }
    return true;
}

// Input
let S1 = "GeeksForGeeks";
let S2 = "GeeksForGeeks";

// Function Call
let ans = compareStrings(S1, S2);

document.write(ans ? "True" : "False");

// This code is contributed by patel2127
</script>
```

**Output**

```
True
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)