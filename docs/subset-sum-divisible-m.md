# 和可被 m 整除的子集

> 原文:[https://www.geeksforgeeks.org/subset-sum-divisible-m/](https://www.geeksforgeeks.org/subset-sum-divisible-m/)

给定一组非负的不同整数和值 m，确定给定集合中是否有一个子集的和可被 m 整除。
输入约束
集合的大小，即 n < = 1000000，m < = 1000
**示例:**

```
Input : arr[] = {3, 1, 7, 5};
        m = 6;
Output : YES

Input : arr[] = {1, 6};
        m = 5;
Output : NO
```

这个问题是[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)的变种。在[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)中，我们检查给定的和子集是否存在，这里我们需要发现是否存在一些和可被 m 整除的子集。看到输入约束，看起来典型的动态规划解决方案将在 0(纳米)时间内工作。但是在竞争编程的严格时间限制下，解决方案可能会奏效。此外，DP 表的辅助空间很高，但这里是 catch。
如果 **n > m** 总会有一个和可被 m 整除的子集(用[鸽子洞原理](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)很容易证明)。所以我们只需要处理 **n < = m** 的情况。
对于 **n < = m** 我们创建一个布尔 DP 表，该表将存储从 0 到 m-1 的每个值的状态，这些值是迄今为止遇到的可能子集和(模 m)。
现在我们循环遍历给定数组 arr[]的每个元素，并添加 DP[j] = true 的(模 m) j，并将所有这样的(j+arr[i])%m 个可能的子集和存储在一个布尔数组 temp 中，在 j 上迭代结束时，我们用 temp 更新 DP 表。我们还在 DP ie 中添加了 arr[i]..DP[arr[i]%m] =真。
最后，如果 DP[0]为真，则意味着是，存在一个和可被 m 整除的子集，否则为否

## C++

```
// C++ program to check if there is a subset
// with sum divisible by m.
#include <bits/stdc++.h>
using namespace std;

// Returns true if there is a subset
// of arr[] with sum divisible by m
bool modularSum(int arr[], int n, int m)
{
    if (n > m)
        return true;

    // This array will keep track of all
    // the possible sum (after modulo m)
    // which can be made using subsets of arr[]
    // initialising boolean array with all false
    bool DP[m];
    memset(DP, false, m);

    // we'll loop through all the elements of arr[]
    for (int i=0; i<n; i++)
    {
        // anytime we encounter a sum divisible
        // by m, we are done
        if (DP[0])
            return true;

        // To store all the new encountered sum (after
        // modulo). It is used to make sure that arr[i]
        // is added only to those entries for which DP[j]
        // was true before current iteration. 
        bool temp[m];
        memset(temp,false,m);

        // For each element of arr[], we loop through
        // all elements of DP table from 1 to m and
        // we add current element i. e., arr[i] to
        // all those elements which are true in DP
        // table
        for (int j=0; j<m; j++)
        {
            // if an element is true in DP table
            if (DP[j] == true)
            {
                if (DP[(j+arr[i]) % m] == false)

                    // We update it in temp and update
                    // to DP once loop of j is over
                    temp[(j+arr[i]) % m] = true;
            }
        }

        // Updating all the elements of temp
        // to DP table since iteration over
        // j is over
        for (int j=0; j<m; j++)
            if (temp[j])
                DP[j] = true;

        // Also since arr[i] is a single element
        // subset, arr[i]%m is one of the possible
        // sum
        DP[arr[i]%m] = true;
    }

    return DP[0];
}

// Driver code
int main()
{
    int arr[] = {1, 7};
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = 5;

    modularSum(arr, n, m) ?  cout << "YES\n" :
                             cout << "NO\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there is a subset
// with sum divisible by m.
import java.util.Arrays;

class GFG {

    // Returns true if there is a subset
    // of arr[] with sum divisible by m
    static boolean modularSum(int arr[],
                                int n, int m)
    {
        if (n > m)
            return true;

        // This array will keep track of all
        // the possible sum (after modulo m)
        // which can be made using subsets of arr[]
        // initialising boolean array with all false
        boolean DP[]=new boolean[m];

        Arrays.fill(DP, false);

        // we'll loop through all the elements
        // of arr[]
        for (int i = 0; i < n; i++)
        {

            // anytime we encounter a sum divisible
            // by m, we are done
            if (DP[0])
                return true;

            // To store all the new encountered sum
            // (after modulo). It is used to make
            // sure that arr[i] is added only to
            // those entries for which DP[j]
            // was true before current iteration.
            boolean temp[] = new boolean[m];
            Arrays.fill(temp, false);

            // For each element of arr[], we loop
            // through all elements of DP table
            // from 1 to m and we add current
            // element i. e., arr[i] to all those
            // elements which are true in DP table
            for (int j = 0; j < m; j++)
            {

                // if an element is true in
                // DP table
                if (DP[j] == true)
                {
                    if (DP[(j + arr[i]) % m] == false)

                        // We update it in temp and update
                        // to DP once loop of j is over
                        temp[(j + arr[i]) % m] = true;
                }
            }

            // Updating all the elements of temp
            // to DP table since iteration over
            // j is over
            for (int j = 0; j < m; j++)
                if (temp[j])
                    DP[j] = true;

            // Also since arr[i] is a single
            // element subset, arr[i]%m is one
            // of the possible sum
            DP[arr[i] % m] = true;
        }

        return DP[0];
    }

    //driver code
    public static void main(String arg[])
    {
        int arr[] = {1, 7};
        int n = arr.length;
        int m = 5;

        if(modularSum(arr, n, m))
            System.out.print("YES\n");
        else
            System.out.print("NO\n");
    }
}

//This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check if there is
# a subset with sum divisible by m.

# Returns true if there is a subset
# of arr[] with sum divisible by m
def modularSum(arr, n, m):

    if (n > m):
        return True

    # This array will keep track of all
    # the possible sum (after modulo m)
    # which can be made using subsets of arr[]
    # initialising boolean array with all false
    DP = [False for i in range(m)]

    # we'll loop through all the elements of arr[]
    for i in range(n):

        # anytime we encounter a sum divisible
        # by m, we are done
        if (DP[0]):
            return True

        # To store all the new encountered sum (after
        # modulo). It is used to make sure that arr[i]
        # is added only to those entries for which DP[j]
        # was true before current iteration.
        temp = [False for i in range(m)]

        # For each element of arr[], we loop through
        # all elements of DP table from 1 to m and
        # we add current element i. e., arr[i] to
        # all those elements which are true in DP
        # table
        for j in range(m):

            # if an element is true in DP table
            if (DP[j] == True):

                if (DP[(j + arr[i]) % m] == False):

                    # We update it in temp and update
                    # to DP once loop of j is over
                    temp[(j + arr[i]) % m] = True

        # Updating all the elements of temp
        # to DP table since iteration over
        # j is over
        for j in range(m):
            if (temp[j]):
                DP[j] = True

        # Also since arr[i] is a single element
        # subset, arr[i]%m is one of the possible
        # sum
        DP[arr[i] % m] = True

    return DP[0]

# Driver code
arr = [1, 7]
n = len(arr)
m = 5
print("YES") if(modularSum(arr, n, m)) else print("NO")

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to check if there is
// a subset with sum divisible by m.
using System;

class GFG {

// Returns true if there is a subset
// of arr[] with sum divisible by m
static bool modularSum(int []arr, int n,
                                  int m)
{
    if (n > m)
        return true;

    // This array will keep track of all
    // the possible sum (after modulo m)
    // which can be made using subsets of arr[]
    // initialising boolean array with all false
    bool []DP=new bool[m];
    for (int l=0;l<DP.Length;l++)
        DP[l]=false;

    // we'll loop through all the elements of arr[]
    for (int i=0; i<n; i++)
    {
        // anytime we encounter a sum divisible
        // by m, we are done
        if (DP[0])
            return true;

        // To store all the new encountered sum (after
        // modulo). It is used to make sure that arr[i]
        // is added only to those entries for which DP[j]
        // was true before current iteration. 
        bool []temp=new bool[m];
        for (int l=0;l<temp.Length;l++)
        temp[l]=false;

        // For each element of arr[], we loop through
        // all elements of DP table from 1 to m and
        // we add current element i. e., arr[i] to
        // all those elements which are true in DP
        // table
        for (int j=0; j<m; j++)
        {
            // if an element is true in DP table
            if (DP[j] == true)
            {
                if (DP[(j+arr[i]) % m] == false)

                    // We update it in temp and update
                    // to DP once loop of j is over
                    temp[(j+arr[i]) % m] = true;
            }
        }

        // Updating all the elements of temp
        // to DP table since iteration over
        // j is over
        for (int j=0; j<m; j++)
            if (temp[j])
                DP[j] = true;

        // Also since arr[i] is a single element
        // subset, arr[i]%m is one of the possible
        // sum
        DP[arr[i]%m] = true;
    }

    return DP[0];
}

//driver code
public static void Main()
{
     int []arr = {1, 7};
    int n = arr.Length;
    int m = 5;

    if(modularSum(arr, n, m))
    Console.Write("YES\n");
    else
    Console.Write("NO\n");
}
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to check if there is a
// subset with sum divisible by m.

// Returns true if there is a subset
// of arr[] with sum divisible by m
function modularSum($arr, $n, $m)
{
    if ($n > $m)
        return true;

    // This array will keep track of all
    // the possible sum (after modulo m)
    // which can be made using subsets of arr[]
    // initialising boolean array with all false
    $DP = Array_fill(0, $m, false);

    // we'll loop through all the elements of arr[]
    for ($i = 0; $i < $n; $i++)
    {
        // anytime we encounter a sum divisible
        // by m, we are done
        if ($DP[0])
            return true;

        // To store all the new encountered sum
        // (after modulo). It is used to make
        // sure that arr[i] is added only to those 
        // entries for which DP[j] was true before
        // current iteration.
        $temp = array_fill(0, $m, false) ;

        // For each element of arr[], we loop through
        // all elements of DP table from 1 to m and
        // we add current element i. e., arr[i] to
        // all those elements which are true in DP
        // table
        for ($j = 0; $j < $m; $j++)
        {
            // if an element is true in DP table
            if ($DP[$j] == true)
            {
                if ($DP[($j + $arr[$i]) % $m] == false)

                    // We update it in temp and update
                    // to DP once loop of j is over
                    $temp[($j + $arr[$i]) % $m] = true;
            }
        }

        // Updating all the elements of temp
        // to DP table since iteration over
        // j is over
        for ($j = 0; $j < $m; $j++)
            if ($temp[$j])
                $DP[$j] = true;

        // Also since arr[i] is a single element
        // subset, arr[i]%m is one of the possible
        // sum
        $DP[$arr[$i] % $m] = true;
    }

    return $DP[0];
}

// Driver Code
$arr = array(1, 7);
$n = sizeof($arr);
$m = 5;

if (modularSum($arr, $n, $m) == true )
    echo "YES\n";
else
    echo "NO\n";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript program to check if there is
    // a subset with sum divisible by m.

    // Returns true if there is a subset
    // of arr[] with sum divisible by m
    function modularSum(arr, n, m)
    {
        if (n > m)
            return true;

        // This array will keep track of all
        // the possible sum (after modulo m)
        // which can be made using subsets of arr[]
        // initialising boolean array with all false
        let DP = new Array(m);
        for (let l=0;l<m;l++)
            DP[l]=false;

        // we'll loop through all the elements of arr[]
        for (let i=0; i<n; i++)
        {
            // anytime we encounter a sum divisible
            // by m, we are done
            if (DP[0])
                return true;

            // To store all the new encountered sum (after
            // modulo). It is used to make sure that arr[i]
            // is added only to those entries for which DP[j]
            // was true before current iteration. 
            let temp=new Array(m);
            for (let l=0;l<m;l++)
                temp[l]=false;

            // For each element of arr[], we loop through
            // all elements of DP table from 1 to m and
            // we add current element i. e., arr[i] to
            // all those elements which are true in DP
            // table
            for (let j=0; j<m; j++)
            {
                // if an element is true in DP table
                if (DP[j] == true)
                {
                    if (DP[(j+arr[i]) % m] == false)

                        // We update it in temp and update
                        // to DP once loop of j is over
                        temp[(j+arr[i]) % m] = true;
                }
            }

            // Updating all the elements of temp
            // to DP table since iteration over
            // j is over
            for (let j=0; j<m; j++)
                if (temp[j])
                    DP[j] = true;

            // Also since arr[i] is a single element
            // subset, arr[i]%m is one of the possible
            // sum
            DP[arr[i]%m] = true;
        }

        return DP[0];
    }

    let arr = [1, 7];
    let n = arr.length;
    let m = 5;

    if(modularSum(arr, n, m))
        document.write("YES" + "</br>");
    else
        document.write("NO" + "</br>");

</script>
```

**输出:**

```
NO
```

**时间复杂度:**o(m^2)
T3】辅助空间: O(m)
本文由 **Pratik Chhajer** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。