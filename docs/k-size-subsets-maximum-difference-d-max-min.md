# 最大值和最小值之间最大差值为 d 的 k 个大小子集

> 原文:[https://www . geesforgeks . org/k-size-subsets-maximum-difference-d-max-min/](https://www.geeksforgeeks.org/k-size-subsets-maximum-difference-d-max-min/)

## C++

```
// C++ code to find no. of subsets with
// maximum difference d between max and
#include <bits/stdc++.h>
using namespace std;

// function to calculate factorial of a numb
int fact(int i)
{

    if (i == 0)
        return 1;
    return i * fact(i - 1);
}

int ans(int a[], int n, int k, int x)
{
    if (k > n || n < 1)
        return 0;

    sort(a, a + n);
    int count = 0;
    int j = 1;
    int i = 0;
    int kfactorial = fact(k);
    while (j <= n) {
        while (j < n && a[j] - a[i] <= x) {
            j++;
        }
        if ((j - i) >= k) {
            count = count
                    + fact(j - i)
                          / (kfactorial * fact(j - i - k));
        }
        else {
            i++;
            j++;
            continue;
        }
        if (j == n)
            break;
        while (i < j && a[j] - a[i] > x) {
            i++;
        }
        if ((j - i) >= k) {
            count = count
                    - fact(j - i)
                          / (kfactorial * fact(j - i - k));
        }
    }

    return count;
}

// driver program to test the above
// function
int main()
{
    int arr[] = { 1, 12, 9, 2, 4, 2, 5, 8, 4, 6 },
    k = 3,x = 5;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << ans(arr, n, k, x);
    return 0;
}
// This code is contributed by Vishakha Chauhan
```

**Output**

```
52
```

给定一个数组和两个整数 k 和 d，求这个大小为 k 的数组的子集数，其中子集的最大值和最小值之差为**atmat**d .
示例:

```
Input : a[] = [5, 4, 2, 1, 3],
        k = 3, d = 5 
Output : 10
Explanation:
{1,2,3}, {1,2,4}, {1,2,5}, {1,3,4}, {1,3,5}, 
{1,4,5}, {2,3,4}, {2,3,5}, {2,4,5}, {3,4,5}.
We can see each subset has atmost 
difference d=5 between the minimum
and maximum element of each subset.
No of such subsets = 10 

Input : a[] = [1, 2, 3, 4, 5, 6],
        k = 3, d = 5 
Output : 20
```

**天真的方法**:找到大小为 k 的所有子集，并为每个子集找到最大和最小元素之间的差异。如果差值小于或等于 d，则进行计数。
**高效进场** :
1) **排序**:先**按递增顺序排序**阵列。现在，假设我们想要找出第 i **个**元素的所需子集的数量，其中整数 a[i]作为该子集的最小元素。这样一个子集的最大值永远不会超过 a[i] + d .
2) **求最大索引 j** :我们可以对每个 I 在这个数组上应用**二分搜索法**，求最大索引 j，这样 a[j] < = a[i]+d .现在包括 a[i]和 i+1…j 范围内的任何其他元素的任何子集都将是必需的子集，因为元素 a[i]是该子集的最小值， 而任何其他元素与 a[i]的差总是小于等于 d.
3) **应用基本组合学公式**:现在我们要找到大小为 k 的所需子集的个数，这将是在必须从给定的 n 个数中选择 r 项时，通过使用组合的基本公式。 同样，我们需要从已经包含[i]的(j-i)元素中选择(k-1)个数字，I 是每个子集中的最小数字。每个 I**元素的该过程的总和将是最终答案。
这里我用了一个简单的递归方法来求一个数字的阶乘，也可以用动态规划来求它。** 

> ****图解:**
> 输入:a = [5，4，2，1，3]，
> k = 3，d = 5
> 输出:10
> 解释:
> 按升序排序的数组:【1，2，3，4，5】
> 对于 a[0] = 1 作为最小元素
> 子集的编号将是 6，它们是{1，2，3}、{1，2，
> 4}、{1，2，5}、{1，3，3
> 对于作为最小元素的 a[1]= 2
> 而言，子集的数量将是 3，它们是{2，3，4}、{2，
> 3，5}、{2，4，5}
> 对于作为最小元素的 a[2]= 3
> 而言，子集的数量将是 1，它们是{3，4，5}
> 而不会通过将 a[3] = 4 或 a[4] = 5 作为最小元素而形成大小为 k = 3 的其他子集**

## **C++**

```
// C++ code to find no. of subsets with
// maximum difference d between max and
// min of all K-size subsets function to
// calculate factorial of a number
#include <bits/stdc++.h>
using namespace std;

int fact (int n){
    if (n==0)
        return 1;
    else
        return n * fact(n-1);
}

// function to count ways to select r
// numbers from n given numbers
int findcombination (int n,int r){
    return( fact(n) / (fact(n - r) *
                        fact(r)));
}

// function to return the total number
// of required subsets :
// n is the number of elements in array
// d is the maximum difference between
// minimum and maximum element in each
// subset of size k
int find(int arr[], int n, int d, int k)
{
    sort(arr,arr+n);
    int ans = 0, end = n, co = 0,
        start = 0;

    // loop to traverse from 0-n
    for (int i = 0; i < n; i++) {

    int val = arr[i] + d;

    // binary search to get the position
    // which will be stored in start

    start = i;
    while (start < end - 1){
        int mid = (start + end) / 2;

        // if mid value greater than
        // arr[i]+d do search in
        // arr[start:mid]
        if (arr[mid] > val)
            end = mid;

        else
            start = mid + 1;
    }

    if (start != n and arr[start]
                       <= val)
            start += 1;

    int c = start-i;

    // if the numbers of elements 'c'
    // is greater or equal to the given
    // size k, then only subsets of
    // required size k can be formed
    if (c >= k){
        co += findcombination(c - 1, k - 1);}
    }
    return co;
}

// driver program to test the above
// function
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6},
        k = 3, d = 5;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << find(arr, n,d,k);
    return 0;
}
// This code is contributed by Prerna Saini
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to find no. of subsets
// with maximum difference d between
// max and min of all K-size subsets
import java.util.*;

class GFG {

// function to calculate factorial
// of a number
static int fact (int n){
    if (n==0)
        return 1;
    else
        return n * fact(n-1);
}

// function to count ways to select r
// numbers from n given numbers
static int findcombination(int n, int r){
    return( fact(n) / (fact(n - r) *
                           fact(r)));
}

// function to return the total number
// of required subsets :
// n is the number of elements in array
// d is the maximum difference between
// minimum and maximum element in each
// subset of size k
static int find(int arr[], int n, int d,
                            int k)
{
    Arrays.sort(arr);
    int ans = 0, end = n, co = 0,
        start = 0;

    // loop to traverse from 0-n
    for (int i = 0; i < n; i++) {

    int val = arr[i] + d;

    // binary search to get the position
    // which will be stored in start
    start=i;
    while (start < end - 1){
        int mid = (start + end) / 2;

        // if mid value greater than
        // arr[i]+d do search in
        // arr[start:mid]
        if (arr[mid] > val)
            end = mid;
        else
            start = mid+1;
        }

    if (start !=n && arr[start] <= val)
            start += 1;

        int c = start-i;

    // if the numbers of elements 'c' is
    // greater or equal to the given size k,
    // then only subsets of required size k
    // can be formed
    if (c >= k){
        co += findcombination(c - 1, k - 1);}
    }

    return co;
}

// driver program to test the above function
public static void main(String[] args)
{
    int arr[] = {1, 2, 3, 4, 5, 6}, k = 3,
        d = 5;
    int n = arr.length;
    System.out.println(find(arr, n,d,k));
}
}
// This code is contributed by Prerna Saini
```

## **计算机编程语言**

```
# Python code to find no. of subsets with maximum
# difference d between max and min of all K-size
# subsets function to calculate factorial of a
# number
def fact (n):
    if (n==0):
        return (1)
    else:
        return n * fact(n-1)

# function to count ways to select r numbers
# from n given numbers
def findcombination (n,r):
    return( fact(n)//(fact(n-r)*fact(r)))

# function to return the total number of required
# subsets :
# n is the number of elements in list l[0..n-1]
# d is the maximum difference between minimum and
#    maximum element in each subset of size k   
def find (a, n, d, k):

    # sort the list first in ascending order
    a.sort()
    (start, end, co) = (0, n, 0)

    for i in range(0, n):
        val = a[i]+ d

        # binary search to get the position
        # which will be stored in start
        # such that a[start] <= a[i]+d
        start = i
        while (start< end-1):
            mid = (start+end)//2

            # if mid value greater than a[i]+d
            # do search in l[start:mid]
            if (a[mid] > val):
                end = mid

            # if mid value less or equal to a[i]+d
            # do search in a[mid+1:end]
            else:
                start = mid+1

        if (start!=n and a[start]<=val):
            start += 1

        # count the numbers of elements that fall
        # in range i to start
        c = start-i

        # if the numbers of elements 'c' is greater
        # or equal to the given size k, then only
        # subsets of required size k can be formed
        if (c >= k):
            co += findcombination(c-1,k-1)

    return co

# Driver code
n = 6  # Number of elements
d = 5  # maximum diff
k = 3  # Size of subsets
print(find([1, 2, 3, 4, 5, 6], n, d, k)) 
```

## **C#**

```
// C# code to find no. of subsets
// with maximum difference d between
// max and min of all K-size subsets
using System;

class GFG {

    // function to calculate factorial
    // of a number
    static int fact (int n)
    {
        if (n == 0)
            return 1;
        else
            return n * fact(n - 1);
    }

    // function to count ways to select r
    // numbers from n given numbers
    static int findcombination(int n, int r)
    {
        return( fact(n) / (fact(n - r) *
                               fact(r)));
    }

    // function to return the total number
    // of required subsets :
    // n is the number of elements in array
    // d is the maximum difference between
    // minimum and maximum element in each
    // subset of size k
    static int find(int []arr, int n, int d,
                                      int k)
    {
        Array.Sort(arr);

        //int ans = 0,
        int end = n, co = 0,
            start = 0;

        // loop to traverse from 0-n
        for (int i = 0; i < n; i++)
        {
            int val = arr[i] + d;

            // binary search to get the
            // position which will be
            // stored in start
            start = i;
            while (start < end - 1){
                int mid = (start + end) / 2;

                // if mid value greater than
                // arr[i]+d do search in
                // arr[start:mid]
                if (arr[mid] > val)
                    end = mid;
                else
                    start = mid+1;
                }

            if (start !=n && arr[start] <= val)
                    start += 1;

                int c = start-i;

            // if the numbers of elements 'c' is
            // greater or equal to the given size k,
            // then only subsets of required size k
            // can be formed
            if (c >= k)
                co += findcombination(c - 1, k - 1);
        }

        return co;
    }

    // driver program to test the above function
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5, 6};
        int k = 3;
        int d = 5;
        int n = arr.Length;
        Console.WriteLine(find(arr, n, d, k));
    }
}

// This code is contributed by anuj_67.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php

// Php code to find no. of subsets with
// maximum difference d between max and
// min of all K-size subsets function to
// calculate factorial of a number

function fact ($n){
    if ($n==0)
        return 1;
    else
        return $n * fact($n-1);
}

// function to count ways to select r
// numbers from n given numbers
function findcombination ($n,$r){
    return( fact($n) / (fact($n - $r) *
                        fact($r)));
}

// function to return the total number
// of required subsets :
// n is the number of elements in array
// d is the maximum difference between
// minimum and maximum element in each
// subset of size k
function find(&$arr, $n, $d, $k)
{
    sort($arr);
    $ans = 0;
    $end = $n;
    $co = 0;
    $start = 0;

    // loop to traverse from 0-n
    for ($i = 0; $i < $n; $i++) {

    $val = $arr[$i] + $d;

    // binary search to get the position
    // which will be stored in start

    $start = $i;
    while ($start < $end - 1){
        $mid = intval (($start + $end) / 2);

        // if mid value greater than
        // arr[i]+d do search in
        // arr[start:mid]
        if ($arr[$mid] > $val)
            $end = $mid;

        else
            $start = $mid + 1;
    }

    if ($start != $n && $arr[$start]
                       <= $val)
            $start += 1;

    $c = $start-$i;

    // if the numbers of elements 'c'
    // is greater or equal to the given
    // size k, then only subsets of
    // required size k can be formed
    if ($c >= $k){
        $co += findcombination($c - 1, $k - 1);}
    }
    return $co;
}

// driver program to test the above
// function

    $arr = array(1, 2, 3, 4, 5, 6);
    $k = 3;
    $d = 5;
    $n = sizeof($arr) / sizeof($arr[0]);
    echo find($arr, $n,$d,$k);
    return 0;
?>
```

## **java 描述语言**

```
<script>
// Javascript code to find no. of subsets
// with maximum difference d between
// max and min of all K-size subsets

    // function to calculate factorial
    // of a number
    function fact(n)
    {
        let answer=1;
        if (n == 0 || n == 1)
           {    return answer;}
        else
        {
            for(var i = n; i >= 1; i--){
                  answer = answer * i;
            }
            return answer;
        }
    }

// function to count ways to select r
// numbers from n given numbers
function findcombination(n,r)
{
    return( Math.floor(fact(n) / (fact(n - r) *
                           fact(r))));
}

// function to return the total number
// of required subsets :
// n is the number of elements in array
// d is the maximum difference between
// minimum and maximum element in each
// subset of size k
function find(arr, n, d, k)
{
    arr.sort(function(a, b){return a-b;});
    let ans = 0, end = n, co = 0,
        start = 0;

    // loop to traverse from 0-n
    for (let i = 0; i < n; i++) {

    let val = arr[i] + d;

    // binary search to get the position
    // which will be stored in start
    start=i;
    while (start < end - 1){
        let mid = Math.floor((start + end) / 2);

        // if mid value greater than
        // arr[i]+d do search in
        // arr[start:mid]
        if (arr[mid] > val)
            end = mid;
        else
            start = mid+1;
        }

    if (start !=n && arr[start] <= val)
            start += 1;

        let c = start-i;

    // if the numbers of elements 'c' is
    // greater or equal to the given size k,
    // then only subsets of required size k
    // can be formed
    if (c >= k){
        co += findcombination(c - 1, k - 1);}
    }

    return co;
}

// driver program to test the above function
let arr = [1, 2, 3, 4, 5, 6];
let k = 3, d = 5;
let n = arr.length;
document.write(find(arr, n, d, k));

    // This code is contributed by rag2127.
</script>
```

****Output**

```
20
```** 

****输出:**** 

```
20
```

**本文由 [**Sruti Rai**](https://auth.geeksforgeeks.org/profile.php?user=Sruti Rai&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**