# 所有可能子集之和的总和

> 原文:[https://www . geeksforgeeks . org/所有可能子集的总和/](https://www.geeksforgeeks.org/sum-of-the-sums-of-all-possible-subsets/)

给定一个大小为 **N** 的数组**。任务是找出所有可能子集的总和。
**例:**** 

> ****输入:** a[] = {3，7}
> **输出:** 20
> 子集为:{3} {7} {3，7}
> {3，7 } = 10
> { 3 } = 3
> { 7 } = 7
> 10+3+7 = 20
> **输入:** a[] = {10，16，14，9}
> **输出:****

****天真法**:天真法是利用幂集找到所有子集，然后对所有可能的子集求和得到答案。
**时间复杂度** : O(2 <sup>N</sup> )
**高效方法**:一个高效的方法就是用观察来解决问题。如果我们写出所有的子序列，一个共同的观察点是每个数在一个子集中出现**2<sup>(N–1)</sup>**次，因此将导致 **2 <sup>(N-1)</sup>** 作为对总和的贡献。遍历数组，在答案中添加**(arr[I]* 2<sup>N-1</sup>)**。
以下是上述方法的实施:** 

## **C++**

```
// C++ program to find the sum of
// the addition of all possible subsets.
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
// of sum of all the subset
int sumOfSubset(int a[], int n)
{
    int times = pow(2, n - 1);

    int sum = 0;

    for (int i = 0; i < n; i++) {
        sum = sum + (a[i] * times);
    }

    return sum;
}

// Driver Code
int main()
{
    int a[] = { 3, 7 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << sumOfSubset(a, n);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the sum of
// the addition of all possible subsets.
class GFG
{

// Function to find the sum
// of sum of all the subset
static int sumOfSubset(int []a, int n)
{
    int times = (int)Math.pow(2, n - 1);

    int sum = 0;

    for (int i = 0; i < n; i++)
    {
        sum = sum + (a[i] * times);
    }

    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int []a = { 3, 7 };
    int n = a.length;
    System.out.println(sumOfSubset(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to find the Sum of
# the addition of all possible subsets.

# Function to find the sum
# of sum of all the subset
def SumOfSubset(a, n):

    times = pow(2, n - 1)

    Sum = 0

    for i in range(n):
        Sum = Sum + (a[i] * times)

    return Sum

# Driver Code
a = [3, 7]
n = len(a)
print(SumOfSubset(a, n))

# This code is contributed by Mohit Kumar
```

## **C#**

```
// C# program to find the sum of
// the addition of all possible subsets.
using System;

class GFG
{

// Function to find the sum
// of sum of all the subset
static int sumOfSubset(int []a, int n)
{
    int times = (int)Math.Pow(2, n - 1);

    int sum = 0;

    for (int i = 0; i < n; i++)
    {
        sum = sum + (a[i] * times);
    }

    return sum;
}

// Driver Code
public static void Main()
{
    int []a = { 3, 7 };
    int n = a.Length;
    Console.Write(sumOfSubset(a, n));
}
}

// This code is contributed by Nidhi
```

## **java 描述语言**

```
<script>
// javascript program to find the sum of
// the addition of all possible subsets.   
// Function to find the sum
    // of sum of all the subset
    function sumOfSubset(a , n) {
        var times = parseInt( Math.pow(2, n - 1));

        var sum = 0;

        for (i = 0; i < n; i++) {
            sum = sum + (a[i] * times);
        }

        return sum;
    }

    // Driver Code

        var a = [ 3, 7 ];
        var n = a.length;
        document.write(sumOfSubset(a, n));

// This code is contributed by todaysgaurav
</script>
```

****Output:** 

```
20
```** 

****时间复杂度** : O(N)
**空间复杂度** : O(1)
**注**:如果 N 大，答案会溢出，从而使用更大的数据类型。**