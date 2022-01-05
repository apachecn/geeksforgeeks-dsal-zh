# 对给定范围内除数最大的元素进行计数

> 原文:[https://www . geesforgeks . org/count-给定范围内具有最大除数的元素/](https://www.geeksforgeeks.org/count-elements-in-the-given-range-which-have-maximum-number-of-divisors/)

给定两个数字 X 和 Y。任务是找出[X，Y]范围内的元素数量，这两个范围都包含在内，并且具有最大除数。

**示例**:

> **输入** : X = 2，Y = 9
> **输出** : 2
> 6，8 是除数最多的数字。
> 
> **输入** : X = 1，Y = 10
> **输出** : 3
> 6，8，10 是除数最多的数字。

**方法 1:**

*   逐一遍历从 X 到 Y 的所有元素。
*   [求每个元素的除数。](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)
*   将除数存储在数组中，并更新除数的最大值(最大除数)。
*   遍历包含除数的数组，计算等于最大除数的元素数。
*   返回计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the divisors
int countDivisors(int n)
{
    int count = 0;

    // Note that this loop runs till square root
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {

            // If divisors are equal, print only one
            if (n / i == i)
                count++;

            else // Otherwise print both
                count += 2;
        }
    }

    return count;
}

// Function to count the number with
// maximum divisors
int MaximumDivisors(int X, int Y)
{
    int maxDivisors = INT_MIN, result = 0;

    // to store number of divisors
    int arr[Y - X + 1];

    // Traverse from X to Y
    for (int i = X; i <= Y; i++) {

            // Count the number of divisors of i
             int Div = countDivisors(i);

            // Store the value of div in an array
             arr[i - X] = Div;

            // Update the value of maxDivisors
             maxDivisors = max(Div, maxDivisors);

    }

    // Traverse the array
    for (int i = 0; i < (Y - X + 1); i++)

        // Count the value equals to maxDivisors
        if (arr[i] == maxDivisors)
            result++;

    return result;
}

// Driver Code
int main()
{
    int X = 1, Y = 10;

    // function call
    cout << MaximumDivisors(X, Y) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to count the divisors
static int countDivisors(int n)
{
int count = 0;

// Note that this loop
// runs till square root
for (int i = 1; i <= Math.sqrt(n); i++)
{
    if (n % i == 0)
    {

        // If divisors are equal,
        // print only one
        if (n / i == i)
            count++;

        else // Otherwise print both
            count += 2;
    }
}

return count;
}

// Function to count the number
// with maximum divisors
static int MaximumDivisors(int X, int Y)
{
int maxDivisors = 0, result = 0;

// to store number of divisors
int[] arr = new int[Y - X + 1];

// Traverse from X to Y
for (int i = X; i <= Y; i++)
{

    // Count the number of divisors of i
    int Div = countDivisors(i);

    // Store the value of div in an array
    arr[i - X] = Div;

    // Update the value of maxDivisors
    maxDivisors = Math.max(Div, maxDivisors);

}

// Traverse the array
for (int i = 0; i < (Y - X + 1); i++)

    // Count the value equals
    // to maxDivisors
    if (arr[i] == maxDivisors)
        result++;

return result;
}

// Driver Code
public static void main(String[] args)
{
    int X = 1, Y = 10;

    // function call
    System.out.println(MaximumDivisors(X, Y));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# from math module import everything
from math import *

# Python 3 implementation of above approach

# Function to count the divisors
def countDivisors(n) :
    count = 0

    # Note that this loop runs till square root
    for i in range(1,int(sqrt(n)+1)) :
        if n % i == 0 :

            # If divisors are equal, print only one
            if n / i == i :
                count += 1

            # Otherwise print both
            else :
                count += 2

    return count

# Function to count the number with
# maximum divisors
def MaximumDivisors(X,Y) :
    result = 0
    maxDivisors = 0

    # create list to store number of divisors
    arr = []

    # initialize with 0 upto length Y-X+1
    for i in range(Y - X + 1) :
        arr.append(0)

    # Traverse from X to Y  
    for i in range(X,Y+1) :

        # Count the number of divisors of i
        Div = countDivisors(i)

        # Store the value of div in an array
        arr[i - X] = Div

        # Update the value of maxDivisors
        maxDivisors = max(Div,maxDivisors)

    # Traverse the array 
    for i in range (Y - X + 1) :

        # Count the value equals to maxDivisors
        if arr[i] == maxDivisors :
            result += 1

    return result

# Driver code
if __name__ == "__main__" :

    X, Y = 1, 10

    # function call
    print(MaximumDivisors(X,Y))
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to count the divisors
static int countDivisors(int n)
{
int count = 0;

// Note that this loop
// runs till square root
for (int i = 1; i <= Math.Sqrt(n); i++)
{
    if (n % i == 0)
    {

        // If divisors are equal,
        // print only one
        if (n / i == i)
            count++;

        else // Otherwise print both
            count += 2;
    }
}

return count;
}

// Function to count the number
// with maximum divisors
static int MaximumDivisors(int X, int Y)
{
int maxDivisors = 0, result = 0;

// to store number of divisors
int[] arr = new int[Y - X + 1];

// Traverse from X to Y
for (int i = X; i <= Y; i++)
{

    // Count the number of divisors of i
    int Div = countDivisors(i);

    // Store the value of div in an array
    arr[i - X] = Div;

    // Update the value of maxDivisors
    maxDivisors = Math.Max(Div, maxDivisors);

}

// Traverse the array
for (int i = 0; i < (Y - X + 1); i++)

    // Count the value equals
    // to maxDivisors
    if (arr[i] == maxDivisors)
        result++;

return result;
}

// Driver Code
public static void Main()
{
    int X = 1, Y = 10;

    // function call
    Console.Write(MaximumDivisors(X, Y));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to count the divisors
function countDivisors($n)
{
    $count = 0;

    // Note that this loop
    // runs till square root
    for ($i = 1; $i <= sqrt($n); $i++)
    {
        if ($n % $i == 0)
        {

            // If divisors are equal,
            // print only one
            if ($n / $i == $i)
                $count++;

            else // Otherwise print both
                $count += 2;
        }
    }

    return $count;
}

// Function to count the number
// with maximum divisors
function MaximumDivisors($X, $Y)
{
    $maxDivisors = PHP_INT_MIN;
    $result = 0;

    // to store number of divisors
    $arr = array_fill(0, ($Y - $X + 1), NULL);

    // Traverse from X to Y
    for ($i = $X; $i <= $Y; $i++)
    {

        // Count the number of divisors of i
        $Div = countDivisors($i);

        // Store the value of div in an array
        $arr[$i - $X] = $Div;

        // Update the value of maxDivisors
        $maxDivisors = max($Div, $maxDivisors);
    }

    // Traverse the array
    for ($i = 0; $i < ($Y - $X + 1); $i++)

        // Count the value equals to maxDivisors
        if ($arr[$i] == $maxDivisors)
            $result++;

    return $result;
}

// Driver Code
$X = 1;
$Y = 10;

// function call
echo MaximumDivisors($X, $Y)." ";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to count the divisors
function countDivisors(n)
{
    let count = 0;

    // Note that this loop
    // runs till square root
    for(let i = 1; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {

            // If divisors are equal,
            // print only one
            if (Math.floor(n / i) == i)
                count++;

            else

                // Otherwise print both
                count += 2;
        }
    }
    return count;
}

// Function to count the number
// with maximum divisors
function MaximumDivisors(X, Y)
{
    let maxDivisors = 0, result = 0;

    // To store number of divisors
    let arr = new Array(Y - X + 1);

    // Traverse from X to Y
    for(let i = X; i <= Y; i++)
    {

        // Count the number of divisors of i
        let Div = countDivisors(i);

        // Store the value of div in an array
        arr[i - X] = Div;

        // Update the value of maxDivisors
        maxDivisors = Math.max(Div, maxDivisors);
    }

    // Traverse the array
    for(let i = 0; i < (Y - X + 1); i++)

        // Count the value equals
        // to maxDivisors
        if (arr[i] == maxDivisors)
            result++;

    return result;
}

// Driver Code
let X = 1, Y = 10;

// Function call
document.write(MaximumDivisors(X, Y));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
3
```

**方法二:**

*   创建一个大小为 **Y-X+1** 的数组，以存储 arr[0]中 X 的除数，arr[1]中 X+1 的除数……最多为 Y
*   为了得到从 X 到 Y 的所有数的除数，运行两个循环(嵌套的)。
*   从 **1 到 sqrt(Y)** 运行一个外环。
*   运行一个从**第一个可分到 Y** 的内部循环。
*   First _ 整除是第一个可被 I 整除的数(外环)，大于或等于 x

这里先用[求最接近 n 且可被 m 除尽的数](https://www.geeksforgeeks.org/find-number-closest-n-divisible-m/)法计算 first _ 除尽。然后[找到数字](http://Find the number of divisors of each element.)的约数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the elements
// with maximum number of divisors
int MaximumDivisors(int X, int Y)
{
    // to store number of divisors
    int arr[Y - X + 1];

    // initialise with zero
    memset(arr, 0, sizeof(arr));

    // to store the maximum number of divisors
    int mx = INT_MIN;

    // to store required answer
    int cnt = 0;

    for (int i = 1; i * i <= Y; i++) {
        int sq = i * i;
        int first_divisible;

        // Find the first divisible number
        if ((X / i) * i >= X)
            first_divisible = (X / i) * i;
        else
            first_divisible = (X / i + 1) * i;

        // Count number of divisors
        for (int j = first_divisible; j <= Y; j += i) {
            if (j < sq)
                continue;
            else if (j == sq)
                arr[j - X]++;
            else
                arr[j - X] += 2;
        }
    }

    // Find number of elements with
    // maximum number of divisors
    for (int i = X; i <= Y; i++) {
        if (arr[i - X] > mx) {
            cnt = 1;
            mx = arr[i - X];
        }
        else if (arr[i - X] == mx)
            cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    int X = 1, Y = 10;
    cout << MaximumDivisors(X, Y) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to count the elements
// with maximum number of divisors
static int MaximumDivisors(int X, int Y)
{

// to store number of divisors
int[] arr = new int[Y - X + 1];

// initialise with zero
for(int i = 0; i < arr.length; i++)
    arr[i] = 0;

// to store the maximum
// number of divisors
int mx = 0;

// to store required answer
int cnt = 0;

for (int i = 1; i * i <= Y; i++)
{
    int sq = i * i;
    int first_divisible;

    // Find the first divisible number
    if ((X / i) * i >= X)
        first_divisible = (X / i) * i;
    else
        first_divisible = (X / i + 1) * i;

    // Count number of divisors
    for (int j = first_divisible;
             j <= Y; j += i)
    {
        if (j < sq)
            continue;
        else if (j == sq)
            arr[j - X]++;
        else
            arr[j - X] += 2;
    }
}

// Find number of elements with
// maximum number of divisors
for (int i = X; i <= Y; i++)
{
    if (arr[i - X] > mx)
    {
        cnt = 1;
        mx = arr[i - X];
    }
    else if (arr[i - X] == mx)
        cnt++;
}

return cnt;
}

// Driver code
public static void main(String[] args)
{
    int X = 1, Y = 10;
    System.out.println(MaximumDivisors(X, Y));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to count the elements
# with maximum number of divisors
def MaximumDivisors(X, Y):

    # to store number of divisors
    # initialise with zero
    arr = [0] * (Y - X + 1)

    # to store the maximum
    # number of divisors
    mx = 0

    # to store required answer
    cnt = 0

    i = 1
    while i * i <= Y :
        sq = i * i

        # Find the first divisible number
        if ((X // i) * i >= X) :
            first_divisible = (X // i) * i
        else:
            first_divisible = (X // i + 1) * i

        # Count number of divisors
        for j in range(first_divisible, Y + 1, i):
            if j < sq :
                continue
            elif j == sq :
                arr[j - X] += 1
            else:
                arr[j - X] += 2
        i += 1

    # Find number of elements with
    # maximum number of divisors
    for i in range(X, Y + 1):
        if arr[i - X] > mx :
            cnt = 1
            mx = arr[i - X]

        elif arr[i - X] == mx :
            cnt += 1

    return cnt

# Driver code
if __name__ == "__main__":
    X = 1
    Y = 10
    print(MaximumDivisors(X, Y))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to count the elements
// with maximum number of divisors
static int MaximumDivisors(int X, int Y)
{

// to store number of divisors
int[] arr = new int[Y - X + 1];

// initialise with zero
for(int i = 0; i < arr.Length; i++)
    arr[i] = 0;

// to store the maximum
// number of divisors
int mx = 0;

// to store required answer
int cnt = 0;

for (int i = 1; i * i <= Y; i++)
{
    int sq = i * i;
    int first_divisible;

    // Find the first divisible number
    if ((X / i) * i >= X)
        first_divisible = (X / i) * i;
    else
        first_divisible = (X / i + 1) * i;

    // Count number of divisors
    for (int j = first_divisible;
             j <= Y; j += i)
    {
        if (j < sq)
            continue;
        else if (j == sq)
            arr[j - X]++;
        else
            arr[j - X] += 2;
    }
}

// Find number of elements with
// maximum number of divisors
for (int i = X; i <= Y; i++)
{
    if (arr[i - X] > mx)
    {
        cnt = 1;
        mx = arr[i - X];
    }
    else if (arr[i - X] == mx)
        cnt++;
}

return cnt;
}

// Driver code
public static void Main()
{
    int X = 1, Y = 10;
    Console.Write(MaximumDivisors(X, Y));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to count the elements
// with maximum number of divisors
function MaximumDivisors($X, $Y)
{
    // to store number of divisors
    // initialise with zero
    $arr = array_fill(0,($Y - $X + 1), NULL);

    // to store the maximum
    // number of divisors
    $mx = PHP_INT_MIN;

    // to store required answer
    $cnt = 0;

    for ($i = 1; $i * $i <= $Y; $i++)
    {
        $sq = $i * $i;

        // Find the first divisible number
        if (($X / $i) * $i >= $X)
            $first_divisible = ($X / $i) * $i;
        else
            $first_divisible = ($X / $i + 1) * $i;

        // Count number of divisors
        for ($j = $first_divisible;
             $j < $Y; $j += $i)
        {
            if ($j < $sq)
                continue;
            else if ($j == $sq)
                $arr[$j - $X]++;
            else
                $arr[$j - $X] += 2;
        }
    }

    // Find number of elements with
    // maximum number of divisors
    for ($i = $X; $i <= $Y; $i++)
    {
        if ($arr[$i - $X] > $mx) 
        {
            $cnt = 1;
            $mx = $arr[$i - $X];
        }
        else if ($arr[$i - $X] == $mx)
            $cnt++;
    }

    return $cnt;
}

// Driver code
$X = 1;
$Y = 10;
echo MaximumDivisors($X, $Y)."\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to count the elements
// with maximum number of divisors
function MaximumDivisors(X, Y)
{

    // To store number of divisors
    let arr = new Array(Y - X + 1);

    // Initialise with zero
    for(let i = 0; i < arr.length; i++)
        arr[i] = 0;

    // To store the maximum
    // number of divisors
    let mx = 0;

    // To store required answer
    let cnt = 0;

    for(let i = 1; i * i <= Y; i++)
    {
        let sq = i * i;
        let first_divisible;

        // Find the first divisible number
        if (Math.floor(X / i) * i >= X)
            first_divisible = Math.floor(X / i) * i;
        else
            first_divisible = (Math.floor(X / i) +
                                         1) * i;

        // Count number of divisors
        for(let j = first_divisible;
                j <= Y; j += i)
        {
            if (j < sq)
                continue;
            else if (j == sq)
                arr[j - X]++;
            else
                arr[j - X] += 2;
        }
    }

    // Find number of elements with
    // maximum number of divisors
    for(let i = X; i <= Y; i++)
    {
        if (arr[i - X] > mx)
        {
            cnt = 1;
            mx = arr[i - X];
        }
        else if (arr[i - X] == mx)
            cnt++;
    }
    return cnt;
}

// Driver code
let X = 1, Y = 10;

document.write(MaximumDivisors(X, Y));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```