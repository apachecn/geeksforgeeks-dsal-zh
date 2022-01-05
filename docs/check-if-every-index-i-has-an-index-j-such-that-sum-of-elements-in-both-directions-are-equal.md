# 检查每个索引 I 是否有一个索引 j，使得两个方向上的元素之和相等

> 原文:[https://www . geeksforgeeks . org/check-if-even-index-I-has-index-j-这样双向元素之和等于/](https://www.geeksforgeeks.org/check-if-every-index-i-has-an-index-j-such-that-sum-of-elements-in-both-directions-are-equal/)

给定大小为 N 的圆形数组，任务是检查对于从 0 到 N-1 开始的每个索引 I，是否存在不等于 I 的索引 j，使得从 I 到 j 的顺时针方向上的所有数字之和等于从 I 到 j 的逆时针方向上的所有数字之和。
**示例:**

> **输入:** a[] = {1，4，1，4}
> **输出:**是
> 圆阵为 1- > 4- > 1- > 4。
> 对于索引 0，j 为 2，那么从索引 0 到 2 顺时针方向的元素之和为 1 + 4 + 1 = 6，从索引 0 到 2 逆时针方向的元素之和为 1 + 4 + 1 = 6。
> 对于索引 1，j 为 3，那么从索引 1 到 3 顺时针方向的元素之和为 4 + 1 + 4 = 9，从索引 1 到 3 逆时针方向的元素之和为 4 + 1 + 4 = 9。
> 对于索引 2，j 将为 0，那么从索引 2 到 0 的顺时针方向的元素之和将为 1 + 4 + 1 = 6，从索引 2 到 0 的逆时针方向的元素之和将为 1 + 4 + 1 = 6
> 对于索引 3，j 将为 1， 那么顺时针方向从索引 3 到 1 的元素之和为 4 + 1 + 4 = 9，逆时针方向从索引 3 到 1 的元素之和为 4 + 1 + 4 = 9
> **输入:** a[] = {1，1，1，1，1，1}
> **输出:**是

**进场:**

*   当 N 是奇数时，答案总是“否”，因为不可能为每个指数 I 找到一个指数 j。
*   如果 N 是偶数，那么检查对于每个索引 I，相反的元素是否完全相同，那么答案是“是”。
*   如果指数的任一相反元素，即 **a[(i+(n/2))]不等于 a[i]** ，则答案为“否”。

以下是上述方法的实现:

## C++

```
// C++ program to check if the
// number lies in given range
#include <bits/stdc++.h>
using namespace std;

// Function that returns the maximum element.
bool check(int a[], int n)
{

    // check for odd
    if (n % 2 == 1)
        return false;

    // check if the opposite element is same
    // as a[i]
    for (int i = 0; i < n / 2; i++) {
        if (a[i] != a[i + (n / 2)])
            return false;
    }

    return true;
}

// Driver code
int main()
{
    int a[] = { 1, 4, 1, 4 };

    int n = sizeof(a) / sizeof(a[0]);

    if (check(a, n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to check if the
//number lies in given range

public class GFG {

    //Function that returns the maximum element.
    static boolean check(int a[], int n)
    {

     // check for odd
     if (n % 2 == 1)
         return false;

     // check if the opposite element is same
     // as a[i]
     for (int i = 0; i < n / 2; i++) {
         if (a[i] != a[i + (n / 2)])
             return false;
     }

     return true;
    }

    //Driver code
    public static void main(String[] args) {

        int a[] = { 1, 4, 1, 4 };

         int n = a.length;

         if (check(a, n))
             System.out.println("YES");
         else
             System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python 3 Program  to check if the
# number lies in given range

# Function that returns the maximum element.
def check(a, n) :

    # check for odd
    if n % 2 == 1:
        return False

    # check if the opposite element is same
    # as a[i]
    for i in range(n//2) :
        if a[i] != a[i + (n//2)]:
            return False

    return True

# Driver Code
if __name__ == "__main__" :
    a = [ 1, 4, 1, 4]

    n = len(a)

    if check(a, n) :
        print("YES")
    else :
        print("NO")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to check if the
// number lies in given range

class GFG
{

// Function that returns the
// maximum element.
static bool check(int[] a, int n)
{

// check for odd
if (n % 2 == 1)
    return false;

// check if the opposite
// element is same as a[i]
for (int i = 0; i < (int)n / 2; i++)
{
    if (a[i] != a[i + (int)(n / 2)])
        return false;
}

return true;
}

// Driver code
public static void Main()
{
    int[] a = new int[]{ 1, 4, 1, 4 };

    int n = a.Length;

    if (check(a, n))
        System.Console.WriteLine("YES");
    else
        System.Console.WriteLine("NO");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if the
// number lies in given range

// Function that returns the
// maximum element.
function check($a, $n)
{

    // check for odd
    if ($n % 2 == 1)
        return false;

    // check if the opposite
    // element is same as a[i]
    for ($i = 0; $i < $n / 2; $i++)
    {
        if ($a[$i] != $a[$i + ($n / 2)])
            return false;
    }

    return true;
}

// Driver code
$a = array( 1, 4, 1, 4 );

$n = sizeof($a);

if (check($a, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// Javascript program to check if the
// number lies in given range

// Function that returns the maximum element.
function check( a, n)
{

    // check for odd
    if (n % 2 == 1)
        return false;

    // check if the opposite element is same
    // as a[i]
    for (var i = 0; i < parseInt(n / 2); i++) {
        if (a[i] != a[i + parseInt(n / 2)])
            return false;
    }

    return true;
}

// Driver code
var a = [ 1, 4, 1, 4 ];
var n = a.length;
if (check(a, n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
YES
```