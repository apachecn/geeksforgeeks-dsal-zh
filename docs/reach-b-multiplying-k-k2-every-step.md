# 在每一步将 a 和 b 乘以 k 和 k^2

> 原文:[https://www . geesforgeks . org/reach-b-乘法-k-k2-每一步/](https://www.geeksforgeeks.org/reach-b-multiplying-k-k2-every-step/)

给我们两个数字 A 和 B，我们需要写一个程序，按照给定的步骤，从(1，1)开始判断 A 和 B 是否可以到达。从(1，1)开始，每一步选择一个随机数 K，将 K 乘以上一步得到的两个数中的任意一个，并将 K <sup>2</sup> 乘以另一个数。
**例:**

```
Input : A = 3,   B = 9 
Output : yes
Explanation: Starting from A = 1 and B = 1\. 
We choose k=3 and multiply 3 with the first number
to get A=3 and multiply k2=9 to the second- 
number to get B=9\. 

Input : A = 60,   B = 450 
Output : yes
Explanation : Starting from A = 1 and B = 1,
Step 1: multiply k=3 and k2 to get 3 and 9 
Step 2: Multiply k=5 and k2 = 25 to get to 15 and 225 
Step 3: Multiply k2=4 and k=2 to get to A=60 and B=450 
```

解决这个问题的想法是仔细观察，在每一步，我们都将 k 和 k <sup>2</sup> 相乘。因此，如果 a 和 b 可以达到，它将在每一步都有 **k^3 作为 A*B** 的因素。简单来说，如果数字 **A*B 是一个完美的立方体，并且它将 A 和 B 都除以**，那么只有执行给定的步骤，才能从 1 和 1 开始得出这个数字。
以下是上述思路的实现:

## C++

```
// CPP program to determine if
// A and B can be reached starting
// from 1, 1 following the given steps.
#include <bits/stdc++.h>
using namespace std;

// function to check is it is possible to reach
// A and B starting from 1 and 1
bool possibleToReach(int a, int b)
{
    // find the cuberoot of the number
    int c = cbrt(a * b);

    // divide the number by cuberoot
    int re1 = a / c;
    int re2 = b / c;

    // if it is a perfect cuberoot and divides a and b
    if ((re1 * re1 * re2 == a) && (re2 * re2 * re1 == b))
        return true;
    else
        return false;
}

int main()
{
    int A = 60, B = 450;

    if (possibleToReach(A, B))
        cout << "yes";
    else
        cout << "no";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine if
// A and B can be reached starting
// from 1, 1 following the given
// steps.
class GFG {

    // function to check is it is
    // possible to reach A and B
    // starting from 1 and 1
    static boolean possibleToReach(int a, int b)
    {

        // find the cuberoot of the number
        int c = (int)Math.cbrt(a * b);

        // divide the number by cuberoot
        int re1 = a / c;
        int re2 = b / c;

        // if it is a perfect cuberoot and
        // divides a and b
        if ((re1 * re1 * re2 == a) &&
                         (re2 * re2 * re1 == b))
            return true;
        else
            return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int A = 60, B = 450;

        if (possibleToReach(A, B))
            System.out.println("yes");
        else
            System.out.println("no");
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to determine if
# A and B can be reached starting
# from 1, 1 following the given steps.
import numpy as np

# function to check is it is possible to
# reach A and B starting from 1 and 1
def possibleToReach(a, b):

    # find the cuberoot of the number
    c = np.cbrt(a * b)

    # divide the number by cuberoot
    re1 = a // c
    re2 = b // c

    # if it is a perfect cuberoot and
    # divides a and b
    if ((re1 * re1 * re2 == a) and
        (re2 * re2 * re1 == b)):
        return True
    else:
        return False

# Driver Code
if __name__ == "__main__":

    A = 60
    B = 450

    if (possibleToReach(A, B)):
        print("yes")
    else:
        print("no")

# This code is contributed by ita_c
```

## C#

```
// C# program to determine if
// A and B can be reached starting
// from 1, 1 following the given
// steps.
using System;

public class GFG{

    // function to check is it is
    // possible to reach A and B
    // starting from 1 and 1
    public static bool possibleToReach(int a, int b)
    {

        // find the cuberoot of the number
        int c = (int)Math.Pow(a * b, (double) 1 / 3);
        // divide the number by cuberoot
        int re1 = a / c;
        int re2 = b / c;

        // if it is a perfect cuberoot 
        // and divides a and b
        if ((re1 * re1 * re2 == a) &&
              (re2 * re2 * re1 == b))
            return true;
        else
            return false;
    }

// Driver Code
    static public void Main (String []args)
    {

        int A = 60, B = 450;

        if (possibleToReach(A, B))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to determine if
// A and B can be reached starting
// from 1, 1 following the given steps.

// function to check is it is
// possible to reach A and B
// starting from 1 and 1
function possibleToReach($a, $b)
{

    // find the cuberoot
    // of the number
    $c =($a * $b);

    // divide the number
    // by cuberoot
    $re1 = $a / $c;
    $re2 = $b / $c;

    // if it is a perfect cuberoot
    // and divides a and b
    if (($re1 * $re1 * $re2 == $a) &&
        ($re2 * $re2 * $re1 == $b))
        return 1;
    else
        return -1;
}

    // Driver Code
    $A = 60;
    $B = 450;
    if (possibleToReach($A, $B))
        echo "yes";
    else
        echo "no";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to determine if
// A and B can be reached starting
// from 1, 1 following the given steps.

    // function to check is it is
    // possible to reach A and B
    // starting from 1 and 1
    function possibleToReach(a, b)
    {

        // find the cuberoot of the number
        let c = Math.cbrt(a * b);

        // divide the number by cuberoot
        let re1 = a / c;
        let re2 = b / c;

        // if it is a perfect cuberoot and
        // divides a and b
        if ((re1 * re1 * re2 == a) &&
                         (re2 * re2 * re1 == b))
            return true;
        else
            return false;
    }

// Driver code

        let A = 60, B = 450;

        if (possibleToReach(A, B))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by splevel62.
</script>
```

输出:

```
Yes
```