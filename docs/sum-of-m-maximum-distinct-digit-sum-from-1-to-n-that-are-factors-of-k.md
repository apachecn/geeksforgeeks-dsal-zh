# 从 1 到 N 的 M 个最大不同数字和之和，是 K 的因子

> 原文:[https://www . geeksforgeeks . org/m-sum-max-distinct-digital-sum-from-1-n-is-of-k 因子/](https://www.geeksforgeeks.org/sum-of-m-maximum-distinct-digit-sum-from-1-to-n-that-are-factors-of-k/)

给定一组直到 **N** 的自然数和两个数字 **M** 和 **K** ，任务是从 **N** 自然数中找出 M 个最大相异数字和 **M** 的和，它们是 **K** 的因子。

**示例:**

> **输入:** N = 50，M = 4，K = 30
> **输出:** 16
> **说明:**
> 从 1 到 50，30 的因子= {1，2，3，5，6，10，15，30}。
> 每个因子的数字和= {1，2，3，5，6，1，6，3}。
> 4 个最大数字之和= 2、3、5、6。
> 总和= 16
> 
> **输入:** N = 5，M = 3，K = 74
> **输出:** 3
> **说明:**
> 从 1 到 5 的 74 个因子= {1，2}
> 每个因子的数字和= {1，2}。
> 3 个最大数字之和= 1，2(这里只有 2 个这样的数字。但是要求大气，所以只考虑这两个。)
> 总和= 3

**天真方法:**简单的解决方法是运行[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)从 1 到 N，找到所有完美划分 k 的数字的列表，找到每个因子的数字和并按降序排序并从这个列表中从顶部打印 M 个不同的元素。

**有效方法:**

*   通过从 2 到√K 的迭代，找到 1 到 N 范围内 K 的所有因子，使得元素完全除数。关于这种方法的详细解释，请参考[这篇](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)文章，并将它们存储在一个数组中。
*   求存储在因子数组中的数字的[位数和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)。
    **例如:**

```
For the Given Array - {4, 10, 273 }

Digit Sum of the Elements - 
Element 0 Digit Sum - "4" = 4
Element 1 Digit Sum - "10" = 1 + 0 = 10
Element 2 Digit Sum - "273" = 2 + 7 + 3 = 12
```

*   删除数字总和中的重复项，因为我们需要不同的元素。
*   [以相反的顺序对不同的数字和进行排序](https://www.geeksforgeeks.org/sorting-algorithms/)，并从这个数字和数组中找出最多 M 个元素的总和。

下面是上述方法的实现。

## C++

```
// C++ implementation to find the sum of
// maximum distinct digit sum of at most
// M numbers from 1 to N that are factors of K

#include <bits/stdc++.h>
using namespace std;

// Function to find the factors
// of K in N
vector<int> findFactors(int n, int k)
{

    // Initialise a vector
    vector<int> factors;

    // Find out the factors of
    // K less than N
    for (int i = 1; i <= sqrt(k); i++) {
        if (k % i == 0) {
            if (k / i == i && i <= n)
                factors.push_back(i);
            else {
                if (i <= n)
                    factors.push_back(i);
                if (k / i <= n)
                    factors.push_back(k / i);
            }
        }
    }

    return factors;
}

// Find the digit sum of each factor
vector<int> findDigitSum(vector<int> a)
{

    // Sum of digits for each
    // element in vector
    for (int i = 0; i < a.size(); i++) {
        int c = 0;
        while (a[i] > 0) {

            c += a[i] % 10;
            a[i] = a[i] / 10;
        }
        a[i] = c;
    }

    return a;
}

// Find the largest M distinct digit
// sum from the digitSum vector
int findMMaxDistinctDigitSum(
    vector<int> distinctDigitSum,
    int m)
{
    // Find the sum of last M numbers.
    int sum = 0;
    for (int i = distinctDigitSum.size() - 1;
         i >= 0 && m > 0;
         i--, m--)
        sum += distinctDigitSum[i];

    return sum;
}

// Find the at most M numbers from N natural
// numbers whose digit sum is distinct
// and those M numbers are factors of K.
int findDistinctMnumbers(int n, int k, int m)
{

    // Find out the factors of
    // K less than N
    vector<int> factors = findFactors(n, k);

    // Sum of digits for each
    // element in vector
    vector<int> digitSum = findDigitSum(factors);

    // Sorting the digitSum vector
    sort(digitSum.begin(), digitSum.end());

    // Removing the duplicate elements
    vector<int>::iterator ip;
    ip = unique(digitSum.begin(), digitSum.end());

    digitSum.resize(distance(
        digitSum.begin(),
        ip));

    // Finding the sum and returning it
    return findMMaxDistinctDigitSum(digitSum, m);
}

// Driver Code
int main()
{
    int n = 100, k = 80, m = 4;

    // Function Call
    cout
        << findDistinctMnumbers(n, k, m)
        << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum of
// maximum distinct digit sum of at most
// M numbers from 1 to N that are factors of K
import java.util.*;

class GFG
{

// Function to find the factors
// of K in N
public static Vector<Integer> findFactors(int n, int k)
{

    Vector<Integer> factors = new Vector<Integer>();
    // Initialise a vector

    // Find out the factors of
    // K less than N
    for (int i = 1; i <= Math.sqrt(k); i++)
    {
        if (k % i == 0)
        {
            if (k / i == i && i <= n)
                factors.add(i);
            else
            {
                if (i <= n)
                    factors.add(i);
                if (k / i <= n)
                    factors.add(k / i);
            }
        }
    }

    return factors;
}

// Find the digit sum of each factor
public static Vector<Integer> findDigitSum(Vector<Integer> a)
{

    // Sum of digits for each
    // element in vector
    for (int i = 0; i < a.size(); i++)
    {
        int c = 0;
        while (a.get(i) > 0)
        {

            c += (a.get(i) % 10);
            a.set(i,(a.get(i)/10));
        }
        a.set(i,c);
    }

    return a;
}

// Find the largest M distinct digit
// sum from the digitSum vector
public static int findMMaxDistinctDigitSum(Vector<Integer> distinctDigitSum,int m)
{
    // Find the sum of last M numbers.
    int sum = 0;
    for (int i = distinctDigitSum.size() - 1;
            i >= 0 && m > 0;i--, m--)
        sum += distinctDigitSum.get(i);

    return sum;
}

// Find the at most M numbers from N natural
// numbers whose digit sum is distinct
// and those M numbers are factors of K.
public static int findDistinctMnumbers(int n, int k, int m)
{

    // Find out the factors of
    // K less than N
    Vector<Integer> factors = findFactors(n, k);

    // Sum of digits for each
    // element in vector
    Vector<Integer> digitSum = findDigitSum(factors);

    // Sorting the digitSum vector

    Collections.sort(digitSum);

    // Removing the duplicate elements

    HashSet<Integer> hs1 = new HashSet<Integer>(digitSum);

    //"HashSet" is stores only unique elements

    Vector<Integer> vect2 = new Vector<Integer>(hs1);

    // Finding the sum and returning it
    return findMMaxDistinctDigitSum(vect2, m);
}

// Driver Code
public static void main(String args[])
{
    int n = 100, k = 80, m = 4;

    // Function Call
    System.out.println(findDistinctMnumbers(n, k, m));
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python 3 implementation to find the sum of
# maximum distinct digit sum of at most
# M numbers from 1 to N that are factors of K
import math

# Function to find the factors
# of K in N
def findFactors(n, k):

    # Initialise a vector
    factors = []

    # Find out the factors of
    # K less than N
    sqt = (int)(math.sqrt(k))
    for i in range(1, sqt):
        if (k % i == 0):
            if (k // i == i and i <= n):
                factors.append(i)
            else:
                if (i <= n):
                    factors.append(i)
                if (k // i <= n):
                    factors.append(k // i)
    return factors

# Find the digit sum of each factor
def findDigitSum(a):

    # Sum of digits for each
    # element in vector
    for i in range(len(a)):
        c = 0
        while (a[i] > 0):
            c += a[i] % 10
            a[i] = a[i] // 10
        a[i] = c
    return a

# Find the largest M distinct digit
# sum from the digitSum vector
def findMMaxDistinctDigitSum(
        distinctDigitSum, m):

    # Find the sum of last M numbers.
    sum = 0
    i = len(distinctDigitSum) - 1
    while (i >= 0 and m > 0):
        sum += distinctDigitSum[i]
        i -= 1
        m -= 1
    return sum

# Find the at most M numbers from N natural
# numbers whose digit sum is distinct
# and those M numbers are factors of K
def findDistinctMnumbers(n, k, m):

    # Find out the factors of
    # K less than N
    factors = findFactors(n, k)

    # Sum of digits for each
    # element in vector
    digitSum = findDigitSum(factors)

    # Sorting the digitSum vector
    digitSum.sort()

    # Removing the duplicate elements
    ip = list(set(digitSum))

    # Finding the sum and returning it
    return findMMaxDistinctDigitSum(ip, m)

# Driver Code
if __name__ == "__main__":

    n = 100
    k = 80
    m = 4

    # Function Call
    print(findDistinctMnumbers(n, k, m))

    # This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation to find the sum of
// maximum distinct digit sum of at most
// M numbers from 1 to N that are factors of K

// Function to find the factors
// of K in N
function findFactors(n, k)
{
    let factors = [];

    // Initialise a vector

    // Find out the factors of
    // K less than N
    for(let i = 1; i <= Math.sqrt(k); i++)
    {
        if (k % i == 0)
        {
            if (k / i == i && i <= n)
                factors.push(i);
            else
            {
                if (i <= n)
                    factors.push(i);
                if (k / i <= n)
                    factors.push(k / i);
            }
        }
    }
    return factors;
}

// Find the digit sum of each factor
function findDigitSum(a)
{

    // Sum of digits for each
    // element in vector
    for(let i = 0; i < a.length; i++)
    {
        let c = 0;

        while (a[i] > 0)
        {
            c += (a[i] % 10);
            a[i] = Math.floor(a[i] / 10);
        }
        a[i] = c;
    }
    return a;
}

// Find the largest M distinct digit
// sum from the digitSum vector
function findMMaxDistinctDigitSum(distinctDigitSum, m)
{

    // Find the sum of last M numbers.
    let sum = 0;
    for(let i = distinctDigitSum.length - 1;
            i >= 0 && m > 0;i--, m--)
        sum += distinctDigitSum[i];

    return sum;
}

// Find the at most M numbers from N natural
// numbers whose digit sum is distinct
// and those M numbers are factors of K.
function findDistinctMnumbers(n, k, m)
{

    // Find out the factors of
    // K less than N
    let factors = findFactors(n, k);

    // Sum of digits for each
    // element in vector
    let digitSum = findDigitSum(factors);

    // Sorting the digitSum vector
    digitSum.sort(function(a, b){return a - b;});

    // Removing the duplicate elements
    let hs1 = new Set(digitSum);

    // "HashSet" is stores only unique elements
    let vect2 = Array.from(hs1);

    // Finding the sum and returning it
    return findMMaxDistinctDigitSum(vect2, m);
}

// Driver Code
let n = 100, k = 80, m = 4;

// Function Call
document.write(findDistinctMnumbers(n, k, m));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
24
```

**性能分析:**

*   **时间复杂度:**在给定的方法中，主要有如下两个过程–
    *   求一个数的因子的时间复杂度是:O(√(K))
    *   对唯一元素进行排序和存储的时间复杂度:O(√(K)log(√(K))
*   **辅助空间:**在给定的方法中，有一个额外的数组用于存储数字 K 的因子，即: **O(√(K))**