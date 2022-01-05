# 通过交换和为奇数的元素来打印字典上最小的数组

> 原文:[https://www . geeksforgeeks . org/print-按字典序最小数组交换元素-其和为奇数/](https://www.geeksforgeeks.org/print-the-lexicographically-smallest-array-by-swapping-elements-whose-sum-is-odd/)

给定一组 **N 个**整数。任务是通过多次应用给定的操作来找到字典上最小的数组。操作是选取两个元素**a<sub>I</sub>T5】和**a<sub>j</sub>T9】(1<= I，j < =N)使得**a<sub>I</sub>+a<sub>j</sub>T15】为奇数，然后互换**a<sub>I</sub>T19】和**a<sub>j</sub>T23】。
**举例:************ 

> **输入:** a[] = {1，5，4，3，2}
> **输出:** 1 2 3 4 5
> **解释:**先换(5，2)再换(4，3)。这是通过
> 交换满足给定条件
> **输入:** a[] = {4，2}
> **输出:** 4 2
> **解释:**不可能交换任何元素可以得到的
> 字典上最小的可能数组。

**接近**:观察两个元素如果奇偶性不同，是否有可能互换。如果数组中的所有元素具有相同的奇偶校验**(奇数+奇数和偶数+偶数不是奇数)**，则不可能进行交换。因此，答案将只是输入数组。否则，您实际上可以交换任何一对元素。假设你想交换两个元素，a 和 b，它们具有相同的奇偶性。必须有第三个元素 c 具有不同的奇偶性。不失一般性，假设数组为**【a，b，c】**。让我们进行以下交换:

*   交换 a 和 c:
*   交换 b 和 c: [b，c，a]
*   交换 a 和 c: [b，a，c]

换句话说，用 c 作为一个中间元素来交换 a 和 b，之后它总是会回到原来的位置。因为任何一对元素之间都可以交换，所以我们总是可以[对数组进行排序](https://www.geeksforgeeks.org/sort-c-stl/)，这将是字典上最小的数组。
以下是上述办法的实施情况:

## C++

```
// CPP program to find possible
// lexicographically smaller array
// by swapping only elements whose sum is odd
#include <bits/stdc++.h>
using namespace std;

// Function to find possible lexicographically smaller array
void lexicographically_smaller(int arr[], int n)
{
    // To store number of even and odd integers
    int odd = 0, even = 0;

    // Find number of even and odd integers
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2)
            odd++;
        else
            even++;
    }

    // If it possible to make
    // lexicographically smaller
    if (odd && even)
        sort(arr, arr + n);

    // Print the array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 4, 3, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    lexicographically_smaller(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find possible
// lexicographically smaller array
// by swapping only elements whose sum is odd
import java.util.*;

class GFG
{

// Function to find possible lexicographically smaller array
static void lexicographically_smaller(int arr[], int n)
{
    // To store number of even and odd integers
    int odd = 0, even = 0;

    // Find number of even and odd integers
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If it possible to make
    // lexicographically smaller
    if (odd > 0 && even > 0)
        Arrays.sort(arr);

    // Print the array
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 4, 3, 2 };

    int n = arr.length;

    // Function call
    lexicographically_smaller(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find possible
# lexicographically smaller array
# by swapping only elements whose sum is odd

# Function to find possible
# lexicographically smaller array
def lexicographically_smaller(arr, n):

    # To store number of even and odd integers
    odd, even = 0, 0;

    # Find number of even and odd integers
    for i in range(n):
        if (arr[i] % 2 == 1):
            odd += 1;
        else:
            even += 1;

    # If it possible to make
    # lexicographically smaller
    if (odd > 0 and even > 0):
        arr.sort();

    # Print the array
    for i in range(n):
        print(arr[i], end = " ");

# Driver code
if __name__ == '__main__':

    arr = [ 1, 5, 4, 3, 2 ];

    n = len(arr);

    # Function call
    lexicographically_smaller(arr, n);

# This code contributed by Rajput-Ji
```

## C#

```
// C# program to find possible
// lexicographically smaller array by
// swapping only elements whose sum is odd
using System;

class GFG
{

// Function to find possible
// lexicographically smaller array
static void lexicographically_smaller(int []arr, int n)
{
    // To store number of even and odd integers
    int odd = 0, even = 0;

    // Find number of even and odd integers
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If it possible to make
    // lexicographically smaller
    if (odd > 0 && even > 0)
        Array.Sort(arr);

    // Print the array
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 5, 4, 3, 2 };

    int n = arr.Length;

    // Function call
    lexicographically_smaller(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program to find possible
// lexicographically smaller array
// by swapping only elements whose sum is odd

// Function to find possible lexicographically smaller array
function lexicographically_smaller(arr , n)
{
    // To store number of even and odd integers
    var odd = 0, even = 0;

    // Find number of even and odd integers
    for (var i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If it possible to make
    // lexicographically smaller
    if (odd > 0 && even > 0)
        arr.sort((a,b)=>a-b);

    // Print the array
    for (i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver code
var arr = [ 1, 5, 4, 3, 2 ];

var n = arr.length;

// Function call
lexicographically_smaller(arr, n);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
1 2 3 4 5
```

**时间复杂度** : O(N log N)