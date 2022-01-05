# 根据数字的乘积对数字进行排序

> 原文:[https://www . geesforgeks . org/根据数字产品对数字进行排序/](https://www.geeksforgeeks.org/sort-the-numbers-according-to-their-product-of-digits/)

给定一个非负整数 **N** 的数组 **arr[]** ，任务是根据这些整数的数字乘积对它们进行排序。
**例:**

> **输入:** arr[] = {12，10，102，31，15}
> **输出:**10 102 12 31 15
> 10->1 * 0 = 0
> 102->1 * 0 * 2 = 0
> 12->1 * 2 = 2
> 31->3 * 1 = 3
> 15->1 * 5

**方法:**思想是将每个元素及其数字乘积存储在一个向量对中，然后根据存储的数字乘积对向量的所有元素进行排序。最后，按顺序打印元素。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the product
// of the digits of n
int productOfDigit(int n)
{
    int product = 1;
    while (n > 0) {
        product *= n % 10;
        n = n / 10;
    }
    return product;
}

// Function to sort the array according to
// the product of the digits of elements
void sortArr(int arr[], int n)
{
    // Vector to store the digit product
    // with respective elements
    vector<pair<int, int> > vp;

    // Inserting digit product with elements
    // in the vector pair
    for (int i = 0; i < n; i++) {
        vp.push_back(make_pair(productOfDigit(arr[i]), arr[i]));
    }

    // Sort the vector, this will sort the pair
    // according to the product of the digits
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " ";
}

// Driver code
int main()
{
    int arr[] = { 12, 10, 102, 31, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the product
# of the digits of n
def productOfDigit(n) :

    product = 1;
    while (n > 0) :
        product *= (n % 10);
        n = n // 10;

    return product;

# Function to sort the array according to
# the product of the digits of elements
def sortArr(arr, n) :

    # Vector to store the digit product
    # with respective elements
    vp = [];

    # Inserting digit product with elements
    # in the vector pair
    for i in range(n) :
        vp.append((productOfDigit(arr[i]), arr[i]));

    # Sort the vector, this will sort the pair
    # according to the product of the digits
    vp.sort();

    # Print the sorted vector content
    for i in range(len(vp)) :
        print(vp[i][1], end = " ");

# Driver code
if __name__ == "__main__" :

    arr = [ 12, 10, 102, 31, 15 ];
    n = len(arr);

    sortArr(arr, n);

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to return the product
// of the digits of n
function productOfDigit(n)
{
    var product = 1;
    while (n > 0) {
        product *= n % 10;
        n = Math.floor(n / 10);
    }
    return product;
}

// Function to sort the array according to
// the product of the digits of elements
function sortArr(arr, n)
{
    // Vector to store the digit product
    // with respective elements
    var vp = new Array(n);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < vp.length; i++) {
        vp[i] = [];
    }

    // Inserting digit product with elements
    // in the vector pair
    for (var i = 0; i < n; i++) {
        vp[i].push(productOfDigit(arr[i]));
        vp[i].push(arr[i]);
    }

    // Sort the vector, this will sort the pair
    // according to the product of the digits
    vp.sort();

    // Print the sorted vector content
    for (var i = 0; i < n; i++)
        document.write(vp[i][1] + " ");
}

// Driver code
var arr = [ 12, 10, 102, 31, 15];
var n = arr.length;
sortArr(arr, n);

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
10 102 12 31 15
```

**时间复杂度:** O(nlogn)