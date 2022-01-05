# 将数组划分为三个相等的和段

> 原文:[https://www . geesforgeks . org/将数组划分为三个等份/](https://www.geeksforgeeks.org/partition-the-array-into-three-equal-sum-segments/)

给定一个 n 个整数的数组，我们必须把数组分成三段，这样所有的段都有相等的和。段总和是段中所有元素的总和。

**示例:**

```
Input :  1, 3, 6, 2, 7, 1, 2, 8
Output : [1, 3, 6], [2, 7, 1], [2, 8]

Input :  7, 6, 1, 7
Output :  [7], [6, 1], [7]

Input :  7, 6, 2, 7
Output : Cannot divide the array into segments 
```

一个**简单的解决方案**是考虑所有的索引对，对于每一对，检查它是否将数组分成三个相等的部分。如果是，那么返回真。这个解的时间复杂度为 O(n <sup>2</sup>

一种**有效的方法**是使用两个辅助数组，并将前缀和后缀数组和分别存储在这些数组中。然后我们使用双指针方法，变量' I '指向前缀数组的开始，变量' j '指向后缀数组的结束。如果 pre[i] > suf[j]，则递减' j '，否则递增' I '。
我们维护一个变量，它的值是数组的总和，每当我们遇到 pre[i] = total_sum / 3 或 suf[j] = total_sum / 3 时，我们将 I 或 j 的值分别存储为段边界。

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// First segment's end index
static int pos1 = -1;

// Third segment's start index
static int pos2 = -1;

// This function returns true if the array
// can be divided into three equal sum segments
bool equiSumUtil(int arr[],int n)
{

    // Prefix Sum Array
    int pre[n];
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum += arr[i];
        pre[i] = sum;
    }

    // Suffix Sum Array
    int suf[n];
    sum = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        sum += arr[i];
        suf[i] = sum;
    }

    // Stores the total sum of the array
    int total_sum = sum;

    int i = 0, j = n - 1;
    while (i < j - 1)
    {

        if (pre[i] == total_sum / 3)
        {
                pos1 = i;
        }

        if (suf[j] == total_sum / 3)
        {
            pos2 = j;
        }

        if (pos1 != -1 && pos2 != -1)
        {

            // We can also take pre[pos2 - 1] - pre[pos1] ==
            // total_sum / 3 here.
            if (suf[pos1 + 1] - suf[pos2] == total_sum / 3)
            {
                return true;
            }
            else
            {
                return false;
            }
        }

        if (pre[i] < suf[j])
        {
            i++;
        }
        else
        {
            j--;
        }
    }

    return false;
}

void equiSum(int arr[],int n)
{
    bool ans = equiSumUtil(arr,n);
    if (ans)
    {

        cout << "First Segment : ";
        for (int i = 0; i <= pos1; i++)
        {
            cout << arr[i] << " ";
        }

        cout << endl;

        cout << "Second Segment : ";
        for (int i = pos1 + 1; i < pos2; i++)
        {
            cout << arr[i] << " ";
        }

        cout << endl;

        cout << "Third Segment : ";
        for (int i = pos2; i < n; i++)
        {
            cout << arr[i] << " ";
        }

        cout<<endl;
    }
    else
    {
        cout << "Array cannot be divided into three equal sum segments";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 6, 2, 7, 1, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    equiSum(arr,n);
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class Main {

    //  First segment's end index
    public static int pos1 = -1;

    //  Third segment's start index
    public static int pos2 = -1;

    // This function returns true if the array
    // can be divided into three equal sum segments
    public static boolean equiSumUtil(int[] arr)
    {
        int n = arr.length;

        // Prefix Sum Array
        int[] pre = new int[n];
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            pre[i] = sum;
        }

        // Suffix Sum Array
        int[] suf = new int[n];
        sum = 0;
        for (int i = n - 1; i >= 0; i--) {
            sum += arr[i];
            suf[i] = sum;
        }

        // Stores the total sum of the array
        int total_sum = sum;

        int i = 0, j = n - 1;
        while (i < j - 1) {

            if (pre[i] == total_sum / 3) {
                pos1 = i;
            }

            if (suf[j] == total_sum / 3) {
                pos2 = j;
            }

            if (pos1 != -1 && pos2 != -1) {

                // We can also take pre[pos2 - 1] - pre[pos1] ==
                // total_sum / 3 here.
                if (suf[pos1 + 1] - suf[pos2] == total_sum / 3) {
                    return true;
                }
                else {
                    return false;
                }
            }

            if (pre[i] < suf[j]) {
                i++;
            }
            else {
                j--;
            }
        }

        return false;
    }

    public static void equiSum(int[] arr)
    {
        boolean ans = equiSumUtil(arr);
        if (ans) {

            System.out.print("First Segment : ");
            for (int i = 0; i <= pos1; i++) {
                System.out.print(arr[i] + " ");
            }

            System.out.println();

            System.out.print("Second Segment : ");
            for (int i = pos1 + 1; i < pos2; i++) {
                System.out.print(arr[i] + " ");
            }

            System.out.println();

            System.out.print("Third Segment : ");
            for (int i = pos2; i < arr.length; i++) {
                System.out.print(arr[i] + " ");
            }

            System.out.println();
        }
        else {
            System.out.println("Array cannot be " +
            "divided into three equal sum segments");
        }
    }
    public static void main(String[] args)
    {
        int[] arr = { 1, 3, 6, 2, 7, 1, 2, 8 };
        equiSum(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the given approach

# This function returns true if the array
# can be divided into three equal sum segments
def equiSumUtil(arr, pos1, pos2):

    n = len(arr);

    # Prefix Sum Array
    pre = [0] * n;
    sum = 0;
    for i in range(n):
        sum += arr[i];
        pre[i] = sum;

    # Suffix Sum Array
    suf = [0] * n;
    sum = 0;
    for i in range(n - 1, -1, -1):
        sum += arr[i];
        suf[i] = sum;

    # Stores the total sum of the array
    total_sum = sum;

    i = 0;
    j = n - 1;
    while (i < j - 1):

        if (pre[i] == total_sum // 3):
            pos1 = i;

        if (suf[j] == total_sum // 3):
            pos2 = j;

        if (pos1 != -1 and pos2 != -1):

            # We can also take pre[pos2 - 1] - pre[pos1] ==
            # total_sum / 3 here.
            if (suf[pos1 + 1] -
                suf[pos2] == total_sum // 3):
                return [True, pos1, pos2];
            else:
                return [False, pos1, pos2];

        if (pre[i] < suf[j]):
            i += 1;
        else:
            j -= 1;

    return [False, pos1, pos2];

def equiSum(arr):

    pos1 = -1;
    pos2 = -1;
    ans = equiSumUtil(arr, pos1, pos2);
    pos1 = ans[1];
    pos2 = ans[2];
    if (ans[0]):
        print("First Segment : ", end = "");
        for i in range(pos1 + 1):
            print(arr[i], end = " ");

        print("");

        print("Second Segment : ", end = "");
        for i in range(pos1 + 1, pos2):
            print(arr[i], end = " ");

        print("");

        print("Third Segment : ", end = "");
        for i in range(pos2, len(arr)):
            print(arr[i], end = " ");

        print("");
    else:
        println("Array cannot be divided into",
                "three equal sum segments");

# Driver Code
arr = [1, 3, 6, 2, 7, 1, 2, 8 ];
equiSum(arr);

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // First segment's end index
    public static int pos1 = -1;

    // Third segment's start index
    public static int pos2 = -1;

    // This function returns true if the array
    // can be divided into three equal sum segments
    public static bool equiSumUtil(int[] arr)
    {
        int n = arr.Length;

        // Prefix Sum Array
        int[] pre = new int[n];
        int sum = 0,i;
        for (i = 0; i < n; i++)
        {
            sum += arr[i];
            pre[i] = sum;
        }

        // Suffix Sum Array
        int[] suf = new int[n];
        sum = 0;
        for (i = n - 1; i >= 0; i--)
        {
            sum += arr[i];
            suf[i] = sum;
        }

        // Stores the total sum of the array
        int total_sum = sum;

        int j = n - 1;
        i = 0;
        while (i < j - 1)
        {

            if (pre[i] == total_sum / 3)
            {
                pos1 = i;
            }

            if (suf[j] == total_sum / 3)
            {
                pos2 = j;
            }

            if (pos1 != -1 && pos2 != -1)
            {

                // We can also take pre[pos2 - 1] - pre[pos1] ==
                // total_sum / 3 here.
                if (suf[pos1 + 1] - suf[pos2] == total_sum / 3)
                {
                    return true;
                }
                else
                {
                    return false;
                }
            }

            if (pre[i] < suf[j])
            {
                i++;
            }
            else
            {
                j--;
            }
        }

        return false;
    }

    public static void equiSum(int[] arr)
    {
        bool ans = equiSumUtil(arr);
        if (ans)
        {

            Console.Write("First Segment : ");
            for (int i = 0; i <= pos1; i++)
            {
                Console.Write(arr[i] + " ");
            }

            Console.WriteLine();

            Console.Write("Second Segment : ");
            for (int i = pos1 + 1; i < pos2; i++)
            {
                Console.Write(arr[i] + " ");
            }

            Console.WriteLine();

            Console.Write("Third Segment : ");
            for (int i = pos2; i < arr.Length; i++)
            {
                Console.Write(arr[i] + " ");
            }

            Console.WriteLine();
        }
        else
        {
            Console.WriteLine("Array cannot be " +
            "divided into three equal sum segments");
        }
    }
    public static void Main(String[] args)
    {
        int[] arr = { 1, 3, 6, 2, 7, 1, 2, 8 };
        equiSum(arr);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the given approach

// First segment's end index
$pos1 = -1;

// Third segment's start index
$pos2 = -1;

// This function returns true if the array
// can be divided into three equal sum segments
function equiSumUtil($arr)
{
    global $pos2, $pos1;
    $n = count($arr);

    // Prefix Sum Array
    $pre = array_fill(0, $n, 0);
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $sum += $arr[$i];
        $pre[$i] = $sum;
    }

    // Suffix Sum Array
    $suf = array_fill(0, $n, 0);
    $sum = 0;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        $sum += $arr[$i];
        $suf[$i] = $sum;
    }

    // Stores the total sum of the array
    $total_sum = $sum;

    $i = 0;
    $j = $n - 1;
    while ($i < $j - 1)
    {

        if ($pre[$i] == $total_sum / 3)
        {
            $pos1 = $i;
        }

        if ($suf[$j] == $total_sum / 3)
        {
            $pos2 = $j;
        }

        if ($pos1 != -1 && $pos2 != -1)
        {

            // We can also take pre[pos2 - 1] - pre[pos1] ==
            // total_sum / 3 here.
            if ($suf[$pos1 + 1] -
                     $suf[$pos2] == $total_sum / 3)
            {
                return true;
            }
            else
            {
                return false;
            }
        }

        if ($pre[$i] < $suf[$j])
        {
            $i++;
        }
        else
        {
            $j--;
        }
    }

    return false;
}

function equiSum($arr)
{
    global $pos2,$pos1;
    $ans = equiSumUtil($arr);
    if ($ans)
    {

        print("First Segment : ");
        for ($i = 0; $i <= $pos1; $i++)
        {
            print($arr[$i] . " ");
        }

        print("\n");

        print("Second Segment : ");
        for ($i = $pos1 + 1; $i < $pos2; $i++)
        {
            print($arr[$i] . " ");
        }

        print("\n");

        print("Third Segment : ");
        for ($i = $pos2; $i < count($arr); $i++)
        {
            print($arr[$i] . " ");
        }

        print("\n");
    }
    else
    {
        println("Array cannot be divided into ",
                "three equal sum segments");
    }
}

// Driver Code
$arr = array(1, 3, 6, 2, 7, 1, 2, 8 );
equiSum($arr);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// C# implementation of the approach

// First segment's end index
let pos1 = -1;

// Third segment's start index
let pos2 = -1;

// This function returns true if the array
// can be divided into three equal sum segments
function equiSumUtil(arr)
{
    let n = arr.length;

    // Prefix Sum Array
    let pre = new Array(n);
    let sum = 0,i;
    for (i = 0; i < n; i++)
    {
        sum += arr[i];
        pre[i] = sum;
    }

    // Suffix Sum Array
    let suf = new Array(n);
    sum = 0;
    for (i = n - 1; i >= 0; i--)
    {
        sum += arr[i];
        suf[i] = sum;
    }

    // Stores the total sum of the array
    let total_sum = sum;

    let j = n - 1;
    i = 0;
    while (i < j - 1)
    {

        if (pre[i] == total_sum / 3)
        {
            pos1 = i;
        }

        if (suf[j] == total_sum / 3)
        {
            pos2 = j;
        }

        if (pos1 != -1 && pos2 != -1)
        {

            // We can also take pre[pos2 - 1] - pre[pos1] ==
            // total_sum / 3 here.
            if (suf[pos1 + 1] - suf[pos2] == total_sum / 3)
            {
                return true;
            }
            else
            {
                return false;
            }
        }

        if (pre[i] < suf[j])
        {
            i++;
        }
        else
        {
            j--;
        }
    }

    return false;
}

function equiSum(arr)
{
    let ans = equiSumUtil(arr);
    if (ans)
    {

        document.write("First Segment : ");
        for (let i = 0; i <= pos1; i++)
        {
            document.write(arr[i] + " ");
        }

        document.write("<br>");

        document.write("Second Segment : ");
        for (let i = pos1 + 1; i < pos2; i++)
        {
            document.write(arr[i] + " ");
        }

        document.write("<br>");

        document.write("Third Segment : ");
        for (let i = pos2; i < arr.length; i++)
        {
            document.write(arr[i] + " ");
        }

        document.write("<br>");
    }
    else
    {
        document.writeLine("Array cannot be" +
        " divided into three equal sum segments");
    }
}

let arr =[1, 3, 6, 2, 7, 1, 2, 8];
equiSum(arr);

</script>
```

**Output:** 

```
First Segment : 1 3 6 
Second Segment : 2 7 1 
Third Segment : 2 8
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)