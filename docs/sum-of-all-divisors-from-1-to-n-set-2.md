# 从 1 到 N 的所有除数之和|集合 2

> 原文:[https://www . geeksforgeeks . org/all-dividers 之和-从-1 到-n-set-2/](https://www.geeksforgeeks.org/sum-of-all-divisors-from-1-to-n-set-2/)

给定一个正整数 **N** ，任务是求第一个 **N** 个自然数的除数之和。

**示例:**

> **输入:** N = 4
> **输出:** 15
> **解释:**
> 除数之和 1 = (1)
> 除数之和 2 = (1+2)
> 除数之和 3 = (1+3)
> 除数之和 4 = (1+2+4)
> 因此，总和= 1 + (1+2) + (1+3) + (1+2+4) =
> 
> **输入:** N = 5
> **输出:** 21
> **解释:**
> 除数之和 1 = (1)
> 除数之和 2 = (1+2)
> 除数之和 3 = (1+3)
> 除数之和 4 = (1+2+4)
> 除数之和 5 = (1+5)
> 因此，总和=(1)+(T0)

对于线性时间方法，参考[从 1 到 N 的所有除数之和](https://www.geeksforgeeks.org/sum-divisors-1-n/)

**方法:**
要优化上面提到的帖子中的方法，需要寻找对数复杂度的解决方案。一个数字 **D** 在最终答案中被多次添加。让我们试着观察一种重复加法的模式。
考虑 **N** = **12** :

<figure class="table">

| D | 添加的次数 |
| --- | --- |
| one | Twelve |
| Two | six |
| three | four |
| 5, 6 | Two |
| 7, 8, 9, 10, 11, 12 | one |

从上面的模式，观察每一个数字 **D** 加( **N** / **D** )次。此外，还有多个 D 具有相同的(不适用)。因此，我们可以得出结论，对于给定的 **N** ，以及特定的 **i** ，从(**N**/(**I**+**1**)+**1**到( **N** / **i** 的数字)将被添加 **i** 次。

> **插图:**
> 
> 1.  N = 12，i = 1
>     (N/(i+1))+1 = 6+1 = 7 和(N/i) = 12
>     所有数字都是 7、8、9、10、11、12，只加 1 次。
> 2.  N = 12，i = 2
>     (N/(i+1))+1 = 4+1 = 5 和(N/i) = 6
>     所有数字都是 5，6，加 2 次。

现在，假设 **A** = (N / (i + 1))， **B** = (N / i)
从 A + 1 到 B 的数之和=从 1 到 B 的数之和–从 1 到 A 的数之和
同样，不是每次只增加 1，而是像这样找到下一个 I，i = N/(N/(i+1))

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include<bits/stdc++.h>
using namespace std;

int mod = 1000000007;

// Functions returns sum
// of numbers from 1 to n
int linearSum(int n)
{
    return (n * (n + 1) / 2) % mod;
}

// Functions returns sum
// of numbers from a+1 to b
int rangeSum(int b, int a)
{
    return (linearSum(b) -
            linearSum(a)) % mod;
}

// Function returns total
// sum of divisors
int totalSum(int n)
{

    // Stores total sum
    int result = 0;
    int i = 1;

    // Finding numbers and
    //its occurence
    while(true)
    {

        // Sum of product of each
        // number and its occurence
        result += rangeSum(n / i, n / (i + 1)) *
                          (i % mod) % mod;

        result %= mod;

        if (i == n)
            break;

        i = n / (n / (i + 1));
    }
    return result;
}       

// Driver code
int main()
{
    int N = 4;
    cout << totalSum(N) << endl;

    N = 12;
    cout << totalSum(N) << endl;
    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

static final int mod = 1000000007;

// Functions returns sum
// of numbers from 1 to n
public static int linearSum(int n)
{
    return (n * (n + 1) / 2) % mod;
}

// Functions returns sum
// of numbers from a+1 to b
public static int rangeSum(int b, int a)
{
    return (linearSum(b) -
            linearSum(a)) % mod;
}

// Function returns total
// sum of divisors
public static int totalSum(int n)
{

    // Stores total sum
    int result = 0;
    int i = 1;

    // Finding numbers and
    //its occurence
    while(true)
    {

        // Sum of product of each
        // number and its occurence
        result += rangeSum(n / i,
                           n / (i + 1)) *
                          (i % mod) % mod;

        result %= mod;

        if (i == n)
            break;

        i = n / (n / (i + 1));
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    System.out.println(totalSum(N));

    N = 12;
    System.out.println(totalSum(N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

mod = 1000000007

# Functions returns sum
# of numbers from 1 to n
def linearSum(n):
    return n*(n + 1)//2 % mod

# Functions returns sum
# of numbers from a+1 to b
def rangeSum(b, a):
    return (linearSum(b) - (
          linearSum(a))) % mod

# Function returns total
# sum of divisors
def totalSum(n):

    # Stores total sum
    result = 0
    i = 1

    # Finding numbers and
    # its occurence
    while True:

        # Sum of product of each
        # number and its occurence
        result += rangeSum(
            n//i, n//(i + 1)) * (
                  i % mod) % mod;

        result %= mod;
        if i == n:
            break
        i = n//(n//(i + 1))

    return result       

# Driver code

N= 4
print(totalSum(N))

N= 12
print(totalSum(N))
```

## C#

```
// C# program for
// the above approach
using System;

class GFG{

static readonly int mod = 1000000007;

// Functions returns sum
// of numbers from 1 to n
public static int linearSum(int n)
{
    return (n * (n + 1) / 2) % mod;
}

// Functions returns sum
// of numbers from a+1 to b
public static int rangeSum(int b, int a)
{
    return (linearSum(b) -
            linearSum(a)) % mod;
}

// Function returns total
// sum of divisors
public static int totalSum(int n)
{

    // Stores total sum
    int result = 0;
    int i = 1;

    // Finding numbers and
    //its occurence
    while(true)
    {

        // Sum of product of each
        // number and its occurence
        result += rangeSum(n / i,
                           n / (i + 1)) *
                          (i % mod) % mod;

        result %= mod;

        if (i == n)
            break;

        i = n / (n / (i + 1));
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;
    Console.WriteLine(totalSum(N));

    N = 12;
    Console.WriteLine(totalSum(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach
let mod = 1000000007;

// Functions returns sum
// of numbers from 1 to n
function linearSum(n)
{
    return (n * (n + 1) / 2) % mod;
}

// Functions returns sum
// of numbers from a+1 to b
function rangeSum(b, a)
{
    return (linearSum(b) -
            linearSum(a)) % mod;
}

// Function returns total
// sum of divisors
function totalSum(n)
{

    // Stores total sum
    let result = 0;
    let i = 1;

    // Finding numbers and
    //its occurence
    while(true)
    {

        // Sum of product of each
        // number and its occurence
        result += rangeSum(Math.floor(n / i),
                           Math.floor(n / (i + 1))) *
                                     (i % mod) % mod;

        result %= mod;

        if (i == n)
            break;

        i = Math.floor(n / (n / (i + 1)));
    }
    return result;
}

// Driver Code
let N = 4;
document.write(totalSum(N) + "<br/>");

N = 12;
document.write(totalSum(N));

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
15
127
```

***时间复杂度:** O(√n)*

</figure>