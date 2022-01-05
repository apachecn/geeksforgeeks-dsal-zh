# 一个数组中乘积大于总和的对的数量

> 原文:[https://www . geesforgeks . org/number-pairs-array-product-greater-sum/](https://www.geeksforgeeks.org/number-pairs-array-product-greater-sum/)

给定非负整数数组 a[。计算数组中的对(I，j)的数量，使得 a[i] + a[j] < a[i]*a[j]. (the pair (i, j) and (j, i) are considered same and i should not be equal to j)
示例:

```
Input : a[] = {3, 4, 5}
Output : 3
Pairs are (3, 4) , (4, 5) and (3,5)

Input  : a[] = {1, 1, 1}
Output : 0
```

**天真的方法**
对于每个值 a[i]计算 a[j] (i > j)的个数，使得 a[i]*a[j] > a[i] + a[j]

## C++

```
// Naive C++ program to count number of pairs
// such that their sum is more than product.
#include<bits/stdc++.h>
using namespace std;

// Returns the number of valid pairs
int countPairs (int arr[], int n)
{   
    int ans = 0;  // initializing answer

    // Traversing the array. For each array
    // element, checking its predecessors that
    // follow the condition
    for (int i = 0; i<n; i++)
        for (int j = i-1; j>= 0; j--)
            if (arr[i]*arr[j] > arr[i] + arr[j])
                ans++;
    return ans;
}

// Driver function
int main()
{
    int arr[] = {3, 4, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << countPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Naive java program to count number of pairs
// such that their sum is more than product.
import java.*;

public class GFG
{

    // Returns the number of valid pairs
    static int countPairs (int arr[], int n)
    {
        int ans = 0; // initializing answer

        // Traversing the array. For each array
        // element, checking its predecessors that
        // follow the condition
        for (int i = 0; i<n; i++)
            for (int j = i-1; j>= 0; j--)
                if (arr[i]*arr[j] > arr[i] + arr[j])
                    ans++;
        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {3, 4, 5};
        int n = arr.length;
        System.out.println(countPairs(arr, n));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Naive Python program to count number
# of pairs such that their sum is more
# than product.

# Returns the number of valid pairs
def countPairs(arr, n):

    # initializing answer
    ans = 0

    # Traversing the array. For each
    # array element, checking its
    # predecessors that follow the
    # condition
    for i in range(0, n):
        j = i-1
        while(j >= 0):
            if (arr[i] * arr[j] >
                     arr[i] + arr[j]):
                ans = ans + 1
            j = j - 1
    return ans

# Driver program to test above function.
arr = [3, 4, 5]
n = len(arr)
k = countPairs(arr, n)
print(k)

# This code is contributed by Sam007.
```

## C#

```
// Naive C# program to count number of pairs
// such that their sum is more than product.
using System;

public class GFG
{
    // Returns the number of valid pairs
    static int countPairs (int []arr, int n)
    {
        int ans = 0; // initializing answer

        // Traversing the array. For each array
        // element, checking its predecessors that
        // follow the condition
        for (int i = 0; i<n; i++)
            for (int j = i-1; j>= 0; j--)
                if (arr[i]*arr[j] > arr[i] + arr[j])
                    ans++;
        return ans;
    }

    // driver program
    public static void Main()
    {
        int []arr = {3, 4, 5};
        int n = arr.Length;
        Console.Write( countPairs(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Naive PHP program to
// count number of pairs
// such that their sum
// is more than product.

// Returns the number
// of valid pairs
function countPairs ($arr, $n)
{
    // initializing answer
    $ans = 0;

    // Traversing the array.
    // For each array
    // element, checking
    // its predecessors that
    // follow the condition
    for ($i = 0; $i < $n; $i++)
        for ($j = $i - 1; $j >= 0; $j--)
            if ($arr[$i] * $arr[$j] >
                $arr[$i] + $arr[$j])
                $ans++;
    return $ans;
}

// Driver Code
$arr = array(3, 4, 5);
$n = sizeof($arr);
echo(countPairs($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Naive Javascript program to count number of pairs
    // such that their sum is more than product.

    // Returns the number of valid pairs
    function countPairs(arr, n)
    {
        let ans = 0; // initializing answer

        // Traversing the array. For each array
        // element, checking its predecessors that
        // follow the condition
        for (let i = 0; i<n; i++)
            for (let j = i-1; j>= 0; j--)
                if (arr[i]*arr[j] > (arr[i] + arr[j]))
                    ans++;
        return ans;
    }

    let arr = [3, 4, 5];
    let n = arr.length;
    document.write( countPairs(arr, n));

</script>
```

输出:

```
3
```

**高效进场**
***当 a[i] = 0*** 时:a[i]*a[j] = 0 且 a[i] + a[j] > = 0 所以如果 a[i] = 0 则找不到配对。
***当 a[I]= 1***:a[I]* a[j]= a[j]和 a[i] + a[j] = 1 + a[j]时，因此当 a[i] = 1
***当 a[i] = 2 且 a[j]= 2:***a[I]* a[j]= a[I]时，找不到配对
要解决这个问题，统计数组中 2s 的个数，比如 twoCount。计算数组中大于 2 的数字，比如 twoGreaterCount。答案是两个计数*两个更大的计数+两个更大的计数*(两个更大的计数-1)/2

## C++

```
// C++ implementation of efficient approach
// to count valid pairs.
#include<bits/stdc++.h>
using namespace std;

// returns the number of valid pairs
int CountPairs (int arr[], int n)
{
    // traversing the array, counting the
    // number of 2s and greater than 2
    // in array
    int twoCount = 0, twoGrCount = 0;
    for (int i = 0; i<n; i++)
    {
        if (arr[i] == 2)
            twoCount++;
        else if (arr[i] > 2)
            twoGrCount++;
    }
    return twoCount*twoGrCount +
          (twoGrCount*(twoGrCount-1))/2;
}

// Driver function
int main()
{
    int arr[] = {3, 4, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << CountPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of efficient approach
// to count valid pairs.
import java.*;

public class GFG
{
    // Returns the number of valid pairs
    static int countPairs (int arr[], int n)
    {
        // traversing the array, counting the
        // number of 2s and greater than 2
        // in array
        int twoCount = 0, twoGrCount = 0;
        for (int i = 0; i<n; i++)
        {
          if (arr[i] == 2)
            twoCount++;
          else if (arr[i] > 2)
            twoGrCount++;
        }
        return twoCount*twoGrCount +
        (twoGrCount*(twoGrCount-1))/2;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {3, 4, 5};
        int n = arr.length;
        System.out.println(countPairs(arr, n));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# python implementation of efficient approach
# to count valid pairs.

# returns the number of valid pairs
def CountPairs (arr,n):

    # traversing the array, counting the
    # number of 2s and greater than 2
    # in array
    twoCount = 0
    twoGrCount = 0
    for i in range(0, n):

        if (arr[i] == 2):
            twoCount += 1
        elif (arr[i] > 2):
            twoGrCount += 1

    return ((twoCount * twoGrCount)
      + (twoGrCount * (twoGrCount - 1)) / 2)

# Driver function
arr = [3, 4, 5]
n = len(arr)
print( CountPairs(arr, n))

# This code is contributed by Sam007.
```

## C#

```
// C# implementation of efficient approach
// to count valid pairs.
using System;

public class GFG
{
    // Returns the number of valid pairs
    static int countPairs (int []arr, int n) {

    // traversing the array, counting the
    // number of 2s and greater than 2
    // in array
    int twoCount = 0, twoGrCount = 0;
    for (int i = 0; i<n; i++)
    {
        if (arr[i] == 2)
            twoCount++;
        else if (arr[i] > 2)
            twoGrCount++;
    }
    return twoCount*twoGrCount +
           (twoGrCount*(twoGrCount-1))/2;
    }

    // driver program
    public static void Main()
    {
        int []arr = {3, 4, 5};
        int n = arr.Length;
        Console.Write( countPairs(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// efficient approach
// to count valid pairs.

// returns the number
// of valid pairs
function CountPairs ($arr, $n)
{

    // traversing the array, counting
    // the number of 2s and greater
    // than 2 in array
    $twoCount = 0; $twoGrCount = 0;

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == 2)
            $twoCount++;
        else if ($arr[$i] > 2)
            $twoGrCount++;
    }
    return $twoCount * $twoGrCount +
          ($twoGrCount * ($twoGrCount -
                               1)) / 2;
}

// Driver Code
$arr = array(3, 4, 5);
$n = sizeof($arr);
echo(CountPairs($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of efficient approach to count valid pairs.

    // returns the number of valid pairs
    function CountPairs(arr, n)
    {
        // traversing the array, counting the
        // number of 2s and greater than 2
        // in array
        let twoCount = 0, twoGrCount = 0;
        for (let i = 0; i<n; i++)
        {
            if (arr[i] == 2)
                twoCount++;
            else if (arr[i] > 2)
                twoGrCount++;
        }
        return twoCount*twoGrCount + parseInt((twoGrCount*(twoGrCount-1))/2, 10);
    }

    let arr = [3, 4, 5];
    let n = arr.length;
    document.write(CountPairs(arr, n));

</script>
```

输出:

```
3
```

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。