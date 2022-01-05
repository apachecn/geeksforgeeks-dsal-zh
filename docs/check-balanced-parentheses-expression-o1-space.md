# 检查表达式| O(1)空间中的平衡括号

> 原文:[https://www . geesforgeks . org/check-balanced-括号-expression-o1-space/](https://www.geeksforgeeks.org/check-balanced-parentheses-expression-o1-space/)

给定一个长度为 n 的带圆括号的字符串，你的任务是找出给定的字符串是否有平衡圆括号。请注意，空间是有限制的，即我们只能使用 0(1)个额外空间。
**另请参见:** [检查平衡括号](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)
**示例:**

```
Input : (())[]
Output : Yes

Input : ))(({}{
Output : No
```

如果 k = 1，那么我们将简单地保持一个计数变量 c = 0，每当我们遇到一个左括号我们将增加 c，每当我们遇到一个右括号我们将减少 c 的计数，在任何阶段我们都不应该有 c < 0 and at the end we must have c = 0 for string to be balanced. 
下面是我们的算法对这个问题的想法。对于任何左括号，说“[”我们找到它匹配的右括号“]”。假设“[”的索引是 I，而“]”的索引是 j，那么下列条件必须为真:

1.  i < j
2.  对于所有的 k，例如 i < k < j，对于所有的左括号(index-k)，它匹配的右括号 x 必须满足 k < x < j，对于所有的右括号(index-k)，它匹配的左括号 x 必须满足 i < x < k

## C++

```
// C++ code to check balanced parentheses with
// O(1) space.
#include <stdio.h>
#include <stdlib.h>

// Function1 to match closing bracket
int matchClosing(char X[], int start,
                int end, char open, char close)
{
    int c = 1;
    int i = start + 1;
    while (i <= end) {
        if (X[i] == open)
            c++;
        else if (X[i] == close)
            c--;
        if (c == 0)
            return i;
        i++;
    }
    return i;
}

// Function1 to match opening bracket
int matchingOpening(char X[], int start,
                    int end, char open, char close)
{
    int c = -1;
    int i = end - 1;

    while (i >= start) {
        if (X[i] == open)
            c++;
        else if (X[i] == close)
            c--;
        if (c == 0)
            return i;
        i--;
    }
    return -1;
}

// Function to check balanced parentheses
bool isBalanced(char X[], int n)
{
    // helper variables
    int i, j, k, x, start, end;

    for (i = 0; i < n; i++) {
        // Handling case of opening parentheses
        if (X[i] == '(')
            j = matchClosing(X, i, n - 1, '(', ')');
        else if (X[i] == '{')
            j = matchClosing(X, i, n - 1, '{', '}');
        else if (X[i] == '[')
            j = matchClosing(X, i, n - 1, '[', ']');

        // Handling case of closing parentheses
        else {
            if (X[i] == ')')
                j = matchingOpening(X, 0, i, '(', ')');
            else if (X[i] == '}')
                j = matchingOpening(X, 0, i, '{', '}');
            else if (X[i] == ']')
                j = matchingOpening(X, 0, i, '[', ']');

            // If corresponding matching
            // opening parentheses doesn't
            // lie in given interval return 0
            if (j < 0 || j >= i)
                return false;

            // else continue
            continue;
        }

        // If corresponding closing parentheses
        // doesn't lie in given interval
        // return 0
        if (j >= n || j < 0)
            return false;

        // if found, now check for each
        // opening and closing parentheses
        // in this interval
        start = i;
        end = j;

        for (k = start + 1; k < end; k++) {
            if (X[k] == '(') {
                x = matchClosing(X, k, end, '(', ')');
                if (!(k < x && x < end)) {
                    return false;
                }
            }
            else if (X[k] == ')') {
                x = matchingOpening(X, start, k, '(', ')');
                if (!(start < x && x < k)) {
                    return false;
                }
            }

            if (X[k] == '{') {
                x = matchClosing(X, k, end, '{', '}');
                if (!(k < x && x < end)) {
                    return false;
                }
            }

            else if (X[k] == '}') {
                x = matchingOpening(X, start, k, '{', '}');
                if (!(start < x && x < k)) {
                    return false;
                }
            }
            if (X[k] == '[') {
                x = matchClosing(X, k, end, '[', ']');
                if (!(k < x && x < end)) {
                    return false;
                }
            }
            else if (X[k] == ']') {
                x = matchingOpening(X, start, k, '[', ']');
                if (!(start < x && x < k)) {
                    return false;
                }
            }
        }
    }

    return true;
}

// Driver Code
int main()
{
    char X[] = "[()]()";
    int n = 6;
    if (isBalanced(X, n))
        printf("Yes\n");
    else
        printf("No\n");

    char Y[] = "[[()]])";
    n = 7;
    if (isBalanced(Y, n))
        printf("Yes\n");
    else
        printf("No\n");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check balanced parentheses with
// O(1) space.

class GFG {

// Function1 to match closing bracket
    static int matchClosing(char X[], int start,
            int end, char open, char close) {
        int c = 1;
        int i = start + 1;
        while (i <= end) {
            if (X[i] == open) {
                c++;
            } else if (X[i] == close) {
                c--;
            }
            if (c == 0) {
                return i;
            }
            i++;
        }
        return i;
    }

// Function1 to match opening bracket
    static int matchingOpening(char X[], int start,
            int end, char open, char close) {
        int c = -1;
        int i = end - 1;

        while (i >= start) {
            if (X[i] == open) {
                c++;
            } else if (X[i] == close) {
                c--;
            }
            if (c == 0) {
                return i;
            }
            i--;
        }
        return -1;
    }

// Function to check balanced parentheses
    static boolean isBalanced(char X[], int n) {
        // helper variables
        int i, j = 0, k, x, start, end;

        for (i = 0; i < n; i++) {
            // Handling case of opening parentheses
            if (X[i] == '(') {
                j = matchClosing(X, i, n - 1, '(', ')');
            } else if (X[i] == '{') {
                j = matchClosing(X, i, n - 1, '{', '}');
            } else if (X[i] == '[') {
                j = matchClosing(X, i, n - 1, '[', ']');
            } // Handling case of closing parentheses
            else {
                if (X[i] == ')') {
                    j = matchingOpening(X, 0, i, '(', ')');
                } else if (X[i] == '}') {
                    j = matchingOpening(X, 0, i, '{', '}');
                } else if (X[i] == ']') {
                    j = matchingOpening(X, 0, i, '[', ']');
                }

                // If corresponding matching
                // opening parentheses doesn't
                // lie in given interval return 0
                if (j < 0 || j >= i) {
                    return false;
                }

                // else continue
                continue;
            }

            // If corresponding closing parentheses
            // doesn't lie in given interval
            // return 0
            if (j >= n || j < 0) {
                return false;
            }

            // if found, now check for each
            // opening and closing parentheses
            // in this interval
            start = i;
            end = j;

            for (k = start + 1; k < end; k++) {
                if (X[k] == '(') {
                    x = matchClosing(X, k, end, '(', ')');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == ')') {
                    x = matchingOpening(X, start, k, '(', ')');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }

                if (X[k] == '{') {
                    x = matchClosing(X, k, end, '{', '}');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == '}') {
                    x = matchingOpening(X, start, k, '{', '}');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }
                if (X[k] == '[') {
                    x = matchClosing(X, k, end, '[', ']');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == ']') {
                    x = matchingOpening(X, start, k, '[', ']');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }
            }
        }

        return true;
    }

// Driver Code
    public static void main(String[] args) {

    char X[] = "[()]()".toCharArray();
    int n = 6;
    if (isBalanced(X, n))
        System.out.printf("Yes\n");
    else
        System.out.printf("No\n");

    char Y[] = "[[()]])".toCharArray();
    n = 7;
    if (isBalanced(Y, n))
        System.out.printf("Yes\n");
    else
        System.out.printf("No\n");
    }
}
//this code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 code to check balanced
# parentheses with O(1) space.

# Function1 to match closing bracket
def matchClosing(X, start, end,
                   open, close):

    c = 1
    i = start + 1
    while (i <= end):
        if (X[i] == open):
            c += 1
        elif (X[i] == close):
            c -= 1
        if (c == 0):
            return i
        i += 1
    return i

# Function1 to match opening bracket
def matchingOpening(X, start, end,
                      open, close):

    c = -1
    i = end - 1

    while (i >= start):
        if (X[i] == open):
            c += 1
        elif (X[i] == close):
            c -= 1
        if (c == 0):
            return i
        i -= 1

    return -1

# Function to check balanced
# parentheses
def isBalanced(X, n):

    for i in range(n):

        # Handling case of opening
        # parentheses
        if (X[i] == '('):
            j = matchClosing(X, i, n - 1, '(', ')')
        elif (X[i] == '{'):
            j = matchClosing(X, i, n - 1, '{', '}')
        elif (X[i] == '['):
            j = matchClosing(X, i, n - 1, '[', ']')

        # Handling case of closing
        # parentheses
        else :
            if (X[i] == ')'):
                j = matchingOpening(X, 0, i, '(', ')')
            elif (X[i] == '}'):
                j = matchingOpening(X, 0, i, '{', '}')
            elif (X[i] == ']'):
                j = matchingOpening(X, 0, i, '[', ']')

            # If corresponding matching opening
            # parentheses doesn't lie in given
            # interval return 0
            if (j < 0 or j >= i):
                return False

            # else continue
            continue

        # If corresponding closing parentheses
        # doesn't lie in given interval, return 0
        if (j >= n or j < 0):
            return False

        # if found, now check for each opening and
        # closing parentheses in this interval
        start = i
        end = j

        for k in range(start + 1, end) :
            if (X[k] == '(') :
                x = matchClosing(X, k, end, '(', ')')
                if (not(k < x and x < end)):
                    return False

            elif (X[k] == ')'):
                x = matchingOpening(X, start, k, '(', ')')
                if (not(start < x and x < k)):
                    return False

            if (X[k] == '{'):
                x = matchClosing(X, k, end, '{', '}')
                if (not(k < x and x < end)):
                    return False

            elif (X[k] == '}'):
                x = matchingOpening(X, start, k, '{', '}')
                if (not(start < x and x < k)):
                    return False

            if (X[k] == '['):
                x = matchClosing(X, k, end, '[', ']')
                if (not(k < x and x < end)):
                    return False

            elif (X[k] == ']'):
                x = matchingOpening(X, start, k, '[', ']')
                if (not(start < x and x < k)):
                    return False

    return True

# Driver Code
if __name__ == "__main__":

    X = "[()]()"
    n = 6
    if (isBalanced(X, n)):
        print("Yes")
    else:
        print("No")

    Y = "[[()]])"
    n = 7
    if (isBalanced(Y, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ita_c
```

## C#

```

// C# code to check balanced parentheses with
// O(1) space.
using System;
public class GFG {

// Function1 to match closing bracket
    static int matchClosing(char []X, int start,
            int end, char open, char close) {
        int c = 1;
        int i = start + 1;
        while (i <= end) {
            if (X[i] == open) {
                c++;
            } else if (X[i] == close) {
                c--;
            }
            if (c == 0) {
                return i;
            }
            i++;
        }
        return i;
    }

// Function1 to match opening bracket
    static int matchingOpening(char []X, int start,
            int end, char open, char close) {
        int c = -1;
        int i = end - 1;

        while (i >= start) {
            if (X[i] == open) {
                c++;
            } else if (X[i] == close) {
                c--;
            }
            if (c == 0) {
                return i;
            }
            i--;
        }
        return -1;
    }

// Function to check balanced parentheses
    static bool isBalanced(char []X, int n) {
        // helper variables
        int i, j = 0, k, x, start, end;

        for (i = 0; i < n; i++) {
            // Handling case of opening parentheses
            if (X[i] == '(') {
                j = matchClosing(X, i, n - 1, '(', ')');
            } else if (X[i] == '{') {
                j = matchClosing(X, i, n - 1, '{', '}');
            } else if (X[i] == '[') {
                j = matchClosing(X, i, n - 1, '[', ']');
            } // Handling case of closing parentheses
            else {
                if (X[i] == ')') {
                    j = matchingOpening(X, 0, i, '(', ')');
                } else if (X[i] == '}') {
                    j = matchingOpening(X, 0, i, '{', '}');
                } else if (X[i] == ']') {
                    j = matchingOpening(X, 0, i, '[', ']');
                }

                // If corresponding matching
                // opening parentheses doesn't
                // lie in given interval return 0
                if (j < 0 || j >= i) {
                    return false;
                }

                // else continue
                continue;
            }

            // If corresponding closing parentheses
            // doesn't lie in given interval
            // return 0
            if (j >= n || j < 0) {
                return false;
            }

            // if found, now check for each
            // opening and closing parentheses
            // in this interval
            start = i;
            end = j;

            for (k = start + 1; k < end; k++) {
                if (X[k] == '(') {
                    x = matchClosing(X, k, end, '(', ')');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == ')') {
                    x = matchingOpening(X, start, k, '(', ')');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }

                if (X[k] == '{') {
                    x = matchClosing(X, k, end, '{', '}');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == '}') {
                    x = matchingOpening(X, start, k, '{', '}');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }
                if (X[k] == '[') {
                    x = matchClosing(X, k, end, '[', ']');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == ']') {
                    x = matchingOpening(X, start, k, '[', ']');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }
            }
        }

        return true;
    }

// Driver Code
    public static void Main() {

    char []X = "[()]()".ToCharArray();
    int n = 6;
    if (isBalanced(X, n))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");

    char []Y = "[[()]])".ToCharArray();
    n = 7;
    if (isBalanced(Y, n))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
    }
}
// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check balanced parentheses
// with O(1) space.

// Function1 to match closing bracket
function matchClosing($X, $start, $end,
                          $open, $close)
{
    $c = 1;
    $i = $start + 1;
    while ($i <= $end)
    {
        if ($X[$i] == $open)
        {
            $c++;
        }
        else if ($X[$i] == $close)
        {
            $c--;
        }
        if ($c == 0)
        {
            return $i;
        }
        $i++;
    }
    return $i;
}

// Function1 to match opening bracket
function matchingOpening($X, $start, $end,
                             $open, $close)
{
    $c = -1;
    $i = $end - 1;

    while ($i >= $start)
    {
        if ($X[$i] == $open)
        {
            $c++;
        }
        else if ($X[$i] == $close)
        {
            $c--;
        }
        if ($c == 0)
        {
            return $i;
        }
        $i--;
    }
    return -1;
}

// Function to check balanced parentheses
function isBalanced($X, $n)
{
    // helper variables
    $i; $j = 0; $k; $x; $start; $end;

    for ($i = 0; $i < $n; $i++)
    {
        // Handling case of opening parentheses
        if ($X[$i] == '(')
        {
            $j = matchClosing($X, $i, $n - 1, '(', ')');
        }
        else if ($X[$i] == '{')
        {
            $j = matchClosing($X, $i, $n - 1, '{', '}');
        }
        else if ($X[$i] == '[')
        {
            $j = matchClosing($X, $i, $n - 1, '[', ']');
        }

        // Handling case of closing parentheses
        else
        {
            if ($X[$i] == ')')
            {
                $j = matchingOpening($X, 0, $i, '(', ')');
            }
            else if ($X[$i] == '}')
            {
                $j = matchingOpening($X, 0, $i, '{', '}');
            }
            else if ($X[$i] == ']')
            {
                $j = matchingOpening($X, 0, $i, '[', ']');
            }

            // If corresponding matching opening parentheses
            // doesn't lie in given interval return 0
            if ($j < 0 || $j >= $i)
            {
                return false;
            }

            // else continue
            continue;
        }

        // If corresponding closing parentheses
        // doesn't lie in given interval
        // return 0
        if ($j >= $n || $j < 0)
        {
            return false;
        }

        // if found, now check for each opening
        // and closing parentheses in this interval
        $start = $i;
        $end = $j;

        for ($k = $start + 1; $k < $end; $k++)
        {
            if ($X[$k] == '(')
            {
                $x = matchClosing($X, $k, $end, '(', ')');
                if (!($k < $x && $x < $end))
                {
                    return false;
                }
            }
            else if ($X[$k] == ')')
            {
                $x = matchingOpening($X, $start, $k, '(', ')');
                if (!($start < $x && $x < $k))
                {
                    return false;
                }
            }

            if ($X[$k] == '{')
            {
                $x = matchClosing($X, $k, $end, '{', '}');
                if (!($k < $x && $x < $end))
                {
                    return false;
                }
            }
            else if ($X[$k] == '}')
            {
                $x = matchingOpening($X, $start, $k, '{', '}');
                if (!($start < $x && $x < $k))
                {
                    return false;
                }
            }
            if ($X[$k] == '[')
            {
                $x = matchClosing($X, $k, $end, '[', ']');
                if (!($k < $x && $x < $end))
                {
                    return false;
                }
            }
            else if ($X[$k] == ']')
            {
                $x = matchingOpening($X, $start, $k, '[', ']');
                if (!($start < $x && $x < $k))
                {
                    return false;
                }
            }
        }
    }

    return true;
}

// Driver Code
$X = str_split("[()]()");
$n = 6;
if (isBalanced($X, $n))
    echo("Yes\n");
else
    echo("No\n");

$Y = str_split("[[()]])");
$n = 7;
if (isBalanced($Y, $n))
    echo("Yes\n");
else
    echo("No\n");

// This code contributed by Mukul Singh
?>
```

## java 描述语言

```
<script>
// Javascript code to check balanced parentheses with
// O(1) space.

    // Function1 to match closing bracket
    function matchClosing(X,start,end,open,close)
    {
        let c = 1;
        let i = start + 1;
        while (i <= end) {
            if (X[i] == open) {
                c++;
            } else if (X[i] == close) {
                c--;
            }
            if (c == 0) {
                return i;
            }
            i++;
        }
        return i;
    }

    // Function1 to match opening bracket
    function matchingOpening(X,start,end,open,close)
    {
        let c = -1;
        let i = end - 1;

        while (i >= start) {
            if (X[i] == open) {
                c++;
            } else if (X[i] == close) {
                c--;
            }
            if (c == 0) {
                return i;
            }
            i--;
        }
        return -1;
    }

    // Function to check balanced parentheses
    function isBalanced(X,n)
    {
        // helper variables
        let i, j = 0, k, x, start, end;

        for (i = 0; i < n; i++) {
            // Handling case of opening parentheses
            if (X[i] == '(') {
                j = matchClosing(X, i, n - 1, '(', ')');
            } else if (X[i] == '{') {
                j = matchClosing(X, i, n - 1, '{', '}');
            } else if (X[i] == '[') {
                j = matchClosing(X, i, n - 1, '[', ']');
            } // Handling case of closing parentheses
            else {
                if (X[i] == ')') {
                    j = matchingOpening(X, 0, i, '(', ')');
                } else if (X[i] == '}') {
                    j = matchingOpening(X, 0, i, '{', '}');
                } else if (X[i] == ']') {
                    j = matchingOpening(X, 0, i, '[', ']');
                }

                // If corresponding matching
                // opening parentheses doesn't
                // lie in given interval return 0
                if (j < 0 || j >= i) {
                    return false;
                }

                // else continue
                continue;
            }

            // If corresponding closing parentheses
            // doesn't lie in given interval
            // return 0
            if (j >= n || j < 0) {
                return false;
            }

            // if found, now check for each
            // opening and closing parentheses
            // in this interval
            start = i;
            end = j;

            for (k = start + 1; k < end; k++) {
                if (X[k] == '(') {
                    x = matchClosing(X, k, end, '(', ')');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == ')') {
                    x = matchingOpening(X, start, k, '(', ')');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }

                if (X[k] == '{') {
                    x = matchClosing(X, k, end, '{', '}');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == '}') {
                    x = matchingOpening(X, start, k, '{', '}');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }
                if (X[k] == '[') {
                    x = matchClosing(X, k, end, '[', ']');
                    if (!(k < x && x < end)) {
                        return false;
                    }
                } else if (X[k] == ']') {
                    x = matchingOpening(X, start, k, '[', ']');
                    if (!(start < x && x < k)) {
                        return false;
                    }
                }
            }
        }

        return true;
    }

    // Driver Code
    let X="[()]()".split("");
    let n = 6;
    if (isBalanced(X, n))
        document.write("Yes<br>");
    else
        document.write("No<br>");

    let Y = "[[()]])".split("");
    n = 7;
    if (isBalanced(Y, n))
        document.write("Yes<br>");
    else
        document.write("No<br>");

   // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Yes
No
```

**时间复杂度:** O(n <sup>3</sup>

**辅助空间:** O(1)