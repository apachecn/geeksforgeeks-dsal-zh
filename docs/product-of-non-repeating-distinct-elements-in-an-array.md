# 数组中不重复(不同)元素的乘积

> 原文:[https://www . geeksforgeeks . org/非重复不同元素阵列产品/](https://www.geeksforgeeks.org/product-of-non-repeating-distinct-elements-in-an-array/)

给定一个带有**重复元素**的整数数组。任务是找到给定数组中所有不同元素的乘积。
**示例** :

> **输入** : arr[] = {12，10，9，45，2，10，10，45，10 }；
> **输出** : 97200
> 这里我们取 12、10、9、45、2 为产品
> 因为这些是唯一不同的元素
> **输入** : arr[] = {1、10、9、4、2、10、10、45、4 }；
> **输出** : 32400

一个**简单的解决方案**是使用两个嵌套循环。外部循环从最左边的元素开始一个接一个地选取一个元素。内部循环检查元素是否在它的左侧。如果存在，则忽略该元素。
**时间复杂度** : O(N <sup>2</sup> )
**辅助空间** : O(1)
A **这个问题的更好的解决方案**是先将数组的所有元素按照升序排序，在数组中找到一个个截然不同的元素。最后，找到所有不同元素的乘积。
以下是本办法的实施情况:

## C++

```
// C++ program to find the product of all
// non-repeated elements in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the product of all
// non-repeated elements in an array
int findProduct(int arr[], int n)
{
    // sort all elements of array
    sort(arr, arr + n);

    int prod = 1;
    for (int i = 0; i < n; i++) {
        if (arr[i] != arr[i + 1])
            prod = prod * arr[i];
    }

    return prod;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 1, 1, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(int);

    cout << findProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product of all
// non-repeated elements in an array
import java.util.Arrays;

class GFG {

// Function to find the product of all
// non-repeated elements in an array
static int findProduct(int arr[], int n)
{
    // sort all elements of array
    Arrays.sort(arr);

    int prod = 1 * arr[0];
    for (int i = 0; i < n - 1; i++)
    {
        if (arr[i] != arr[i + 1])
        {
            prod = prod * arr[i + 1];
        }

    }
    return prod;
}

// Driver code
public static void main(String[] args) {
    int arr[] = {1, 2, 3, 1, 1, 4, 5, 6};
    int n = arr.length;
    System.out.println(findProduct(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to find the product
# of all non-repeated elements in an array

# Function to find the product of all
# non-repeated elements in an array
def findProduct(arr, n):

    # sort all elements of array
    sorted(arr)

    prod = 1
    for i in range(0, n, 1):
        if (arr[i - 1] != arr[i]):
            prod = prod * arr[i]

    return prod;

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 1, 1, 4, 5, 6]

    n = len(arr)

    print(findProduct(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the product of all
// non-repeated elements in an array
using System;

class GFG
{

// Function to find the product of all
// non-repeated elements in an array
static int findProduct(int []arr, int n)
{
    // sort all elements of array
    Array.Sort(arr);

    int prod = 1 * arr[0];
    for (int i = 0; i < n - 1; i++)
    {
        if (arr[i] != arr[i + 1])
        {
            prod = prod * arr[i + 1];
        }

    }
    return prod;
}

// Driver code
public static void Main()
{
    int []arr = {1, 2, 3, 1, 1, 4, 5, 6};
    int n = arr.Length;
    Console.WriteLine(findProduct(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to find the product of all
// non-repeated elements in an array

    // Function to find the product of all
    // non-repeated elements in an array
    function findProduct(arr , n) {
        // sort all elements of array
        arr.sort();

        var prod = 1 * arr[0];
        for (i = 0; i < n - 1; i++) {
            if (arr[i] != arr[i + 1]) {
                prod = prod * arr[i + 1];
            }

        }
        return prod;
    }

    // Driver code

        var arr = [ 1, 2, 3, 1, 1, 4, 5, 6 ];
        var n = arr.length;
        document.write(findProduct(arr, n));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
720
```

**时间复杂度** : O(N * logN)
**辅助空间** : O(1)
一个**高效的解决方案**是遍历数组并保留一个哈希映射来检查元素是否重复。遍历时，如果当前元素是否已经存在于哈希中，如果是，则意味着它是重复的，不应该与乘积相乘，如果它不存在于哈希中，则将其与乘积相乘并将其插入哈希中。
以下是本办法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the product of all
// non- repeated elements in an array
#include <bits/stdc++.h>
using namespace std;

// Function to find the product of all
// non-repeated elements in an array
int findProduct(int arr[], int n)
{
    int prod = 1;

    // Hash to store all element of array
    unordered_set<int> s;
    for (int i = 0; i < n; i++) {
        if (s.find(arr[i]) == s.end()) {
            prod *= arr[i];
            s.insert(arr[i]);
        }
    }

    return prod;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 1, 1, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(int);

    cout << findProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product of all
// non- repeated elements in an array
import java.util.HashSet;

class GFG
{

    // Function to find the product of all
    // non-repeated elements in an array
    static int findProduct(int arr[], int n)
    {
        int prod = 1;

        // Hash to store all element of array
        HashSet<Integer> s = new HashSet<>();
        for (int i = 0; i < n; i++)
        {
            if (!s.contains(arr[i]))
            {
                prod *= arr[i];
                s.add(arr[i]);
            }
        }

        return prod;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 1, 1, 4, 5, 6};
        int n = arr.length;

        System.out.println(findProduct(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 计算机编程语言

```
# Python3 program to find the product of all
# non- repeated elements in an array

# Function to find the product of all
# non-repeated elements in an array
def findProduct( arr, n):

    prod = 1

    # Hash to store all element of array
    s = dict()
    for i in range(n):
        if (arr[i] not in s.keys()):
            prod *= arr[i]
            s[arr[i]] = 1

    return prod

# Driver code
arr= [1, 2, 3, 1, 1, 4, 5, 6]
n = len(arr)

print(findProduct(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find the product of all
// non- repeated elements in an array
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the product of all
    // non-repeated elements in an array
    static int findProduct(int []arr, int n)
    {
        int prod = 1;

        // Hash to store all element of array
        HashSet<int> s = new HashSet<int>();
        for (int i = 0; i < n; i++)
        {
            if (!s.Contains(arr[i]))
            {
                prod *= arr[i];
                s.Add(arr[i]);
            }
        }

        return prod;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 2, 3, 1, 1, 4, 5, 6};
        int n = arr.Length;

        Console.WriteLine(findProduct(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find the product of all
// non- repeated elements in an array

// Function to find the product of all
// non-repeated elements in an array
function findProduct(arr,n)
{
    let prod = 1;

        // Hash to store all element of array
        let s = new Set();
        for (let i = 0; i < n; i++)
        {
            if (!s.has(arr[i]))
            {
                prod *= arr[i];
                s.add(arr[i]);
            }
        }

        return prod;
}

// Driver code
let arr=[1, 2, 3, 1, 1, 4, 5, 6];
let n = arr.length;
document.write(findProduct(arr, n));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
720
```

**时间复杂度**:O(N)
T3】辅助空间 : O(N)