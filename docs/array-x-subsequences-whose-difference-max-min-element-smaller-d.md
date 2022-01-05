# 构建具有最大差值小于 d 的 X 个子序列的数组

> 原文:[https://www . geesforgeks . org/array-x-subseries-what-difference-max-min-element-small-d/](https://www.geeksforgeeks.org/array-x-subsequences-whose-difference-max-min-element-smaller-d/)

给定两个数字 X 和 d，其中 X 表示非空子序列的数量，d 表示差值。输出一个大小为 N 的数组，其非空子序列等于 X，其中每个子序列的最大元素和最小元素之差应小于 d

> **约束:**
> 1≤N≤500
> 1≤X≤10<sup>9</sup>

**示例:**

```
Input : X = 10, d = 5
Output : 5 50 7 15 6 100
"10" desired subsequences are: [5], [50], [7], 
[15], [6], [100], [5, 7], [5, 6], [7, 6], 
[5, 7, 6].

Input : X = 4, d = 10
Output : 10 100 1000 10000
"4" desired subsequences are: [10], [100], 
[1000], [10000].
```

**方法:**可以清楚地看到，如果 d = 5，那么数组[1，7]将只有 2 个期望的子序列([1]和[7]，而不是[1，7])。因此，类似地，如果我们在那个数组中添加许多 1 和许多 7，那么也不会接受 1 和 7 在一起的子序列。所以，差大于 d 的元素总是会形成不相交的集合。例如在[1，5，9，9，12，13]中，如果 d = 2，则有 4 个不相交的集合[1]，[5]，[9，9]，[12，13]。

大小为 N 的数组中非空子序列的总数等于![2^n   ](img/bb4628d02d6ec1a9b5db5e0bc5956f49.png "Rendered by QuickLaTeX.com") -1。因此，我们只需要找到子序列总数小于或等于 X 的不相交集的长度，并输出该不相交集的元素。如果它不等于 X，那么必须在约化的 X 上进行相同的步骤，以找到下一个不相交的集合，直到 X 变成 0。为了使所有集合不相交，一种方法是将第一个数组元素取为 1，然后在第一个不相交集合中加上等于这个不相交集合长度的 1，然后在前一个不相交集合中的元素上加上“d”以形成另一个不相交集合，以此类推。

> 例如:X = 25，d = 100
> 第一个不相交的集合将有 4 个元素，因为它有 15 个子序列。所以 1 <sup>st</sup> 不相交集将是{ 1，1，1，1 }。
> 现在 X 变成 10，因此第二个不相交集将只包含 3 个元素。So 2 <sup>nd</sup> 。不相交将是{ 101，101，101 }(通过在 1 中添加 100 使其与第一个集合不相交)。现在 X 变成 3，因此最终的不相交集将包含两个元素，3 <sup>rd</sup> 不相交集将是{ 201，201 }(再次在 101 中添加 100，使其与前面的两个集不相交)。
> 最终输出将是[1，1，1，1，101，101，101，201，201]。

下面是上述方法的实现。

## C++

```
// C++ Program to output an array having exactly X
// subsequences where difference between maximum
// and minimum element of each subsequence is less
// than d
#include <bits/stdc++.h>
using namespace std;

// This function outputs the desired array.
void printArray(int X, int d, int first_ele)
{
    // Iterate till all the disjoint sets are found.
    while (X > 0) {

        // count_ele the elements in one disjoint
        // set.  pow_of_two will keep all the
        // powers of twos.
        int count_ele = 0, pow_of_two = 2;

        // Iterate to know the maximum length of
        // disjoint set by checking whether X is
        // greater than the total number of
        // possible not empty sequences of that
        // disjoint set.
        while (X - pow_of_two + 1 >= 0) {
            count_ele++;
            pow_of_two *= 2;
        }

        // now deleting the total subsequences of
        // the maximum length disjoint set from X.
        X = X - (pow_of_two / 2) + 1;

        // outputting the disjoint set having equal
        // elements.
        for (int j = 0; j < count_ele; j++)
            cout << first_ele << " ";

        // by adding d, it makes another disjoint
        // set of equal elements.
        first_ele += d;
    }
}

// Driver Code
int main()
{
    int d = 100, X = 25;
    printArray(X, d, 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to output
// an array having exactly
// X subsequences where
// difference between maximum
// and minimum element of
// each subsequence is less
// than d
import java.io.*;

class GFG
{

// This function outputs
// the desired array.
static void printArray(int X, int d,
                       int first_ele)
{
    // Iterate till all the
    // disjoint sets are found.
    while (X > 0)
    {

        // count_ele the elements
        // in one disjoint set.
        // pow_of_two will keep
        // all the powers of twos.
        int count_ele = 0,
            pow_of_two = 2;

        // Iterate to know the
        // maximum length of
        // disjoint set by checking
        // whether X is greater than
        // the total number of possible
        // not empty sequences of that
        // disjoint set.
        while (X - pow_of_two + 1 >= 0)
        {
            count_ele++;
            pow_of_two *= 2;
        }

        // now deleting the total
        // subsequences of the maximum
        // length disjoint set from X.
        X = X - (pow_of_two / 2) + 1;

        // outputting the disjoint
        // set having equal elements.
        for (int j = 0;
                 j < count_ele; j++)
            System.out.print(first_ele + " ");

        // by adding d, it makes
        // another disjoint set
        // of equal elements.
        first_ele += d;
    }
}

// Driver Code
public static void main (String[] args)
{
    int d = 100, X = 25;
    printArray(X, d, 1);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to output an array having
# exactly X subsequences where difference
# between maximum and minimum element of each
# subsequence is less than d

# This function outputs the desired array.
def printArray(X, d, first_ele):

    # Iterate till all the disjoint
    # sets are found.
    while (X > 0):

        # count_ele the elements in one
        # disjoint set. pow_of_two will
        # keep all the powers of twos.
        count_ele, pow_of_two = 0, 2

        # Iterate to know the maximum length of
        # disjoint set by checking whether X is
        # greater than the total number of
        # possible not empty sequences of that
        # disjoint set.
        while (X - pow_of_two + 1 >= 0):
            count_ele += 1
            pow_of_two *= 2

        # now deleting the total subsequences of
        # the maximum length disjoint set from X.
        X = X - (pow_of_two / 2) + 1

        # outputting the disjoint set having
        # equal elements.
        for j in range(count_ele):
            print(first_ele, end = " ")

        # by adding d, it makes another
        # disjoint set of equal elements.
        first_ele += d

# Driver Code
if __name__ == '__main__':
    d, X = 100, 25
    printArray(X, d, 1)

# This code is contributed by PrinciRaj19992
```

## C#

```
// C# Program to output
// an array having exactly
// X subsequences where
// difference between maximum
// and minimum element of
// each subsequence is less
// than d
using System;

class GFG
{

// This function outputs
// the desired array.
static void printArray(int X, int d,
                       int first_ele)
{
    // Iterate till all the
    // disjoint sets are found.
    while (X > 0)
    {

        // count_ele the elements
        // in one disjoint set.
        // pow_of_two will keep
        // all the powers of twos.
        int count_ele = 0,
            pow_of_two = 2;

        // Iterate to know the
        // maximum length of
        // disjoint set by checking
        // whether X is greater than
        // the total number of possible
        // not empty sequences of that
        // disjoint set.
        while (X - pow_of_two + 1 >= 0)
        {
            count_ele++;
            pow_of_two *= 2;
        }

        // now deleting the total
        // subsequences of the maximum
        // length disjoint set from X.
        X = X - (pow_of_two / 2) + 1;

        // outputting the disjoint
        // set having equal elements.
        for (int j = 0;
                 j < count_ele; j++)
            Console.Write(first_ele + " ");

        // by adding d, it makes
        // another disjoint set
        // of equal elements.
        first_ele += d;
    }
}

// Driver Code
public static void Main ()
{
    int d = 100, X = 25;
    printArray(X, d, 1);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to output an array
// having exactly X subsequences
// where difference between maximum
// and minimum element of each 
// subsequence is less than d

// This function outputs the
// desired array.
function printArray($X, $d,$first_ele)
{
    // Iterate till all the disjoint
    // sets are found.
    while ($X > 0)
    {

        // count_ele the elements in
        // one disjoint set. pow_of_two
        // will keep all the powers of twos.
        $count_ele = 0;
        $pow_of_two = 2;

        // Iterate to know the maximum
        // length of disjoint set by
        // checking whether X is greater
        // than the total number of possible
        // not empty sequences of that
        // disjoint set.
        while ($X - $pow_of_two + 1 >= 0)
        {
            $count_ele++;
            $pow_of_two *= 2;
        }

        // now deleting the total subsequences of
        // the maximum length disjoint set from X.
        $X = $X - ($pow_of_two / 2) + 1;

        // outputting the disjoint set
        // having equal elements.
        for ($j = 0; $j < $count_ele; $j++)
                echo $first_ele , " ";

        // by adding d, it makes another
        // disjoint set of equal elements.
        $first_ele += $d;
    }
}

// Driver Code
$d = 100;
$X = 25;
printArray($X, $d, 1);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Program to output
    // an array having exactly
    // X subsequences where
    // difference between maximum
    // and minimum element of
    // each subsequence is less
    // than d

    // This function outputs
    // the desired array.
    function printArray(X, d, first_ele)
    {
        // Iterate till all the
        // disjoint sets are found.
        while (X > 0)
        {

            // count_ele the elements
            // in one disjoint set.
            // pow_of_two will keep
            // all the powers of twos.
            let count_ele = 0,
                pow_of_two = 2;

            // Iterate to know the
            // maximum length of
            // disjoint set by checking
            // whether X is greater than
            // the total number of possible
            // not empty sequences of that
            // disjoint set.
            while (X - pow_of_two + 1 >= 0)
            {
                count_ele++;
                pow_of_two *= 2;
            }

            // now deleting the total
            // subsequences of the maximum
            // length disjoint set from X.
            X = X - parseInt(pow_of_two / 2, 10) + 1;

            // outputting the disjoint
            // set having equal elements.
            for (let j = 0; j < count_ele; j++)
                document.write(first_ele + " ");

            // by adding d, it makes
            // another disjoint set
            // of equal elements.
            first_ele += d;
        }
    }

    let d = 100, X = 25;
    printArray(X, d, 1);

</script>
```

**Output:** 

```
1 1 1 1 101 101 101 201 201
```