# N 个自然数之和与乘积之差形成的级数之和

> 原文:[https://www . geeksforgeeks . org/由 n 个自然数的乘积和和之差形成的数列之和/](https://www.geeksforgeeks.org/sum-of-series-formed-by-difference-between-product-and-sum-of-n-natural-numbers/)

给定一个自然数 **N** ，任务是找到直到**第 N 项**的级数之和，其中 **i <sup>第</sup>T7】项表示第一 I 个自然数的乘积与第一 I 个自然数的和之间的*差，即，***

> { 1 – 1 } + { (1 * 2) – (2 + 1) } + { (1 * 2 * 3) – (3 + 2 + 1) } + { (1 * 2 * 3 * 4) – (4 + 3 + 2 + 1) } + ………

**示例:**

> **输入:** 2
> **输出:** -1
> **解释:**{ 1–1 }+{(1 * 2)–(2+1)} = { 0 }+{-1 } =-1
> 
> **输入:**4
> T3】输出:13
> T6】解释:T8】{ 0 }+{(1 * 2)–(2+1)}+{(1 * 2 * 3)–(3+2+1)}+{(1 * 2 * 3 * 4)–(4+3+2+1)}
> = { 0 }+{-1 }+{ 0 }+{ 14 }
> = 0–1+0+14

**迭代方法:**
按照以下步骤解决问题:

*   初始化三个变量:
    *   **currProd:** 存储截至当前期限的所有自然数的乘积。
    *   **currSum:** 存储截至当前期限的所有自然数的总和。
    *   **总和:**存储截至当前期限的系列总和
*   初始化 **currSum = 1，currSum = 1** ，和 **sum = 0** (自，1–1 = 0)以存储它们各自的第一项值。
*   迭代范围**【2，N】**并为每一次 **i <sup>第</sup>T5】次迭代更新以下内容:**
    *   **咖喱角=咖喱角+和**
    *   **currProd = currProd * i**
    *   sum = curricum-curricum
*   返回**和**的最终值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to
// calculate the
// sum upto Nth term
int seriesSum(int n)
{
    // Stores the sum
    // of the series
    int sum = 0;

    // Stores the
    // product of
    // natural numbers
    // upto the
    // current term
    int currProd = 1;

    // Stores the sum
    // of natural numbers
    // upto the
    // upto current term
    int currSum = 1;

    // Generate the remaining
    // terms and calculate sum
    for (int i = 2; i <= n; i++) {
        currProd *= i;
        currSum += i;

        // Update the sum
        sum += currProd
               - currSum;
    }

    // Return the sum
    return sum;
}

// Driver Program
int main()
{
    int N = 5;
    cout << seriesSum(N) << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.lang.*;

class GFG{

// Function to calculate the
// sum upto Nth term
static int seriesSum(int n)
{

    // Stores the sum
    // of the series
    int sum = 0;

    // Stores the product of
    // natural numbers upto
    // the current term
    int currProd = 1;

    // Stores the sum of natural
    // numbers upto the upto
    // current term
    int currSum = 1;

    // Generate the remaining
    // terms and calculate sum
    for(int i = 2; i <= n; i++)
    {
       currProd *= i;
       currSum += i;

       // Update the sum
       sum += currProd - currSum;
    }

    // Return the sum
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    System.out.print(seriesSum(N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the
# sum upto Nth term
def seriesSum(n):

    # Stores the sum
    # of the series
    sum1 = 0;

    # Stores the product of
    # natural numbers upto the
    # current term
    currProd = 1;

    # Stores the sum of natural numbers
    # upto the upto current term
    currSum = 1;

    # Generate the remaining
    # terms and calculate sum
    for i in range(2, n + 1):
        currProd *= i;
        currSum += i;

        # Update the sum
        sum1 += currProd - currSum;

    # Return the sum
    return sum1;

# Driver Code
N = 5;
print(seriesSum(N), end = " ");

# This code is contributed by Code_Mech
```

## C#

```
// C# program to implement the
// above approach
using System;
class GFG{

// Function to calculate the
// sum upto Nth term
static int seriesSum(int n)
{

    // Stores the sum
    // of the series
    int sum = 0;

    // Stores the product of
    // natural numbers upto
    // the current term
    int currProd = 1;

    // Stores the sum of natural
    // numbers upto the upto
    // current term
    int currSum = 1;

    // Generate the remaining
    // terms and calculate sum
    for(int i = 2; i <= n; i++)
    {
        currProd *= i;
        currSum += i;

        // Update the sum
        sum += currProd - currSum;
    }

    // Return the sum
    return sum;
}

// Driver code
public static void Main()
{
    int N = 5;

    Console.Write(seriesSum(N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to
    // calculate the
    // sum upto Nth term
    function seriesSum(n)
    {
        // Stores the sum
        // of the series
        let sum = 0;

        // Stores the
        // product of
        // natural numbers
        // upto the
        // current term
        let currProd = 1;

        // Stores the sum
        // of natural numbers
        // upto the
        // upto current term
        let currSum = 1;

        // Generate the remaining
        // terms and calculate sum
        for (let i = 2; i <= n; i++) {
            currProd *= i;
            currSum += i;

            // Update the sum
            sum += currProd
                   - currSum;
        }

        // Return the sum
        return sum;
    }

    let N = 5;
    document.write(seriesSum(N) + " ");

</script>
```

**Output:** 

```
118
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**递归方法:**

*   通过调用函数更新 K(表示当前项)递归计算和。
*   通过添加**多* K–添加+ K** 更新预计算的**前一个**
*   递归计算 K 的所有值，在每次迭代时更新 prevSum、multi 和 add。
*   最后，返回 prevSum 的值。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the
// sum upto the Nth term of the
// given series

#include <bits/stdc++.h>
using namespace std;

// Recursive Function to calculate the
// sum upto Nth term
int seriesSumUtil(int k, int n,
                  int prevSum,
                  int multi, int add)
{
    // If N-th term is calculated
    if (k == n + 1) {
        return prevSum;
    }

    // Update multi to store
    // product upto K
    multi = multi * k;

    // Update add to store
    // sum upto K
    add = add + k;

    // Update prevSum to store sum
    // upto K
    prevSum = prevSum + multi - add;

    // Proceed to next K
    return seriesSumUtil(k + 1, n, prevSum,
                         multi, add);
}

// Function to calculate
// and return the
// Sum upto Nth term
int seriesSum(int n)
{
    if (n == 1)
        return 0;
    int prevSum = 0;
    int multi = 1;
    int add = 1;

    // Recursive Function
    return seriesSumUtil(2, n, prevSum,
                         multi, add);
}

// Driver Program
int main()
{
    int N = 5;
    cout << seriesSum(N) << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the
// sum upto the Nth term of the
// given series
class GFG{

// Recursive Function to calculate the
// sum upto Nth term
static int seriesSumUtil(int k, int n,
                         int prevSum,
                         int multi, int add)
{

    // If N-th term is calculated
    if (k == n + 1)
    {
        return prevSum;
    }

    // Update multi to store
    // product upto K
    multi = multi * k;

    // Update add to store
    // sum upto K
    add = add + k;

    // Update prevSum to store sum
    // upto K
    prevSum = prevSum + multi - add;

    // Proceed to next K
    return seriesSumUtil(k + 1, n, prevSum,
                         multi, add);
}

// Function to calculate and
// return the Sum upto Nth term
static int seriesSum(int n)
{
    if (n == 1)
        return 0;

    int prevSum = 0;
    int multi = 1;
    int add = 1;

    // Recursive Function
    return seriesSumUtil(2, n, prevSum,
                         multi, add);
}

// Driver code
public static void main(String []args)
{
    int N = 5;
    System.out.println(seriesSum(N));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to calculate the
# sum upto the Nth term of the
# given series

# Recursive Function to calculate the
# sum upto Nth term
def seriesSumUtil(k, n, prevSum, multi, add):

    # If N-th term is calculated
    if (k == n + 1):
        return prevSum;

    # Update multi to store
    # product upto K
    multi = multi * k;

    # Update add to store
    # sum upto K
    add = add + k;

    # Update prevSum to store sum
    # upto K
    prevSum = prevSum + multi - add;

    # Proceed to next K
    return seriesSumUtil(k + 1, n,
                         prevSum, multi, add);

# Function to calculate and
# return the Sum upto Nth term
def seriesSum(n):
    if (n == 1):
        return 0;

    prevSum = 0;
    multi = 1;
    add = 1;

    # Recursive Function
    return seriesSumUtil(2, n, prevSum,
                         multi, add);

# Driver code
if __name__ == '__main__':
    N = 5;
    print(seriesSum(N));

# This code is contributed by Princi Singh
```

## C#

```
// C# program to calculate the
// sum upto the Nth term of the
// given series
using System;
class GFG{

// Recursive Function to calculate the
// sum upto Nth term
static int seriesSumUtil(int k, int n,
                         int prevSum,
                         int multi, int add)
{

    // If N-th term is calculated
    if (k == n + 1)
    {
        return prevSum;
    }

    // Update multi to store
    // product upto K
    multi = multi * k;

    // Update add to store
    // sum upto K
    add = add + k;

    // Update prevSum to store sum
    // upto K
    prevSum = prevSum + multi - add;

    // Proceed to next K
    return seriesSumUtil(k + 1, n, prevSum,
                         multi, add);
}

// Function to calculate and
// return the Sum upto Nth term
static int seriesSum(int n)
{
    if (n == 1)
        return 0;

    int prevSum = 0;
    int multi = 1;
    int add = 1;

    // Recursive Function
    return seriesSumUtil(2, n, prevSum,
                         multi, add);
}

// Driver code
public static void Main(String []args)
{
    int N = 5;
    Console.WriteLine(seriesSum(N));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program to calculate the
// sum upto the Nth term of the
// given series

// Recursive Function to calculate the
// sum upto Nth term
function seriesSumUtil(k, n, prevSum, multi, add)
{

    // If N-th term is calculated
    if (k == n + 1)
    {
        return prevSum;
    }

    // Update multi to store
    // product upto K
    multi = multi * k;

    // Update add to store
    // sum upto K
    add = add + k;

    // Update prevSum to store sum
    // upto K
    prevSum = prevSum + multi - add;

    // Proceed to next K
    return seriesSumUtil(k + 1, n, prevSum,
                         multi, add);
}

// Function to calculate and
// return the Sum upto Nth term
function seriesSum(n)
{
    if (n == 1)
        return 0;

    let prevSum = 0;
    let multi = 1;
    let add = 1;

    // Recursive Function
    return seriesSumUtil(2, n, prevSum,
                         multi, add);
}

// Driver code
let N = 5;
document.write(seriesSum(N));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
118
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*