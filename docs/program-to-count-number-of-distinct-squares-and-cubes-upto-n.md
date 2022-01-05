# 将不同正方形和立方体的数量计数到

的程序

> 原文:[https://www . geesforgeks . org/program-to-count-number-of-distinct-squares-and-cubes-up-n/](https://www.geeksforgeeks.org/program-to-count-number-of-distinct-squares-and-cubes-upto-n/)

给定一个数字 N，任务是找出从 1 到给定整数 N(包括两者)的完美正方形和完美立方体的数量。
**注:**既是正方体又是正方体的数字要算一次。
**示例:**

> 输入:N = 70
> 输出:10 个完美正方形或完美立方体
> 的数字 1，4，8，9，16，25，27，36，49，64
> 输入:N = 25
> 输出:6 个完美正方形或完美立方体
> 的数字 1，4，8，9，16，25

一种**天真的方法**是检查从 1 到 N 的所有数字，如果它是正方形或立方体。
以下是上述办法的实施:

## C++

```
// C++ implementation of above approach
#include <iostream>
#include <math.h> // For sqrt() and cbrt()
using namespace std;

// Function to check if the
// number is a perfect square
bool isSquare(int num)
{
    int root = sqrt(num);
    return (root * root) == num;
}

// Function to check if the
// number is a perfect cube
bool isCube(int num)
{
    int root = cbrt(num);
    return (root * root * root) == num;
}

// Function to count the number
// of perfect squares and cubes
int countSC(int N)
{
    int count = 0;
    for (int i = 1; i <= N; i++) {

        // If a number is perfect square,
        if (isSquare(i))
            count++;

        // Else if the number is cube or not
        else if (isCube(i))
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int N = 20;

    cout<< "Number of squares and cubes is " << countSC(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
class GFG
{

// Function to check if the
// number is a perfect square
static boolean isSquare(int num)
{
    int root = (int)Math.sqrt(num);
    return (root * root) == num;
}

// Function to check if the
// number is a perfect cube
static boolean isCube(int num)
{
    int root = (int)Math.cbrt(num);
    return (root * root *
            root) == num;
}

// Function to count the number
// of perfect squares and cubes
static int countSC(int N)
{
    int count = 0;
    for (int i = 1; i <= N; i++)
    {

        // If a number is perfect
        // square,
        if (isSquare(i))
            count++;

        // Else if the number is
        // cube or not
        else if (isCube(i))
            count++;
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 20;

    System.out.println("Number of squares " +
                            "and cubes is " +
                                 countSC(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# Function to check if the
# number is a perfect square
def isSquare(num) :
    root = int(num ** (1 / 2))

    return (root * root) == num

# Function to check if the
# number is a perfect cube
def isCube(num) :
    root = int(num ** (1 / 3))
    return (root * root * root ) == num

# Function to count the number
# of perfect squares and cubes
def countSC(N) :
    count = 0
    for i in range(1, N + 1) :

        # If a number is perfect square,
        if isSquare(i) :
            count += 1

        # Else if the number is cube
        elif isCube(i) :
            count += 1

    return count

# Driver code
if __name__ == "__main__" :

    N = 20

    print("Number of squares and cubes is ",
                                 countSC(N))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{

// Function to check if the
// number is a perfect square
static bool isSquare(int num)
{
    int root = (int)Math.Sqrt(num);
    return (root * root) == num;
}

// Function to check if the
// number is a perfect cube
static bool isCube(int num)
{
    int root = (int)Math.Pow(num,
                    (1.0 / 3.0));
    return (root * root * root) == num;
}

// Function to count the number
// of perfect squares and cubes
static int countSC(int N)
{
    int count = 0;
    for (int i = 1; i <= N; i++)
    {

        // If a number is perfect
        // square,
        if (isSquare(i))
            count++;

        // Else if the number is
        // cube or not
        else if (isCube(i))
            count++;
    }

    return count;
}

// Driver code
public static void Main()
{
    int N = 20;

    Console.Write("Number of squares and " +
                  "cubes is " + countSC(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check if the
// number is a perfect square
function isSquare($num)
{
    $root = (int)sqrt($num);
    return ($root * $root) == $num;
}

// Function to check if the
// number is a perfect cube
function isCube($num)
{
    $root = (int)pow($num, 1 / 3);
    return ($root * $root *
            $root) == $num;
}

// Function to count the number
// of perfect squares and cubes
function countSC($N)
{
    $count = 0;
    for ($i = 1; $i <= $N; $i++)
    {

        // If a number is
        // perfect square,
        if (isSquare($i))
            $count++;

        // Else if the number
        // is cube or not
        else if (isCube($i))
            $count++;
    }

    return $count;
}

// Driver code
$N = 20;

echo "Number of squares and " .
     "cubes is " . countSC($N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to check if the
    // number is a perfect square
    function isSquare(num)
    {
        let root = parseInt(Math.sqrt(num), 10);
        return (root * root) == num;
    }

    // Function to check if the
    // number is a perfect cube
    function isCube(num)
    {
        let root = parseInt(Math.cbrt(num), 10);
        return (root * root * root) == num;
    }

    // Function to count the number
    // of perfect squares and cubes
    function countSC(N)
    {
        let count = 0;
        for (let i = 1; i <= N; i++) {

            // If a number is perfect square,
            if (isSquare(i))
                count++;

            // Else if the number is cube or not
            else if (isCube(i))
                count++;
        }

        return count;
    }

    let N = 20;

    document.write("Number of squares and cubes is " + countSC(N));

</script>
```

**Output:** 

```
Number of squares and cubes is 5
```

**高效方法:**

1.  从 1 到 N 的方块数为**层(sqrt(N))** 。
2.  立方体数量从 1 到 N 为**层(cbrt(N))** 。
3.  去掉既有正方形又有立方体的数字(比如 1，64…)通过从中减去**楼层(sqrt(cbrt(N)))** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <iostream>
#include <math.h> // For sqrt() and cbrt()
using namespace std;

// Function to count the number
// of perfect squares and cubes
int countSC(int N)
{
    int res = (int)sqrt(N) + (int)cbrt(N)
              - (int)(sqrt(cbrt(N)));

    return res;
}

// Driver code
int main()
{
    int N = 20;

    cout << "Number of squares and cubes is " << countSC(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
class GFG
{

// Function to count the number
// of perfect squares and cubes
static int countSC(int N)
{
    int res = (int)Math.sqrt(N) +
              (int)Math.cbrt(N) -
              (int)(Math.sqrt(Math.cbrt(N)));

    return res;
}

// Driver code
public static void main(String[] args)
{
    int N = 20;

    System.out.println("Number of squares " +
                            "and cubes is " +
                                 countSC(N));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python implementation of
# above approach
import math # for sqrt()

# Function to count the number
# of perfect squares and cubes
def countSC(N):
    res = (int(math.sqrt(N)) +
           int(N ** (1 / 3)) -
           int(math.sqrt(N ** (1 / 3))))

    return res

# Driver code
N = 20
print("Number of squares and cubes is",
                            countSC(N))

# This code is contributed
# by vaibhav29498
```

## C#

```
//C# implementation of
// above approach
using System;
public class GFG {

    // Function to count the number
    // of perfect squares and cubes
    static int countSC(int N)
    {
        int res = (int)(Math.Sqrt(N) +
            Math.Ceiling(Math.Pow(N, (double)1 / 3)) -
            (Math.Sqrt(Math.Ceiling(Math.Pow(N, (double)1 / 3)))));

        return res;
    }

    // Driver code
    public static void Main()
    {
        int N = 20;

        Console.Write("Number of squares " + "and cubes is " +
                countSC(N));
    }
}

/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to count the number
// of perfect squares and cubes
function countSC($N)
{
    $res = sqrt($N) + pow($N, 1 / 3) -
                (sqrt(pow($N, 1 / 3)));

    return floor($res);
}

// Driver code
$N = 20;

echo "Number of squares and cubes is " ,
                            countSC($N);

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to count the number
    // of perfect squares and cubes
    function countSC(N)
    {
        let res = parseInt(Math.sqrt(N), 10) + parseInt(Math.cbrt(N), 10) - parseInt(Math.sqrt(parseInt(Math.cbrt(N), 10)), 10);

        return res;
    }

    let N = 20;

    document.write("Number of squares and cubes is " + countSC(N));

</script>
```

**Output:** 

```
Number of squares and cubes is 5
```