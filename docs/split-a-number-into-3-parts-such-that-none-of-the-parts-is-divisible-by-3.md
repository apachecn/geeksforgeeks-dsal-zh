# 将一个数分成 3 个部分，这样没有一个部分能被 3 整除

> 原文:[https://www . geeksforgeeks . org/将一个数字拆分为 3 个部分，这样所有部分都不能被 3 整除/](https://www.geeksforgeeks.org/split-a-number-into-3-parts-such-that-none-of-the-parts-is-divisible-by-3/)

给你一个数字“N”。你的任务是把这个数分成 3 个正整数 x，y 和 z，这样它们的和等于‘N’，这 3 个整数都不是 3 的倍数。假设 N>=2。

**示例:**

> **输入:**N = 10
> T3】输出: x = 1，y = 2，z = 7
> 注意 x + y + z = N 和 x，y & z 不能被 N 整除
> T7】输入:18
> T10】输出: x = 1，y = 1，z = 16

**方法:**
要把 N 分成 3 个数字，我们把 N 分成

1.  如果 N 能被 3 整除，那么数字 x，y，z 分别可以是 1，1 和 N-2。所有的 x，y 和 z 都不能被 3 整除。和(1)+(1)+(N-2)=N。
2.  如果 N 不能被 3 整除，那么 N-3 也不能被 3 整除。因此，我们可以有 x=1，y=2，z=N-3。还有，(1)+(2)+(N-3)=N。

## C++

```
// CPP program to split a number into three parts such
// than none of them is divisible by 3.
#include <iostream>
using namespace std;

void printThreeParts(int N)
{
    // Print x = 1, y = 1 and z = N - 2
    if (N % 3 == 0)
        cout << " x = 1, y = 1, z = " << N - 2 << endl;

    // Otherwise, print x = 1, y = 2 and z = N - 3
    else
        cout << " x = 1, y = 2, z = " << N - 3 << endl;
}

// Driver code
int main()
{
    int N = 10;
    printThreeParts(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split a number into three parts such
// than none of them is divisible by 3.
import java.util.*;

class solution
{

static void printThreeParts(int N)
{
    // Print x = 1, y = 1 and z = N - 2
    if (N % 3 == 0)

        System.out.println("x = 1, y = 1, z = "+ (N-2));

    // Otherwise, print x = 1, y = 2 and z = N - 3
    else
        System.out.println(" x = 1, y = 2, z = "+ (N-3));
}

// Driver code
public static void main(String args[])
{
    int N = 10;
    printThreeParts(N);

}
}
```

## 蟒蛇 3

```
# Python3 program to split a number into three parts such
# than none of them is divisible by 3.

def printThreeParts(N) :

    # Print x = 1, y = 1 and z = N - 2
    if (N % 3 == 0) :
        print(" x = 1, y = 1, z = ",N - 2)

    # Otherwise, print x = 1, y = 2 and z = N - 3
    else :
        print(" x = 1, y = 2, z = ",N - 3)

# Driver code
if __name__ == "__main__" :

    N = 10
    printThreeParts(N)

# This code is contributed by Ryuga
```

## C#

```
// C# program to split a number into three parts such
// than none of them is divisible by 3.
using System;

public class GFG{
    static void printThreeParts(int N)
{
    // Print x = 1, y = 1 and z = N - 2
    if (N % 3 == 0)
        Console.WriteLine(" x = 1, y = 1, z = "+(N - 2));

    // Otherwise, print x = 1, y = 2 and z = N - 3
    else
        Console.WriteLine(" x = 1, y = 2, z = "+(N - 3));
}

// Driver code
    static public void Main (){
    int N = 10;
    printThreeParts(N);

    }
// This code is contributed by ajit.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to split a number into
// three parts such than none of them
// is divisible by 3.
function printThreeParts($N)
{
    // Print x = 1, y = 1 and z = N - 2
    if ($N % 3 == 0)
        echo " x = 1, y = 1, z = " .
                    ($N - 2) . "\n";

    // Otherwise, print x = 1,
    // y = 2 and z = N - 3
    else
        echo " x = 1, y = 2, z = " .
                    ($N - 3) . "\n";
}

// Driver code
$N = 10;
printThreeParts($N);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// javascript program to split a number into three parts such
// than none of them is divisible by 3.

function printThreeParts(N)
{
    // Print x = 1, y = 1 and z = N - 2
    if (N % 3 == 0)

        document.write("x = 1, y = 1, z = "+ (N-2));

    // Otherwise, print x = 1, y = 2 and z = N - 3
    else
        document.write(" x = 1, y = 2, z = "+ (N-3));
}

// Driver code

var N = 10;
printThreeParts(N);

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
x = 1, y = 2, z = 7
```

**时间复杂度:** **O(1)**

**辅助空间:O(1)**