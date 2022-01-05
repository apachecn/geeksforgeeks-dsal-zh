# 生成一个可被 N 整除的数的所有可能排列

> 原文:[https://www . geeksforgeeks . org/generate-所有可能的被 n 整除的数字排列/](https://www.geeksforgeeks.org/generate-all-possible-permutations-of-a-number-divisible-by-n/)

给定一个数字字符串 **S** ，任务是打印该字符串中可被 **N** 整除的所有排列。

**示例:**

> **输入:** N = 5，S = "125"
> **输出:** 125 215
> **解释:**
> 所有可能的排列都是 S 是{125，152，215，251，5 21，512}。
> 在这 6 个排列中，只有 2 个{125，215}能被 N (= 5)整除。
> 
> **输入:** N = 7，S =【4321】
> T3】输出: 4312 4123 3241

**方法:**想法是生成所有可能的排列，对于每个排列，检查它是否能被 **N** 整除。对于每个被 **N 整除的排列，打印出来。**

下面是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Swap two
// characters
void swap_(char& a, char& b)
{
    char temp;
    temp = a;
    a = b;
    b = temp;
}

// Function to generate all permutations
// and print the ones that are
// divisible by the N
void permute(char* str, int l, int r, int n)
{
    int i;

    if (l == r) {

        // Convert string to integer
        int j = atoi(str);

        // Check for divisibility
        // and print it
        if (j % n == 0)
            cout << str << endl;

        return;
    }

    // Print all the permutations
    for (i = l; i < r; i++) {

        // Swap characters
        swap_(str[l], str[i]);

        // Permute remaining
        // characters
        permute(str, l + 1, r, n);

        // Revoke the swaps
        swap_(str[l], str[i]);
    }
}

// Driver Code
int main()
{
    char str[100] = "125";
    int n = 5;
    int len = strlen(str);

    if (len > 0)
        permute(str, 0, len, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to Swap two
// characters
static void swap_(char []a, int l, int i)
{
    char temp;
    temp = a[l];
    a[l] = a[i];
    a[i] = temp;
}

// Function to generate all permutations
// and print the ones that are
// divisible by the N
static void permute(char[] str, int l,
                         int r, int n)
{
    int i;

    if (l == r)
    {

        // Convert String to integer
        int j = Integer.valueOf(String.valueOf(str));

        // Check for divisibility
        // and print it
        if (j % n == 0)
            System.out.print(String.valueOf(str) + "\n");

        return;
    }

    // Print all the permutations
    for(i = l; i < r; i++)
    {

        // Swap characters
        swap_(str, l, i);

        // Permute remaining
        // characters
        permute(str, l + 1, r, n);

        // Revoke the swaps
        swap_(str, l, i);
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "125";
    int n = 5;
    int len = str.length();

    if (len > 0)
        permute(str.toCharArray(), 0, len, n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to generate all
# permutations and print
# the ones that are
# divisible by the N
def permute(st, l, r, n):

    if (l == r):

        # Convert string
        # to integer
        p = ''.join(st)
        j = int(p)

        # Check for divisibility
        # and print it
        if (j % n == 0):
            print (p)

        return

    # Print all the
    # permutations
    for i in range(l, r):

        # Swap characters
        st[l], st[i] = st[i], st[l]

        # Permute remaining
        # characters
        permute(st, l + 1, r, n)

        # Revoke the swaps
        st[l], st[i] = st[i] ,st[l]

# Driver Code
if __name__ == "__main__":

    st = "125"
    n = 5
    length = len(st)

    if (length > 0):
      p = list(st)
      permute(p, 0, length, n);

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to Swap two
// characters
static void swap_(char []a, int l,
                            int i)
{
    char temp;
    temp = a[l];
    a[l] = a[i];
    a[i] = temp;
}

// Function to generate all permutations
// and print the ones that are
// divisible by the N
static void permute(char[] str, int l,
                         int r, int n)
{
    int i;

    if (l == r)
    {

        // Convert String to integer
        int j = Int32.Parse(new string(str));

        // Check for divisibility
        // and print it
        if (j % n == 0)
            Console.Write(new string(str) + "\n");

        return;
    }

    // Print all the permutations
    for(i = l; i < r; i++)
    {

        // Swap characters
        swap_(str, l, i);

        // Permute remaining
        // characters
        permute(str, l + 1, r, n);

        // Revoke the swaps
        swap_(str, l, i);
    }
}

// Driver Code
public static void Main(string[] args)
{
    string str = "125";
    int n = 5;
    int len = str.Length;

    if (len > 0)
        permute(str.ToCharArray(), 0, len, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to Swap two
// characters
function swap_(a, l, i)
{
    let temp;
    temp = a[l];
    a[l] = a[i];
    a[i] = temp;
}

// Function to generate all permutations
// and print the ones that are
// divisible by the N
function permute(str, l, r, n)
{
    let i;

    if (l == r)
    {

        // Convert String to integer
        let j = parseInt((str).join(""));

        // Check for divisibility
        // and print it
        if (j % n == 0)
            document.write((str).join("") + "<br>");

        return;
    }

    // Print all the permutations
    for(i = l; i < r; i++)
    {

        // Swap characters
        swap_(str, l, i);

        // Permute remaining
        // characters
        permute(str, l + 1, r, n);

        // Revoke the swaps
        swap_(str, l, i);
    }
}

// Driver Code
let str = "125";
let n = 5;
let len = str.length;

if (len > 0)
    permute(str.split(""), 0, len, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
125
215
```

***时间复杂度:** O(N！)*
***辅助空间:** O(N)*