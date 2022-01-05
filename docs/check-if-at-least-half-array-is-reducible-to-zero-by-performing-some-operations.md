# 通过执行一些操作

检查是否至少有一半数组可约为零

> 原文:[https://www . geeksforgeeks . org/check-如果通过执行某些操作至少可以将半数组还原为零/](https://www.geeksforgeeks.org/check-if-at-least-half-array-is-reducible-to-zero-by-performing-some-operations/)

给定 n 个正元素的数组。在每个操作中，您可以选择一些元素，并将它们减少 1，将剩余的元素增加 m。任务是确定在一些迭代之后，给定数组的至少一半元素是否可能等于零。
**例** :

```
Input : arr[] = {3, 5, 6, 8}, m = 2 
Output : Yes

Input : arr[] = {4, 7, 12, 13, 34},  m = 7
Output : No
```

如果我们试图分析问题陈述，我们会发现在任何一步，要么你把一个元素减少 1，要么增加 m。这意味着在执行的每一步中，如果我们比较两个元素，总共有三种可能性。
假设 a1 和 a2 是两个元素，那么:

1.  两个元素都减少了 1，因此它们的实际差值没有变化。
2.  这两个元素都增加了 m，因此它们的实际差值没有变化。
3.  一个元素减少了 1，另一个元素增加了 m，因此导致它们的实际差值发生了(m+1)的变化。

这意味着在每一步中，你都要保持任意两个元素之间的差相同或者增加(m+1)。
所以如果你取所有元素的模(m+1)并保持它的频率，我们可以检查在任何时间点有多少元素可以等于零。
**算法:**

*   创建大小为 m+1 的哈希表
*   将元素的频率捕获为(arr[i] % (m+1))，并存储在哈希表中。
*   找出最大频率，如果大于或等于 n/2，则答案为是，否则为否

以下是上述方法的实现:

## C++

```
// C++ program to find whether half-array
// reducible to 0
#include <bits/stdc++.h>
using namespace std;

// Function to print the desired
// result after computation
void isHalfReducible(int arr[], int n, int m)
{
    int frequencyHash[m + 1];
    int i;

    memset(frequencyHash, 0, sizeof(frequencyHash));
    for (i = 0; i < n; i++) {
        frequencyHash[arr[i] % (m + 1)]++;
    }

    for (i = 0; i <= m; i++) {
        if (frequencyHash[i] >= n / 2)
            break;
    }

    if (i <= m)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    int arr[] = { 8, 16, 32, 3, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int m = 7;

    isHalfReducible(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find whether half-array
// reducible to 0

public class GFG {

    // Function to print the desired
    // result after computation
    static void isHalfReducible(int arr[], int n, int m)
    {
        int frequencyHash[] = new int[m + 1];
        int i;

        for(i = 0 ; i < frequencyHash.length ; i++)
            frequencyHash[i] = 0 ;

        for (i = 0; i < n; i++) {
            frequencyHash[arr[i] % (m + 1)]++;
        }

        for (i = 0; i <= m; i++) {
            if (frequencyHash[i] >= n / 2)
                break;
        }

        if (i <= m)
            System.out.println("Yes") ;
        else
            System.out.println("No") ;
    }

// Driver code
    public static void main(String args[])
    {
            int arr[] = { 8, 16, 32, 3, 12 };
            int n = arr.length ;

            int m = 7;

            isHalfReducible(arr, n, m);

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to find whether
# half-array reducible to 0

# Function to print the desired
# result after computation
def isHalfReducible(arr, n, m):

    frequencyHash =[0]*(m + 1);
    i = 0;
    while(i < n):
        frequencyHash[(arr[i] % (m + 1))] += 1;
        i += 1;

    i = 0;
    while(i <= m):
        if(frequencyHash[i] >= (n / 2)):
            break;
        i += 1;

    if (i <= m):
        print("Yes");
    else:
        print("No");

# Driver Code
arr = [ 8, 16, 32, 3, 12 ];
n = len(arr);

m = 7;
isHalfReducible(arr, n, m);

# This code is contributed by mits
```

## C#

```
// C# Program to find whether half-array
// reducible to 0

using System;

public class GFG {

    // Function to print the desired
    // result after computation
    static void isHalfReducible(int[] arr, int n, int m)
    {
        int[] frequencyHash = new int[m + 1];
        int i;

        for(i = 0 ; i < frequencyHash.Length ; i++)
            frequencyHash[i] = 0 ;

        for (i = 0; i < n; i++) {
            frequencyHash[arr[i] % (m + 1)]++;
        }

        for (i = 0; i <= m; i++) {
            if (frequencyHash[i] >= n / 2)
                break;
        }

        if (i <= m)
            Console.WriteLine("Yes") ;
        else
            Console.WriteLine("No") ;
    }

// Driver code
    public static void Main()
    {
            int[] arr = { 8, 16, 32, 3, 12 };
            int n = arr.Length ;

            int m = 7;

            isHalfReducible(arr, n, m);

    }
    // This code is contributed by Subhadeep
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find whether 
// half-array reducible to 0

// Function to print the desired
// result after computation
function isHalfReducible($arr, $n, $m)
{
    $frequencyHash = array_fill(0, $m + 1, 0);
    $i = 0;
    for (;$i < $n; $i++)
    {
        $frequencyHash[($arr[$i] % ($m + 1))]++;
    }

    for ($i = 0; $i <= $m; $i++)
    {
        if ($frequencyHash[$i] >= ($n / 2))
            break;
    }

    if ($i <= $m)
        echo "Yes\n";
    else
        echo "No\n";
}

// Driver Code
$arr = array( 8, 16, 32, 3, 12 );
$n = sizeof($arr);

$m = 7;
isHalfReducible($arr, $n, $m);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find whether half-array
// reducible to 0

// Function to print the desired
// result after computation
function isHalfReducible(arr, n, m)
{
    var frequencyHash = Array(m+1).fill(0);
    var i;

    for (i = 0; i < n; i++) {
        frequencyHash[arr[i] % (m + 1)]++;
    }

    for (i = 0; i <= m; i++) {
        if (frequencyHash[i] >= n / 2)
            break;
    }

    if (i <= m)
        document.write( "Yes" );
    else
        document.write( "No" );
}

// Driver Code
var arr = [ 8, 16, 32, 3, 12 ];
var n = arr.length;
var m = 7;
isHalfReducible(arr, n, m);

</script>
```

**Output:** 

```
Yes
```