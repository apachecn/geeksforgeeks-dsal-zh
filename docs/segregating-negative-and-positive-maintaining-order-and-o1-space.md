# 分隔正负维持秩序和 O(1)空间

> 原文:[https://www . geeksforgeeks . org/separating-negative-和-positive-维持秩序-和-o1-space/](https://www.geeksforgeeks.org/segregating-negative-and-positive-maintaining-order-and-o1-space/)

在不使用额外空间的情况下分离数组中的负数和正数，并保持插入顺序和 O(n)时间复杂度。
**例:**

```
Input :9
       12 11 -13 -5 6 -7 5 -3 -6
Output :-13 -5 -7 -3 -6 12 11 6 5 

Input :5
       11 -13 6 -7 5
Output :-13 -7 11 6 5
```

我们已经在下面的帖子中讨论了这个问题。

1.  ers-开头-正结尾-常量-额外空间/" >在不维持顺序的情况下重新排列正数和负数。
2.  [用不变的额外空间重新排列正数和负数](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers/)

在这篇文章中，我们讨论了一种占用 0(1)个额外空间的新方法。我们首先计算负数总数，然后将负数一个接一个地移动到正确的位置。

## C++

```
// C++ program to move all negative numbers
// to beginning and positive numbers to end
// keeping order.
#include <iostream>
using namespace std;

void segregate(int arr[], int n)
{
    // Count negative numbers
    int count_negative = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] < 0)
            count_negative++;   

    // Run a loop until all negative
    // numbers are moved to the beginning
    int i = 0, j = i + 1;
    while (i != count_negative) {

        // If number is negative, update
        // position of next positive number.
        if (arr[i] < 0) {
            i++;
            j = i + 1;
        }

        // If number is positive, move it to
        // index j and increment j.
        else if (arr[i] > 0 && j < n) {
            swap(arr[i], arr[j]);
            j++;
        }
    }
}

int main()
{
    int count_negative = 0;
    int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    segregate(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to move all
// negative numbers to beginning
// and positive numbers to end
// keeping order.
class GFG
{
static void segregate(int arr[],
                      int n)
{

// Count negative numbers
int count_negative = 0;
for (int i = 0; i < n; i++)
    if (arr[i] < 0)
        count_negative++;

// Run a loop until all
// negative numbers are
// moved to the beginning
int i = 0, j = i + 1;
while (i != count_negative)
{

    // If number is negative,
    // update position of next
    // positive number.
    if (arr[i] < 0)
    {
        i++;
        j = i + 1;
    }

    // If number is positive, move
    // it to index j and increment j.
    else if (arr[i] > 0 && j < n)
    {
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
        j++;
    }
}
}

// Driver code
public static void main(String[] args)
{
    int count_negative = 0;
    int arr[] = { -12, 11, -13, -5,
                   6, -7, 5, -3, -6 };
    int n = arr.length;
    segregate(arr, n);
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
}

// This code is contributed
// by ChitraNayal
```

## C#

```
// C# program to move all
// negative numbers to beginning
// and positive numbers to end
// keeping order.
using System;

class GFG
{
static void segregate(int[] arr,
                      int n)
{

// Count negative numbers
int count_negative = 0,i;
for (i = 0; i < n; i++)
    if (arr[i] < 0)
        count_negative++;

// Run a loop until all
// negative numbers are
// moved to the beginning
i = 0;
int j = i + 1;
while (i != count_negative)
{

    // If number is negative,
    // update position of next
    // positive number.
    if (arr[i] < 0)
    {
        i++;
        j = i + 1;
    }

    // If number is positive, move
    // it to index j and increment j.
    else if (arr[i] > 0 && j < n)
    {
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
        j++;
    }
}
}

// Driver code
public static void Main()
{
    int[] arr = { -12, 11, -13, -5,
                    6, -7, 5, -3, -6 };
    int n = arr.Length;
    segregate(arr, n);
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to move all
# negative numbers to beginning
# and positive numbers to end
# keeping order.

def segregate(arr, n):

    # Count negative numbers
    count_negative = 0
    for i in range(n):
        if (arr[i] < 0):
            count_negative += 1

    # Run a loop until all
    # negative numbers are
    # moved to the beginning
    i = 0
    j = i + 1
    while (i != count_negative):

        # If number is negative,
        # update position of next
        # positive number.
        if (arr[i] < 0) :
            i += 1
            j = i + 1

        # If number is positive, move
        # it to index j and increment j.
        elif (arr[i] > 0 and j < n):
            t = arr[i]
            arr[i] = arr[j]
            arr[j] = t
            j += 1

# Driver Code
count_negative = 0
arr = [-12, 11, -13, -5,
        6, -7, 5, -3, -6 ]
segregate(arr, 9)
for i in range(9):
    print(arr[i] , end =" ")

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to move all
// negative numbers to
// beginning and positive
// numbers to end keeping order.

function segregate(&$arr, $n)
{
    // Count negative numbers
    $count_negative = 0;
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] < 0)
            $count_negative++;

    // Run a loop until all
    // negative numbers are
    // moved to the beginning
    $i = 0;
    $j = $i + 1;
    while ($i != $count_negative)
    {

        // If number is negative,
        // update position of next
        // positive number.
        if ($arr[$i] < 0)
        {
            $i++;
            $j = $i + 1;
        }

        // If number is positive, move
        // it to index j and increment j.
        else if ($arr[$i] > 0 && $j < $n)
        {
            $t = $arr[$i];
            $arr[$i] = $arr[$j];
            $arr[$j] = $t;
            $j++;
        }
    }
}

// Driver Code
$count_negative = 0;
$arr = array(-12, 11, -13, -5,
              6, -7, 5, -3, -6);
$n = sizeof($arr);
segregate($arr, $n);
for ($i = 0; $i < $n; $i++)
    echo $arr[$i] ." ";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// JavaScript program to move all negative numbers
// to beginning and positive numbers to end
// keeping order.
function segregate(arr, n)
{

    // Count negative numbers
    let count_negative = 0;
    for (let i = 0; i < n; i++)
        if (arr[i] < 0)
            count_negative++;   

    // Run a loop until all negative
    // numbers are moved to the beginning
    let i = 0, j = i + 1;
    while (i != count_negative) {

        // If number is negative, update
        // position of next positive number.
        if (arr[i] < 0) {
            i++;
            j = i + 1;
        }

        // If number is positive, move it to
        // index j and increment j.
        else if (arr[i] > 0 && j < n) {
            let t = arr[i];
            arr[i] = arr[j];
            arr[j] = t;
            j++;
        }
    }
}

    let count_negative = 0;
    let arr = [ -12, 11, -13, -5, 6, -7, 5, -3, -6 ];
    let n = arr.length;
    segregate(arr, n);
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
-12 -13 -5 -7 -3 -6 11 6 5 
```