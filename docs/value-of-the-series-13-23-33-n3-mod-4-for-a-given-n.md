# 给定 n

的系列值(1^3 + 2^3 + 3^3 + … + n^3) mod 4

> 原文:[https://www . geesforgeks . org/系列价值-13-23-33-n3-mod-4-for-a-给定-n/](https://www.geeksforgeeks.org/value-of-the-series-13-23-33-n3-mod-4-for-a-given-n/)

给定一个函数 f(n)=(1<sup>3</sup>+2<sup>3</sup>+3<sup>3</sup>+…+n<sup>3</sup>，任务是为给定的正整数“n”找到 f(n) mod 4 的值。
**示例**

```
Input: n=6
Output: 1
Explanation: f(6) = 1+8+27+64+125+216=441
f(n) mod 4=441 mod 4 = 1

Input: n=4
Output: 0
Explanation: f(4)=1+8+27+64 = 100
f(n) mod 4 =100 mod 4 = 0
```

解决这个问题的时候，你可以直接计算(1<sup>3</sup>+2<sup>3</sup>+3<sup>3</sup>+…+n<sup>3</sup>)mod 4。但这需要 O(n)个时间。我们可以对立方之和使用直接公式，但是对于大的 n，我们可能会使 f(n)超出 long long int 的范围。
这里有一个高效的 O(1)解:
从除法算法中我们知道，每个整数都可以表示为 4k、4k+1、4k+2 或 4k+3。
现在，

> (4k)<sup>3</sup>= 64k<sup>3</sup>mod 4 = 0。
> (4k+1)<sup>3</sup>=(64k<sup>【3】</sup>+48k<sup>【2】</sup>+12k+1)mod 4 = 1
> (4k+2)=(64k)】

现在让 x 是最大的整数，不大于被 4 整除的 n。所以我们很容易看到，
(1<sup>3</sup>+2<sup>3</sup>+3<sup>3</sup>…..+x <sup>3</sup> ) mod 4=0。
现在，

*   如果 n 是 4 的除数，那么 x=n，f(n) mod 4 =0。
*   否则，如果 n 是 4k + 1 的形式，那么 x= n-1。所以，f(n)= 1<sup>3</sup>+2<sup>3</sup>+3<sup>3</sup>…..+x<sup>3</sup>+n<sup>3</sup>)mod 4 = n^3 mod 4 = 1
*   类似地，如果 n 是 4k+2 的形式(即 x=n-2)，我们可以很容易地证明 f(n)=((n-1)<sup>3</sup>+n<sup>3</sup>)mod 4 =(1+0)mod 4 = 1
*   如果 n 是 4k+3 的形式(x=n-3)。同样，我们得到 f(n)mod 4 =((n-2)<sup>3</sup>+(n-1)<sup>3</sup>+n<sup>3</sup>)mod 4 =(1+0+3)mod 4 = 0

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// function for obtaining the value of f(n) mod 4
int fnMod(int n)
{
    // Find the remainder of n when divided by 4
    int rem = n % 4;

    // If n is of the form 4k or 4k+3
    if (rem == 0 || rem == 3)
        return 0;

    // If n is of the form 4k+1 or 4k+2
    else if (rem == 1 || rem == 2)
        return 1;
}

// Driver code
int main()
{
    int n = 6;
    cout << fnMod(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java .io.*;

class GFG {

// function for obtaining the value of f(n) mod 4
static int fnMod(int n)
{
    // Find the remainder of n when divided by 4
    int rem = n % 4;

    // If n is of the form 4k or 4k+3
    if (rem == 0 || rem == 3)
        return 0;

    // If n is of the form 4k+1 or 4k+2
    else if (rem == 1 || rem == 2)
        return 1;
        return 0;
}

// Driver code

    public static void main (String[] args) {
            int n = 6;
    System.out.print( fnMod(n));
    }
}
//This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# function for obtaining the
# value of f(n) mod 4
def fnMod(n) :

    # Find the remainder of n
    # when divided by 4
    rem = n % 4

    # If n is of the form 4k or 4k+3
    if (rem == 0 or rem == 3) :
        return 0

    # If n is of the form
    # 4k+1 or 4k+2
    elif (rem == 1 or rem == 2) :
        return 1

# Driver code    
if __name__ == "__main__" :

    n = 6
    print(fnMod(n))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# implementation of the approach

using System;
class GFG {

// function for obtaining the value of f(n) mod 4
static int fnMod(int n)
{
    // Find the remainder of n when divided by 4
    int rem = n % 4;

    // If n is of the form 4k or 4k+3
    if (rem == 0 || rem == 3)
        return 0;

    // If n is of the form 4k+1 or 4k+2
    else if (rem == 1 || rem == 2)
        return 1;
        return 0;
}

// Driver code

    public static void Main () {
            int n = 6;
    Console.Write( fnMod(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// function for obtaining the
// value of f(n) mod 4
function fnMod($n)
{
    // Find the remainder of n
    // when divided by 4
    $rem = $n % 4;

    // If n is of the form 4k or 4k+3
    if ($rem == 0 or $rem == 3)
        return 0;

    // If n is of the form 4k+1 or 4k+2
    else if ($rem == 1 or $rem == 2)
        return 1;
}

// Driver code
$n = 6;
echo fnMod($n);

// This code is contributed
// by anuj_67..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function for obtaining the value
// of f(n) mod 4
function fnMod(n)
{

    // Find the remainder of n
    // when divided by 4
    var rem = n % 4;

    // If n is of the form 4k or 4k+3
    if (rem == 0 || rem == 3)
        return 0;

    // If n is of the form 4k+1 or 4k+2
    else if (rem == 1 || rem == 2)
        return 1;

    return 0;
}

// Driver Code
var n = 6;

document.write(fnMod(n));

// This code is contributed by Kirti

</script>
```

**Output:** 

```
1
```