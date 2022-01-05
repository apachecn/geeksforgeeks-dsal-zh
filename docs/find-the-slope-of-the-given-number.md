# 求给定数的斜率

> 原文:[https://www . geesforgeks . org/find-给定数字的斜率/](https://www.geeksforgeeks.org/find-the-slope-of-the-given-number/)

求给定数**数**的斜率。一个数的斜率是其中最小和最大数字的计数。如果一个数字小于它前后的数字，这个数字被称为最小值。类似地，如果一个数字大于它前后的数字，这个数字被称为最大值。

**示例:**

```
Input : 1213321
Output : 2
1213321- The highlighted digit '2' is a maxima and
highlighted digit '1' is a minima.

Input : 273299302236131
Output : 6
```

**来源:** [巴克莱面试经历(校内)](https://www.geeksforgeeks.org/barclays-interview-experience-on-campus-2/)。

**方法:**遍历给定数字的数字，从第二个数字到最后一个数字。对于每个数字，检查该数字是大于还是小于其前后的数字。算出这些数字的个数。

## C++

```
// C++ implementation to find slope of a number
#include <bits/stdc++.h>

using namespace std;

// function to find slope of a number
int slopeOfNum(string num, int n)
{
    // to store slope of the given
    // number 'num'
    int slope = 0;

    // loop from the 2nd digit up to the 2nd last digit
    // of the given number 'num'
    for (int i = 1; i < n - 1; i++) {

        // if the digit is a maxima
        if (num[i] > num[i - 1] && num[i] > num[i + 1])
            slope++;

        // if the digit is a minima
        else if (num[i] < num[i - 1] && num[i] < num[i + 1])
            slope++;
    }

    // required slope
    return slope;
}

// Driver program to test above
int main()
{
    string num = "1213321";
    int n = num.size();
    cout << "Slope = "
         << slopeOfNum(num, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find slope of a number
import java.io.*;

class GFG
{

    // function to find
    // slope of a number
    static int slopeOfNum(String num, int n)
    {
        // to store slope of the
        // given number 'num'
        int slope = 0;

        // loop from the 2nd digit
        // up to the 2nd last digit
        // of the given number 'num'
        for (int i = 1; i < n - 1; i++)
        {

            // if the digit is a maxima
            if (num.charAt(i) > num.charAt(i - 1) &&
                num.charAt(i) > num.charAt(i + 1))
                slope++;

            // if the digit is a minima
            else if (num.charAt(i) < num.charAt(i - 1) &&
                     num.charAt(i) < num.charAt(i + 1))
                slope++;
        }

        // required slope
        return slope;
    }

    // Driver code
    public static void main (String[] args)
    {
        String num = "1213321";
        int n = num.length();
        System.out.println("Slope = " +
                    slopeOfNum(num, n));
    }
}

// This code is contributed by Mahadev99
```

## 蟒蛇 3

```
# Python 3 implementation to find
# slope of a number

# function to find slope of a number
def slopeOfNum(num, n):

    # to store slope of the given
    # number 'num'
    slope = 0

    # loop from the 2nd digit up
    # to the 2nd last digit
    # of the given number 'num'
    for i in range(1, n - 1) :

        # if the digit is a maxima
        if (num[i] > num[i - 1] and
            num[i] > num[i + 1]):
            slope += 1

        # if the digit is a minima
        elif (num[i] < num[i - 1] and
              num[i] < num[i + 1]):
            slope += 1

    # required slope
    return slope

# Driver Code
if __name__ == "__main__":

    num = "1213321"
    n = len(num)
    print("Slope =", slopeOfNum(num, n))

# This code is contributed by ita_c
```

## C#

```
// C# implementation to
// find slope of a number
class GFG
{

// function to find slope of a number
static int slopeOfNum(string num, int n)
{
    // to store slope of the
    // given number 'num'
    int slope = 0;

    // loop from the 2nd digit
    // up to the 2nd last digit
    // of the given number 'num'
    for (int i = 1; i < n - 1; i++)
    {

        // if the digit is a maxima
        if (num[i] > num[i - 1] &&
            num[i] > num[i + 1])
            slope++;

        // if the digit is a minima
        else if (num[i] < num[i - 1] &&
                 num[i] < num[i + 1])
            slope++;
    }

    // required slope
    return slope;
}

// Driver code
public static void Main()
{
    string num = "1213321";
    int n = num.Length;
    System.Console.WriteLine("Slope = " +
                     slopeOfNum(num, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// slope of a number

// function to find slope of a number
function slopeOfNum($num, $n)
{
    // to store slope of the given
    // number 'num'
    $slope = 0;

    // loop from the 2nd digit up
    // to the 2nd last digit of
    // the given number 'num'
    for ($i = 1; $i < $n - 1; $i++)
    {

        // if the digit is a maxima
        if ($num[$i] > $num[$i - 1] &&
            $num[$i] > $num[$i + 1])
            $slope++;

        // if the digit is a minima
        else if ($num[$i] < $num[$i - 1] &&
                 $num[$i] < $num[$i + 1])
            $slope++;
    }

    // required slope
    return $slope;
}

// Driver Code
$num = "1213321";
$n = strlen($num);
echo "Slope = " . slopeOfNum($num, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation to
// find slope of a number

    // function to find
    // slope of a number
    function slopeOfNum(num,n)
    {
        // to store slope of the
        // given number 'num'
        let slope = 0;

        // loop from the 2nd digit
        // up to the 2nd last digit
        // of the given number 'num'
        for (let i = 1; i < n - 1; i++)
        {

            // if the digit is a maxima
            if (num[i] > num[i-1] &&
                num[i] > num[i+1])
                slope++;

            // if the digit is a minima
            else if (num[i] < num[i-1] &&
                     num[i] < num[i+1])
                slope++;
        }

        // required slope
        return slope;
    }

    // Driver code
    let num = "1213321";
    let n = num.length;
    document.write("Slope = " +
                    slopeOfNum(num, n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Slope = 2
```

**时间复杂度:** O(n)。