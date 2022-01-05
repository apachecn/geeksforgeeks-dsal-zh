# 通过给定数组的每个元素乘以 K 生成一个数组

> 原文:[https://www . geeksforgeeks . org/给定数组的每个元素乘以 k 生成一个数组/](https://www.geeksforgeeks.org/generate-an-array-by-multiplying-each-element-of-given-array-by-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K** 。任务是将数组的每个元素乘以 **K** 。

**示例:**

> **输入:** arr[] = { 3，4 }，K = 2
> **输出:** 6 8
> **说明:**元素变为 3*2 = 6，4*2 = 8。
> 
> **输入:** arr[] = { 0，1，2 }，K = 7
> **输出:** { 0，7，14 }

**方法:**给定的问题可以通过以下步骤解决:

*   遍历列表中的所有元素
*   将每个元素乘以 K
*   返回修改后的列表

下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to multiply all
// the elements of array by K
void multiplyAllByK(vector<int> arr, int K)
{
    int N = arr.size();

    // Loop to multiply all
    // the array elements
    for (int i = 0; i < N; i++) {
        int x = arr[i];
        arr[i] = K * x;
    }

    // Print the modified array
    for (int i = 0; i < N; i++)
        cout << (arr[i]) << " ";
}

// Driver code
int main()
{

    vector<int> arr;
    arr.push_back(3);
    arr.push_back(4);
    int K = 2;
    multiplyAllByK(arr, K);
    return 0;
}

// This code is contributed by lokeshpotta20.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to multiply all
    // the elements of array by K
    public static void multiplyAllByK(
        ArrayList<Integer> arr, int K)
    {
        int N = arr.size();

        // Loop to multiply all
        // the array elements
        for (int i = 0; i < N; i++) {
            int x = arr.get(i);
            arr.set(i, K * x);
        }

        // Print the modified array
        for (int i = 0; i < N; i++)
            System.out.print(arr.get(i) + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        ArrayList<Integer> arr = new ArrayList<Integer>();
        arr.add(3);
        arr.add(4);
        int K = 2;
        multiplyAllByK(arr, K);
    }
}
```

## 计算机编程语言

```
# Python code to implement above approach

# Function to multiply all
# the elements of array by K
def multiplyAllByK(arr, K):

    n = len(arr)

    for i in range(n):
        x = arr[i]
        arr[i] = K * x

    for i in range(n):
        print(arr[i], end = ' ')

# Driver code
arr = [3, 4]
K = 2
multiplyAllByK(arr, K)

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement above approach

using System;
using System.Collections.Generic;

public class GFG {

    // Function to multiply all
    // the elements of array by K
    public static void multiplyAllByK(
        List<int> arr, int K)
    {
        int N = arr.Count;

        // Loop to multiply all
        // the array elements
        for (int i = 0; i < N; i++) {
            int x = arr[i];
            arr[i] =( K * x);
        }

        // Print the modified array
        for (int i = 0; i < N; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main(String[] args)
    {
        List<int> arr = new List<int>();
        arr.Add(3);
        arr.Add(4);
        int K = 2;
        multiplyAllByK(arr, K);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to multiply all
    // the elements of array by K
    const multiplyAllByK = (arr, K) => {
        let N = arr.length;

        // Loop to multiply all
        // the array elements
        for (let i = 0; i < N; i++) {
            let x = arr[i];
            arr[i] = K * x;
        }

        // Print the modified array
        for (let i = 0; i < N; i++)
            document.write(`${arr[i]} `);
    }

    // Driver code
    let arr = [];
    arr.push(3);
    arr.push(4);
    let K = 2;
    multiplyAllByK(arr, K);

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
6 8 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

**使用λ表达式的方法:**这也可以使用[λ表达式](https://www.geeksforgeeks.org/lambda-expressions-java-8/)来实现。

> **n - > n * K**
> 其中 n 可以是特定的元素，也可以是完整的数组。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to multiply all
    // the elements of array by K
    public static void multiplyAllByK(
        ArrayList<Integer> arr, int K)
    {
        arr.replaceAll(n -> n * K);
        for (Integer x : arr)
            System.out.print(x + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        ArrayList<Integer> arr
            = new ArrayList<Integer>();
        arr.add(3);
        arr.add(4);
        int K = 2;
        multiplyAllByK(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python3 code to implement above approach

# Function to multiply all
# the elements of array by K
def multiplyAllByK(arr, K):

    lambda_func = lambda n: n * K
    for i in range(len(arr)):
        print(lambda_func(arr[i]), end = ' ')

# Driver code
arr = [3, 4]
K = 2

multiplyAllByK(arr, K)

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement above approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG {

    // Function to multiply all
    // the elements of array by K
    public static void multiplyAllByK(
        List<int> arr, int K)
    {
        var temp = arr.Select(n => n * K);
        foreach (int x in temp)
            Console.Write(x + " ");
    }

    // Driver code
    public static void Main(String[] args)
    {
        List<int> arr
            = new List<int>();
        arr.Add(3);
        arr.Add(4);
        int K = 2;
        multiplyAllByK(arr, K);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code to implement above approach

// Function to multiply all
// the elements of array by K
function multiplyAllByK(arr, K) {
    arr = arr.map(k => {
        return k * K
    });
    for (x of arr)
        document.write(x + " ");
}

// Driver code
let arr = [];
arr.push(3);
arr.push(4);
let K = 2;
multiplyAllByK(arr, K);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
6 8 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)