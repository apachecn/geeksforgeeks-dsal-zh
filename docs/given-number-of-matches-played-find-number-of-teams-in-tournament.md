# 给定比赛场次，找出锦标赛中的队伍数量

> 原文:[https://www . geeksforgeeks . org/给定比赛场次-比赛场次-查找比赛队数/](https://www.geeksforgeeks.org/given-number-of-matches-played-find-number-of-teams-in-tournament/)

给定一个整数 **M** ，这是一场锦标赛中的比赛次数，每个参赛队都与所有其他队进行了一场比赛。任务是找出锦标赛中有多少支队伍。
**例:**

> **输入:** M = 3
> **输出:** 3
> 如果有 A、B、C 三支队伍，那么
> A 将与 B、C 进行一场比赛
> B 将与 C 进行一场比赛(B 已经与 A 进行了一场比赛)
> C 已经与 A、B 队进行了比赛
> 总共进行了 3 场比赛
> **输入:** M = 45
> **输出:** 10 【T16

**进场:**由于每场比赛都是两队之间进行。所以这个问题类似于从给定的 N 个对象中选择 2 个对象。因此比赛总数将为 C(N，2)，其中 N 为参赛队伍数。因此，

> M = C(N，2)
> M =(N *(N–1))/2
> N<sup>2</sup>–N–2 * M = 0
> 这是一个 ax 型二次方程 <sup>2</sup> + bx + c = 0。这里 a = 1，b = -1，c = 2 * M .因此，应用公式
> x =(-b+ sqrt(b<sup>2</sup>–4ac))/2a 和 x =(-b–sqrt(b<sup>2</sup>–4ac))/2a
> N =[(-1 *-1)+sqrt((-1 *-1)–(4 * 1 *(2 * M)))]/2
> N =(1+sqrt(M)

解完上面两个方程，我们会得到 n 的两个值，一个值为正，一个为负。忽略负值。因此，团队数量将是上述等式的正根。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <cmath>
#include <iostream>
using namespace std;

// Function to return the number of teams
int number_of_teams(int M)
{
    // To store both roots of the equation
    int N1, N2, sqr;

    // sqrt(b^2 - 4ac)
    sqr = sqrt(1 + (8 * M));

    // First root (-b + sqrt(b^2 - 4ac)) / 2a
    N1 = (1 + sqr) / 2;

    // Second root (-b - sqrt(b^2 - 4ac)) / 2a
    N2 = (1 - sqr) / 2;

    // Return the positive root
    if (N1 > 0)
        return N1;
    return N2;
}

// Driver code
int main()
{
    int M = 45;
    cout << number_of_teams(M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the number of teams
static int number_of_teams(int M)
{
    // To store both roots of the equation
    int N1, N2, sqr;

    // sqrt(b^2 - 4ac)
    sqr = (int)Math.sqrt(1 + (8 * M));

    // First root (-b + sqrt(b^2 - 4ac)) / 2a
    N1 = (1 + sqr) / 2;

    // Second root (-b - sqrt(b^2 - 4ac)) / 2a
    N2 = (1 - sqr) / 2;

    // Return the positive root
    if (N1 > 0)
        return N1;
    return N2;
}

    // Driver code
    public static void main (String[] args)
    {
        int M = 45;
        System.out.println( number_of_teams(M));
    }
}

// this code is contributed by vt_m..
```

## 蟒蛇 3

```
# Python implementation of the approach
import math

# Function to return the number of teams
def number_of_teams(M):

    # To store both roots of the equation
    N1, N2, sqr = 0,0,0

    # sqrt(b^2 - 4ac)
    sqr = math.sqrt(1 + (8 * M))

    # First root (-b + sqrt(b^2 - 4ac)) / 2a
    N1 = (1 + sqr) / 2

    # Second root (-b - sqrt(b^2 - 4ac)) / 2a
    N2 = (1 - sqr) / 2

    # Return the positive root
    if (N1 > 0):
        return int(N1)
    return int(N2)

# Driver code
def main():
    M = 45
    print(number_of_teams(M))
if __name__ == '__main__':
    main()

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number of teams
    static int number_of_teams(int M)
    {
        // To store both roots of the equation
        int N1, N2, sqr;

        // sqrt(b^2 - 4ac)
        sqr = (int)Math.Sqrt(1 + (8 * M));

        // First root (-b + sqrt(b^2 - 4ac)) / 2a
        N1 = (1 + sqr) / 2;

        // Second root (-b - sqrt(b^2 - 4ac)) / 2a
        N2 = (1 - sqr) / 2;

        // Return the positive root
        if (N1 > 0)
            return N1;
        return N2;
    }

    // Driver code
    public static void Main()
    {
        int M = 45;
        Console.WriteLine( number_of_teams(M));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of teams
function number_of_teams($M)
{
    // To store both roots of the equation

    // sqrt(b^2 - 4ac)
    $sqr = sqrt(1 + (8 * $M));

    // First root (-b + sqrt(b^2 - 4ac)) / 2a
    $N1 = (1 + $sqr) / 2;

    // Second root (-b - sqrt(b^2 - 4ac)) / 2a
    $N2 = (1 - $sqr) / 2;

    // Return the positive root
    if ($N1 > 0)
        return $N1;
    return $N2;
}

// Driver code
$M = 45;
echo number_of_teams($M);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the number of teams
    function number_of_teams(M) {
        // To store both roots of the equation
        var N1, N2, sqr;

        // sqrt(b^2 - 4ac)
        sqr = parseInt( Math.sqrt(1 + (8 * M)));

        // First root (-b + sqrt(b^2 - 4ac)) / 2a
        N1 = (1 + sqr) / 2;

        // Second root (-b - sqrt(b^2 - 4ac)) / 2a
        N2 = (1 - sqr) / 2;

        // Return the positive root
        if (N1 > 0)
            return N1;
        return N2;
    }

    // Driver code

        var M = 45;
        document.write(number_of_teams(M));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
10
```