# 检查二进制字符串是否包含 A 对 0 和 B 对独立的 0

> 原文:[https://www . geesforgeks . org/check-if-a-binary-string-contains-a-pairs-of-0-and-b-independent-0-or-not/](https://www.geeksforgeeks.org/check-if-a-binary-string-contains-a-pairs-of-0s-and-b-independent-0s-or-not/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和两个正整数 **A** 和 **B** ，任务是检查该字符串是否由[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)中的 **A** 独立的相邻对 **0s** 和 **B** 独立的 **0s** 组成。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** S = "10100 "，A = 1，B = 1
> **输出:**是
> **解释:**
> 给定的字符串由 A (=1)对相邻的 0 和 B (=1)对独立的 0 组成。
> 
> **输入:** S = "0101010 "，A = 1，B = 2
> **输出:**否
> **说明:**
> 给定字符串没有相邻的 0 对。

**方法:**按照以下步骤解决问题:

*   [使用变量遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，说出 **i，**并执行以下步骤:
    *   如果当前字符为**‘0’**，其相邻字符为**‘0’**， **A** 至少为**1**，那么将 **A** 减少 **1** ，将指针 **i** 增加 **1** 。
    *   否则，如果当前字符为**‘0’**， **B** 至少为**1**，则以 **1** 减少 **B** 。
*   完成上述步骤后，如果**A****B**的值为 **0** ，则打印“**是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exists
// A adjacent 0s and B 0s in the
// given binary string or not
void parking(string S, int a, int b)
{
    // Traverse the string
    for (int i = 0; i < S.size(); i++) {
        if (S[i] == '0') {
            // If there are adjacent
            // 0s and a is positive
            if (i + 1 < S.size()
                && S[i + 1] == '0'
                && a > 0) {

                i++;
                a--;
            }

            // If b is positive
            else if (b > 0) {
                b--;
            }
        }
    }

    // Condition for Yes
    if (a == 0 && b == 0) {
        cout << "Yes\n";
    }
    else
        cout << "No\n";
}

// Driver Code
int main()
{
    string S = "10100";
    int A = 1, B = 1;
    parking(S, A, B);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if there exists
// A adjacent 0s and B 0s in the
// given binary string or not
static void parking(String S, int a, int b)
{

    // Traverse the string
    for(int i = 0; i < S.length(); i++)
    {
        if (S.charAt(i) == '0')
        {

            // If there are adjacent
            // 0s and a is positive
            if (i + 1 < S.length() &&
                S.charAt(i + 1) == '0' && a > 0)
            {
                i++;
                a--;
            }

            // If b is positive
            else if (b > 0)
            {
                b--;
            }
        }
    }

    // Condition for Yes
    if (a == 0 && b == 0)
    {
        System.out.print("Yes\n");
    }
    else
        System.out.print("No\n");
}

// Driver Code
public static void main (String[] args)
{

    // Given string
    String S = "10100";
    int A = 1, B = 1;

    parking(S, A, B);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exists
# A adjacent 0s and B 0s in the
# given binary string or not
def parking(S, a, b):

    # Traverse the string
    for i in range(len(S)):
        if (S[i] == '0'):

            # If there are adjacent
            # 0s and a is positive
            if (i + 1 < len(S) and
              S[i + 1] == '0' and a > 0):
                i += 1
                a -= 1

            # If b is positive
            elif (b > 0):
                b -= 1

    # Condition for Yes
    if (a == 0 and b == 0):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    S = "10100"
    A = 1
    B = 1

    parking(S, A, B)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if there exists
// A adjacent 0s and B 0s in the
// given binary string or not
static void parking(string S, int a, int b)
{

    // Traverse the string
    for(int i = 0; i < S.Length; i++)
    {
        if (S[i] == '0')
        {

            // If there are adjacent
            // 0s and a is positive
            if (i + 1 < S.Length &&
                 S[i + 1] == '0' && a > 0)
            {
                i++;
                a--;
            }

            // If b is positive
            else if (b > 0)
            {
                b--;
            }
        }
    }

    // Condition for Yes
    if (a == 0 && b == 0)
    {
        Console.WriteLine("Yes");
    }
    else
         Console.WriteLine("No");
}

// Driver Code
public static void Main (string[] args)
{

    // Given string
    string S = "10100";
    int A = 1, B = 1;

    parking(S, A, B);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Function to check if there exists
// A adjacent 0s and B 0s in the
// given binary string or not
function parking( S, a, b)
{
    // Traverse the string
    for (var i = 0; i < S.length; i++) {
        if (S[i] == '0') {
            // If there are adjacent
            // 0s and a is positive
            if (i + 1 < S.length
                && S[i + 1] == '0'
                && a > 0) {

                i++;
                a--;
            }

            // If b is positive
            else if (b > 0) {
                b--;
            }
        }
    }

    // Condition for Yes
    if (a == 0 && b == 0) {
        document.write("Yes"+"<br>");
    }
    else
        document.write( "No"+"<br>");
}

var S = "10100";
var A = 1, B = 1;
parking(S, A, B);

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助** **空间:** O(1)