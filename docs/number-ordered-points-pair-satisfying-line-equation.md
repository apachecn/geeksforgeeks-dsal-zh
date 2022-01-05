# 满足线方程的有序点对的数量

> 原文:[https://www . geeksforgeeks . org/number-ordered-points-pair-compliance-line-equation/](https://www.geeksforgeeks.org/number-ordered-points-pair-satisfying-line-equation/)

给定 n 个整数的数组，直线的斜率即 m，直线的截距即 c，计算 i ≠ j 的点的有序对(I，j)的数量，使得点(A <sub>i</sub> ，A <sub>j</sub> )满足给定斜率和截距形成的直线。
**注**:直线方程为 y = mx + c，其中 m 为直线斜率，c 为截距。
**示例:**

> 输入:m = 1，c = 1，arr[] = [ 1，2，3，4，2 ]
> 输出:5 个有序点
> **说明:**给定斜率和截距的直线方程为:y = x + 1。(arr <sub>i</sub> 、arr <sub>j</sub> )满足上式的线对数(I，j)为:(1，2)、(1，5)、(2，3)、(3，4)、(5，3)。
> 输入:m = 2，c = 1，arr[] = [ 1，2，3，4，2，5 ]
> 输出:3 个有序点

**方法 1(蛮力):**
生成所有可能的对(I，j)并检查特定的有序对(I，j)是否是这样的，(arr <sub>i</sub> ，arr <sub>j</sub> )满足线 y = mx + c 和 i ≠ j 的给定等式。如果点有效(如果满足上述条件，则点有效)，则递增存储有效点总数的计数器。

## C++

```
// CPP code to count the number of ordered
// pairs satisfying Line Equation
#include <bits/stdc++.h>

using namespace std;

/* Checks if (i, j) is valid, a point (i, j)
   is valid if point (arr[i], arr[j])
   satisfies the equation y = mx + c And
   i is not equal to j*/
bool isValid(int arr[], int i, int j,
             int m, int c)
{

    // check if i equals to j
    if (i == j)
        return false;

    // Equation LHS = y, and RHS = mx + c
    int lhs = arr[j];   
    int rhs = m * arr[i] + c;

    return (lhs == rhs);
}

/* Returns the number of ordered pairs
   (i, j) for which point (arr[i], arr[j])
   satisfies the equation of the line
   y = mx + c */
int findOrderedPoints(int arr[], int n,
                      int m, int c)
{

    int counter = 0;

    // for every possible (i, j) check
    // if (a[i], a[j]) satisfies the
    // equation y = mx + c
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            // (firstIndex, secondIndex)
            // is same as (i, j)
            int firstIndex = i, secondIndex = j;

            // check if (firstIndex,
            // secondIndex) is a valid point
            if (isValid(arr, firstIndex, secondIndex, m, c))
                counter++;
        }
    }
    return counter;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // equation of line is y = mx + c
    int m = 1, c = 1;
    cout << findOrderedPoints(arr, n, m, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find number of ordered
// points satisfying line equation
import java.io.*;

public class GFG {

    // Checks if (i, j) is valid,
    // a point (i, j) is valid if
    // point (arr[i], arr[j])
    // satisfies the equation
    // y = mx + c And
    // i is not equal to j
    static boolean isValid(int []arr, int i,
                        int j, int m, int c)
    {

        // check if i equals to j
        if (i == j)
            return false;

        // Equation LHS = y,
        // and RHS = mx + c
        int lhs = arr[j];
        int rhs = m * arr[i] + c;

        return (lhs == rhs);
    }

    /* Returns the number of ordered pairs
    (i, j) for which point (arr[i], arr[j])
    satisfies the equation of the line
    y = mx + c */
    static int findOrderedPoints(int []arr,
                       int n, int m, int c)
    {

        int counter = 0;

        // for every possible (i, j) check
        // if (a[i], a[j]) satisfies the
        // equation y = mx + c
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                // (firstIndex, secondIndex)
                // is same as (i, j)
                int firstIndex = i,
                   secondIndex = j;

                // check if (firstIndex,
                // secondIndex) is a
                // valid point
                if (isValid(arr, firstIndex,
                         secondIndex, m, c))
                    counter++;
            }
        }
        return counter;
    }

    // Driver Code
    public static void main(String args[])
    {
        int []arr = { 1, 2, 3, 4, 2 };
        int n = arr.length;

        // equation of line is y = mx + c
        int m = 1, c = 1;
        System.out.print(
           findOrderedPoints(arr, n, m, c));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python code to count the number of ordered
# pairs satisfying Line Equation

# Checks if (i, j) is valid, a point (i, j)
# is valid if point (arr[i], arr[j])
# satisfies the equation y = mx + c And
# i is not equal to j
def isValid(arr, i, j, m, c) :

    # check if i equals to j
    if (i == j) :
        return False

    # Equation LHS = y, and RHS = mx + c
    lhs = arr[j];
    rhs = m * arr[i] + c

    return (lhs == rhs)

# Returns the number of ordered pairs
# (i, j) for which point (arr[i], arr[j])
# satisfies the equation of the line
# y = mx + c */
def findOrderedPoints(arr, n, m, c) :

    counter = 0

    # for every possible (i, j) check
    # if (a[i], a[j]) satisfies the
    # equation y = mx + c
    for i in range(0, n) :
        for j in range(0, n) :
            # (firstIndex, secondIndex)
            # is same as (i, j)
            firstIndex = i
            secondIndex = j

            # check if (firstIndex,
            # secondIndex) is a valid point
            if (isValid(arr, firstIndex,
                      secondIndex, m, c)) :
                counter = counter + 1

    return counter

# Driver Code
arr = [ 1, 2, 3, 4, 2 ]
n = len(arr)

# equation of line is y = mx + c
m = 1
c = 1
print (findOrderedPoints(arr, n, m, c))

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# code to find number of ordered
// points satisfying line equation
using System;
class GFG {

    // Checks if (i, j) is valid,
    // a point (i, j) is valid if
    // point (arr[i], arr[j])
    // satisfies the equation
    // y = mx + c And
    // i is not equal to j
    static bool isValid(int []arr, int i,
                     int j, int m, int c)
    {

        // check if i equals to j
        if (i == j)
            return false;

        // Equation LHS = y,
        // and RHS = mx + c
        int lhs = arr[j];
        int rhs = m * arr[i] + c;

        return (lhs == rhs);
    }

    /* Returns the number of ordered pairs
      (i, j) for which point (arr[i], arr[j])
      satisfies the equation of the line
       y = mx + c */
    static int findOrderedPoints(int []arr, int n,
                                     int m, int c)
    {

        int counter = 0;

        // for every possible (i, j) check
        // if (a[i], a[j]) satisfies the
        // equation y = mx + c
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                // (firstIndex, secondIndex)
                // is same as (i, j)
                int firstIndex = i, secondIndex = j;

                // check if (firstIndex,
                // secondIndex) is a valid point
                if (isValid(arr, firstIndex, secondIndex, m, c))
                    counter++;
            }
        }
        return counter;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 2 };
        int n = arr.Length;

        // equation of line is y = mx + c
        int m = 1, c = 1;
        Console.Write(findOrderedPoints(arr, n, m, c));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count the
// number of ordered pairs
// satisfying Line Equation

/* Checks if (i, j) is valid,
a point (i, j) is valid if
point (arr[i], arr[j]) satisfies
the equation y = mx + c And i
is not equal to j*/
function isValid($arr, $i,
                 $j, $m, $c)
{
    // check if i equals to j
    if ($i == $j)
        return false;

    // Equation LHS = y, and
    // RHS = mx + c
    $lhs = $arr[$j];
    $rhs = $m * $arr[$i] + $c;

    return ($lhs == $rhs);
}

/* Returns the number of
ordered pairs (i, j) for
which point (arr[i], arr[j])
satisfies the equation of
the line y = mx + c */
function findOrderedPoints($arr, $n,
                           $m, $c)
{

    $counter = 0;

    // for every possible (i, j)
    // check if (a[i], a[j])
    // satisfies the equation
    // y = mx + c
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            // (firstIndex, secondIndex)
            // is same as (i, j)
            $firstIndex = $i; $secondIndex = $j;

            // check if (firstIndex,
            // secondIndex) is a valid point
            if (isValid($arr, $firstIndex,
                        $secondIndex, $m, $c))
                $counter++;
        }
    }
    return $counter;
}

// Driver Code
$arr = array( 1, 2, 3, 4, 2 );
$n = count($arr);

// equation of line
// is y = mx + c
$m = 1; $c = 1;
echo (findOrderedPoints($arr, $n, $m, $c));

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>
      // JavaScript code to find number of ordered
      // points satisfying line equation
      // Checks if (i, j) is valid,
      // a point (i, j) is valid if
      // point (arr[i], arr[j])
      // satisfies the equation
      // y = mx + c And
      // i is not equal to j
      function isValid(arr, i, j, m, c)
      {

        // check if i equals to j
        if (i == j) return false;

        // Equation LHS = y,
        // and RHS = mx + c
        var lhs = arr[j];
        var rhs = m * arr[i] + c;

        return lhs == rhs;
      }

      /* Returns the number of ordered pairs
    (i, j) for which point (arr[i], arr[j])
    satisfies the equation of the line
    y = mx + c */
      function findOrderedPoints(arr, n, m, c) {
        var counter = 0;

        // for every possible (i, j) check
        // if (a[i], a[j]) satisfies the
        // equation y = mx + c
        for (var i = 0; i < n; i++)
        {
          for (var j = 0; j < n; j++)
          {

            // (firstIndex, secondIndex)
            // is same as (i, j)
            var firstIndex = i,
              secondIndex = j;

            // check if (firstIndex,
            // secondIndex) is a valid point
            if (isValid(arr, firstIndex, secondIndex, m, c)) counter++;
          }
        }
        return counter;
      }

      // Driver Code
      var arr = [1, 2, 3, 4, 2];
      var n = arr.length;

      // equation of line is y = mx + c
      var m = 1,
        c = 1;
      document.write(findOrderedPoints(arr, n, m, c));

      // This code is contributed by rdtank.
    </script>
```

**Output :** 

```
5
```

**时间复杂度:** O(n <sup>2</sup> )
**方法 2(高效):**
给定一个点的 x 坐标，对于每个 x 都有一个唯一的 y 值，而 y 的值只不过是 m * x + c。因此，对于数组 arr 的每个可能的 x 坐标，计算满足直线方程的 y 的唯一值在该数组中出现多少次。存储数组中所有整数的计数。现在，对于每个值，arr <sub>i</sub> ，将 m * arr <sub>i</sub> + c 的出现次数加到答案中，对于给定的 I，m * a[i] + c 在数组中出现 x 次，然后，将 x 加到我们的计数器中以获得总有效点，但是需要检查如果 a[i] = m * a[i] + c，那么， 很明显，由于这在数组中出现了 x 次，因此一次出现在第 i <sup>次</sup>索引处，其余(x–1)次出现是有效的 y 坐标，因此将(x–1)添加到我们的点数计数器中。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP code to find number of ordered
// points satisfying line equation
#include <bits/stdc++.h>
using namespace std;

/* Returns the number of ordered pairs
   (i, j) for which point (arr[i], arr[j])
   satisfies the equation of the line
   y = mx + c */
int findOrderedPoints(int arr[], int n,
                      int m, int c)
{
    int counter = 0;

    // map stores the frequency
    // of arr[i] for all i
    unordered_map<int, int> frequency;

    for (int i = 0; i < n; i++)
        frequency[arr[i]]++;

    for (int i = 0; i < n; i++)
    {
        int xCoordinate = arr[i];
        int yCoordinate = (m * arr[i] + c);

        // if for a[i](xCoordinate),
        // a yCoordinate exists in the map
        // add the frequency of yCoordinate
        // to the counter

        if (frequency.find(yCoordinate) !=
            frequency.end())
            counter += frequency[yCoordinate];

        // check if xCoordinate = yCoordinate,
        // if this is true then since we only
        // want (i, j) such that i != j, decrement
        // the counter by one to avoid points
        // of type (arr[i], arr[i])
        if (xCoordinate == yCoordinate)
            counter--;
    }
    return counter;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 1, c = 1;
    cout << findOrderedPoints(arr, n, m, c);
    return 0;
}
```

**Output:** 

```
5
```

**时间复杂度:** O(n)