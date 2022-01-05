# 检查所有数组元素的乘积是否为完美平方

> 原文:[https://www . geeksforgeeks . org/check-如果所有数组元素的乘积是一个完美的平方或非/](https://www.geeksforgeeks.org/check-if-the-product-of-all-array-elements-is-a-perfect-square-or-not/)

给定一个由正整数 **N** 组成的数组 **arr[]** ，任务是检查给定数组 arr[]的所有元素的**乘积是否为完美平方。如果发现是真的，则打印“是”。否则，打印否。**

**示例:**

> **输入:** arr[] = {1，4，100}
> **输出:**是
> **说明:**所有数字的乘积是 1×4×100 = 400，这是一个完美的正方形。因此，打印“是”。
> 
> **输入:** arr[] = {1，3 }
> T3】输出:否

**天真法:**找出数组所有元素的乘积，试着找出这是否是一个完美的正方形。但是这种方法的问题是，产品可能太大，我们无法储存，因此**这种方法会失败**。
T5】时间复杂度:O(N)
T8】辅助空间: O(1)

高效方法:这种方法基于数学观察。如果一个数的所有质因数都是偶数的幂，那么这个数就是一个完美的正方形。我们将使用这个概念来发现产品是否是一个完美的正方形。遵循以下步骤:

*   创建一个**频率数组**来存储质因数的幂。
*   开始遍历数组。
*   对于每个元素**arr【I】**使用厄拉多塞 的 [**筛找出 arr【I】的**素因子**的**次幂**，并在频率数组中添加**。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   遍历完数组后，开始遍历**频率数组**。
*   如果**任意元素**(1 除外)有**奇频**则返回**假**，否则返回真。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check if the product
// of all elements is perfect square or not
bool isPerfectSquare(vector<int>& arr)
{
    // Map to store the power of prime factors
    map<int, int> freq;

    // Loop to implement the concept
    // of Sieve of Eratosthenes
    for (int x : arr) {
        for (int i = 2; i <= sqrt(x); i++) {
            while (x > 1 and x % i == 0) {
                freq[i]++;
                x /= i;
            }
        }
        if (x >= 2)
            freq[x]++;
    }

    // Loop to check if all the prime factors
    // have even power
    for (auto it = freq.begin();
         it != freq.end(); it++)
        if (it->second % 2)
            return false;

    return true;
}

// Driver code
int main()
{
    vector<int> arr = { 1, 4, 100 };

    isPerfectSquare(arr)
        ? cout << "YES\n"
        : cout << "NO\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;

class GFG {

    // Function to check if the product
    // of all elements is perfect square or not
    public static boolean isPerfectSquare(int[] arr)
    {

        // Map to store the power of prime factors
        HashMap<Integer, Integer> freq = new HashMap<Integer, Integer>();

        // Loop to implement the concept
        // of Sieve of Eratosthenes
        for (int x : arr) {
            for (int i = 2; i <= Math.sqrt(x); i++) {
                while (x > 1 && x % i == 0) {
                    if (freq.containsKey(i)) {
                        freq.put(i, freq.get(i) + 1);
                    } else {
                        freq.put(i, 1);
                    }
                    x /= i;
                }
            }
            if (x >= 2) {
                if (freq.containsKey(x)) {
                    freq.put(x, freq.get(x) + 1);
                } else {
                    freq.put(x, 1);
                }
            }
        }

        // Loop to check if all the prime factors
        // have even power
        for (int it : freq.values())
            if (it % 2 > 0)
                return false;

        return true;
    }

    // Driver code
    public static void main(String args[]) {
        int[] arr = { 1, 4, 100 };

        if (isPerfectSquare(arr) == true)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
import math

# Function to check if the product
# of all elements is perfect square or not
def isPerfectSquare(arr):

    # Map to store the power of prime factors
    freq = dict()

    # Loop to implement the concept
    # of Sieve of Eratosthenes
    for x in arr:
        for i in range(2, math.floor(math.sqrt(x)) + 1):
            while (x > 1 and x % i == 0):
                if (i in freq):
                    freq[i] += + 1
                else:
                    freq[i] = 1

                x = x // i
        if (x >= 2):
            freq[x] += 1

    # Loop to check if all the prime factors
    # have even power
    for value in freq.values():
        if (value % 2 == 1):
            return False
    return True

# Driver code
arr = [1, 4, 100]
print("YES") if isPerfectSquare(arr) else print("NO")

# This code is contributed by gfgking
```

## C#

```
using System;
using System.Collections.Generic;

public class GFG {

    // Function to check if the product
    // of all elements is perfect square or not
    public static bool isPerfectSquare(int[] arr)
    {

        // Map to store the power of prime factors
        Dictionary<int, int> freq = new Dictionary<int, int>();

        // Loop to implement the concept
        // of Sieve of Eratosthenes
        int new_x = 0;
        foreach (int x in arr) {
            new_x = x;
            for (int i = 2; i <= Math.Sqrt(new_x); i++) {
                while (new_x > 1 && x % i == 0) {
                    if (freq.ContainsKey(i)) {
                        freq[i] = freq[i] + 1;
                    } else {
                        freq.Add(i, 1);
                    }
                    new_x = new_x/i;
                }
            }
            if (new_x >= 2) {
                if (freq.ContainsKey(new_x)) {
                    freq[new_x] = freq[new_x] + 1;
                } else {
                    freq.Add(new_x, 1);
                }
            }
        }

        // Loop to check if all the prime factors
        // have even power
        foreach (int it in freq.Values)
            if (it % 2 > 0)
                return false;

        return true;
    }

    // Driver code
    public static void Main(String []args) {
        int[] arr = { 1, 4, 100 };

        if (isPerfectSquare(arr) == true)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to check if the product
        // of all elements is perfect square or not
        function isPerfectSquare(arr)
        {

            // Map to store the power of prime factors
            let freq = new Map();

            // Loop to implement the concept
            // of Sieve of Eratosthenes
            for (let x of arr) {
                for (let i = 2; i <= Math.floor(Math.sqrt(x)); i++) {
                    while (x > 1 && x % i == 0) {
                        if (freq.has(i))
                            freq.set(i, freq.get(i) + 1);
                        else
                            freq.set(i, 1);

                        x = Math.floor(x / i);
                    }
                }
                if (x >= 2)
                    freq.set(x, freq.get(x) + 1)
            }

            // Loop to check if all the prime factors
            // have even power
            for (let value of freq.values()) {
                if (value % 2 == 1)
                    return false;
            }

            return true;
        }

        // Driver code
        let arr = [1, 4, 100];

        isPerfectSquare(arr)
            ? document.write("YES" + '<br>')
            : document.write("NO" + '<br>');

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
YES
```

**时间复杂度:** O(N * log X)其中 X 是数组的最大元素
T3】辅助空间: O(N)