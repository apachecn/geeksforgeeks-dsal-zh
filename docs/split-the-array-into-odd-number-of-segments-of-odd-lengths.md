# 将数组拆分成奇数个奇数长度的段

> 原文:[https://www . geeksforgeeks . org/将数组拆分成奇数个奇数长度的段/](https://www.geeksforgeeks.org/split-the-array-into-odd-number-of-segments-of-odd-lengths/)

给定一个长度为 n 的数组。任务是检查给定的数组是否可以拆分成奇数个以奇数开头的子段，并且子段的长度必须是奇数。如果可能，打印“1”，否则打印“0”。

**示例:**

```
Input: arr[] = {1, 3, 1}
Output: 1
1, 3, 1, can be split into 3 sub-segments of length odd i.e. 1
with starting and ending elements as odd.

Input: arr[] = {1, 3, 1, 1}
Output: 0
```

## [<u>推荐:请先在</u>***<u>{ IDE }</u>***<u>上尝试你的方法，然后再进入解决方案。</u>](https://ide.geeksforgeeks.org/)

**进场:**
分阶段思考后再进行实际解决:

*   将偶数个奇数阶的集合相加得到的集合的顺序总是偶数，反之亦然。
*   用奇数相加得到的集合的顺序总是奇数，反之亦然。

利用数论的上述引理，可以用下面提出的逻辑很容易地计算出给定问题的解:
如果给定的数组以奇数开始和结束，并且数组的大小也是奇数，那么只有给定的数组可以分解成奇数个子段，以奇数结束，否则不能。

下面是上述方法的实现:

## C++

```
// CPP to check whether given
// array is breakable or not
#include <bits/stdc++.h>
using namespace std;

// Function to check
bool checkArray(int arr[], int n)
{
    // Check the result by processing
    // the first & last element and size
    return (arr[0] % 2) && (arr[n - 1] % 2) && (n % 2);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << (int)checkArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to check whether given
// array is breakable or not

class GFG
{

// Function to check
static int checkArray(int []arr, int n)
{
    // Check the result by processing
    // the first & last element and size
    return ((arr[0] % 2) > 0 &&
            (arr[n - 1] % 2) > 0 &&
            (n % 2) > 0) ? 1 : 0;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.length;
    System.out.println(checkArray(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 to check whether given
# array is breakable or not

# Function to check
def checkArray(arr, n):

    # Check the result by processing
    # the first & last element and size
    return ((arr[0] % 2) and
            (arr[n - 1] % 2) and (n % 2))

# Driver code
arr = [1, 2, 3, 4, 5 ]
n = len(arr);
if checkArray(arr, n):
    print(1)
else:
    print(0)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# to check whether given
// array is breakable or not
using System;

class GFG
{

// Function to check
static int checkArray(int []arr, int n)
{
    // Check the result by processing
    // the first & last element and size
    return ((arr[0] % 2) > 0 &&
            (arr[n - 1] % 2) > 0 &&
               (n % 2) > 0) ? 1 : 0;
}

// Driver code
static void Main()
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;
    Console.WriteLine(checkArray(arr, n));

}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to check whether given
// array is breakable or not

// Function to check
function checkArray($arr, $n)
{
    // Check the result by processing
    // the first & last element and size
    return ($arr[0] % 2) &&
           ($arr[$n - 1] % 2) && ($n % 2);
}

// Driver code
$arr = array( 1, 2, 3, 4, 5 );
$n = sizeof($arr);
echo checkArray($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// javascript to check whether given
// array is breakable or not

// Function to check
function checkArray(arr,  n)
{
    // Check the result by processing
    // the first & last element and size
    return ((arr[0] % 2) > 0 &&
            (arr[n - 1] % 2) > 0 &&
               (n % 2) > 0) ? 1 : 0;
}

// Driver code

    var arr = [ 1, 2, 3, 4, 5 ];
    var n = arr.length;
    document.write(checkArray(arr, n));

</script>
```

**输出:**

```
1
```