# 产生 n 位格雷码的回溯方法

> 原文:[https://www . geesforgeks . org/回溯-进场-生成-n-bit-gray-codes/](https://www.geeksforgeeks.org/backtracking-approach-generate-n-bit-gray-codes/)

给定数字 n，任务是生成 n 位格雷码(生成从 0 到 2^n-1 的位模式，使得连续模式相差一位)

**示例:**

```
Input : 2 
Output : 0 1 3 2
Explanation : 
00 - 0
01 - 1
11 - 3
10 - 2

Input : 3 
Output : 0 1 3 2 6 7 5 4

```

我们在[中讨论了一种生成 n 位格雷码](https://www.geeksforgeeks.org/given-a-number-n-generate-bit-patterns-from-0-to-2n-1-so-that-successive-patterns-differ-by-one-bit/)
的方法，本文提供了一种**回溯方法**来解决同样的问题。我们的想法是，对于 n 位中的每一位，我们可以选择忽略它，或者反转该位，这意味着对于 n 位，我们的灰度序列高达 2 ^。因此，我们进行两次递归调用，要么反转位，要么保持位不变。

## C++

```
// CPP program to find the gray sequence of n bits.
#include <iostream>
#include <vector>
using namespace std;

/* we have 2 choices for each of the n bits either we
   can include i.e invert the bit or we can exclude the
   bit i.e we can leave the number as it is. */
void grayCodeUtil(vector<int>& res, int n, int& num)
{
    // base case when we run out bits to process
    // we simply include it in gray code sequence.
    if (n == 0) {
        res.push_back(num);
        return;
    }

    // ignore the bit.
    grayCodeUtil(res, n - 1, num);

    // invert the bit.
    num = num ^ (1 << (n - 1));
    grayCodeUtil(res, n - 1, num);
}

// returns the vector containing the gray
// code sequence of n bits.
vector<int> grayCodes(int n)
{
    vector<int> res;

    // num is passed by reference to keep
    // track of current code.
    int num = 0;
    grayCodeUtil(res, n, num);

    return res;
}

// Driver function.
int main()
{
    int n = 3;
    vector<int> code = grayCodes(n);
    for (int i = 0; i < code.size(); i++)
        cout << code[i] << endl;   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find the gray sequence of n bits.
import java.util.*;

class GFG
{

static int num;

/* we have 2 choices for each of the n bits either we
can include i.e invert the bit or we can exclude the
bit i.e we can leave the number as it is. */
static void grayCodeUtil(Vector<Integer> res, int n)
{
    // base case when we run out bits to process
    // we simply include it in gray code sequence.
    if (n == 0)
    {
        res.add(num);
        return;
    }

    // ignore the bit.
    grayCodeUtil(res, n - 1);

    // invert the bit.
    num = num ^ (1 << (n - 1));
    grayCodeUtil(res, n - 1);
}

// returns the vector containing the gray
// code sequence of n bits.
static Vector<Integer> grayCodes(int n)
{
    Vector<Integer> res = new Vector<Integer>();

    // num is passed by reference to keep
    // track of current code.
    num = 0;
    grayCodeUtil(res, n);

    return res;
}

// Driver function.
public static void main(String[] args)
{
    int n = 3;
    Vector<Integer> code = grayCodes(n);
    for (int i = 0; i < code.size(); i++)
        System.out.print(code.get(i) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the
# gray sequence of n bits.

""" we have 2 choices for each of the n bits
either we can include i.e invert the bit or
we can exclude the bit i.e we can leave
the number as it is. """
def grayCodeUtil(res, n, num):

    # base case when we run out bits to process
    # we simply include it in gray code sequence.
    if (n == 0):
        res.append(num[0])
        return

    # ignore the bit.
    grayCodeUtil(res, n - 1, num)

    # invert the bit.
    num[0] = num[0] ^ (1 << (n - 1))
    grayCodeUtil(res, n - 1, num)

# returns the vector containing the gray
# code sequence of n bits.
def grayCodes(n):
    res = []

    # num is passed by reference to keep
    # track of current code.
    num = [0]
    grayCodeUtil(res, n, num)
    return res

# Driver Code
n = 3
code = grayCodes(n)
for i in range(len(code)):
    print(code[i])

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find the gray sequence of n bits.
using System;
using System.Collections.Generic;

class GFG
{

static int num;

/* we have 2 choices for each of the n bits either we
can include i.e invert the bit or we can exclude the
bit i.e we can leave the number as it is. */
static void grayCodeUtil(List<int> res, int n)
{
    // base case when we run out bits to process
    // we simply include it in gray code sequence.
    if (n == 0)
    {
        res.Add(num);
        return;
    }

    // ignore the bit.
    grayCodeUtil(res, n - 1);

    // invert the bit.
    num = num ^ (1 << (n - 1));
    grayCodeUtil(res, n - 1);
}

// returns the vector containing the gray
// code sequence of n bits.
static List<int> grayCodes(int n)
{
    List<int> res = new List<int>();

    // num is passed by reference to keep
    // track of current code.
    num = 0;
    grayCodeUtil(res, n);

    return res;
}

// Driver function.
public static void Main(String[] args)
{
    int n = 3;
    List<int> code = grayCodes(n);
    for (int i = 0; i < code.Count; i++)
        Console.Write(code[i] +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the gray sequence of n bits.

/* We have 2 choices for each of the n bits either we
can include i.e invert the bit or we can exclude the
bit i.e we can leave the number as it is. */
function grayCodeUtil(res, n, num)
{

    // Base case when we run out bits to process
    // we simply include it in gray code sequence.
    if (n == 0)
    {
        res.push(num[0]);
        return;
    }

    // Ignore the bit.
    grayCodeUtil(res, n - 1, num);

    // Invert the bit.
    num[0] = num[0] ^ (1 << (n - 1));
    grayCodeUtil(res, n - 1, num);
}

// Returns the vector containing the gray
// code sequence of n bits.
function grayCodes(n)
{
    let res = [];

    // num is passed by reference to keep
    // track of current code.
    let num = [0];
    grayCodeUtil(res, n, num);

    return res;
}

// Driver code
let n = 3;
let code = grayCodes(n);
for(let i = 0; i < code.length; i++)
    document.write(code[i] + "<br>");

// This code is contributed by gfgking

</script>
```

**输出:**

```
0
1
3
2
6
7
5
4
```