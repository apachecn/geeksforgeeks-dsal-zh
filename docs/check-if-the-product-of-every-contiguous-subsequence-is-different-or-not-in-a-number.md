# 检查每个相邻子序列的乘积在一个数字中是否不同

> 原文:[https://www . geeksforgeeks . org/check-如果每个连续子序列的乘积是不同或不在一个数字中/](https://www.geeksforgeeks.org/check-if-the-product-of-every-contiguous-subsequence-is-different-or-not-in-a-number/)

给定一个整数 **N** ，任务是检查每组连续数字的乘积是否不同。

**示例:**

> **输入:**N = 234
> T3】输出:是
> T6】
> 
> | 一组 | 产品 |
> | --- | --- |
> | {2} | **2** |
> | {2, 3} | 2 * 3 = **6** |
> | {2, 3, 4} | 2 * 3 * 4 = **24** |
> | {3} | three |
> | {3, 4} | 3 * 4 = **12** |
> | {4} | **4** |
> 
> 所有的产品都是不同的。
> 
> **输入:** N = 1234
> **输出:**否
> 将{1，2}和{2}设置为同一产品，即 2。

**方法:**将每个相邻子序列的数字乘积存储在一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。如果要插入的产品在任何时候都已经存在于集合中，那么答案是“否”，否则最终所有产品都是不同的。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the product
// of every digit of a contiguous subsequence
// is distinct
bool productsDistinct(int N)
{
    // To store the given number as a string
    string s = "";

    // Append all the digits
    // starting from the end
    while (N) {
        s += (char)(N % 10 + '0');
        N /= 10;
    }

    // Reverse the string to get
    // the  original number
    reverse(s.begin(), s.end());

    // Store size of the string
    int sz = s.size();

    // Set to store product of
    // each contiguous subsequence
    set<int> se;

    // Find product of every
    // contiguous subsequence
    for (int i = 0; i < sz; i++) {
        int product = 1;
        for (int j = i; j < sz; j++) {
            product *= (int)(s[j] - '0');

            // If current product already
            // exists in the set
            if (se.find(product) != se.end())
                return false;
            else
                se.insert(product);
        }
    }

    return true;
}

// Driver code
int main()
{
    int N = 2345;

    if (productsDistinct(N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if
// the product of every digit of a
// contiguous subsequence is distinct
static boolean productsDistinct(int N)
{

    // To store the given number
    // as a string
    String s = "";

    // Append all the digits
    // starting from the end
    while (N > 0)
    {
        s += (char)(N % 10 + '0');
        N /= 10;
    }

    // Reverse the string to get
    // the original number
    s = reverse(s);

    // Store size of the string
    int sz = s.length();

    // Set to store product of
    // each contiguous subsequence
    HashSet<Integer> se = new HashSet<Integer>();

    // Find product of every
    // contiguous subsequence
    for (int i = 0; i < sz; i++)
    {
        int product = 1;
        for (int j = i; j < sz; j++)
        {
            product *= (int)(s.charAt(j) - '0');

            // If current product already
            // exists in the set
            if (se.contains(product))
                return false;
            else
                se.add(product);
        }
    }
    return true;
}

static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r;
    r = a.length - 1;
    for (l = 0; l < r; l++, r--)
    {
        // Swap values of l and r
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver code
public static void main(String[] args)
{
    int N = 2345;

    if (productsDistinct(N))
        System.out.println("Yes");
    else
        System.out.println("No");
    }
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if the product
# of every digit of a contiguous subsequence
# is distinct
def productsDistinct(N):

    # To store the given number as a string
    s = ""

    # Append all the digits
    # starting from the end
    while (N):
        s += chr(N % 10 + ord('0'))
        N //= 10

    # Reverse the string to get
    # the original number
    s = s[::-1]

    # Store size of the string
    sz = len(s)

    # Set to store product of
    # each contiguous subsequence
    se = []

    # Find product of every
    # contiguous subsequence
    for i in range(sz):
        product = 1
        for j in range(i, sz, 1):
            product *= ord(s[j]) - ord('0')

            # If current product already
            # exists in the set
            for p in range(len(se)):
                if se[p] == product:
                    return False
                else:
                    se.append(product)

    return True

# Driver code
if __name__ == '__main__':
    N = 2345

    if (productsDistinct(N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns true if
// the product of every digit of a
// contiguous subsequence is distinct
static Boolean productsDistinct(int N)
{

    // To store the given number
    // as a string
    String s = "";

    // Append all the digits
    // starting from the end
    while (N > 0)
    {
        s += (char)(N % 10 + '0');
        N /= 10;
    }

    // Reverse the string to get
    // the original number
    s = reverse(s);

    // Store size of the string
    int sz = s.Length;

    // Set to store product of
    // each contiguous subsequence
    HashSet<int> se = new HashSet<int>();

    // Find product of every
    // contiguous subsequence
    for (int i = 0; i < sz; i++)
    {
        int product = 1;
        for (int j = i; j < sz; j++)
        {
            product *= (int)(s[j] - '0');

            // If current product already
            // exists in the set
            if (se.Contains(product))
                return false;
            else
                se.Add(product);
        }
    }
    return true;
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r;
    r = a.Length - 1;
    for (l = 0; l < r; l++, r--)
    {
        // Swap values of l and r
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver code
public static void Main(String[] args)
{
    int N = 2345;

    if (productsDistinct(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if the product
// of every digit of a contiguous subsequence
// is distinct
function productsDistinct(N)
{

    // To store the given number as a string
    var s = "";

    // Append all the digits
    // starting from the end
    while (N)
    {
        s += String.fromCharCode(
            N % 10 + '0'.charCodeAt(0));
        N = parseInt(N / 10);
    }

    // Reverse the string to get
    // the  original number
    s = s.split('').reverse().join('');

    // Store size of the string
    var sz = s.length;

    // Set to store product of
    // each contiguous subsequence
    var se = new Set();

    // Find product of every
    // contiguous subsequence
    for(var i = 0; i < sz; i++)
    {
        var product = 1;
        for(var j = i; j < sz; j++)
        {
            product *= (s[j].charCodeAt(0) -
                         '0'.charCodeAt(0));

            // If current product already
            // exists in the set
            if (se.has(product))
                return false;
            else
                se.add(product);
        }
    }
    return true;
}

// Driver code
var N = 2345;
if (productsDistinct(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
Yes
```