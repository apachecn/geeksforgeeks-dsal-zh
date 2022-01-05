# K 差排列

> 原文:[https://www.geeksforgeeks.org/k-difference-permutation/](https://www.geeksforgeeks.org/k-difference-permutation/)

给定两个整数 n 和 k。考虑自然数 n 的第一个排列，P =“1 2 3…n”，打印一个排列“结果”，使得 **abs(结果<sub>I</sub>–P<sub>I</sub>)= k**，其中 P <sub>i</sub> 表示 I 在排列 P 中的位置。P <sub>i</sub> 的值从 1 到 n 不等。如果有多个可能的结果，则打印字典上最小的一个。

```
Input: n = 6 k = 3
Output: 4 5 6 1 2 3
Explanation:
     P = 1 2 3 4 5 6
Result = 4 5 6 1 2 3
We can notice that the difference between
individual numbers (at same positions) of 
P and result is 3 and "4 5 6 1 2 3" is 
lexicographically smallest such permutation.
Other greater permutations could be 

Input  : n = 6 k = 2
Output : Not possible
Explanation: No permutation is possible 
with difference is k 
```

**朴素方法**是生成从 1 到 n 的所有排列，选出满足绝对差 k 条件的最小排列，该方法的时间复杂度为ω(n！)这对于大数值的 n.
肯定会超时**有效的方法**是观察指数每个位置的模式。对于索引 I 的每个位置，只能存在两个候选，即 i + k 和 I–k。由于我们需要找到字典上最小的排列，因此我们将首先寻找 I–k 候选(如果可能)，然后寻找 i + k 候选。

```
 Illustration:
 n = 8, k = 2
 P : 1 2 3 4 5 6 7 8

 For any i<sup>th position we will check which candidate</sup>
 <sup>is possible i.e., i + k or i - k</sup> 

 1st pos = 1 + 2 = 3 (1 - 2 not possible)
 2nd pos = 2 + 2 = 4 (2 - 2 not possible)
 3rd pos = 3 - 2 = 1 (possible)
 4th pos = 4 - 2 = 2 (possible)
 5th pos = 5 + 2 = 7 (5 - 2 already placed, not possible)
 6th pos = 6 + 2 = 8 (6 - 2 already placed, not possible)
 7th pos = 7 - 2 = 5 (possible)
 8th pos = 8 - 2 = 6 (possible)
```

**注:**如果我们观察上图，我们会发现 i + k 和 I–k 在第 k 个<sup>连续间隔后交替出现。另一个观察结果是，只有当 n 是偶数时，整个排列才能被分成两部分，其中每个部分都必须被 k 整除</sup> 

## C++

```
// C++ program to find k absolute difference
// permutation
#include<bits/stdc++.h>
using namespace std;

void kDifferencePermutation(int n, int k)
{
    // If k is 0 then we just print the
    // permutation from 1 to n
    if (!k)
    {
        for (int i = 0; i < n; ++i)
            cout << i + 1 << " ";
    }

    // Check whether permutation is feasible or not
    else if (n % (2 * k) != 0)
        cout <<"Not Possible";

    else
    {
        for (int i = 0; i < n; ++i)
        {
            // Put i + k + 1 candidate if position is
            // feasible, otherwise put the i - k - 1
            // candidate
            if ((i / k) % 2 == 0)
                cout << i + k + 1 << " ";
            else
                cout << i - k + 1 << " ";
        }
    }
    cout << "\n";
}

// Driver code
int main()
{
    int n = 6 , k = 3;
    kDifferencePermutation(n, k);

    n = 6 , k = 2;
    kDifferencePermutation(n, k);

    n = 8 , k = 2;
    kDifferencePermutation(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k absolute
// difference permutation
import java.io.*;

class GFG {

    static void kDifferencePermutation(int n,
                                    int k)
    {
        // If k is 0 then we just print the
        // permutation from 1 to n
        if (!(k > 0))
        {
            for (int i = 0; i < n; ++i)
                System.out.print( i + 1 + " ");
        }

        // Check whether permutation is
        // feasible or not
        else if (n % (2 * k) != 0)
            System.out.print("Not Possible");

        else
        {
            for (int i = 0; i < n; ++i)
            {
                // Put i + k + 1 candidate
                // if position is feasible,
                // otherwise put the
                // i - k - 1 candidate
                if ((i / k) % 2 == 0)
                    System.out.print( i + k
                            + 1 + " ");
                else
                    System.out.print( i - k
                            + 1 + " ");
            }
        }
        System.out.println() ;
    }

    // Driver code
    static public void main (String[] args)
    {
        int n = 6 , k = 3;
        kDifferencePermutation(n, k);

        n = 6 ;
        k = 2;
        kDifferencePermutation(n, k);

        n = 8 ;
        k = 2;
        kDifferencePermutation(n, k);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find k
# absolute difference permutation
def kDifferencePermutation(n, k):

    # If k is 0 then we just print the
    # permutation from 1 to n
    if (k == 0):
        for i in range(n):
            print(i + 1, end = " ")

    # Check whether permutation
    # is feasible or not
    elif (n % (2 * k) != 0):
        print("Not Possible", end = "")

    else:
        for i in range(n):

            # Put i + k + 1 candidate if position is
            # feasible, otherwise put the i - k - 1
            # candidate
            if (int(i / k) % 2 == 0):
                print(i + k + 1, end = " ")
            else:
                print(i - k + 1, end = " ")

    print("\n", end = "")

# Driver code
if __name__ == '__main__':
    n = 6
    k = 3
    kDifferencePermutation(n, k)

    n = 6
    k = 2
    kDifferencePermutation(n, k)

    n = 8
    k = 2
    kDifferencePermutation(n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find k absolute
// difference permutation
using System;

class GFG {

    static void kDifferencePermutation(int n,
                                       int k)
    {
        // If k is 0 then we just print the
        // permutation from 1 to n
        if (!(k > 0))
        {
            for (int i = 0; i < n; ++i)
                Console.Write( i + 1 + " ");
        }

        // Check whether permutation is
        // feasible or not
        else if (n % (2 * k) != 0)
            Console.Write("Not Possible");

        else
        {
            for (int i = 0; i < n; ++i)
            {
                // Put i + k + 1 candidate
                // if position is feasible,
                // otherwise put the
                // i - k - 1 candidate
                if ((i / k) % 2 == 0)
                    Console.Write( i + k
                              + 1 + " ");
                else
                    Console.Write( i - k
                              + 1 + " ");
            }
        }
        Console.WriteLine() ;
    }

    // Driver code
    static public void Main ()
    {
        int n = 6 , k = 3;
        kDifferencePermutation(n, k);

        n = 6 ;
        k = 2;
        kDifferencePermutation(n, k);

        n = 8 ;
        k = 2;
        kDifferencePermutation(n, k);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find k absolute
// difference permutation

function kDifferencePermutation( $n, $k)
{

    // If k is 0 then we just print the
    // permutation from 1 to n
    if (!$k)
    {
        for($i = 0; $i < $n; ++$i)
            echo $i + 1 ," ";
    }

    // Check whether permutation
    // is feasible or not
    else if ($n % (2 * $k) != 0)
        echo"Not Possible";

    else
    {
        for($i = 0; $i < $n; ++$i)
        {

            // Put i + k + 1 candidate
            // if position is feasible,
            // otherwise put the i - k - 1
            // candidate
            if (($i / $k) % 2 == 0)
                echo $i + $k + 1 , " ";
            else
                echo $i - $k + 1 , " ";
        }
    }
    echo "\n";
}

    // Driver Code
    $n = 6 ; $k = 3;
    kDifferencePermutation($n, $k);

    $n = 6 ; $k = 2;
    kDifferencePermutation($n, $k);

    $n = 8 ;$k = 2;
    kDifferencePermutation($n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find k absolute difference permutation

    function kDifferencePermutation(n, k)
    {
        // If k is 0 then we just print the
        // permutation from 1 to n
        if (!(k > 0))
        {
            for (let i = 0; i < n; ++i)
                document.write( i + 1 + " ");
        }

        // Check whether permutation is
        // feasible or not
        else if (n % (2 * k) != 0)
            document.write("Not Possible");

        else
        {
            for (let i = 0; i < n; ++i)
            {
                // Put i + k + 1 candidate
                // if position is feasible,
                // otherwise put the
                // i - k - 1 candidate
                if (parseInt(i / k, 10) % 2 == 0)
                    document.write( i + k
                              + 1 + " ");
                else
                    document.write( i - k
                              + 1 + " ");
            }
        }
        document.write("</br>") ;
    }

    let n = 6 , k = 3;
    kDifferencePermutation(n, k);

    n = 6 ;
    k = 2;
    kDifferencePermutation(n, k);

    n = 8 ;
    k = 2;
    kDifferencePermutation(n, k);

 // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
4 5 6 1 2 3 
Not Possible
3 4 1 2 7 8 5 6 
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。