# 给定数组中缺少偶数和奇数元素

> 原文:[https://www . geeksforgeeks . org/给定数组中缺少偶数和奇数元素/](https://www.geeksforgeeks.org/missing-even-and-odd-elements-from-the-given-arrays/)

给定两个整数数组，**偶[]** 和**奇[]** ，它们分别包含连续的偶和奇元素，每个数组中缺少一个元素。任务是找到丢失的元素。

**示例:**

> **输入:**偶数[] = {6，4，8，14，10}，奇数[] = {7，5，3，11，13}
> **输出:**
> 偶数= 12
> 奇数= 9
> 
> **输入:**偶[] = {4，6，2，10}，奇[] = {7，5，9，13，11，17}
> **输出:**
> 偶= 8
> 奇= 15

**方法:**将**偶[]** 数组中的最小偶元素和最大偶元素存储在变量 **minEven** 和 **maxEven** 中。我们知道，前 N 个偶数的**和为 **N * (N + 1)** 。计算从 **2** 到**的偶数之和我甚至**说 **sum1** 和从 **2** 到 **maxEven** 说 **sum2** 的偶数之和。现在，偶数数组所需的和将是**req sum = sum 2–sum 1+minEven**，从这个 **reqSum** 中减去**even【】**数组的和将会给出缺失的偶数。
同样，缺失的奇数也可以找到，因为我们知道前 N 个奇数**的**和为 **N <sup>2</sup>** 。
以下是上述方法的实施:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the missing numbers
void findMissingNums(int even[], int sizeEven, int odd[], int sizeOdd)
{

    // To store the minimum and the maximum
    // odd and even elements from the arrays
    int minEven = INT_MAX;
    int maxEven = INT_MIN;
    int minOdd = INT_MAX;
    int maxOdd = INT_MIN;

    // To store the sum of the array elements
    int sumEvenArr = 0, sumOddArr = 0;

    // Get the minimum and the maximum
    // even elements from the array
    for (int i = 0; i < sizeEven; i++) {
        minEven = min(minEven, even[i]);
        maxEven = max(maxEven, even[i]);
        sumEvenArr += even[i];
    }

    // Get the minimum and the maximum
    // odd elements from the array
    for (int i = 0; i < sizeOdd; i++) {
        minOdd = min(minOdd, odd[i]);
        maxOdd = max(maxOdd, odd[i]);
        sumOddArr += odd[i];
    }

    // To store the total terms in the series
    // and the required sum of the array
    int totalTerms = 0, reqSum = 0;

    // Total terms from 2 to minEven
    totalTerms = minEven / 2;

    // Sum of all even numbers from 2 to minEven
    int evenSumMin = totalTerms * (totalTerms + 1);

    // Total terms from 2 to maxEven
    totalTerms = maxEven / 2;

    // Sum of all even numbers from 2 to maxEven
    int evenSumMax = totalTerms * (totalTerms + 1);

    // Required sum for the even array
    reqSum = evenSumMax - evenSumMin + minEven;

    // Missing even number
    cout << "Even = " << reqSum - sumEvenArr << "\n";

    // Total terms from 1 to minOdd
    totalTerms = (minOdd / 2) + 1;

    // Sum of all odd numbers from 1 to minOdd
    int oddSumMin = totalTerms * totalTerms;

    // Total terms from 1 to maxOdd
    totalTerms = (maxOdd / 2) + 1;

    // Sum of all odd numbers from 1 to maxOdd
    int oddSumMax = totalTerms * totalTerms;

    // Required sum for the odd array
    reqSum = oddSumMax - oddSumMin + minOdd;

    // Missing odd number
    cout << "Odd = " << reqSum - sumOddArr;
}

// Driver code
int main()
{
    int even[] = { 6, 4, 8, 14, 10 };
    int sizeEven = sizeof(even) / sizeof(even[0]);
    int odd[] = { 7, 5, 3, 11, 13 };
    int sizeOdd = sizeof(odd) / sizeof(odd[0]);
    findMissingNums(even, sizeEven, odd, sizeOdd);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the missing numbers
static void findMissingNums(int even[], int sizeEven,
                            int odd[], int sizeOdd)
{

    // To store the minimum and the maximum
    // odd and even elements from the arrays
    int minEven =Integer.MAX_VALUE;
    int maxEven =Integer.MIN_VALUE;
    int minOdd = Integer.MAX_VALUE;
    int maxOdd = Integer.MIN_VALUE;

    // To store the sum of the array elements
    int sumEvenArr = 0, sumOddArr = 0;

    // Get the minimum and the maximum
    // even elements from the array
    for (int i = 0; i < sizeEven; i++)
    {
        minEven = Math.min(minEven, even[i]);
        maxEven = Math.max(maxEven, even[i]);
        sumEvenArr += even[i];
    }

    // Get the minimum and the maximum
    // odd elements from the array
    for (int i = 0; i < sizeOdd; i++)
    {
        minOdd = Math.min(minOdd, odd[i]);
        maxOdd = Math.max(maxOdd, odd[i]);
        sumOddArr += odd[i];
    }

    // To store the total terms in the series
    // and the required sum of the array
    int totalTerms = 0, reqSum = 0;

    // Total terms from 2 to minEven
    totalTerms = minEven / 2;

    // Sum of all even numbers
    // from 2 to minEven
    int evenSumMin = (totalTerms *
                     (totalTerms + 1));

    // Total terms from 2 to maxEven
    totalTerms = maxEven / 2;

    // Sum of all even numbers from
    // 2 to maxEven
    int evenSumMax = (totalTerms *
                     (totalTerms + 1));

    // Required sum for the even array
    reqSum = evenSumMax - evenSumMin + minEven;

    // Missing even number
    System.out.println("Even = " +
                      (reqSum - sumEvenArr));

    // Total terms from 1 to minOdd
    totalTerms = (minOdd / 2) + 1;

    // Sum of all odd numbers
    // from 1 to minOdd
    int oddSumMin = totalTerms * totalTerms;

    // Total terms from 1 to maxOdd
    totalTerms = (maxOdd / 2) + 1;

    // Sum of all odd numbers
    // from 1 to maxOdd
    int oddSumMax = totalTerms * totalTerms;

    // Required sum for the odd array
    reqSum = oddSumMax - oddSumMin + minOdd;

    // Missing odd number
    System.out.println("Odd = " +
                      (reqSum - sumOddArr));
}

// Driver code
public static void main(String[] args)
{
    int even[] = { 6, 4, 8, 14, 10 };
    int sizeEven = even.length;
    int odd[] = { 7, 5, 3, 11, 13 };
    int sizeOdd = odd.length;
    findMissingNums(even, sizeEven,
                     odd, sizeOdd);
}
}

// This code is contributed
// by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to find the missing numbers
def findMissingNums(even, sizeEven,
                      odd, sizeOdd):

    # To store the minimum and the
    # maximum odd and even elements
    # from the arrays
    minEven = sys.maxsize ;
    maxEven = -(sys.maxsize - 1);
    minOdd = sys.maxsize ;
    maxOdd = -(sys.maxsize - 1);

    # To store the sum of the
    # array elements
    sumEvenArr = 0;
    sumOddArr = 0;

    # Get the minimum and the maximum
    # even elements from the array
    for i in range(sizeEven) :
        minEven = min(minEven, even[i]);
        maxEven = max(maxEven, even[i]);
        sumEvenArr += even[i];

    # Get the minimum and the maximum
    # odd elements from the array
    for i in range(sizeOdd) :
        minOdd = min(minOdd, odd[i]);
        maxOdd = max(maxOdd, odd[i]);
        sumOddArr += odd[i];

    # To store the total terms in
    # the series and the required
    # sum of the array
    totalTerms = 0;
    reqSum = 0;

    # Total terms from 2 to minEven
    totalTerms = minEven // 2;

    # Sum of all even numbers from
    # 2 to minEven
    evenSumMin = (totalTerms *
                 (totalTerms + 1));

    # Total terms from 2 to maxEven
    totalTerms = maxEven // 2;

    # Sum of all even numbers from
    # 2 to maxEven
    evenSumMax = (totalTerms *
                 (totalTerms + 1));

    # Required sum for the even array
    reqSum = (evenSumMax -
              evenSumMin + minEven);

    # Missing even number
    print("Even =", reqSum -
                    sumEvenArr);

    # Total terms from 1 to minOdd
    totalTerms = (minOdd // 2) + 1;

    # Sum of all odd numbers from
    # 1 to minOdd
    oddSumMin = totalTerms * totalTerms;

    # Total terms from 1 to maxOdd
    totalTerms = (maxOdd // 2) + 1;

    # Sum of all odd numbers from
    # 1 to maxOdd
    oddSumMax = totalTerms * totalTerms;

    # Required sum for the odd array
    reqSum = (oddSumMax -
              oddSumMin + minOdd);

    # Missing odd number
    print("Odd =", reqSum - sumOddArr);

# Driver code
if __name__ == "__main__" :

    even = [ 6, 4, 8, 14, 10 ];
    sizeEven = len(even)
    odd = [ 7, 5, 3, 11, 13 ];
    sizeOdd = len(odd) ;
    findMissingNums(even, sizeEven,
                    odd, sizeOdd);

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the missing numbers
static void findMissingNums(int []even, int sizeEven,
                            int []odd, int sizeOdd)
{

    // To store the minimum and the maximum
    // odd and even elements from the arrays
    int minEven =int.MaxValue;
    int maxEven =int.MinValue;
    int minOdd = int.MaxValue;
    int maxOdd = int.MinValue;

    // To store the sum of the array elements
    int sumEvenArr = 0, sumOddArr = 0;

    // Get the minimum and the maximum
    // even elements from the array
    for (int i = 0; i < sizeEven; i++)
    {
        minEven = Math.Min(minEven, even[i]);
        maxEven = Math.Max(maxEven, even[i]);
        sumEvenArr += even[i];
    }

    // Get the minimum and the maximum
    // odd elements from the array
    for (int i = 0; i < sizeOdd; i++)
    {
        minOdd = Math.Min(minOdd, odd[i]);
        maxOdd = Math.Max(maxOdd, odd[i]);
        sumOddArr += odd[i];
    }

    // To store the total terms in the series
    // and the required sum of the array
    int totalTerms = 0, reqSum = 0;

    // Total terms from 2 to minEven
    totalTerms = minEven / 2;

    // Sum of all even numbers
    // from 2 to minEven
    int evenSumMin = (totalTerms *
                    (totalTerms + 1));

    // Total terms from 2 to maxEven
    totalTerms = maxEven / 2;

    // Sum of all even numbers from
    // 2 to maxEven
    int evenSumMax = (totalTerms *
                    (totalTerms + 1));

    // Required sum for the even array
    reqSum = evenSumMax - evenSumMin + minEven;

    // Missing even number
    Console.WriteLine("Even = " +
                    (reqSum - sumEvenArr));

    // Total terms from 1 to minOdd
    totalTerms = (minOdd / 2) + 1;

    // Sum of all odd numbers
    // from 1 to minOdd
    int oddSumMin = totalTerms * totalTerms;

    // Total terms from 1 to maxOdd
    totalTerms = (maxOdd / 2) + 1;

    // Sum of all odd numbers
    // from 1 to maxOdd
    int oddSumMax = totalTerms * totalTerms;

    // Required sum for the odd array
    reqSum = oddSumMax - oddSumMin + minOdd;

    // Missing odd number
    Console.WriteLine("Odd = " +
                    (reqSum - sumOddArr));
}

// Driver code
static void Main()
{
    int []even = { 6, 4, 8, 14, 10 };
    int sizeEven = even.Length;
    int []odd = { 7, 5, 3, 11, 13 };
    int sizeOdd = odd.Length;
    findMissingNums(even, sizeEven,
                    odd, sizeOdd);
}
}

// This code is contributed
// by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find the missing numbers
function findMissingNums($even, $sizeEven,
                          $odd, $sizeOdd)
{

    // To store the minimum and the maximum
    // odd and even elements from the arrays
    $minEven = PHP_INT_MAX;
    $maxEven = PHP_INT_MIN;
    $minOdd = PHP_INT_MAX;
    $maxOdd = PHP_INT_MIN;

    // To store the sum of the array elements
    $sumEvenArr = $sumOddArr = 0;

    // Get the minimum and the maximum
    // even elements from the array
    for ($i = 0; $i < $sizeEven; $i++)
    {
        $minEven = min($minEven, $even[$i]);
        $maxEven = max($maxEven, $even[$i]);
        $sumEvenArr += $even[$i];
    }

    // Get the minimum and the maximum
    // odd elements from the array
    for ($i = 0; $i < $sizeOdd; $i++)
    {
        $minOdd = min($minOdd, $odd[$i]);
        $maxOdd = max($maxOdd, $odd[$i]);
        $sumOddArr += $odd[$i];
    }

    // To store the total terms in the series
    // and the required sum of the array
    $totalTerms = $reqSum = 0;

    // Total terms from 2 to minEven
    $totalTerms = (int)($minEven / 2);

    // Sum of all even numbers
    // from 2 to minEven
    $evenSumMin = $totalTerms *
                 ($totalTerms + 1);

    // Total terms from 2 to maxEven
    $totalTerms = (int)($maxEven / 2);

    // Sum of all even numbers
    // from 2 to maxEven
    $evenSumMax = $totalTerms *
                 ($totalTerms + 1);

    // Required sum for the even array
    $reqSum = ($evenSumMax -
               $evenSumMin + $minEven);

    // Missing even number
    echo "Even = " . ($reqSum -
                      $sumEvenArr) . "\n";

    // Total terms from 1 to minOdd
    $totalTerms = (int)(($minOdd / 2) + 1);

    // Sum of all odd numbers
    // from 1 to minOdd
    $oddSumMin = $totalTerms * $totalTerms;

    // Total terms from 1 to maxOdd
    $totalTerms = (int)(($maxOdd / 2) + 1);

    // Sum of all odd numbers
    // from 1 to maxOdd
    $oddSumMax = $totalTerms * $totalTerms;

    // Required sum for the odd array
    $reqSum = ($oddSumMax -
               $oddSumMin + $minOdd);

    // Missing odd number
    echo "Odd = " . ($reqSum - $sumOddArr);
}

// Driver code
$even = array( 6, 4, 8, 14, 10 );
$sizeEven = count($even);
$odd = array( 7, 5, 3, 11, 13 );
$sizeOdd = count($odd);
findMissingNums($even, $sizeEven,
                 $odd, $sizeOdd);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to find the missing numbers
    function findMissingNums(even, sizeEven, odd, sizeOdd)
    {

        // To store the minimum and the maximum
        // odd and even elements from the arrays
        let minEven = Number.MAX_VALUE;
        let maxEven = Number.MIN_VALUE;
        let minOdd = Number.MAX_VALUE;
        let maxOdd = Number.MIN_VALUE;

        // To store the sum of the array elements
        let sumEvenArr = 0, sumOddArr = 0;

        // Get the minimum and the maximum
        // even elements from the array
        for (let i = 0; i < sizeEven; i++)
        {
            minEven = Math.min(minEven, even[i]);
            maxEven = Math.max(maxEven, even[i]);
            sumEvenArr += even[i];
        }

        // Get the minimum and the maximum
        // odd elements from the array
        for (let i = 0; i < sizeOdd; i++)
        {
            minOdd = Math.min(minOdd, odd[i]);
            maxOdd = Math.max(maxOdd, odd[i]);
            sumOddArr += odd[i];
        }

        // To store the total terms in the series
        // and the required sum of the array
        let totalTerms = 0, reqSum = 0;

        // Total terms from 2 to minEven
        totalTerms = parseInt(minEven / 2, 10);

        // Sum of all even numbers
        // from 2 to minEven
        let evenSumMin = (totalTerms * (totalTerms + 1));

        // Total terms from 2 to maxEven
        totalTerms = parseInt(maxEven / 2, 10);

        // Sum of all even numbers from
        // 2 to maxEven
        let evenSumMax = (totalTerms * (totalTerms + 1));

        // Required sum for the even array
        reqSum = evenSumMax - evenSumMin + minEven;

        // Missing even number
        document.write("Even = " + (reqSum - sumEvenArr) + "</br>");

        // Total terms from 1 to minOdd
        totalTerms = parseInt(minOdd / 2, 10) + 1;

        // Sum of all odd numbers
        // from 1 to minOdd
        let oddSumMin = totalTerms * totalTerms;

        // Total terms from 1 to maxOdd
        totalTerms = parseInt(maxOdd / 2, 10) + 1;

        // Sum of all odd numbers
        // from 1 to maxOdd
        let oddSumMax = totalTerms * totalTerms;

        // Required sum for the odd array
        reqSum = oddSumMax - oddSumMin + minOdd;

        // Missing odd number
        document.write("Odd = " + (reqSum - sumOddArr));
    }

    let even = [ 6, 4, 8, 14, 10 ];
    let sizeEven = even.length;
    let odd = [ 7, 5, 3, 11, 13 ];
    let sizeOdd = odd.length;
    findMissingNums(even, sizeEven, odd, sizeOdd);

</script>
```

**Output:** 

```
Even = 12
Odd = 9
```