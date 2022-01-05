# 检查数组任意子集的数字的按位“与”是否为零

> 原文:[https://www . geeksforgeeks . org/check-按位对数组的任何子集进行数的运算是否为零/](https://www.geeksforgeeks.org/check-whether-bitwise-and-of-a-number-with-any-subset-of-an-array-is-zero-or-not/)

给定一个数组和一个数字 N，任务是检查这个数组是否存在子集，使得这个子集与 N 的按位“与”为零。
**例** :

```
Input : arr[] = {1, 2, 4}  ;  N = 3
Output : YES
Explanation: The subsets are:
(1, 2 ), (1, 4), (1, 2, 4) 

Input : arr[] = {1, 1, 1}  ;  N = 3
Output : NO
```

一个**简单的方法**是找到数组所有子集的按位 and，检查任意子集的 N 的 AND 是否为零。
一种**有效方法**是观察任意两个数字的按位“与”将总是产生一个小于或等于较小数字的数字。所以我们的任务是找到具有按位“与”最小值的子集。如前所述，任何两个数的“与”将总是产生一个小于或等于最小数的数，因此“与”的最小值将是所有数组元素的“与”。因此，任务现在简化为检查所有数组元素和 N 的按位“与”，如果它为零，我们将打印“是”，否则打印“否”。
下面是上述方法的实现:

## C++

```
// C++ program to check whether bitwise AND of a number
// with any subset of an array is zero or not
#include <bits/stdc++.h>
using namespace std;

// Function to check whether bitwise AND of a number
// with any subset of an array is zero or not
void isSubsetAndZero(int array[], int length, int N)
{
    // variable to store the
    // AND of all the elements
    int arrAnd = array[0];

    // find the AND of all the elements
    // of the array
    for (int i = 1; i < length; i++) {
        arrAnd = arrAnd & array[i];
    }

    // if the AND of all the array elements
    // and N is equal to zero
    if ((arrAnd & N) == 0)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

// Driver Code
int main()
{
    int array[] = { 1, 2, 4 };
    int length = sizeof(array) / sizeof(int);

    int N = 3;

    isSubsetAndZero(array, length, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether bitwise AND of a number
// with any subset of an array is zero or not
import java.io.*;

public class GFG {

// Function to check whether bitwise AND of a number
// with any subset of an array is zero or not
static void isSubsetAndZero(int array[], int length, int N)
{
    // variable to store the
    // AND of all the elements
    int arrAnd = array[0];

    // find the AND of all the elements
    // of the array
    for (int i = 1; i < length; i++) {
        arrAnd = arrAnd & array[i];
    }

    // if the AND of all the array elements
    // and N is equal to zero
    if ((arrAnd & N) == 0)
        System.out.println( "YES");
    else
        System.out.println( "NO");
}

// Driver Code
    public static void main (String[] args) {
        int array[] = { 1, 2, 4 };
    int length = array.length;

    int N = 3;

    isSubsetAndZero(array, length, N);
    }
}
//This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 program to check whether
# bitwise AND of a number with any
# subset of an array is zero or not

# Function to check whether bitwise
# AND of a number with any subset
# of an array is zero or not
def isSubsetAndZero(array, length, N):

    # variable to store the
    # AND of all the elements
    arrAnd = array[0]

    # find the AND of all
    # the elements of the array
    for i in range(1, length) :
        arrAnd = arrAnd & array[i]

    # if the AND of all the array
    # elements and N is equal to zero
    if ((arrAnd & N) == 0):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == "__main__":
    array = [ 1, 2, 4 ]
    length = len(array)

    N = 3

    isSubsetAndZero(array, length, N)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to check whether
// bitwise AND of a number with
// any subset of an array is zero or not
using System;

class GFG
{

// Function to check whether bitwise
// AND of a number with any subset
// of an array is zero or not
static void isSubsetAndZero(int []array,
                            int length, int N)
{
    // variable to store the
    // AND of all the elements
    int arrAnd = array[0];

    // find the AND of all the
    // elements of the array
    for (int i = 1; i < length; i++)
    {
        arrAnd = arrAnd & array[i];
    }

    // if the AND of all the array
    // elements and N is equal to zero
    if ((arrAnd & N) == 0)
        Console.WriteLine( "YES");
    else
        Console.WriteLine( "NO");
}

// Driver Code
public static void Main ()
{
    int []array = { 1, 2, 4 };
    int length = array.Length;

    int N = 3;

    isSubsetAndZero(array, length, N);
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// bitwise AND of a number with
// any subset of an array is zero or not

// Function to check whether
// bitwise AND of a number with
// any subset of an array is zero or not
function isSubsetAndZero($array, $length, $N)
{
    // variable to store the
    // AND of all the elements
    $arrAnd = $array[0];

    // find the AND of all the
    // elements of the array
    for ($i = 1; $i <$length; $i++)
    {
        $arrAnd = $arrAnd & $array[$i];
    }

    // if the AND of all the array
    // elements and N is equal to zero
    if (($arrAnd & $N) == 0)
        echo("YES");
    else
        echo("NO");
}

// Driver Code
$array = array( 1, 2, 4 );
$length = count($array);

$N = 3;

isSubsetAndZero($array, $length, $N);

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check whether bitwise AND of a number
// with any subset of an array is zero or not
function isSubsetAndZero(array, len, N)
{
    // variable to store the
    // AND of all the elements
    var arrAnd = array[0];

    // find the AND of all the elements
    // of the array
    for (var i = 1; i < len; i++) {
        arrAnd = arrAnd & array[i];
    }

    // if the AND of all the array elements
    // and N is equal to zero
    if ((arrAnd & N) == 0)
        document.write("YES"+"<br>");
    else
        document.write("NO"+"<br>");
}

var array = [1, 2, 4 ];
var len = array.length;
var N = 3;
isSubsetAndZero(array, len, N);

// This code is contributed bby SoumikMondal

</script>
```

**Output:** 

```
YES
```