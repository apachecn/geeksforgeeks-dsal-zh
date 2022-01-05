# 将 K 表示为 N-bonacci 数的和

> 原文:[https://www . geesforgeks . org/represent-k-as-sum-n-bonacci-numbers/](https://www.geeksforgeeks.org/represent-k-as-sum-of-n-bonacci-numbers/)

给定两个数字 **K** 和 **N** 。任务是将给定的数字 **K** 表示为几个 [**N-bonacci 数字**](https://www.geeksforgeeks.org/n-bonacci-numbers/) 的总和。

**示例:**

> **输入:** K = 21，N = 5
> **输出:**3
> 5-bonacci 数的三个数是:16，4，1。
> **说明:**
> 对于 N = 5，级数将为:1、1、2、4、8、16、31、61、120 等等。三个数字 16、4 和 1 加起来是 21。
> 
> **输入:** K = 500，N = 43
> **输出:**6
> 43-bonacci 加起来等于 500 的数字是:256 128 64 32 16 4

**天真方法:**
最简单的方法是生成最多 50 个项的 N-bonacci 系列，并将它们的值存储在数组中。找到具有给定总和的数组子集，并打印子集的大小。

***时间复杂度:** O(2 <sup>N</sup> )*

**有效方法**:这种方法是基于如何形成 N-bonacci 数的有效方法，在[这篇文章](https://www.geeksforgeeks.org/n-bonacci-numbers/)中讨论过。

按照以下步骤解决问题:

1.  生成 N-bonacci 系列并将值存储在一个数组中，比如 **N_bonacci[]** 。(最多 50 个条款)
2.  初始化另一个数组 **ans[]** ，用于保存数列中和为 **K** 的数字。
3.  以相反的顺序遍历 N-bonacci 数组，并继续检查是否，**K–N _ bonacci[I]>= 0**。如果为真，则将 **N_bonacci[i]** 推至 **ans** 阵，将 **K** 降为**K–N _ bonacci[I]**。
4.  继续递减 **K** 直到变成 **0** ，然后最终输出 **ans** 数组的大小和元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// array to store the N-Bonacci series
long long N_bonacci[100];

// Function to express K as sum of
// several N_bonacci numbers
void N_bonacci_nums(int n, int k)
{
    N_bonacci[0] = 1;

    for (int i = 1; i <= 50; ++i) {
        for (int j = i - 1;
            j >= i - k and j >= 0;
            --j)
            N_bonacci[i]
                += N_bonacci[j];
    }

    vector<long long> ans;
    for (int i = 50; i >= 0; --i)
        if (n - N_bonacci[i] >= 0) {
            ans.push_back(N_bonacci[i]);
            n -= N_bonacci[i];
        }

    if (ans.size() == 1)
        ans.push_back(0);

    cout << ans.size() << endl;
    for (int i = 0; i < ans.size(); ++i)
        cout << ans[i] << ", ";
}

// Driver code
int main()
{
    int n = 21, k = 5;
    N_bonacci_nums(n, k);
    return 0;
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;

class GFG{

// Array to store the N-Bonacci series
public static long []N_bonacci= new long [100];

// Function to express K as sum of
// several N_bonacci numbers
@SuppressWarnings("unchecked")
public static void N_bonacci_nums(int n, int k)
{
    N_bonacci[0] = 1;

    for(int i = 1; i <= 50; ++i)
    {
        for(int j = i - 1;
                j >= i - k && j >= 0 ;--j)
            N_bonacci[i]+= N_bonacci[j];
    }

    Vector ans = new Vector();
    for(int i = 50; i >= 0; --i)
        if (n - N_bonacci[i] >= 0)
        {
            ans.add(N_bonacci[i]);
            n -= N_bonacci[i];
        }

    if (ans.size() == 1)
        ans.add(0);

    System.out.println(ans.size());
    for(int i = 0; i < ans.size(); ++i)
        System.out.print(ans.get(i) + ", ");
}

// Driver code
public static void main(String args[])
{
    int n = 21, k = 5;
    N_bonacci_nums(n, k);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Array to store the N-Bonacci series
N_bonacci = [0] * 100

# Function to express K as sum of
# several N_bonacci numbers
def N_bonacci_nums(n, k):

    N_bonacci[0] = 1

    for i in range(1, 51):
        j = i - 1

        while j >= i - k and j >= 0:
            N_bonacci[i] += N_bonacci[j]
            j -= 1

    ans = []
    for i in range(50, -1, -1):
        if (n - N_bonacci[i] >= 0):
            ans.append(N_bonacci[i])
            n -= N_bonacci[i]

    if (len(ans) == 1):
        ans.append(0)

    print(len(ans))
    for i in ans:
        print(i, end = ", ")

# Driver code
if __name__ == '__main__':

    n = 21
    k = 5

    N_bonacci_nums(n, k)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above problem
using System;
using System.Collections.Generic;

class GFG{

// Array to store the N-Bonacci series    
public static long []N_bonacci = new long [100];

// Function to express K as sum of
// several N_bonacci numbers
static void N_bonacci_nums(long n, long k)
{
    N_bonacci[0] = 1;

    for(int i = 1; i <= 50; ++i)
    {
        for(int j = i - 1;
                j >= i - k && j >= 0; --j)
            N_bonacci[i] += N_bonacci[j];
    }

    List<long> ans = new List<long>();
    for(int i = 50; i >= 0; --i)
        if (n - N_bonacci[i] >= 0)
        {
            ans.Add(N_bonacci[i]);
            n -= N_bonacci[i];
        }

    if (ans.Count == 1)
        ans.Add(0);

    Console.WriteLine(ans.Count);
    for(int i = 0; i < ans.Count; ++i)
        Console.Write(ans[i] + ", ");
}

// Driver code
static void Main()
{
    long n = 21, k = 5;

    N_bonacci_nums(n, k);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above problem

// Array to store the N-Bonacci series
let N_bonacci= new Array(100);
for(let i = 0; i < 100; i++)
{
    N_bonacci[i] = 0;
}

// Function to express K as sum of
// several N_bonacci numbers
function N_bonacci_nums(n, k)
{
    N_bonacci[0] = 1;

    for(let i = 1; i <= 50; ++i)
    {
        for(let j = i - 1;
                j >= i - k && j >= 0 ;--j)
            N_bonacci[i]+= N_bonacci[j];
    }

    let ans = [];
    for(let i = 50; i >= 0; --i)
        if (n - N_bonacci[i] >= 0)
        {
            ans.push(N_bonacci[i]);
            n -= N_bonacci[i];
        }

    if (ans.length == 1)
        ans.push(0);

    document.write(ans.length+"<br>");
    for(let i = 0; i < ans.length; ++i)
        document.write(ans[i] + ", ");
}

// Driver code
let n = 21, k = 5;

N_bonacci_nums(n, k);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
3
16, 4, 1,
```

***时间复杂度:** O(K * K)*
***辅助空间:** O(1)*