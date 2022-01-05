# 生成从 1 到第 n 个素数的新算法

> 原文:[https://www . geesforgeks . org/new-算法生成素数-从-1 到-n-number/](https://www.geeksforgeeks.org/new-algorithm-to-generate-prime-numbers-from-1-to-nth-number/)

除了厄拉多塞法生成素数的[筛外，我们还可以实现一个从 **1** 到 **N** 生成素数的新算法。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

知道**所有质数≥ 5** 都可以从一个模式中追溯出来可能会很神奇:
让我们试着理解这个系列:

> **系列 1:**
> 5+6 = 11
> 11+6 = 17
> 17+6 = 23
> 23+6 = 29
> …
> …

> **系列 2:**
> 7+6 = 13
> 13+6 = 19
> …
> …

我们看到把 **6** 加到 **5** 上，再把 **6** 加到得到的结果上，就能得到另一个素数。同样，将 **6** 加到 **7** 上，再将 **6** 加到所得结果上。我们可以得到另一个质数。因此，我们可以推断，我们可以用同样的方法得到所有素数。
但是，当我们不断地将 **6** 加到前面的结果中，得到下一个素数时，我们可以注意到一些不是素数的数。
例如:

> 13 + 6 = 19(质数)
> 19 + 6 = 25(合成数；说伪素数)
> 29 + 6 = 35(复合数；比如伪素数)

我们可以说这些类型的复合数是伪素数(看起来像素数，但实际上不是)。
现在，如果我们能够把这些伪素数和实素数分开，我们就可以得到实素数。使用 4 个重要的方程，我们可以精确地跟踪所有这些伪素数，并将它们与实素数分开。

将产生级数的方程是:

> y = 6 * x 1
> 其中 x = 1，2，3，4，5，6，7， …
> 例如:
> 6 *(1)–1 = 5(质数)
> 6 * (1) + 1 = 7(质数)
> 6 *(2)–1 = 11(质数)
> 6 * (2) + 1 = 13(质数)
> 6 *(3)–1 = 17(质数)
> 6 * (3) + 1 = 19(质数)
> 6 *(4)–1 = 23(质数)
> 6

我们可以使用 4 个等式跟踪所有伪素数:

**对于 y = 6 * x–1 生产的系列:**

1.  **y = (6 * d * x) + d** 其中，x = {1，2，3，4，5，6，…}
2.  **y = (6 * d * x) + (d * d)** 其中，x = {0，1，2，3，4，5，…}和 d = {5，(5+6)，(5+6+6)，(5+6+6+6)，…，(5+(n-1)*6)}

**对于 y = 6 * x + 1 产生的系列:**

1.  **y = (6 * d * x) + (d * d)** 其中，x = {0，1，2，3，…}
2.  **y =(6 * d * x)+(d * d)–2 * d**其中，x = {1，2，3，4，…}，d = {7，(7+6)，(7+6+6)，…，(7+(n–1)* 6)}和 n = {1，2，3，4，5，…}

> **示例**
> 在等式 2 中取 d = 5 和 x = 0，
> y = 25(伪素数)
> 在等式 1 中取 d = 5 和 x = 1，
> y = 35(伪素数)
> 类似地，将值放在等式 3 和 4 中，我们可以跟踪所有伪素数。

**如何在编程中实现？**

> 我们假设两个相同大小的布尔型数组。
> 先说第一个是**数组 1** ，它的每个元素都初始化为 **0** 。
> 第二个是**数组 2** ，它的每个元素都被初始化为 **1** 。
> 现在，
> 在**数组 1** 中，我们用 **1** 初始化指定的索引，使用公式 **y = (6 * x) 1** 计算索引值。
> 并且，在**数组 2** 中，我们用 **0** 初始化指定的索引，使用上述 4 个等式计算索引值。
> 
> 现在，运行从 **0** 到 **N** 的循环，打印数组的索引值，
> 如果**数组 1[i] = 1** 和**数组 2[i] = 1** (i 为素数)。

以下是该方法的实施情况:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of prime numbers <= n
int countPrimesUpto(int n)
{

    // To store the count of prime numbers
    int count = 0;

    // To mark all the prime numbers according
    // to the equation (y = 6*x -/+ 1)
    // where x = 1, 2, 3, 4, 5, 6, 7, ...
    bool arr1[n + 1];

    // To mark all the Pseudo Prime Numbers
    // using the four equations
    // described in the approach
    bool arr2[n + 1];

    // Starting with >= 5
    int d = 5;

    // 2 and 3 are primes
    arr1[2] = arr2[2] = 1;
    arr1[3] = arr2[3] = 1;

    // Initialize every element of arr1 with 0
    memset(arr1, 0, sizeof(arr1));

    // Initialize every element of arr2 with 1
    memset(arr2, 1, sizeof(arr2));

    // Update arr1[] to mark all the primes
    while (d <= n) {

        // For 5, (5 + 6), (5 + 6 + 6), ...
        memset(arr1 + d, 1, (sizeof(arr1)) / (n + 1));

        // For 7, (7 + 6), (7 + 6 + 6), ...
        memset(arr1 + (d + 2), 1, (sizeof(arr1)) / (n + 1));

        // Increase d by 6
        d = d + 6;
    }

    // Update arr2[] to mark all pseudo primes
    for (int i = 5; i * i <= n; i = i + 6) {
        int j = 0;

        // We will run while loop until we find all
        // pseudo prime numbers <= n
        while (1) {
            int flag = 0;

            // Equation 1
            int temp1 = 6 * i * (j + 1) + i;

            // Equation 2
            int temp2 = ((6 * i * j) + i * i);

            // Equation 3
            int temp3 = ((6 * (i + 2) * j)
                         + ((i + 2) * (i + 2)));

            // Equation 4
            int temp4 = ((6 * (i + 2) * (j + 1))
                         + ((i + 2) * (i + 2)) - 2 * (i + 2));

            // If obtained pseudo prime number <=n then its
            // corresponding index in arr2 is set to 0

            // Result of equation 1
            if (temp1 <= n) {
                arr2[temp1] = 0;
            }
            else {
                flag++;
            }

            // Result of equation 2
            if (temp2 <= n) {
                arr2[temp2] = 0;
            }
            else {
                flag++;
            }

            // Result of equation 3
            if (temp3 <= n) {
                arr2[temp3] = 0;
            }
            else {
                flag++;
            }

            // Result of equation 4
            if (temp4 <= n) {
                arr2[temp4] = 0;
            }
            else {
                flag++;
            }

            if (flag == 4) {
                break;
            }
            j++;
        }
    }

    // Include 2
    if (n >= 2)
        count++;

    // Include 3
    if (n >= 3)
        count++;

    // If arr1[i] = 1 && arr2[i] = 1 then i is prime number
    // i.e. it is a prime which is not a pseudo prime
    for (int p = 5; p <= n; p = p + 6) {
        if (arr2[p] == 1 && arr1[p] == 1)
            count++;

        if (arr2[p + 2] == 1 && arr1[p + 2] == 1)
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int n = 100;
    cout << countPrimesUpto(n);
}
```

**Output:**

```
25

```