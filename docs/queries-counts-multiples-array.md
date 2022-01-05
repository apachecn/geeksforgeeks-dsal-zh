# 查询数组中的倍数计数

> 原文:[https://www . geesforgeks . org/query-counts-multiples-array/](https://www.geeksforgeeks.org/queries-counts-multiples-array/)

给定正整数数组和许多可除性查询。在每个查询中，我们得到一个整数 k ( > 0)，我们需要计算数组中所有能被“k”完全整除的元素。
**例:**

```
Input:
2 4 9 15 21 20
k = 2
k = 3
k = 5

Output:
3
3
2

Explanation:
Multiples of '2' in array are:- {2, 4, 20}
Multiples of '3' in array are:- {9, 15, 21}
Multiples of '5' in array are:- {15, 20}
```

**简单方法**是遍历整个数组中‘k’的每个值，通过检查数组每个元素的模来计算总倍数，即对于 i (0 < i < n)的每个元素，检查 arr[i] % k == 0 与否。如果它能被 k 完全整除，那么递增计数。该方法的时间复杂度为 O(n * k)，对于 k.
的大量查询效率不高**高效方法**是使用厄拉多塞的[筛的概念。让我们定义数组[]中的最大值为“Max”。由于数组[]中所有数字的倍数总是小于最大值，因此我们将只迭代到“最大值”。
现在对每个值(比如‘q’)迭代 **q，2q，3q，… t.k** (tk < = MAX)，因为所有这些数字都是“ **q** 的倍数。同时在 ans[]数组中为 q(1，2，… MAX)的每个值存储所有这些数字的计数。之后我们可以在 O(1)时间内回答每个查询。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to calculate all multiples
// of integer 'k' in array[]
#include <bits/stdc++.h>
using namespace std;

// ans is global pointer so that both countSieve()
// and countMultiples() can access it.
int* ans = NULL;

// Function to pre-calculate all multiples of
// array elements
void countSieve(int arr[], int n)
{
    int MAX = *max_element(arr, arr + n);

    int cnt[MAX + 1];

    // ans is global pointer so that query function
    // can access it.
    ans = new int[MAX + 1];

    // Initialize both arrays as 0.
    memset(cnt, 0, sizeof(cnt));
    memset(ans, 0, (MAX + 1) * sizeof(int));

    // Store the arr[] elements as index
    // in cnt[] array
    for (int i = 0; i < n; ++i)
        ++cnt[arr[i]];

    // Iterate over all multiples as 'i'
    // and keep the count of array[] ( In
    // cnt[] array) elements in ans[] array
    for (int i = 1; i <= MAX; ++i)
        for (int j = i; j <= MAX; j += i)
            ans[i] += cnt[j];
    return;
}

int countMultiples(int k)
{
    // return pre-calculated result
    return ans[k];
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 9, 15, 21, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // pre-calculate all multiples
    countSieve(arr, n);

    int k = 2;
    cout << countMultiples(k) << "\n";

    k = 3;
    cout << countMultiples(k) << "\n";

    k = 5;
    cout << countMultiples(k) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate all multiples
// of integer 'k' in array[]
class CountMultiples {
    // ans is global array so that both
    // countSieve() and countMultiples()
    // can access it.
    static int ans[];

    // Function to pre-calculate all
    // multiples of array elements
    static void countSieve(int arr[], int n)
    {
        int MAX = arr[0];
        for (int i = 1; i < n; i++)
            MAX = Math.max(arr[i], MAX);

        int cnt[] = new int[MAX + 1];

        // ans is global array so that
        // query function can access it.
        ans = new int[MAX + 1];

        // Store the arr[] elements as
        // index in cnt[] array
        for (int i = 0; i < n; ++i)
            ++cnt[arr[i]];

        // Iterate over all multiples as 'i'
        // and keep the count of array[]
        // (In cnt[] array) elements in ans[]
        // array
        for (int i = 1; i <= MAX; ++i)
            for (int j = i; j <= MAX; j += i)
                ans[i] += cnt[j];
        return;
    }

    static int countMultiples(int k)
    {
        // return pre-calculated result
        return ans[k];
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 2, 4, 9, 15, 21, 20 };
        int n = 6;

        // pre-calculate all multiples
        countSieve(arr, n);

        int k = 2;
        System.out.println(countMultiples(k));

        k = 3;
        System.out.println(countMultiples(k));

        k = 5;
        System.out.println(countMultiples(k));
    }
}

/*This code is contributed by Danish Kaleem */
```

## 蟒蛇 3

```
# Python3 program to calculate all multiples
# of integer 'k' in array[]

# ans is global array so that both countSieve()
# and countMultiples() can access it.
ans = []

# Function to pre-calculate all multiples
# of array elements
# Here, the arguments are as follows
# a: given array
# n: length of given array
def countSieve(arr, n):

    MAX=max(arr)

# Accessing the global array in the function
    global ans

# Initializing "ans" array with zeros
    ans = [0]*(MAX + 1)

# Initializing "cnt" array with zeros
    cnt = [0]*(MAX + 1)

#Store the arr[] elements as index in cnt[] array
    for i in range(n):
        cnt[arr[i]] += 1

# Iterate over all multiples as 'i'
# and keep the count of array[] ( In
# cnt[] array) elements in ans[] array
    for i in range(1, MAX+1):
        for j in range(i, MAX+1, i):
            ans[i] += cnt[j]

def countMultiples(k):
# Return pre-calculated result
    return(ans[k])

# Driver code
if __name__ == "__main__":
    arr = [2, 4, 9 ,15, 21, 20]
    n=len(arr)
# Pre-calculate all multiples
    countSieve(arr, n)
    k=2
    print(countMultiples(2))
    k=3
    print(countMultiples(3))
    k=5
    print(countMultiples(5))

# This code is contributed by Pratik Somwanshi
```

## C#

```
// C# program to calculate all multiples
// of integer 'k' in array[]
using System;

class GFG {

    // ans is global array so that both
    // countSieve() and countMultiples()
    // can access it.
    static int[] ans;

    // Function to pre-calculate all
    // multiples of array elements
    static void countSieve(int[] arr, int n)
    {

        int MAX = arr[0];
        for (int i = 1; i < n; i++)
            MAX = Math.Max(arr[i], MAX);

        int[] cnt = new int[MAX + 1];

        // ans is global array so that
        // query function can access it.
        ans = new int[MAX + 1];

        // Store the arr[] elements as
        // index in cnt[] array
        for (int i = 0; i < n; ++i)
            ++cnt[arr[i]];

        // Iterate over all multiples as
        // 'i' and keep the count of
        // array[] (In cnt[] array)
        // elements in ans[] array
        for (int i = 1; i <= MAX; ++i)
            for (int j = i; j <= MAX; j += i)
                ans[i] += cnt[j];

        return;
    }

    static int countMultiples(int k)
    {

        // return pre-calculated result
        return ans[k];
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 4, 9, 15, 21, 20 };
        int n = 6;

        // pre-calculate all multiples
        countSieve(arr, n);

        int k = 2;
        Console.WriteLine(countMultiples(k));

        k = 3;
        Console.WriteLine(countMultiples(k));

        k = 5;
        Console.WriteLine(countMultiples(k));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// all multiples of integer
// 'k' in array[]

// ans is global array so
// that both countSieve()
// and countMultiples()
// can access it.
$ans;

// Function to pre-calculate all
// multiples of array elements
function countSieve($arr, $n)
{
    global $ans;
    $MAX = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $MAX = max($arr[$i], $MAX);

    $cnt = array_fill(0, $MAX + 1, 0);

    // ans is global array so that
    // query function can access it.
    $ans = array_fill(0, $MAX + 1, 0);

    // Store the arr[] elements
    // as index in cnt[] array
    for ($i = 0; $i < $n; ++$i)
        ++$cnt[$arr[$i]];

    // Iterate over all multiples as 'i'
    // and keep the count of array[]
    // (In cnt[] array) elements in ans[]
    // array
    for ($i = 1; $i <= $MAX; ++$i)
        for ($j = $i; $j <= $MAX; $j += $i)
            $ans[$i] += $cnt[$j];
    return;
}

function countMultiples($k)
{
    global $ans;

    // return pre-calculated result
    return $ans[$k];
}

// Driver code
$arr = array( 2, 4, 9, 15, 21, 20);
$n = 6;

// pre-calculate
// all multiples
countSieve($arr, $n);

$k = 2;
echo countMultiples($k) . "\n";

$k = 3;
echo countMultiples($k) . "\n";

$k = 5;
echo countMultiples($k) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to calculate all multiples
// of integer 'k' in array[]

    // ans is global array so that both
    // countSieve() and countMultiples()
    // can access it.
    let ans = [];

    // Function to pre-calculate all
    // multiples of array elements
    function countSieve(arr, n)
    {
        let MAX = arr[0];
        for (let i = 1; i < n; i++)
            MAX = Math.max(arr[i], MAX);

        let cnt = Array.from({length: MAX + 1}, (_, i) => 0);

        // ans is global array so that
        // query function can access it.
        ans = Array.from({length: MAX + 1}, (_, i) => 0);

        // Store the arr[] elements as
        // index in cnt[] array
        for (let i = 0; i < n; ++i)
            ++cnt[arr[i]];

        // Iterate over all multiples as 'i'
        // and keep the count of array[]
        // (In cnt[] array) elements in ans[]
        // array
        for (let i = 1; i <= MAX; ++i)
            for (let j = i; j <= MAX; j += i)
                ans[i] += cnt[j];
        return;
    }

    function countMultiples(k)
    {
        // return pre-calculated result
        return ans[k];
    }

// driver function

        let arr = [ 2, 4, 9, 15, 21, 20 ];
        let n = 6;

        // pre-calculate all multiples
        countSieve(arr, n);

        let k = 2;
        document.write(countMultiples(k) + "<br/>");

        k = 3;
        document.write(countMultiples(k) + "<br/>");

        k = 5;
        document.write(countMultiples(k) + "<br/>");

</script>
```

**输出:**

```
3
3
2
```

**时间复杂度:** O(M*log(M))，其中 M 是数组元素中的最大值。
**辅助空间:** O(MAX)
本文由[舒巴姆·班萨尔](https://www.quora.com/profile/Shubham-Bansal-209)供稿。如果你喜欢 GeeksforGeeks 并想投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章，或者把你的文章发到投稿@ geeksforgeeksorg。看到你的文章出现在极客主页，并帮助其他极客