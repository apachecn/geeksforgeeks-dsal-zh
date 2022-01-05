# 给定数组和 k 的| ai+aj–k |的最小可能值。

> 原文:[https://www . geesforgeks . org/最小可能值-ai-aj-k-给定-array-k/](https://www.geeksforgeeks.org/minimum-possible-value-ai-aj-k-given-array-k/)

给你一个由 n 个整数和一个整数 K 组成的数组，求总无序对{i，j}的个数，使得(ai+aj–K)的绝对值，即| ai+aj–K |在 I！= j.
**例:**

```
Input : arr[] = {0, 4, 6, 2, 4}, 
            K = 7
Output : Minimal Value = 1
         Total  Pairs = 5 
Explanation : Pairs resulting minimal value are :
              {a1, a3}, {a2, a4}, {a2, a5}, {a3, a4}, {a4, a5} 

Input : arr[] = {4, 6, 2, 4}  , K = 9
Output : Minimal Value = 1
         Total Pairs = 4 
Explanation : Pairs resulting minimal value are :
              {a1, a2}, {a1, a4}, {a2, a3}, {a2, a4} 
```

一个**简单的解决方案**是迭代所有可能的对，对于每一对，我们将检查(ai+aj–K)的值是否小于我们当前的最小值 not。因此，根据上述条件，我们总共有三种情况:

1.  *ABS(ai+aj–K)>最小*:不要做任何事情，因为这对不会计入最小可能值。
2.  *ABS(ai+aj–K)=最小*:增加配对计数，得到最小可能值。
3.  *ABS(ai+aj–K)<最小*:更新最小值，设置计数为 1。

## C++

```
// CPP program to find number of pairs  and minimal
// possible value
#include<bits/stdc++.h>
using namespace std;

// function for finding pairs and min value
void pairs(int arr[], int n, int k)
{
    // initialize smallest and count
    int smallest = INT_MAX;
    int count=0;

    // iterate over all pairs
    for (int i=0; i<n; i++)
        for(int j=i+1; j<n; j++)
        {
            // is abs value is smaller than smallest
            // update smallest and reset count to 1
            if ( abs(arr[i] + arr[j] - k) < smallest )
            {
                smallest = abs(arr[i] + arr[j] - k);
                count = 1;
            }

            // if abs value is equal to smallest
            // increment count value
            else if (abs(arr[i] + arr[j] - k) == smallest)
                count++;
        }

        // print result
        cout << "Minimal Value = " << smallest << "\n";
        cout << "Total Pairs = " << count << "\n";   
}

// driver program
int main()
{
    int arr[] = {3, 5, 7, 5, 1, 9, 9};
    int k = 12;
    int n = sizeof(arr) / sizeof(arr[0]);
    pairs(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of pairs
// and minimal possible value
import java.util.*;

class GFG {

    // function for finding pairs and min value
    static void pairs(int arr[], int n, int k)
    {
        // initialize smallest and count
        int smallest = Integer.MAX_VALUE;
        int count=0;

        // iterate over all pairs
        for (int i=0; i<n; i++)
            for(int j=i+1; j<n; j++)
            {
                // is abs value is smaller than
                // smallest update smallest and
                // reset count to 1
                if ( Math.abs(arr[i] + arr[j] - k) <
                                        smallest )
                {
                    smallest = Math.abs(arr[i] + arr[j]
                                             - k);
                    count = 1;
                }

                // if abs value is equal to smallest
                // increment count value
                else if (Math.abs(arr[i] + arr[j] - k)
                                    == smallest)
                    count++;
            }

            // print result
           System.out.println("Minimal Value = " +
                                    smallest);
           System.out.println("Total Pairs = " +
                                       count);   
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {3, 5, 7, 5, 1, 9, 9};
        int k = 12;
        int n = arr.length;
        pairs(arr, n, k);
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find number of pairs
# and minimal possible value

# function for finding pairs and min value
def pairs(arr, n, k):

    # initialize smallest and count
    smallest = 999999999999
    count = 0

    # iterate over all pairs
    for i in range(n):
        for j in range(i + 1, n):

            # is abs value is smaller than smallest
            # update smallest and reset count to 1
            if abs(arr[i] + arr[j] - k) < smallest:
                smallest = abs(arr[i] + arr[j] - k)
                count = 1

            # if abs value is equal to smallest
            # increment count value
            elif abs(arr[i] + arr[j] - k) == smallest:
                count += 1

    # print result
    print("Minimal Value = ", smallest)
    print("Total Pairs = ", count)

# Driver Code
if __name__ == '__main__':
    arr = [3, 5, 7, 5, 1, 9, 9]
    k = 12
    n = len(arr)
    pairs(arr, n, k)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find number
// of pairs and minimal
// possible value
using System;

class GFG
{

// function for finding
// pairs and min value
static void pairs(int []arr,
                  int n, int k)
{
    // initialize
    // smallest and count
    int smallest = 0;
    int count = 0;

    // iterate over all pairs
    for (int i = 0; i < n; i++)
        for(int j = i + 1; j < n; j++)
        {
            // is abs value is smaller
            // than smallest update
            // smallest and reset
            // count to 1
            if (Math.Abs(arr[i] +
                arr[j] - k) < smallest )
            {
                smallest = Math.Abs(arr[i] +
                                    arr[j] - k);
                count = 1;
            }

            // if abs value is equal
            // to smallest increment
            // count value
            else if (Math.Abs(arr[i] +
                              arr[j] - k) ==
                                smallest)
                count++;
        }

    // print result
    Console.WriteLine("Minimal Value = " +
                                smallest);
    Console.WriteLine("Total Pairs = " +
                                 count);
}

// Driver Code
public static void Main()
{
    int []arr = {3, 5, 7,
                 5, 1, 9, 9};
    int k = 12;
    int n = arr.Length;
    pairs(arr, n, k);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// pairs and minimal possible value

// function for finding pairs
// and min value
function pairs($arr, $n, $k)
{

    // initialize smallest and count
    $smallest = PHP_INT_MAX;
    $count = 0;

    // iterate over all pairs
    for ($i = 0; $i < $n; $i++)
        for($j = $i + 1; $j < $n; $j++)
        {

            // is abs value is smaller than smallest
            // update smallest and reset count to 1
            if ( abs($arr[$i] + $arr[$j] - $k) < $smallest )
            {
                $smallest = abs($arr[$i] + $arr[$j] - $k);
                $count = 1;
            }

            // if abs value is equal to smallest
            // increment count value
            else if (abs($arr[$i] +
                     $arr[$j] - $k) == $smallest)
                $count++;
        }

        // print result
        echo "Minimal Value = " , $smallest , "\n";
        echo "Total Pairs = ", $count , "\n";
}

    // Driver Code
    $arr = array (3, 5, 7, 5, 1, 9, 9);
    $k = 12;
    $n = sizeof($arr);
    pairs($arr, $n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of pairs  and minimal
// possible value

// function for finding pairs and min value
function pairs(arr, n, k)
{
    // initialize smallest and count
    var smallest = 1000000000;
    var count=0;

    // iterate over all pairs
    for (var i=0; i<n; i++)
        for(var j=i+1; j<n; j++)
        {
            // is Math.abs value is smaller than smallest
            // update smallest and reset count to 1
            if ( Math.abs(arr[i] + arr[j] - k) < smallest )
            {
                smallest = Math.abs(arr[i] + arr[j] - k);
                count = 1;
            }

            // if Math.abs value is equal to smallest
            // increment count value
            else if (Math.abs(arr[i] + arr[j] - k) == smallest)
                count++;
        }

        // print result
        document.write( "Minimal Value = " + smallest + "<br>");
        document.write( "Total Pairs = " + count + "<br>");   
}

// driver program
var arr = [3, 5, 7, 5, 1, 9, 9];
var k = 12;
var n = arr.length;
pairs(arr, n, k);

</script>
```

**输出:**

```
Minimal Value = 0
Total Pairs = 4
```

一个**有效的解决方案**是使用一个自平衡二叉查找树(在 C++的 set 和 Java 的 TreeSet 中实现)。我们可以在地图上找到 O(log n)时间内最接近的元素。

## C++

```
// C++ program to find number of pairs
// and minimal possible value
#include<bits/stdc++.h>
using namespace std;

// function for finding pairs and min value
void pairs(int arr[], int n, int k)
{
    // initialize smallest and count
    int smallest = INT_MAX, count = 0;
    set<int> s;

    // iterate over all pairs
    s.insert(arr[0]);
    for (int i=1; i<n; i++)
    {
        // Find the closest elements to  k - arr[i]
        int lower = *lower_bound(s.begin(),
                                 s.end(),
                                 k - arr[i]);

        int upper = *upper_bound(s.begin(),
                                 s.end(),
                                 k - arr[i]);

        // Find absolute value of the pairs formed
        // with closest greater and smaller elements.
        int curr_min = min(abs(lower + arr[i] - k),
                           abs(upper + arr[i] - k));

        // is abs value is smaller than smallest
        // update smallest and reset count to 1
        if (curr_min < smallest)
        {
            smallest = curr_min;
            count = 1;
        }

        // if abs value is equal to smallest
        // increment count value
        else if (curr_min == smallest )
            count++;
        s.insert(arr[i]);

    }        // print result

    cout << "Minimal Value = " << smallest <<"\n";
    cout << "Total Pairs = " << count <<"\n";
}

// driver program
int main()
{
    int arr[] = {3, 5, 7, 5, 1, 9, 9};
    int k = 12;
    int n = sizeof(arr) / sizeof(arr[0]);
    pairs(arr, n, k);
    return 0;
}
```

**输出:**

```
Minimal Value = 0
Total Pairs = 4
```

**时间复杂度:** O(n Log n)
本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。