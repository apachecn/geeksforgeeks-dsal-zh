# 数组最大和最小元素的最左和最右索引

> 原文:[https://www . geesforgeks . org/最左和最右数组元素索引/](https://www.geeksforgeeks.org/leftmost-and-rightmost-indices-of-the-maximum-and-the-minimum-element-of-an-array/)

给定一个数组 **arr[]** ，任务是从数组中找到最小和最大元素的最左边和最右边的索引，其中 **arr[]** 由非相异元素组成。
**例:**

> **输入:** arr[] = {2，1，1，2，1，5，6，5}
> **输出:**最小左:1
> 最小右:4
> 最大左:6
> 最大右:6
> 最小元素为 1，存在于索引 1、2 和 4 中。
> 最大元素为 6，仅出现在索引 6 处。
> **输入:** arr[] = {0，1，0，2，7，5，6，7}
> **输出:**最小左:0
> 最小右:2
> 最大左:4
> 最大右:7

**方法 1:** 当数组未排序时。

*   初始化变量**左最小=右最小=左最大=右最大= arr[0]** 和**最小=最大= arr[0]** 。
*   开始从 **1** 到**n–1**遍历数组。
    *   如果**停留【I】<分钟**，则找到一个新的最小值。更新**左最小=右最小= i** 。
    *   否则 **arr[i] = min** 则找到当前最小值的另一个副本。更新 **rightMin = i** 。
    *   如果**达到【I】>最大值**，则找到一个新的最大值。更新**左最大值=右最大值= i** 。
    *   否则 **arr[i] = max** 则找到当前最大值的另一个副本。更新 **rightMax = i** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include<bits/stdc++.h>
using namespace std;

void findIndices(int arr[], int n)
{
    int leftMin = 0, rightMin = 0;
    int leftMax = 0, rightMax = 0;

    int min = arr[0], max = arr[0];
    for (int i = 1; i < n; i++) {

        // If found new minimum
        if (arr[i] < min) {
            leftMin = rightMin = i;
            min = arr[i];
        }

        // If arr[i] = min then rightmost index
        // for min will change
        else if (arr[i] == min)
            rightMin = i;

        // If found new maximum
        if (arr[i] > max) {
            leftMax = rightMax = i;
            max = arr[i];
        }

        // If arr[i] = max then rightmost index
        // for max will change
        else if (arr[i] == max)
            rightMax = i;
    }

    cout << "Minimum left : " <<  leftMin << "\n";
    cout <<  "Minimum right : " << rightMin <<"\n";
    cout << "Maximum left : " <<  leftMax <<"\n";
    cout << "Maximum right : " << rightMax <<"\n";
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 1, 2, 1, 5, 6, 5 };
    int n = sizeof(arr)/sizeof(arr[0]);

    findIndices(arr, n);
}

// This code is contributed
// by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    public static void findIndices(int arr[], int n)
    {
        int leftMin = 0, rightMin = 0;
        int leftMax = 0, rightMax = 0;

        int min = arr[0], max = arr[0];
        for (int i = 1; i < n; i++) {

            // If found new minimum
            if (arr[i] < min) {
                leftMin = rightMin = i;
                min = arr[i];
            }

            // If arr[i] = min then rightmost index
            // for min will change
            else if (arr[i] == min)
                rightMin = i;

            // If found new maximum
            if (arr[i] > max) {
                leftMax = rightMax = i;
                max = arr[i];
            }

            // If arr[i] = max then rightmost index
            // for max will change
            else if (arr[i] == max)
                rightMax = i;
        }

        System.out.println("Minimum left : " + leftMin);
        System.out.println("Minimum right : " + rightMin);
        System.out.println("Maximum left : " + leftMax);
        System.out.println("Maximum right : " + rightMax);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 1, 1, 2, 1, 5, 6, 5 };
        int n = arr.length;

        findIndices(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

def findIndices(arr, n) :
    leftMin, rightMin = 0, 0
    leftMax, rightMax = 0, 0

    min_element = arr[0]
    max_element = arr[0]
    for i in range(n) :

        # If found new minimum
        if (arr[i] < min_element) :
            leftMin = rightMin = i
            min_element = arr[i]

        # If arr[i] = min then rightmost
        # index for min will change
        elif (arr[i] == min_element) :
            rightMin = i

        # If found new maximum
        if (arr[i] > max_element) :
            leftMax = rightMax = i
            max_element = arr[i]

        # If arr[i] = max then rightmost
        # index for max will change
        elif (arr[i] == max_element) :
            rightMax = i
    print("Minimum left : ", leftMin)
    print("Minimum right : ", rightMin)
    print("Maximum left : ", leftMax )
    print("Maximum right : ", rightMax)

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 1, 1, 2, 1, 5, 6, 5 ]
    n = len(arr)

    findIndices(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    static void findIndices(int []arr, int n)
    {
        int leftMin = 0, rightMin = 0;
        int leftMax = 0, rightMax = 0;

        int min = arr[0], max = arr[0];
        for (int i = 1; i < n; i++) {

            // If found new minimum
            if (arr[i] < min) {
                leftMin = rightMin = i;
                min = arr[i];
            }

            // If arr[i] = min then rightmost index
            // for min will change
            else if (arr[i] == min)
                rightMin = i;

            // If found new maximum
            if (arr[i] > max) {
                leftMax = rightMax = i;
                max = arr[i];
            }

            // If arr[i] = max then rightmost index
            // for max will change
            else if (arr[i] == max)
                rightMax = i;
        }

        Console.WriteLine("Minimum left : " + leftMin);
        Console.WriteLine("Minimum right : " + rightMin);
        Console.WriteLine("Maximum left : " + leftMax);
        Console.WriteLine("Maximum right : " + rightMax);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 1, 1, 2, 1, 5, 6, 5 };
        int n = arr.Length;

        findIndices(arr, n);
    }
}
// This code is contributed
// By ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
function findIndices($arr, $n)
{
    $leftMin = 0;
    $rightMin = 0;
    $leftMax = 0;
    $rightMax = 0;

    $min = $arr[0];
    $max = $arr[0];
    for ($i = 1; $i < $n; $i++)
    {

        // If found new minimum
        if ($arr[$i] < $min)
        {
            $leftMin = $rightMin = $i;
            $min = $arr[$i];
        }

        // If arr[i] = min then rightmost
        // index for min will change
        else if ($arr[$i] == $min)
            $rightMin = $i;

        // If found new maximum
        if ($arr[$i] > $max)
        {
            $leftMax = $rightMax = $i;
            $max = $arr[$i];
        }

        // If arr[i] = max then rightmost
        // index for max will change
        else if ($arr[$i] == $max)
            $rightMax = $i;
    }

    echo "Minimum left : ", $leftMin, "\n";
    echo "Minimum right : ", $rightMin,"\n";
    echo "Maximum left : ", $leftMax, "\n";
    echo "Maximum right : ", $rightMax, "\n";
}

// Driver code
$arr = array( 2, 1, 1, 2, 1, 5, 6, 5 );
$n = sizeof($arr);

findIndices($arr, $n);

// This code is contributed
// by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach   

    function findIndices(arr,n)
    {
        let leftMin = 0, rightMin = 0;
        let leftMax = 0, rightMax = 0;

        let min = arr[0], max = arr[0];
        for (let i = 1; i < n; i++) {

            // If found new minimum
            if (arr[i] < min) {
                leftMin = rightMin = i;
                min = arr[i];
            }

            // If arr[i] = min then rightmost index
            // for min will change
            else if (arr[i] == min)
                rightMin = i;

            // If found new maximum
            if (arr[i] > max) {
                leftMax = rightMax = i;
                max = arr[i];
            }

            // If arr[i] = max then rightmost index
            // for max will change
            else if (arr[i] == max)
                rightMax = i;
        }

        document.write("Minimum left : " + leftMin+"<br>");
        document.write("Minimum right : " + rightMin+"<br>");
        document.write("Maximum left : " + leftMax+"<br>");
        document.write("Maximum right : " + rightMax+"<br>");
    }
    // Driver code
    let arr=[2, 1, 1, 2, 1, 5, 6, 5 ];
    let n = arr.length;
    findIndices(arr, n);

    // This code is contributed by unknown2108

</script>
```

**Output:** 

```
Minimum left : 1
Minimum right : 4
Maximum left : 6
Maximum right : 6
```

**方法 2:** 数组排序时。

*   当数组排序后 **leftMin = 0** 和**right max = n–1**。
*   为了找到**右敏**，应用修改后的[二分搜索法](https://www.geeksforgeeks.org/binary-search/):
    *   设置 **i = 1** 。
    *   而 **arr[i] = min** 更新 **rightMin = i** 和 **i = i * 2** 。
    *   最后对从 **rightMin + 1** 到**n–1**的其余元素进行[线性搜索](https://www.geeksforgeeks.org/linear-search/)，同时 **arr[i] = min** 。
    *   最后返回 **rightMin** 。
*   类似地，对于 **leftMax** 重复上述步骤，但方向相反，即从**n–1**开始，并在每次迭代后更新 **i = i / 2** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of above idea
#include<bits/stdc++.h>
using namespace std;

// Function to return the index of the rightmost
// minimum element from the array
int getRightMin(int arr[], int n)
{

    // First element is the minimum in a sorted array
    int min = arr[0];
    int rightMin = 0;
    int i = 1;
    while (i < n) {

        // While the elements are equal to the minimum
        // update rightMin
        if (arr[i] == min)
            rightMin = i;

        i *= 2;
    }

    i = rightMin + 1;

    // Final check whether there are any elements
    // which are equal to the minimum
    while (i < n && arr[i] == min) {
        rightMin = i;
        i++;
    }

    return rightMin;
}

// Function to return the index of the leftmost
// maximum element from the array
 int getLeftMax(int arr[], int n)
{

    // Last element is the maximum in a sorted array
    int max = arr[n - 1];
    int leftMax = n - 1;
    int i = n - 2;
    while (i > 0) {

        // While the elements are equal to the maximum
        // update leftMax
        if (arr[i] == max)
            leftMax = i;

        i /= 2;
    }

    i = leftMax - 1;

    // Final check whether there are any elements
    // which are equal to the maximum
    while (i >= 0 && arr[i] == max) {
        leftMax = i;
        i--;
    }

    return leftMax;
}

// Driver code
int main()
{
    int arr[] = { 0, 0, 1, 2, 5, 5, 6, 8, 8 };
    int n = sizeof(arr)/sizeof(arr[0]);

    // First element is the leftmost minimum in a sorted array
    cout << "Minimum left : " << 0 <<"\n";
    cout << "Minimum right : " << getRightMin(arr, n) << "\n";
    cout << "Maximum left : " << getLeftMax(arr, n) <<"\n";

    // Last element is the rightmost maximum in a sorted array
    cout << "Maximum right : " << (n - 1);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above idea
public class GFG {

    // Function to return the index of the rightmost
    // minimum element from the array
    public static int getRightMin(int arr[], int n)
    {

        // First element is the minimum in a sorted array
        int min = arr[0];
        int rightMin = 0;
        int i = 1;
        while (i < n) {

            // While the elements are equal to the minimum
            // update rightMin
            if (arr[i] == min)
                rightMin = i;

            i *= 2;
        }

        i = rightMin + 1;

        // Final check whether there are any elements
        // which are equal to the minimum
        while (i < n && arr[i] == min) {
            rightMin = i;
            i++;
        }

        return rightMin;
    }

    // Function to return the index of the leftmost
    // maximum element from the array
    public static int getLeftMax(int arr[], int n)
    {

        // Last element is the maximum in a sorted array
        int max = arr[n - 1];
        int leftMax = n - 1;
        int i = n - 2;
        while (i > 0) {

            // While the elements are equal to the maximum
            // update leftMax
            if (arr[i] == max)
                leftMax = i;

            i /= 2;
        }

        i = leftMax - 1;

        // Final check whether there are any elements
        // which are equal to the maximum
        while (i >= 0 && arr[i] == max) {
            leftMax = i;
            i--;
        }

        return leftMax;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 0, 0, 1, 2, 5, 5, 6, 8, 8 };
        int n = arr.length;

        // First element is the leftmost minimum in a sorted array
        System.out.println("Minimum left : " + 0);
        System.out.println("Minimum right : " + getRightMin(arr, n));
        System.out.println("Maximum left : " + getLeftMax(arr, n));

        // Last element is the rightmost maximum in a sorted array
        System.out.println("Maximum right : " + (n - 1));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above idea

# Function to return the index of the
# rightmost minimum element from the array
def getRightMin(arr, n):

    # First element is the minimum
    # in a sorted array
    min = arr[0]
    rightMin = 0
    i = 1
    while (i < n):

        # While the elements are equal to
        # the minimum update rightMin
        if (arr[i] == min):
            rightMin = i

        i *= 2

    i = rightMin + 1

    # Final check whether there are any
    # elements which are equal to the minimum
    while (i < n and arr[i] == min):
        rightMin = i
        i += 1

    return rightMin

# Function to return the index of the
# leftmost maximum element from the array
def getLeftMax(arr, n):

    # Last element is the maximum
    # in a sorted array
    max = arr[n - 1]
    leftMax = n - 1
    i = n - 2
    while (i > 0):

        # While the elements are equal to
        # the maximum update leftMax
        if (arr[i] == max):
            leftMax = i

        i = int(i / 2)

    i = leftMax - 1

    # Final check whether there are any
    # elements which are equal to the maximum
    while (i >= 0 and arr[i] == max):
        leftMax = i
        i -= 1

    return leftMax

# Driver code
if __name__ == '__main__':
    arr = [0, 0, 1, 2, 5, 5, 6, 8, 8]
    n = len(arr)

    # First element is the leftmost
    # minimum in a sorted array
    print("Minimum left :", 0)
    print("Minimum right :", getRightMin(arr, n))
    print("Maximum left :", getLeftMax(arr, n))

    # Last element is the rightmost maximum
    # in a sorted array
    print("Maximum right :", (n - 1))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above idea

using System;
public class GFG {

    // Function to return the index of the rightmost
    // minimum element from the array
    public static int getRightMin(int []arr, int n)
    {

        // First element is the minimum in a sorted array
        int min = arr[0];
        int rightMin = 0;
        int i = 1;
        while (i < n) {

            // While the elements are equal to the minimum
            // update rightMin
            if (arr[i] == min)
                rightMin = i;

            i *= 2;
        }

        i = rightMin + 1;

        // Final check whether there are any elements
        // which are equal to the minimum
        while (i < n && arr[i] == min) {
            rightMin = i;
            i++;
        }

        return rightMin;
    }

    // Function to return the index of the leftmost
    // maximum element from the array
    public static int getLeftMax(int []arr, int n)
    {

        // Last element is the maximum in a sorted array
        int max = arr[n - 1];
        int leftMax = n - 1;
        int i = n - 2;
        while (i > 0) {

            // While the elements are equal to the maximum
            // update leftMax
            if (arr[i] == max)
                leftMax = i;

            i /= 2;
        }

        i = leftMax - 1;

        // Final check whether there are any elements
        // which are equal to the maximum
        while (i >= 0 && arr[i] == max) {
            leftMax = i;
            i--;
        }

        return leftMax;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 0, 0, 1, 2, 5, 5, 6, 8, 8 };
        int n = arr.Length;

        // First element is the leftmost minimum in a sorted array
        Console.WriteLine("Minimum left : " + 0);
        Console.WriteLine("Minimum right : " + getRightMin(arr, n));
        Console.WriteLine("Maximum left : " + getLeftMax(arr, n));

        // Last element is the rightmost maximum in a sorted array
        Console.WriteLine("Maximum right : " + (n - 1));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above idea

// Function to return the index of the
// rightmost minimum element from the array
function getRightMin($arr, $n)
{

    // First element is the minimum
    // in a sorted array
    $min = $arr[0];
    $rightMin = 0;
    $i = 1;
    while ($i < $n)
    {

        // While the elements are equal to
        // the minimum update rightMin
        if ($arr[$i] == $min)
            $rightMin = $i;

        $i *= 2;
    }

    $i = $rightMin + 1;

    // Final check whether there are any
    // elements which are equal to the minimum
    while ($i < $n && $arr[$i] == $min)
    {
        $rightMin = $i;
        $i++;
    }

    return $rightMin;
}

// Function to return the index of the
// leftmost maximum element from the array
function getLeftMax($arr, $n)
{

    // Last element is the maximum in
    // a sorted array
    $max = $arr[$n - 1];
    $leftMax = $n - 1;
    $i = $n - 2;
    while ($i > 0)
    {

        // While the elements are equal to
        // the maximum update leftMax
        if ($arr[$i] == $max)
            $leftMax = $i;

        $i /= 2;
    }

    $i = $leftMax - 1;

    // Final check whether there are any
    // elements which are equal to the maximum
    while ($i >= 0 && $arr[$i] == $max)
    {
        $leftMax = $i;
        $i--;
    }

    return $leftMax;
}

// Driver code
$arr = array(0, 0, 1, 2, 5,
                5, 6, 8, 8 );
$n = sizeof($arr);

// First element is the leftmost
// minimum in a sorted array
echo "Minimum left : ", 0, "\n";
echo "Minimum right : ",
      getRightMin($arr, $n), "\n";
echo "Maximum left : ",
      getLeftMax($arr, $n), "\n";

// Last element is the rightmost
// maximum in a sorted array
echo "Maximum right : ", ($n - 1), "\n";

// This code is Contributed
// by Mukul singh
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above idea

    // Function to return the index of the rightmost
    // minimum element from the array
    function getRightMin(arr, n)
    {

        // First element is the minimum in a sorted array
        let min = arr[0];
        let rightMin = 0;
        let i = 1;
        while (i < n) {

            // While the elements are equal to the minimum
            // update rightMin
            if (arr[i] == min)
                rightMin = i;

            i *= 2;
        }

        i = rightMin + 1;

        // Final check whether there are any elements
        // which are equal to the minimum
        while (i < n && arr[i] == min) {
            rightMin = i;
            i++;
        }

        return rightMin;
    }

    // Function to return the index of the leftmost
    // maximum element from the array
    function getLeftMax(arr, n)
    {

        // Last element is the maximum in a sorted array
        let max = arr[n - 1];
        let leftMax = n - 1;
        let i = n - 2;
        while (i > 0) {

            // While the elements are equal to the maximum
            // update leftMax
            if (arr[i] == max)
                leftMax = i;

            i = parseInt(i / 2, 10);
        }

        i = leftMax - 1;

        // Final check whether there are any elements
        // which are equal to the maximum
        while (i >= 0 && arr[i] == max) {
            leftMax = i;
            i--;
        }

        return leftMax;
    }

    let arr = [ 0, 0, 1, 2, 5, 5, 6, 8, 8 ];
    let n = arr.length;

    // First element is the leftmost minimum in a sorted array
    document.write("Minimum left : " + 0 + "</br>");
    document.write("Minimum right : " + getRightMin(arr, n) + "</br>");
    document.write("Maximum left : " + getLeftMax(arr, n) + "</br>");

    // Last element is the rightmost maximum in a sorted array
    document.write("Maximum right : " + (n - 1));

     // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Minimum left : 0
Minimum right : 1
Maximum left : 7
Maximum right : 8
```