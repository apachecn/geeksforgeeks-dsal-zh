# 计算三胞胎(a，b，c)的数量，使得 a^2 + b^2 = c^2 和 1 < = a < = b < = c < = n

> 原文:[https://www . geesforgeks . org/count-三重数对-a-B- c-so-a2-B2-C2-and-1/](https://www.geeksforgeeks.org/count-number-of-triplet-pairs-a-b-c-such-that-a2-b2-c2-and-1/)

给定一个整数 **N** ，任务是统计三胞胎 **(a，b，c)** 的数量，使得**a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>****1≤a≤b≤c≤N**。

**示例:**

> **输入:** N = 5
> **输出:** 1
> 唯一可能的三元组对是(3，4，5)
> 3^2 + 4^2 = 5^2，即 9 + 16 = 25
> 
> **输入:** N = 10
> **输出:** 2
> (3，4，5)和(6，8，10)为所需的三连音对。

**方法-1:**
运行两个循环一个从 i = 1 到 N，第二个从 j = i+1 到 N。考虑每一对，找到 **i*i + j*j** ，检查这是否是一个完美的正方形，其平方根是否小于 N。如果是，则增加计数。

下面是上述方法的实现:

## C++

```
// C++ program to Find number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
#include <bits/stdc++.h>
using namespace std;

// function to ind number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
int Triplets(int n)
{
    // to store required answer
    int ans = 0;

    // run nested loops for first two numbers.
    for (int i = 1; i <= n; ++i) {
        for (int j = i; j <= n; ++j) {
            int x = i * i + j * j;

            // third number
            int y = sqrt(x);

            // check if third number is perfect
            // square and less than n
            if (y * y == x && y <= n)
                ++ans;
        }
    }

    return ans;
}

// Driver code
int main()
{

    int n = 10;

    // function call
    cout << Triplets(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
class Solution
{
// function to ind number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
static int Triplets(int n)
{
    // to store required answer
    int ans = 0;

    // run nested loops for first two numbers.
    for (int i = 1; i <= n; ++i) {
        for (int j = i; j <= n; ++j) {
            int x = i * i + j * j;

            // third number
            int y =(int) Math.sqrt(x);

            // check if third number is perfect
            // square and less than n
            if (y * y == x && y <= n)
                ++ans;
        }
    }

    return ans;
}

// Driver code
public static void main(String args[])
{

    int n = 10;

    // function call
    System.out.println(Triplets(n));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to Find number of
# Triplets 1 <= a <= b<= c <= n,
# Such that a^2 + b^2 = c^2
import math

# function to ind number of
# Triplets 1 <= a <= b<= c <= n,
# Such that a^2 + b^2 = c^2
def Triplets(n):

    # to store required answer
    ans = 0

    # run nested loops for first two numbers.
    for i in range(1, n + 1):
        for j in range(i, n + 1):
            x = i * i + j * j

            # third number
            y = int(math.sqrt(x))

            # check if third number is perfect
            # square and less than n
            if (y * y == x and y <= n):
                ans += 1
    return ans

# Driver code
if __name__ == "__main__":
    n = 10

    # function call
    print(Triplets(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to Find number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
using System;

class GFG
{
// function to ind number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
static int Triplets(int n)
{
    // to store required answer
    int ans = 0;

    // run nested loops for first two numbers.
    for (int i = 1; i <= n; ++i)
    {
        for (int j = i; j <= n; ++j)
        {
            int x = i * i + j * j;

            // third number
            int y = (int)Math.Sqrt(x);

            // check if third number is perfect
            // square and less than n
            if (y * y == x && y <= n)
                ++ans;
        }
    }

    return ans;
}

// Driver code
static void Main()
{
    int n = 10;
    Console.WriteLine(Triplets(n));
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2

// Function to ind number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2
function Triplets($n)
{
    // to store required answer
    $ans = 0;

    // run nested loops for first
    // two numbers.
    for ($i = 1; $i <= $n; ++$i)
    {
        for ($j =$i; $j <= $n; ++$j)
        {
            $x = $i * $i + $j * $j;

            // third number
            $y = (int)sqrt($x);

            // check if third number is perfect
            // square and less than n
            if ($y * $y == $x && $y <= $n)
                ++$ans;
        }
    }

    return $ans;
}

// Driver code
$n = 10;

// function call
echo Triplets($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to Find number of
// Triplets 1 <= a <= b<= c <= n,
// Such that a^2 + b^2 = c^2

    // function to ind number of
    // Triplets 1 <= a <= b<= c <= n,
    // Such that a^2 + b^2 = c^2
    function Triplets(n)
    {

        // to store required answer
        var ans = 0;

        // run nested loops for first two numbers.
        for (let i = 1; i <= n; ++i) {
            for (let j = i; j <= n; ++j) {
                var x = i * i + j * j;

                // third number
                var y = parseInt( Math.sqrt(x));

                // check if third number is perfect
                // square and less than n
                if (y * y == x && y <= n)
                    ++ans;
            }
        }
        return ans;
    }

    // Driver code
    var n = 10;

    // function call
    document.write(Triplets(n));

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
2
```

**方法-2:**

*   找到直到**n<sup>2</sup>T3】的所有完美方块，并将其保存到[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)中。**
*   现在，对于从 **1** 到 **n** 的每一个 **a** ，执行以下操作:
    *   从之前计算的完美方块列表中选择 **c <sup>2</sup>** 。
    *   那么**b<sup>2</sup>T3 可以计算为**b<sup>2</sup>= c<sup>2</sup>–a<sup>2</sup>**。**
    *   现在检查上一步计算的 **a < = b < = c** 和**b<sup>2</sup>T5 是否一定是一个完美的正方形。**
    *   如果满足上述条件，则增加**计数**。
*   最后打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return an Array containing
// all the perfect squares upto n
vector<int> getPerfectSquares(int n)
{
    vector<int> perfectSquares;
    int current = 1, i = 1;

    // While current perfect square
    // is less than or equal to n
    while (current <= n)
    {
        perfectSquares.push_back(current);
        current = pow(++i, 2);
    }
    return perfectSquares;
}

// Function to return the count of
// triplet (a, b, c) pairs such that
// a^2 + b^2 = c^2 and
// 1 <= a <= b <= c <= n
int countTriplets(int n)
{

    // Vector of perfect squares upto n^2
    vector<int> perfectSquares = getPerfectSquares(
                                 pow(n, 2));

    int count = 0;
    for(int a = 1; a <= n; a++)
    {
        int aSquare = pow(a, 2);

        for(int i = 0; i < perfectSquares.size(); i++)
        {
            int cSquare = perfectSquares[i];

            // Since, a^2 + b^2 = c^2
            int bSquare = abs(cSquare - aSquare);
            int b = sqrt(bSquare);
            int c = sqrt(cSquare);

            // If c < a or bSquare is not a
            // perfect square
            if (c < a || (find(perfectSquares.begin(),
                               perfectSquares.end(),
                               bSquare) ==
                               perfectSquares.end()))
                continue;

            // If triplet pair (a, b, c) satisfy
            // the given condition
            if ((b >= a) && (b <= c) &&
                (aSquare + bSquare == cSquare))
                count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int n = 10;

    cout << countTriplets(n);

    return 0;
}

// This code is contributed by himanshu77
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

public class GFG {

    // Function to return an ArrayList containing
    // all the perfect squares upto n
    public static ArrayList<Integer> getPerfectSquares(int n)
    {
        ArrayList<Integer> perfectSquares = new ArrayList<>();
        int current = 1, i = 1;

        // while current perfect square is less than or equal to n
        while (current <= n) {
            perfectSquares.add(current);
            current = (int)Math.pow(++i, 2);
        }
        return perfectSquares;
    }

    // Function to return the count of triplet (a, b, c) pairs
    // such that a^2 + b^2 = c^2 and 1 <= a <= b <= c <= n
    public static int countTriplets(int n)
    {
        // List of perfect squares upto n^2
        ArrayList<Integer> perfectSquares
            = getPerfectSquares((int)Math.pow(n, 2));

        int count = 0;
        for (int a = 1; a <= n; a++) {
            int aSquare = (int)Math.pow(a, 2);
            for (int i = 0; i < perfectSquares.size(); i++) {
                int cSquare = perfectSquares.get(i);

                // Since, a^2 + b^2 = c^2
                int bSquare = cSquare - aSquare;
                int b = (int)Math.sqrt(bSquare);
                int c = (int)Math.sqrt(cSquare);

                // If c < a or bSquare is not a perfect square
                if (c < a || !perfectSquares.contains(bSquare))
                    continue;

                // If triplet pair (a, b, c) satisfy the given condition
                if ((b >= a) && (b <= c) && (aSquare + bSquare == cSquare))
                    count++;
            }
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10;

        System.out.println(countTriplets(n));
    }
}
```

## 蟒蛇 3

```
# Python3  implementation of the approach
import math

# Function to return an ArrayList containing
# all the perfect squares upto n
def getPerfectSquares(n):

    perfectSquares = []
    current = 1
    i = 1

    # while current perfect square is less than or equal to n
    while (current <= n) :
        perfectSquares.append(current)
        i += 1
        current = i** 2

    return perfectSquares

# Function to return the count of triplet (a, b, c) pairs
# such that a^2 + b^2 = c^2 and 1 <= a <= b <= c <= n
def countTriplets(n):

    # List of perfect squares upto n^2
    perfectSquares= getPerfectSquares(n**2)

    count = 0
    for a in range(1, n +1 ):
        aSquare = a**2
        for i in range(len(perfectSquares)):
            cSquare = perfectSquares[i]

            # Since, a^2 + b^2 = c^2
            bSquare = abs(cSquare - aSquare)
            b = math.sqrt(bSquare)
            b = int(b)
            c = math.sqrt(cSquare)
            c = int(c)

            # If c < a or bSquare is not a perfect square
            if (c < a or (bSquare not in perfectSquares)):
                continue

            # If triplet pair (a, b, c) satisfy the given condition
            if ((b >= a) and (b <= c) and (aSquare + bSquare == cSquare)):
                count += 1

    return count

# Driver code
if __name__ == "__main__":

    n = 10

    print(countTriplets(n))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of the approach
using System.Collections;
using System;

class GFG
{

// Function to return an ArrayList containing
// all the perfect squares upto n
public static ArrayList getPerfectSquares(int n)
{
    ArrayList perfectSquares = new ArrayList();
    int current = 1, i = 1;

    // while current perfect square is less
    // than or equal to n
    while (current <= n)
    {
        perfectSquares.Add(current);
        current = (int)Math.Pow(++i, 2);
    }
    return perfectSquares;
}

// Function to return the count of triplet
// (a, b, c) pairs such that a^2 + b^2 = c^2
// and 1 <= a <= b <= c <= n
public static int countTriplets(int n)
{
    // List of perfect squares upto n^2
    ArrayList perfectSquares = getPerfectSquares((int)Math.Pow(n, 2));

    int count = 0;
    for (int a = 1; a <= n; a++)
    {
        int aSquare = (int)Math.Pow(a, 2);
        for (int i = 0; i < perfectSquares.Count; i++)
        {
            int cSquare = (int)perfectSquares[i];

            // Since, a^2 + b^2 = c^2
            int bSquare = cSquare - aSquare;
            int b = (int)Math.Sqrt(bSquare);
            int c = (int)Math.Sqrt(cSquare);

            // If c < a or bSquare is not a perfect square
            if (c < a || !perfectSquares.Contains(bSquare))
                continue;

            // If triplet pair (a, b, c) satisfy
            // the given condition
            if ((b >= a) && (b <= c) &&
                (aSquare + bSquare == cSquare))
                count++;
        }
    }
    return count;
}

// Driver code
public static void Main()
{
    int n = 10;

    Console.WriteLine(countTriplets(n));
}
}

// This code is contributed by mits.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return an Array containing
// all the perfect squares upto n
function getPerfectSquares(n)
{
    var perfectSquares = [];
    var current = 1, i = 1;

    // While current perfect square
    // is less than or equal to n
    while (current <= n)
    {
        perfectSquares.push(current);
        current = Math.pow(++i, 2);
    }
    return perfectSquares;
}

// Function to return the count of
// triplet (a, b, c) pairs such that
// a^2 + b^2 = c^2 and
// 1 <= a <= b <= c <= n
function countTriplets(n)
{

    // Vector of perfect squares upto n^2
    var perfectSquares = getPerfectSquares(
                                 Math.pow(n, 2));
    var count = 0;
    for(var a = 1; a <= n; a++)
    {
        var aSquare = Math.pow(a, 2);

        for(var i = 0;
                i < perfectSquares.length;
                i++)
        {
            var cSquare = perfectSquares[i];

            // Since, a^2 + b^2 = c^2
            var bSquare = Math.abs(cSquare -
                                   aSquare);
            var b = Math.sqrt(bSquare);
            var c = Math.sqrt(cSquare);

            // If c < a or bSquare is not a
            // perfect square
            if (c < a ||
                !perfectSquares.includes(bSquare))
                continue;

            // If triplet pair (a, b, c) satisfy
            // the given condition
            if ((b >= a) && (b <= c) &&
                (aSquare + bSquare == cSquare))
                count++;
        }
    }
    return count;
}

// Driver code
var n = 10;

document.write(countTriplets(n));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
2
```