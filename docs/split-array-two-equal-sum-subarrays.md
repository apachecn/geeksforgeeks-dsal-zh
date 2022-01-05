# 将一个阵列分成两个相等的求和子阵列

> 原文:[https://www . geesforgeks . org/split-array-two-equal-sum-subarrays/](https://www.geeksforgeeks.org/split-array-two-equal-sum-subarrays/)

给定一个大于零的整数数组，找出是否有可能把它分成两个子数组(不需要重新排序元素)，这样两个子数组的和是相同的。打印两个子阵列。
**例:**

```
Input : Arr[] = { 1 , 2 , 3 , 4 , 5 , 5  }
Output :  { 1 2 3 4 } 
          { 5 , 5 }

Input : Arr[] = { 4, 1, 2, 3 }
Output : {4 1}
         {2 3}

Input : Arr[] = { 4, 3, 2, 1}
Output : Not Possible
```

问于:**脸书采访**T2】

一个**简单的解决方案**是运行两个循环来分割数组，并检查是否有可能将数组分割成两部分，使得第一部分的和等于第二部分的和。
下面是上面想法的实现。

## C++

```
// C++ program to split an array into Two
// equal sum subarrays
#include<bits/stdc++.h>
using namespace std;

// Returns split point. If not possible, then
// return -1.
int findSplitPoint(int arr[], int n)
{
    int leftSum = 0 ;

    // traverse array element
    for (int i = 0; i < n; i++)
    {
        // add current element to left Sum
        leftSum += arr[i] ;

        // find sum of rest array elements (rightSum)
        int rightSum = 0 ;
        for (int j = i+1 ; j < n ; j++ )
            rightSum += arr[j] ;

        // split point index
        if (leftSum == rightSum)
            return i+1 ;
    }

    // if it is not possible to split array into
    // two parts
    return -1;
}

// Prints two parts after finding split point using
// findSplitPoint()
void printTwoParts(int arr[], int n)
{
    int splitPoint = findSplitPoint(arr, n);

    if (splitPoint == -1 || splitPoint == n )
    {
        cout << "Not Possible" <<endl;
        return;
    }
    for (int i = 0; i < n; i++)
    {
        if(splitPoint == i)
            cout << endl;
        cout << arr[i] << " " ;
    }
}

// driver program
int main()
{
    int arr[] = {1 , 2 , 3 , 4 , 5 , 5 };
    int n = sizeof(arr)/sizeof(arr[0]);
    printTwoParts(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split an array
// into two equal sum subarrays
import java.io.*;

class GFG {

    // Returns split point. If
    // not possible, then return -1.
    static int findSplitPoint(int arr[], int n)
    {

    int leftSum = 0 ;

    // traverse array element
    for (int i = 0; i < n; i++)
    {
        // add current element to left Sum
        leftSum += arr[i] ;

        // find sum of rest array
        // elements (rightSum)
        int rightSum = 0 ;

        for (int j = i+1 ; j < n ; j++ )
            rightSum += arr[j] ;

        // split point index
        if (leftSum == rightSum)
            return i+1 ;
    }

    // if it is not possible to
    // split array into two parts
    return -1;
    }  

    // Prints two parts after finding
    // split point using findSplitPoint()
    static void printTwoParts(int arr[], int n)
    {

        int splitPoint = findSplitPoint(arr, n);

        if (splitPoint == -1 || splitPoint == n )
        {
            System.out.println("Not Possible");
            return;
        }

        for (int i = 0; i < n; i++)
        {
            if(splitPoint == i)
               System.out.println();

            System.out.print(arr[i] + " ");

        }
    }

// Driver program

    public static void main (String[] args) {

    int arr[] = {1 , 2 , 3 , 4 , 5 , 5 };
    int n = arr.length;
    printTwoParts(arr, n);

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to split an array into Two
# equal sum subarrays

# Returns split point. If not possible, then
# return -1.
def findSplitPoint(arr, n) :

    leftSum = 0

    # traverse array element
    for i in range(0, n) :

        # add current element to left Sum
        leftSum += arr[i]

        # find sum of rest array elements (rightSum)
        rightSum = 0
        for j in range(i+1, n) :
            rightSum += arr[j]

        # split poindex
        if (leftSum == rightSum) :
            return i+1

    # if it is not possible to split array into
    # two parts
    return -1

# Prints two parts after finding split pousing
# findSplitPoint()
def printTwoParts(arr, n) :

    splitPo = findSplitPoint(arr, n)

    if (splitPo == -1 or splitPo == n ) :
        print ("Not Possible")
        return

    for i in range(0, n) :
        if(splitPo == i) :
            print ("")
        print (str(arr[i]) + ' ',end='')

# driver program
arr = [1 , 2 , 3 , 4 , 5 , 5]
n = len(arr)
printTwoParts(arr, n)

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to split an array
// into two equal sum subarrays
using System;

class GFG {

    // Returns split point. If
    // not possible, then return -1.
    static int findSplitPoint(int []arr, int n)
    {

        int leftSum = 0 ;

        // traverse array element
        for (int i = 0; i < n; i++)
        {

            // add current element to left Sum
            leftSum += arr[i] ;

            // find sum of rest array
            // elements (rightSum)
            int rightSum = 0 ;

            for (int j = i+1 ; j < n ; j++ )
                rightSum += arr[j] ;

            // split point index
            if (leftSum == rightSum)
                return i+1 ;
        }

        // if it is not possible to
        // split array into two parts
        return -1;
    }

    // Prints two parts after finding
    // split point using findSplitPoint()
    static void printTwoParts(int []arr, int n)
    {

        int splitPoint = findSplitPoint(arr, n);

        if (splitPoint == -1 || splitPoint == n )
        {
            Console.Write("Not Possible");
            return;
        }

        for (int i = 0; i < n; i++)
        {
            if(splitPoint == i)
            Console.WriteLine();

            Console.Write(arr[i] + " ");
        }
    }

    // Driver program
    public static void Main ()
    {
        int []arr = {1 , 2 , 3 , 4 , 5 , 5 };
        int n = arr.Length;
        printTwoParts(arr, n);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to split
// an array into Two
// equal sum subarrays

// Returns split point.
// If not possible, then
// return -1.
function findSplitPoint( $arr, $n)
{
    $leftSum = 0 ;

    // traverse array element
    for($i = 0; $i < $n; $i++)
    {

        // add current element
        // to left Sum
        $leftSum += $arr[$i] ;

        // find sum of rest array
        // elements (rightSum)
        $rightSum = 0 ;
        for($j = $i + 1 ; $j < $n ; $j++ )
            $rightSum += $arr[$j] ;

        // split point index
        if ($leftSum == $rightSum)
            return $i+1 ;
    }

    // if it is not possible
    // to split array into
    // two parts
    return -1;
}

// Prints two parts after
// finding split point using
// findSplitPoint()
function printTwoParts($arr, $n)
{
    $splitPoint = findSplitPoint($arr, $n);

    if ($splitPoint == -1 or $splitPoint == $n )
    {
        echo "Not Possible" ;
        return;
    }
    for ( $i = 0; $i < $n; $i++)
    {
        if($splitPoint == $i)
            echo "\n";
        echo $arr[$i] , " " ;
    }
}

    // Driver Code
    $arr = array(1 , 2 , 3 , 4 , 5 , 5);
    $n = count($arr);
    printTwoParts($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Java script program to split an array
// into two equal sum subarrays

    // Returns split point. If
    // not possible, then return -1.
    function findSplitPoint(arr,n)
    {

    let leftSum = 0 ;

    // traverse array element
    for (let i = 0; i < n; i++)
    {
        // add current element to left Sum
        leftSum += arr[i] ;

        // find sum of rest array
        // elements (rightSum)
        let rightSum = 0 ;

        for (let j = i+1 ; j < n ; j++ )
            rightSum += arr[j] ;

        // split point index
        if (leftSum == rightSum)
            return i+1 ;
    }

    // if it is not possible to
    // split array into two parts
    return -1;
    }

    // Prints two parts after finding
    // split point using findSplitPoint()
    function printTwoParts(arr,n)
    {

        let splitPoint = findSplitPoint(arr, n);

        if (splitPoint == -1 || splitPoint == n )
        {
            document.write("Not Possible");
            return;
        }

        for (let i = 0; i < n; i++)
        {
            if(splitPoint == i)
            document.write("<br>");

            document.write(arr[i] + " ");

        }
    }

// Driver program

    let arr = [1 , 2 , 3 , 4 , 5 , 5 ];
    let n = arr.length;
    printTwoParts(arr, n);

// contributed by sravan kumar
</script>
```

输出:

```
1 2 3 4
5 5 
```

时间复杂度:O(n)<sup>2</sup>)
辅助空间:O(1)
一个**高效的解决方案**是先从左到右计算整个数组的和。现在我们从右边遍历数组并跟踪右边的和，左边的和可以通过从整个和中减去当前元素来计算。
以下是以上思路的实现。

## C++

```
// C++ program to split an array into Two
// equal sum subarrays
#include<bits/stdc++.h>
using namespace std;

// Returns split point. If not possible, then
// return -1.
int findSplitPoint(int arr[], int n)
{
    // traverse array element and compute sum
    // of whole array
    int leftSum = 0;
    for (int i = 0 ; i < n ; i++)
        leftSum += arr[i];

    // again traverse array and compute right sum
    // and also check left_sum equal to right
    // sum or not
    int rightSum = 0;
    for (int i=n-1; i >= 0; i--)
    {
        // add current element to right_sum
        rightSum += arr[i];

        // exclude current element to the left_sum
        leftSum -=  arr[i] ;

        if (rightSum == leftSum)
            return i ;
    }

    // if it is not possible to split array
    // into two parts.
    return -1;
}

// Prints two parts after finding split point using
// findSplitPoint()
void printTwoParts(int arr[], int n)
{
    int splitPoint = findSplitPoint(arr, n);

    if (splitPoint == -1 || splitPoint == n )
    {
        cout << "Not Possible" <<endl;
        return;
    }
    for (int i = 0; i < n; i++)
    {
        if(splitPoint == i)
            cout << endl;
        cout << arr[i] << " " ;
    }
}

// driver program
int main()
{
    int arr[] = {1 , 2 , 3 , 4 , 5 , 5 };
    int n = sizeof(arr)/sizeof(arr[0]);
    printTwoParts(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to split an array
// into Two equal sum subarrays
import java.io.*;

class GFG {

    // Returns split point. If not possible, then
    // return -1.
    static int findSplitPoint(int arr[], int n)
    {

    // traverse array element and compute sum
    // of whole array
    int leftSum = 0;

    for (int i = 0 ; i < n ; i++)
        leftSum += arr[i];

    // again traverse array and compute right
    // sum and also check left_sum equal to
    // right sum or not
    int rightSum = 0;

    for (int i = n-1; i >= 0; i--)
    {
        // add current element to right_sum
        rightSum += arr[i];

        // exclude current element to the left_sum
        leftSum -= arr[i] ;

        if (rightSum == leftSum)
            return i ;
    }

    // if it is not possible to split array
    // into two parts.
    return -1;
    }

    // Prints two parts after finding split
    // point using findSplitPoint()
    static void printTwoParts(int arr[], int n)
    {
        int splitPoint = findSplitPoint(arr, n);

        if (splitPoint == -1 || splitPoint == n )
        {
            System.out.println("Not Possible" );
            return;
        }
        for (int i = 0; i < n; i++)
        {
            if(splitPoint == i)
                System.out.println();

            System.out.print(arr[i] + " ");
        }
    }

    // Driver program
    public static void main (String[] args) {

    int arr[] = {1 , 2 , 3 , 4 , 5 , 5 };
    int n = arr.length;

    printTwoParts(arr, n);

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to split
# an array into Two
# equal sum subarrays

# Returns split point.
# If not possible,
# then return -1.
def findSplitPoint(arr, n) :
    # traverse array element and
    # compute sum of whole array
    leftSum = 0
    for i in range(0, n) :
        leftSum += arr[i]

    # again traverse array and
    # compute right sum and also
    # check left_sum equal to
    # right sum or not
    rightSum = 0
    for i in range(n-1, -1, -1) :
        # add current element
        # to right_sum
        rightSum += arr[i]

        # exclude current element
        # to the left_sum
        leftSum -= arr[i]

        if (rightSum == leftSum) :
            return i

    # if it is not possible
    # to split array into
    # two parts.
    return -1

# Prints two parts after
# finding split point
# using findSplitPoint()
def printTwoParts(arr, n) :
    splitPoint = findSplitPoint(arr, n)

    if (splitPoint == -1 or splitPoint == n ) :
        print ("Not Possible")
        return

    for i in range (0, n) :
        if(splitPoint == i) :
            print ("")
        print (arr[i], end = " ")        

# Driver Code
arr = [1, 2, 3, 4, 5, 5]
n = len(arr)
printTwoParts(arr, n)

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to split an array
// into Two equal sum subarrays
using System;

class GFG {

    // Returns split point. If not possible, then
    // return -1.
    static int findSplitPoint(int []arr, int n)
    {

    // traverse array element and compute sum
    // of whole array
    int leftSum = 0;

    for (int i = 0 ; i < n ; i++)
        leftSum += arr[i];

    // again traverse array and compute right
    // sum and also check left_sum equal to
    // right sum or not
    int rightSum = 0;

    for (int i = n-1; i >= 0; i--)
    {
        // add current element to right_sum
        rightSum += arr[i];

        // exclude current element to the left_sum
        leftSum -= arr[i] ;

        if (rightSum == leftSum)
            return i ;
    }

    // if it is not possible to split array
    // into two parts.
    return -1;
    }

    // Prints two parts after finding split
    // point using findSplitPoint()
    static void printTwoParts(int []arr, int n)
    {
        int splitPoint = findSplitPoint(arr, n);

        if (splitPoint == -1 || splitPoint == n )
        {
            Console.Write("Not Possible" );
            return;
        }
        for (int i = 0; i < n; i++)
        {
            if(splitPoint == i)
                 Console.WriteLine();

             Console.Write(arr[i] + " ");
        }
    }

    // Driver program
    public static void Main (String[] args) {

    int []arr = {1 , 2 , 3 , 4 , 5 , 5 };
    int n = arr.Length;

    printTwoParts(arr, n);

    }
}

// This code is contributed by parashar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to split
// an array into Two
// equal sum subarrays

// Returns split point.
// If not possible,
// then return -1.
function findSplitPoint($arr, $n)
{
    // traverse array element and
    // compute sum of whole array
    $leftSum = 0;
    for ( $i = 0 ; $i < $n ; $i++)
        $leftSum += $arr[$i];

    // again traverse array and
    // compute right sum and also
    // check left_sum equal to
    // right sum or not
    $rightSum = 0;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        // add current element
        // to right_sum
        $rightSum += $arr[$i];

        // exclude current element
        // to the left_sum
        $leftSum -= $arr[$i] ;

        if ($rightSum == $leftSum)
            return $i ;
    }

    // if it is not possible
    // to split array into
    // two parts.
    return -1;
}

// Prints two parts after
// finding split point
// using findSplitPoint()
function printTwoParts( $arr, $n)
{
    $splitPoint = findSplitPoint($arr, $n);

    if ($splitPoint == -1 or
        $splitPoint == $n )
    {
        echo "Not Possible" ;
        return;
    }
    for ( $i = 0; $i < $n; $i++)
    {
        if($splitPoint == $i)
            echo "\n";
        echo $arr[$i] , " " ;
    }
}

// Driver Code
$arr = array(1, 2, 3, 4, 5, 5);
$n = count($arr);
printTwoParts($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to split an array
    // into Two equal sum subarrays

    // Returns split point. If not possible, then
    // return -1.
    function findSplitPoint(arr, n)
    {

      // traverse array element and compute sum
      // of whole array
      let leftSum = 0;

      for (let i = 0 ; i < n ; i++)
          leftSum += arr[i];

      // again traverse array and compute right
      // sum and also check left_sum equal to
      // right sum or not
      let rightSum = 0;

      for (let i = n-1; i >= 0; i--)
      {
          // add current element to right_sum
          rightSum += arr[i];

          // exclude current element to the left_sum
          leftSum -= arr[i] ;

          if (rightSum == leftSum)
              return i ;
      }

      // if it is not possible to split array
      // into two parts.
      return -1;
    }

    // Prints two parts after finding split
    // point using findSplitPoint()
    function printTwoParts(arr, n)
    {
        let splitPoint = findSplitPoint(arr, n);

        if (splitPoint == -1 || splitPoint == n )
        {
            document.write("Not Possible" );
            return;
        }
        for (let i = 0; i < n; i++)
        {
            if(splitPoint == i)
                 document.write("</br>");

             document.write(arr[i] + " ");
        }
    }

    let arr = [1 , 2 , 3 , 4 , 5 , 5 ];
    let n = arr.length;

    printTwoParts(arr, n);

 // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
1 2 3 4
5 5 
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。