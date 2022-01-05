# 给定集合的所有可能子集的按位“或”的和

> 原文:[https://www . geeksforgeeks . org/给定集合的所有可能子集的按位或和/](https://www.geeksforgeeks.org/sum-of-bitwise-or-of-all-possible-subsets-of-given-set/)

给定一个大小为 n 的数组 arr[]，我们需要找到所有值的和，这些值来自于对子集的所有元素进行 or 运算。
**先决条件:** [给定集合的子集和](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)
**示例:**

```
Input :  arr[] = {1, 2, 3}
Output : 18
Total Subsets = 23 -1= 7 
1 = 1
2 = 2
3 = 3
1 | 2 = 3
1 | 3 = 3
2 | 3 = 3
1 | 2 | 3 = 3
0(empty subset)
Now SUM of all these ORs = 1 + 2 + 3 + 3 +
                            3 + 3 + 3
                          = 18

Input : arr[] = {1, 2, 3}
Output : 18

```

一种**天真的方法**是取数组[]元素的所有可能的 OR 组合，然后执行所有值的求和。**这种方法的时间复杂度**呈指数增长，因此对于大的 n 值来说不是更好的方法。
一种**高效的**方法是找到关于 or 属性的模式。现在再次考虑二进制形式的子集，如:

```
    1 = 001
    2 = 010
    3 = 011
1 | 2 = 011
1 | 3 = 011
2 | 3 = 011
1|2|3 = 011
```

这里我们不取数组所有可能元素的“或”，而是考虑位为 1 的所有可能子集。
现在，考虑所有结果 ORs 中的第 ith 位，只有当子集中元素的第 ith 位都为 0 时，它才为零。
第 1 位子集的数量=所有可能子集的总数–所有第 0 位子集。这里，全部子集= 2^n–1，所有第 I 位为 0 的子集=数组所有元素的第 I 位的 2^(零计数–1。现在，总子集 OR 具有第 1 位=(第 1 位零的 2^n-1)-(2^(count)-1)。值为 1 的位所贡献的总值=总子集或值为 1 的位*(2^i).
现在，总和=(具有第 1 位的总子集)* 2^i +(具有第 i+1 位的总子集)* 2^(i+1)+……+(具有第 32 位的总子集)* 2^32.

## C++

```
// CPP code to find the OR_SUM
#include <bits/stdc++.h>
using namespace std;

#define INT_SIZE 32

// function to find the OR_SUM
int ORsum(int arr[], int n)
{
    // create an array of size 32
    // and store the sum of bits
    // with value 0 at every index.
    int zerocnt[INT_SIZE] = { 0 };

    for (int i = 0; i < INT_SIZE; i++)    
        for (int j = 0; j < n; j++)       
            if (!(arr[j] & 1 << i))
                zerocnt[i] += 1;           

    // for each index the OR sum contributed
    // by that bit of subset will be 2^(bit index)
    // now the OR of the bits is 0 only if
    // all the ith bit of the elements in subset
    // is 0.
    int ans = 0;
    for (int i = 0; i < INT_SIZE; i++)
    {
        ans += ((pow(2, n) - 1) -
               (pow(2, zerocnt[i]) - 1)) *
                pow(2, i);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << ORsum(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find
// the OR_SUM
import java.io.*;

class GFG {

static int INT_SIZE = 32;

    // function to find
    // the OR_SUM
    static int ORsum(int []arr, int n)
    {

        // create an array of size 32
        // and store the sum of bits
        // with value 0 at every index.
        int zerocnt[] = new int[INT_SIZE] ;

        for (int i = 0; i < INT_SIZE; i++)    
            for (int j = 0; j < n; j++)    
                if ((arr[j] & 1 << i) == 0)
                    zerocnt[i] += 1;        

        // for each index the OR
        // sum contributed by that
        // bit of subset will be
        // 2^(bit index) now the OR
        // of the bits is 0 only if
        // all the ith bit of the 
        // elements in subset is 0.
        int ans = 0;
        for (int i = 0; i < INT_SIZE; i++)
        {
            ans += ((Math.pow(2, n) - 1) -
                (Math.pow(2, zerocnt[i]) - 1)) *
                                 Math.pow(2, i);
        }

        return ans;

    }
    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3 };
        int size = arr.length;
        System.out.println(ORsum(arr, size));

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
INT_SIZE = 32

# function to find the OR_SUM
def ORsum(arr, n):
    # create an array of size 32
    # and store the sum of bits
    # with value 0 at every index.
    zerocnt = [0 for i in range(INT_SIZE)]

    for i in range(INT_SIZE):   
        for j in range(n):   
            if not (arr[j] & (1 << i)):
                zerocnt[i] += 1           

    # for each index the OR sum contributed
    # by that bit of subset will be 2^(bit index)
    # now the OR of the bits is 0 only if
    # all the ith bit of the elements in subset
    # is 0.
    ans = 0
    for i in range(INT_SIZE):
        ans += ((2 ** n - 1) - (2 ** zerocnt[i] - 1)) * 2 ** i

    return ans

# Driver code

if __name__ == "__main__":
    arr= [1, 2, 3]
    size = len(arr)
    print(ORsum(arr, size))

# This code is contributed by vaibhav29498
```

## C#

```
// C# code to find
// the OR_SUM
using System;

class GFG {

static int INT_SIZE = 32;

    // function to find
    // the OR_SUM
    static int ORsum(int []arr, int n)
    {

        // create an array of size 32
        // and store the sum of bits
        // with value 0 at every index.
        int []zerocnt = new int[INT_SIZE] ;

        for (int i = 0; i < INT_SIZE; i++)    
            for (int j = 0; j < n; j++)    
                if ((arr[j] & 1 << i) == 0)
                    zerocnt[i] += 1;        

        // for each index the OR
        // sum contributed by that
        // bit of subset will be
        // 2^(bit index) now the OR
        // of the bits is 0 only if
        // all the ith bit of the
        // elements in subset is 0.
        int ans = 0;
        for (int i = 0; i < INT_SIZE; i++)
        {
            ans += (int)(((Math.Pow(2, n) - 1) -
                 (Math.Pow(2, zerocnt[i]) - 1)) *
                                Math.Pow(2, i));
        }

        return ans;

    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3};
        int size = arr.Length;
        Console.Write(ORsum(arr, size));

    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the OR_SUM

$INT_SIZE = 32;

// function to find the OR_SUM
function ORsum(&$arr, $n)
{
    global $INT_SIZE;

    // create an array of size 32
    // and store the sum of bits
    // with value 0 at every index.
    $zerocnt = array_fill(0, $INT_SIZE, NULL);

    for ($i = 0; $i < $INT_SIZE; $i++)    
        for ($j = 0; $j < $n; $j++)    
            if (!($arr[$j] & 1 << $i))
                $zerocnt[$i] += 1;        

    // for each index the OR sum contributed
    // by that bit of subset will be 2^(bit index)
    // now the OR of the bits is 0 only if
    // all the ith bit of the elements in
    // subset is 0.
    $ans = 0;
    for ($i = 0; $i < $INT_SIZE; $i++)
    {
        $ans += ((pow(2, $n) - 1) -
                 (pow(2, $zerocnt[$i]) - 1)) *
                  pow(2, $i);
    }

    return $ans;
}

// Driver code
$arr = array(1, 2, 3);
$size = sizeof($arr);
echo ORsum($arr, $size);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// JavaScript code to find the OR_SUM

let INT_SIZE = 32;
// function to find the OR_SUM
function ORsum(arr, n)
{
    // create an array of size 32
    // and store the sum of bits
    // with value 0 at every index.
    let zerocnt = new Uint8Array(INT_SIZE);

    for (let i = 0; i < INT_SIZE; i++)    
        for (let j = 0; j < n; j++)        
            if (!(arr[j] & 1 << i))
                zerocnt[i] += 1;            

    // for each index the OR sum contributed
    // by that bit of subset will be 2^(bit index)
    // now the OR of the bits is 0 only if
    // all the ith bit of the elements in subset
    // is 0.
    let ans = 0;
    for (let i = 0; i < INT_SIZE; i++)
    {
        ans += ((Math.pow(2, n) - 1) -
            (Math.pow(2, zerocnt[i]) - 1)) *
                Math.pow(2, i);
    }

    return ans;
}

// Driver code

    let arr = [ 1, 2, 3 ];
    let size = arr.length;
    document.write(ORsum(arr, size));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
18
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)