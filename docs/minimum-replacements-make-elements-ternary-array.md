# 使三进制数组的元素相同的最少替换次数

> 原文:[https://www . geesforgeks . org/minimum-replacements-make-elements-三元数组/](https://www.geeksforgeeks.org/minimum-replacements-make-elements-ternary-array/)

给定一个三进制数组(每个元素有三个可能值 1、2 和 3 中的一个)。我们的任务是替换其中的最小数量的数字，以便数组中的所有数字彼此相等。
**例:**

```
Input :  arr[] = 1 3 2 2 2 1 1 2 3
Output : 5
In this example, frequency of 1 is 3, 
frequency of 2 is 4 and frequency of 3
is 2\. As we can see that 2 is having the 
more frequency than 1 and 3\. So, if we 
replace all the 1's and 3's by 2 then, 
the resultant array has all the elements 
equal to each other in minimum replacements.
Here, total no. of 1's and 3's is 5 so it
takes 5 replacements to replace them by 2\. 
Hence, the output is 5.

Input : arr[] = 3 3 2 2 1 3
Output : 3
In this example, 3 has the max frequency.
Hence, minimum number of replacements are 
3 to replace 1 and 2 by 3\. Hence, the output
is 3.
```

方法是计算给定数组中每个元素的频率。那么，n(元素数量)和 max_frequency(元素在数组中出现的最长时间的频率)之差将是所需的最小替换次数。

## C++

```
// CPP program minimum number of replacements
// needed to be performed to make all the numbers
// in the given array equal.
#include <bits/stdc++.h>
using namespace std;

int minReplacements(int arr[], int n)
{
    // Find the most frequent element
    int freq[3] = { 0 };
    for (int i = 0; i < n; i++)
        freq[arr[i] - 1]++;
    int max_freq = *max_element(freq, freq + 3);

    // Returning count of replacing other elements
    // with the most frequent.
    return (n - max_freq);
}

// Driver Function
int main()
{
    int arr[] = { 1, 3, 2, 2, 2, 1, 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minReplacements(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program minimum
// number of replacements
// needed to be performed
// to make all the numbers
// in the given array equal
import java .io.*;
import java .util.*;

class GFG
{

// Function for
// minimum replacements
static int minReplacements(int []arr,
                           int n)
{
    // Find the most
    // frequent element
    int []freq = new int[3];
    for (int i = 0; i < n; i++)
        freq[arr[i] - 1]++;
        Arrays.sort(freq);
    int max_freq = freq[2];

    // Returning count of
    // replacing other elements
    // with the most frequent
    return (n - max_freq);
}

// Driver code
static public void main (String[] args)
{
    int []arr = {1, 3, 2, 2,
                 2, 1, 1, 2, 3};
    int n = arr.length;
    System.out.println(minReplacements(arr, n));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program minimum number of
# replacements needed to be performed
# to make all the numbers in the given
# array equal.

def minReplacements(arr, n):

    # Find the most frequent element
    freq = [0] * 3
    for i in range(n):
        freq[arr[i] - 1] += 1
    freq.sort()
    max_freq = freq[2]

    # Returning count of replacing other
    # elements with the most frequent.
    return (n - max_freq)

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 3, 2, 2,
            2, 1, 1, 2, 3 ]
    n = len(arr)
    print( minReplacements(arr, n) )

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program minimum number of
// replacements needed to be
// performed to make all the
// numbers in the given array equal
using System;
using System.Linq;

public class GFG
{

// Function for minimum replacements
static int minReplacements(int []arr, int n)
{
    // Find the most frequent element
    int []freq = new int[3];
    for (int i = 0; i < n; i++)
        freq[arr[i] - 1]++;
    int max_freq = freq.Max();

    // Returning count of replacing other
    // elements with the most frequent
    return (n - max_freq);
}

    // Driver code
    static public void Main ()
    {
        int []arr = {1, 3, 2, 2, 2, 1, 1, 2, 3};
        int n = arr.Length;
        Console.WriteLine(minReplacements(arr, n));

    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

    // Javascript program minimum
    // number of replacements
    // needed to be performed
    // to make all the numbers
    // in the given array equal

    // Function for
    // minimum replacements
    function minReplacements(arr, n)
    {
        // Find the most
        // frequent element
        let freq = new Array(3);
        freq.fill(0);
        for (let i = 0; i < n; i++)
            freq[arr[i] - 1]++;
          freq.sort();
        let max_freq = freq[2];

        // Returning count of
        // replacing other elements
        // with the most frequent
        return (n - max_freq);
    }

    let arr = [1, 3, 2, 2, 2, 1, 1, 2, 3];
    let n = arr.length;
    document.write(minReplacements(arr, n));

</script>
```

**输出:**

```
5
```