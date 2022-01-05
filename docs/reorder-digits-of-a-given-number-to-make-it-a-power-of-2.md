# 给定数字的数字重新排序，使其为 2 的幂

> 原文:[https://www . geesforgeks . org/给定数字的重新排序使其成为 2 的幂/](https://www.geeksforgeeks.org/reorder-digits-of-a-given-number-to-make-it-a-power-of-2/)

给定一个正整数 **N** ，任务是重新排列给定整数的位数，使[整数成为**2**T5 的幂。如果存在多个解，则打印最小可能的整数，而不前导 **0** 。否则，打印 **-1** 。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** N = 460
> **输出:** 64
> **说明:**
> 64 是 2 的幂，需要的输出是 64。
> 
> **输入:** 36
> **输出:** -1
> **解释:**
> 整数可能的重排是{ 36，63 }。
> 因此，要求的输出为-1。

**方法:**想法是[生成给定整数](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)的数字的所有排列。对于每个排列，[检查整数是否是 **2** 的幂，或者不是](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。如果发现为真，则打印整数。否则，打印 **-1** 。按照以下步骤解决问题:

*   [将给定的整数转换成字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)比如说**字符串**。
*   [按升序排列字符串](https://www.geeksforgeeks.org/sort-c-stl/)。
*   [生成字符串的所有可能排列](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)。对于每个排列，检查字符串的[等价整数值是否是 **2** 的幂，或者不是](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。如果发现是真的，那就打印号码。
*   如果整数的数字没有这样的排列，那么打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the digits of N
// such that N become power of 2
int reorderedPowerOf2(int n)
{

    // Stores digits of N
    string str = to_string(n);

    // Sort the string
    // ascending order
    sort(str.begin(), str.end());

    // Stores count of digits in N
    int sz = str.length();

    // Generate all permutation and check if
    // the permutation if power of 2 or not
    do {

        // Update n
        n = stoi(str);

        // If n is power of 2
        if (n && !(n & (n - 1))) {

            return n;
        }
    } while (next_permutation(str.begin(), str.end()));

    return -1;
}

// Driver Code
int main()
{
    int n = 460;

    cout << reorderedPowerOf2(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG {

    static void swap(char[] chars, int i, int j)
    {
        char ch = chars[i];
        chars[i] = chars[j];
        chars[j] = ch;
    }

    static void reverse(char[] chars, int start)
    {
        for (int i = start, j = chars.length - 1; i < j;
             i++, j--) {
            swap(chars, i, j);
        }
    }

    // Function to find lexicographically next permutations
    // of a string. It returns true if the string could be
    // rearranged as a lexicographically greater permutation
    // else it returns false
    static boolean next_permutation(char[] chars)
    {

        // Find largest index i such
        // that chars[i - 1] is less than chars[i]
        int i = chars.length - 1;
        while (chars[i - 1] >= chars[i]) {

            // if i is first index of the string,
            // that means we are already at
            // highest possible permutation i.e.
            // string is sorted in desc order
            if (--i == 0) {
                return false;
            }
        }

        // if we reach here, substring chars[i..n)
        // is sorted in descending order
        // i.e. chars[i-1] < chars[i] >= chars[i+1] >=
        // chars[i+2] >= ... >= chars[n-1]

        // Find highest index j to the right of index i such
        // that chars[j] > chars[i–1]
        int j = chars.length - 1;
        while (j > i && chars[j] <= chars[i - 1]) {
            j--;
        }

        // swap characters at index i-1 with index j
        swap(chars, i - 1, j);

        // reverse the substring chars[i..n) and return true
        reverse(chars, i);

        return true;
    }

    // Function to rearrange the digits of N
    // such that N become power of 2
    static int reorderedPowerOf2(int n)
    {

        // Stores digits of N
        String str = Integer.toString(n);
        char[] Str = str.toCharArray();

        // Sort the string
        // ascending order
        Arrays.sort(Str);

        // Stores count of digits in N
        int sz = Str.length;

        // Generate all permutation and check if
        // the permutation if power of 2 or not
        do {

            // Update n
            n = Integer.parseInt(new String(Str));

            // If n is power of 2
            if (n > 0 && ((n & (n - 1)) == 0)) {
                return n;
            }
        } while (next_permutation(Str));

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 460;
        System.out.print(reorderedPowerOf2(n));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python program to implement
# the above approach

def next_permutation():
    global a
    i = len(a) - 2
    while not (i < 0 or int(a[i]) < int(a[i + 1])):
        i -= 1
    if i < 0:
        return False

    # else
    j = len(a) - 1
    while not (int(a[j]) > int(a[i])):
        j -= 1
    a[i], a[j] = a[j], a[i]        # swap
    # reverse elements from position i+1 till the end of the sequence
    a[i + 1:] = reversed(a[i + 1:])
    return True

# Function to rearrange the digits of N
# such that N become power of 2

def reorderedPowerOf2(n):
    global a

    # Sort the string
    # ascending order
    a = sorted(a)

    # Stores count of digits in N
    sz = len(a)

    # Generate all permutation and check if
    # the permutation if power of 2 or not
    while True:

        # Update n
        n = int("".join(a))

        # If n is power of 2
        if (n and not (n & (n - 1))):
            return n
        if not next_permutation():
            break

    return -1

# Driver Code
if __name__ == '__main__':
    n = 460
    a = [i for i in str(n)]

    print(reorderedPowerOf2(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {
    static void swap(char[] chars, int i, int j)
    {
        char ch = chars[i];
        chars[i] = chars[j];
        chars[j] = ch;
    }

    static void reverse(char[] chars, int start)
    {
        for (int i = start, j = chars.Length - 1; i < j;
             i++, j--) {
            swap(chars, i, j);
        }
    }

    // Function to find lexicographically next permutations
    // of a string. It returns true if the string could be
    // rearranged as a lexicographically greater permutation
    // else it returns false
    static bool next_permutation(char[] chars)
    {

        // Find largest index i such
        // that chars[i - 1] is less than chars[i]
        int i = chars.Length - 1;
        while (chars[i - 1] >= chars[i]) {

            // if i is first index of the string,
            // that means we are already at
            // highest possible permutation i.e.
            // string is sorted in desc order
            if (--i == 0) {
                return false;
            }
        }

        // if we reach here, substring chars[i..n)
        // is sorted in descending order
        // i.e. chars[i-1] < chars[i] >= chars[i+1] >=
        // chars[i+2] >= ... >= chars[n-1]

        // Find highest index j to the right of index i such
        // that chars[j] > chars[i–1]
        int j = chars.Length - 1;
        while (j > i && chars[j] <= chars[i - 1]) {
            j--;
        }

        // swap characters at index i-1 with index j
        swap(chars, i - 1, j);

        // reverse the substring chars[i..n) and return true
        reverse(chars, i);

        return true;
    }

    // Function to rearrange the digits of N
    // such that N become power of 2
    static int reorderedPowerOf2(int n)
    {

        // Stores digits of N
        string str = n.ToString();
        char[] Str = str.ToCharArray();

        // Sort the string
        // ascending order
        Array.Sort(Str);

        // Stores count of digits in N
        int sz = Str.Length;

        // Generate all permutation and check if
        // the permutation if power of 2 or not
        do {

            // Update n
            n = Convert.ToInt32(new string(Str));

            // If n is power of 2
            if (n > 0 && ((n & (n - 1)) == 0)) {
                return n;
            }
        } while (next_permutation(Str));

        return -1;
    }

    // Driver code
    static void Main()
    {
        int n = 460;
        Console.WriteLine(reorderedPowerOf2(n));
    }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

function swap(chars,i,j)
{
    let ch = chars[i];
        chars[i] = chars[j];
        chars[j] = ch;
}

function reverse(chars,start)
{
    for (let i = start, j = chars.length - 1; i < j;
             i++, j--) {
            swap(chars, i, j);
        }
}

// Function to find lexicographically next permutations
// of a string. It returns true if the string could be
// rearranged as a lexicographically greater permutation
// else it returns false
function next_permutation(chars)
{
    // Find largest index i such
        // that chars[i - 1] is less than chars[i]
        let i = chars.length - 1;
        while (chars[i - 1] >= chars[i]) {

            // if i is first index of the string,
            // that means we are already at
            // highest possible permutation i.e.
            // string is sorted in desc order
            if (--i == 0) {
                return false;
            }
        }

        // if we reach here, substring chars[i..n)
        // is sorted in descending order
        // i.e. chars[i-1] < chars[i] >= chars[i+1] >=
        // chars[i+2] >= ... >= chars[n-1]

        // Find highest index j to the right of index i such
        // that chars[j] > chars[i–1]
        let j = chars.length - 1;
        while (j > i && chars[j] <= chars[i - 1]) {
            j--;
        }

        // swap characters at index i-1 with index j
        swap(chars, i - 1, j);

        // reverse the substring chars[i..n) and return true
        reverse(chars, i);

        return true;
}

// Function to rearrange the digits of N
// such that N become power of 2
function reorderedPowerOf2(n)
{
     // Stores digits of N
        let str = n.toString();
        let Str = str.split("");

        // Sort the string
        // ascending order
        Str.sort();

        // Stores count of digits in N
        let sz = Str.length;

        // Generate all permutation and check if
        // the permutation if power of 2 or not
        do {

            // Update n
            n = parseInt((Str).join(""));

            // If n is power of 2
            if (n > 0 && ((n & (n - 1)) == 0)) {
                return n;
            }
        } while (next_permutation(Str));

        return -1;
}

// Driver code
let n = 460;
document.write(reorderedPowerOf2(n));

// This code is contributed by patel2127

</script>
```

**Output**

```
64
```

**时间复杂度:**O(log<sub>10</sub>N *(log<sub>10</sub>N)！)
**辅助空间:** O(log <sub>10</sub> N)

**方法 2:**

我们将创建一个数字数组，存储给定数字的数字计数，我们将迭代 2 的幂，并检查是否有任何 digitcount 数组与给定数字 digit count 数组匹配。

以下是该方法的实施情况:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG {

    public static int reorderedPowerOf2(int N)
    {
        int[] arr = digitarr(N);
        // N is the given number
        // arr have the digit count of N
        for (int i = 0; i < 31; i++) {
            // check if arr matches with any digitcount
            // array of 2^i
            if (Arrays.equals(arr, digitarr(1 << i)))
                return (int)Math.pow(2, i);
        }
        return -1;
    }
    public static int[] digitarr(int n)
    {
        int[] res
            = new int[10]; // stores the digit count of n
        while (n > 0) {
            if (n % 10 != 0) {
                res[n % 10]++;
            }
            n /= 10;
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 460;
        System.out.print(reorderedPowerOf2(n));
    }
}
```

**Output**

```
64
```