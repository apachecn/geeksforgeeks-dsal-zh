# 将二进制数组修改为所有元素的按位“与”为 1

> 原文:[https://www . geeksforgeeks . org/modify-a-二进制数组到所有元素的按位和-as-1/](https://www.geeksforgeeks.org/modify-a-binary-array-to-bitwise-and-of-all-elements-as-1/)

给定一个数组，一个[]只由 0 和 1 组成。任务是检查是否可以转换数组，使每对索引之间的“与”值为 1。唯一允许的操作是:

*   取两个索引 I 和 j，将 a[i]和 a[j]替换为 a[i] | a[j]，其中“|”表示按位“或”运算。

如果可能，则输出为“是”，否则输出为“否”。

**示例:**

```
Input:  arr[] = {0, 1, 0, 0, 1}
Output: Yes
Choose these pair of indices (0, 1), (1, 2), (3, 4).

Input: arr[] = {0, 0, 0}
Output: No 
```

**逼近:**主要观察是，如果数组至少由一个 1 组成，那么答案是 YES，否则输出为 NO，因为带 1 的 OR 会给我们 1，因为数组只由 0 和 1 组成。
如果至少有一个 1，那么我们将选择所有具有 0 值的指数，并用具有 1 的或值替换它们，并且或值将总是 1。
在所有操作之后，数组将仅由 1 组成，并且任意一对索引之间的“与”值将为 1，即(1 AND 1)=1。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible or not
bool check(int a[], int n)
{
    for (int i = 0; i < n; i++)
        if (a[i])
            return true;

    return false;
}

// Driver code
int main()
{

    int a[] = { 0, 1, 0, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    check(a, n) ? cout << "YES\n"
                : cout << "NO\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to check if it is possible or not
    static boolean check(int a[], int n)
    {
        for (int i = 0; i < n; i++)
            if (a[i] == 1)
                return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 0, 1, 0, 1 };
        int n = a.length;

        if(check(a, n) == true )
            System.out.println("YES\n") ;
        else
            System.out.println("NO\n");
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function to check if it is
# possible or not
def check(a, n):
    for i in range(n):
        if (a[i]):
            return True

    return False

# Driver code
if __name__ == '__main__':
    a = [0, 1, 0, 1]
    n = len(a)

    if(check(a, n)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to check if it is possible or not
    static bool check(int []a, int n)
    {
        for (int i = 0; i < n; i++)
            if (a[i] == 1)
                return true;

        return false;
    }

    // Driver code
    public static void Main ()
    {
        int []a = { 0, 1, 0, 1 };
        int n = a.Length;

        if(check(a, n) == true )
            Console.Write("YES\n") ;
        else
            Console.Write("NO\n");
    }
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to check if it is
// possible or not
function check($a, $n)
{
    for ($i = 0; $i < $n; $i++)
        if ($a[$i])
            return true;

    return false;
}

// Driver code
$a = array(0, 1, 0, 1);
$n = sizeof($a);

if(check($a, $n))
    echo "YES\n";
else
    echo "NO\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check if it is possible or not
function check(a, n)
{
    for (var i = 0; i < n; i++)
        if (a[i])
            return true;

    return false;
}

// Driver code
var a = [0, 1, 0, 1 ];
var n = a.length;
check(a, n) ? document.write( "YES")
            : document.write( "NO\n");

</script>
```

**Output:** 

```
YES
```