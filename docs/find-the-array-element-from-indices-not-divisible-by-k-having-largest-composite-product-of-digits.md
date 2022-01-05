# 从不能被 K 整除的索引中找到数组元素，其中 K 是数字的最大合成乘积

> 原文:[https://www . geeksforgeeks . org/find-the-array-element-from-indexes-不能被 k 整除-具有最大的复合数字积/](https://www.geeksforgeeks.org/find-the-array-element-from-indices-not-divisible-by-k-having-largest-composite-product-of-digits/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是从不能被 **K** 整除的索引中找到数组元素，这些索引的数字乘积是一个[复合数](https://www.geeksforgeeks.org/composite-number/)。

**示例:**

> **输入:** arr[] = {233，144，89，71，13，21，11，34，55，23}， K = 3
> **输出:** 89
> **说明:**
> 以下元素以数字乘积作为**复合数** :
> arr[0] = 233:数字乘积= 2 * 3 * 3 = 18
> arr[1] = 144:数字乘积= 1 * 4 * 4 = 16
> arr[2] = 89:数字乘积= 8 * 9 = **72 【T15 = 34:位数乘积= 3 * 4 = 12
> arr[8] = 55:位数乘积= 5 * 5 = 25
> 因此，在不能被 K ( = 3)整除的索引处，数组元素位数的最大复合乘积是 **72** 。**
> 
> **输入:** arr[] = {122，566，131，211，721，19，65，1111，111777}，K = 4
> **输出:** 566

**方法:**按照下面给出的步骤解决问题

*   遍历给定数组 **arr[]** 。
*   对于每个数组**元素**，检查其数字的**乘积**是**复合**还是其数字的乘积小于或等于 **1** 。
*   如果它的数字乘积是复合的，并且它的位置能被 k 整除，那么
    *   在向量 **pq** 中插入 **ans** 变量及其复合 [**数字产品**](https://www.geeksforgeeks.org/digit-product-sequence/) 中的元素。
*   最后，对向量 **pq** 中的元素进行排序后，找到复合最大的元素 [**数字产品**](https://www.geeksforgeeks.org/digit-product-sequence/) 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
#include <vector>

using namespace std;

// Function to check if a number
// is a composite number or not
bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // Check if number is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check if number is a multiple
    // of any other prime number
    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to calculate the product
// of digits of a number
int digitProduct(int number)
{
    // Stores the product of digits
    int product = 1;

    while (number > 0) {

        // Extract digits of a number
        product *= (number % 10);

        // Calculate product of digits
        number /= 10;
    }
    return product;
}

// Function to check if the product of digits
// of a number is a composite number or not
bool compositedigitProduct(int num)
{
    // Stores product of digits
    int res = digitProduct(num);

    // If product of digits is equal to 1
    if (res == 1) {
        return false;
    }
    // If product of digits is not prime
    if (isComposite(res)) {
        return true;
    }

    return false;
}
// Function to find the number with largest
// composite product of digits from the indices
// not divisible by k from the given array
int largestCompositeDigitProduct(int a[], int n, int k)
{
    vector<pair<int, int> > pq;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If index is divisible by k
        if ((i % k) == 0) {
            continue;
        }

        // Check if product of digits
        // is a composite number or not
        if (compositedigitProduct(a[i])) {
            int b = digitProduct(a[i]);
            pq.push_back(make_pair(b, a[i]));
        }
    }

    // Sort the products
    sort(pq.begin(), pq.end());

    return pq.back().second;
}

// Driver Code
int main()
{

    int arr[] = { 233, 144, 89, 71, 13,
                  21, 11, 34, 55, 23 };
    int n = sizeof(arr)
            / sizeof(arr[0]);
    int k = 3;

    int ans = largestCompositeDigitProduct(
        arr, n, k);

    cout << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to check if a number
// is a composite number or not
static boolean isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // Check if number is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check if number is a multiple
    // of any other prime number
    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to calculate the product
// of digits of a number
static int digitProduct(int number)
{
    // Stores the product of digits
    int product = 1;
    while (number > 0) {

        // Extract digits of a number
        product *= (number % 10);

        // Calculate product of digits
        number /= 10;
    }
    return product;
}

// Function to check if the product of digits
// of a number is a composite number or not
static boolean compositedigitProduct(int num)
{
    // Stores product of digits
    int res = digitProduct(num);

    // If product of digits is equal to 1
    if (res == 1) {
        return false;
    }

    // If product of digits is not prime
    if (isComposite(res)) {
        return true;
    }
    return false;
}
// Function to find the number with largest
// composite product of digits from the indices
// not divisible by k from the given array
static int largestCompositeDigitProduct(int a[], int n, int k)
{
    Vector<pair> pq = new Vector<pair>();

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If index is divisible by k
        if ((i % k) == 0) {
            continue;
        }

        // Check if product of digits
        // is a composite number or not
        if (compositedigitProduct(a[i]))
        {
            int b = digitProduct(a[i]);
            pq.add(new pair(b, a[i]));
        }
    }

    // Sort the products
    Collections.sort(pq, (x, y) -> x.first - y.first);

    return pq.get(pq.size() - 1).second;
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 233, 144, 89, 71, 13,
                  21, 11, 34, 55, 23 };
    int n = arr.length;
    int k = 3;
    int ans = largestCompositeDigitProduct(
        arr, n, k);
    System.out.print(ans +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import ceil, sqrt

# Function to check if a number
# is a composite number or not
def isComposite(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return False

    # Check if number is divisible by 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return True

    # Check if number is a multiple
    # of any other prime number
    for i in range(5, ceil(sqrt(n)),6):
        if (n % i == 0 or n % (i + 2) == 0):
            return True

    return False

# Function to calculate the product
# of digits of a number
def digitProduct(number):

    # Stores the product of digits
    product = 1

    while (number > 0):

        # Extract digits of a number
        product *= (number % 10)

        # Calculate product of digits
        number //= 10
    return product

# Function to check if the product of digits
# of a number is a composite number or not
def compositedigitProduct(num):

    # Stores product of digits
    res = digitProduct(num)

    # If product of digits is equal to 1
    if (res == 1):
        return False
    # If product of digits is not prime
    if (isComposite(res)):
        return True

    return False

# Function to find the number with largest
# composite product of digits from the indices
# not divisible by k from the given array
def largestCompositeDigitProduct(a, n, k):
    pq = []

    # Traverse the array
    for i in range(n):

        # If index is divisible by k
        if ((i % k) == 0):
            continue

        # Check if product of digits
        # is a composite number or not
        if (compositedigitProduct(a[i])):
            b = digitProduct(a[i])
            pq.append([b, a[i]])

    # Sort the products
    pq = sorted (pq)
    return pq[-1][1]

# Driver Code
if __name__ == '__main__':

    arr = [233, 144, 89, 71, 13, 21, 11, 34, 55, 23]
    n = len(arr)
    k = 3

    ans = largestCompositeDigitProduct(arr, n, k)
    print (ans)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{
    class pair : IComparable<pair>
    {
        public int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }
         public int CompareTo(pair p)
         {
             return this.second-p.first;
         }
    }

// Function to check if a number
// is a composite number or not
static bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // Check if number is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check if number is a multiple
    // of any other prime number
    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to calculate the product
// of digits of a number
static int digitProduct(int number)
{

    // Stores the product of digits
    int product = 1;
    while (number > 0)
    {

        // Extract digits of a number
        product *= (number % 10);

        // Calculate product of digits
        number /= 10;
    }
    return product;
}

// Function to check if the product of digits
// of a number is a composite number or not
static bool compositedigitProduct(int num)
{

    // Stores product of digits
    int res = digitProduct(num);

    // If product of digits is equal to 1
    if (res == 1) {
        return false;
    }

    // If product of digits is not prime
    if (isComposite(res)) {
        return true;
    }
    return false;
}
// Function to find the number with largest
// composite product of digits from the indices
// not divisible by k from the given array
static int largestCompositeDigitProduct(int []a, int n, int k)
{
    List<pair> pq = new List<pair>();

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // If index is divisible by k
        if ((i % k) == 0)
        {
            continue;
        }

        // Check if product of digits
        // is a composite number or not
        if (compositedigitProduct(a[i]))
        {
            int b = digitProduct(a[i]);
            pq.Add(new pair(b, a[i]));
        }
    }

    // Sort the products
    pq.Sort();
    return pq[pq.Count - 1].second;
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 233, 144, 89, 71, 13,
                  21, 11, 34, 55, 23 };
    int n = arr.Length;
    int k = 3;
    int ans = largestCompositeDigitProduct(
        arr, n, k);
    Console.Write(ans +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach
class pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to check if a number
// is a composite number or not
function isComposite(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // Check if number is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check if number is a multiple
    // of any other prime number
    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to calculate the product
// of digits of a number
function digitProduct(number)
{
    // Stores the product of digits
    let product = 1;
    while (number > 0) {

        // Extract digits of a number
        product *= (number % 10);

        // Calculate product of digits
        number = Math.floor(number/10);
    }
    return product;
}

// Function to check if the product of digits
// of a number is a composite number or not
function compositedigitProduct(num)
{
    // Stores product of digits
    let res = digitProduct(num);

    // If product of digits is equal to 1
    if (res == 1) {
        return false;
    }

    // If product of digits is not prime
    if (isComposite(res)) {
        return true;
    }
    return false;
}

// Function to find the number with largest
// composite product of digits from the indices
// not divisible by k from the given array
function largestCompositeDigitProduct(a,n,k)
{
    let pq = [];

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // If index is divisible by k
        if ((i % k) == 0) {
            continue;
        }

        // Check if product of digits
        // is a composite number or not
        if (compositedigitProduct(a[i]))
        {
            let b = digitProduct(a[i]);
            pq.push(new pair(b, a[i]));
        }
    }

    // Sort the products
    pq.sort(function(x, y) {return x.first - y.first});

    return pq[pq.length-1].second;
}

// Driver Code
let arr=[233, 144, 89, 71, 13,
                  21, 11, 34, 55, 23];
let n = arr.length;
let k = 3;
let ans = largestCompositeDigitProduct(
        arr, n, k);
document.write(ans +"<br>");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
89
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)