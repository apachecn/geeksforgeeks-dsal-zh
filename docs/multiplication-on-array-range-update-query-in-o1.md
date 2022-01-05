# 数组上的乘法:O(1)中的范围更新查询

> 原文:[https://www . geesforgeks . org/数组乘法-范围-更新-查询-in-o1/](https://www.geeksforgeeks.org/multiplication-on-array-range-update-query-in-o1/)

考虑整数数组 A[]和以下两种类型的查询。

1.  更新(l，r，x):将 x 乘以从 A[l]到 A[r]的所有值(包括这两个值)。
2.  printArray():打印当前修改的数组。

**例:**

```
Input: A[] = {1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
        update(0, 2, 2)
        update(1, 4, 3)
        print()
        update(4, 8, 5)
        print()
Output: 2 6 6 3 15 5 5 5 5 1
Explanation: 
The query update(0, 2, 2) 
multiply 2 to A[0], A[1] and A[2]. 
After update, A[] becomes {2, 2, 2, 1, 1, 1, 1, 1, 1, 1}       
Query update(1, 4, 3) multiply 3 to A[1],
A[2], A[3] and A[4]. After update, A[] becomes
{2, 6, 6, 3, 3, 1, 1, 1, 1, 1}.
Query update(4, 8, 5) multiply 5, A[4] to A[8]. 
After update, A[] becomes {2, 6, 6, 3, 15, 5, 5, 5, 5, 1}.

Input: A[] = {10, 5, 20, 40}
        update(0, 1, 10)
        update(1, 3, 20)
        update(2, 2, 2)
        print()
Output: 100 1000 800 800
```

**进场:**
一个简单的解决方法是做以下几点:

1.  更新(l，r，x):运行一个从 l 到 r 的循环，并将 x 乘以从 A[l]到 A[r]的所有元素。
2.  print():只需打印 A[]。

上述两种操作的时间复杂度都是 O(n)。
**有效方法:**
一个有效的解决方案是使用两个数组，一个用于乘法，另一个用于除法。分别为 mul[]和 div[]。

1.  将 x 乘以 mul[l]并将 x 乘以 div[r+1]
2.  取 mul 数组 mul[i] = (mul[i] * mul[i-1])的前缀乘法/ div[i]
3.  printArray():做 A[0] = mul[0]并打印。对于其余元素，执行 A[i] = (A[i]*mul[i])

以下是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Creates a mul[] array for A[] and returns
// it after filling initial values.
void initialize(int mul[], int div[], int size)
{

    for (int i = 1; i < size; i++) {
        mul[i] = (mul[i] * mul[i - 1]) / div[i];
    }
}

// Does range update
void update(int l, int r, int x, int mul[], int div[])
{
    mul[l] *= x;
    div[r + 1] *= x;
}

// Prints updated Array
void printArray(int ar[], int mul[], int div[], int n)
{

    for (int i = 0; i < n; i++) {
        ar[i] = ar[i] * mul[i];
        cout << ar[i] << " ";
    }
}

// Driver code;
int main()
{

    // Array to be updated
    int ar[] = { 10, 5, 20, 40 };
    int n = sizeof(ar) / sizeof(ar[0]);

    // Create and fill mul and div Array
    int mul[n + 1], div[n + 1];

    for (int i = 0; i < n + 1; i++) {
        mul[i] = div[i] = 1;
    }

    update(0, 1, 10, mul, div);
    update(1, 3, 20, mul, div);
    update(2, 2, 2, mul, div);

    initialize(mul, div, n + 1);

    printArray(ar, mul, div, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Creates a mul[] array for A[] and returns
// it after filling initial values.
static void initialize(int mul[],
                       int div[], int size)
{

    for (int i = 1; i < size; i++)
    {
        mul[i] = (mul[i] * mul[i - 1]) / div[i];
    }
}

// Does range update
static void update(int l, int r, int x,
                   int mul[], int div[])
{
    mul[l] *= x;
    div[r + 1] *= x;
}

// Prints updated Array
static void printArray(int ar[], int mul[],
                       int div[], int n)
{
    for (int i = 0; i < n; i++)
    {
        ar[i] = ar[i] * mul[i];
        System.out.print(ar[i] + " ");
    }
}

// Driver code;
public static void main(String[] args)
{
    // Array to be updated
    int ar[] = { 10, 5, 20, 40 };
    int n = ar.length;

    // Create and fill mul and div Array
    int []mul = new int[n + 1];
    int []div = new int[n + 1];

    for (int i = 0; i < n + 1; i++)
    {
        mul[i] = div[i] = 1;
    }

    update(0, 1, 10, mul, div);
    update(1, 3, 20, mul, div);
    update(2, 2, 2, mul, div);

    initialize(mul, div, n + 1);

    printArray(ar, mul, div, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Creates a mul[] array for A[] and returns
# it after filling initial values.
def initialize(mul, div, size):

    for i in range(1, size):
        mul[i] = (mul[i] * mul[i - 1]) / div[i];

# Does range update
def update(l, r, x, mul, div):
    mul[l] *= x;
    div[r + 1] *= x;

# Prints updated Array
def printArray(ar, mul, div, n):

    for i in range(n):
        ar[i] = ar[i] * mul[i];
        print(int(ar[i]), end = " ");

# Driver code;
if __name__ == '__main__':

    # Array to be updated
    ar = [ 10, 5, 20, 40 ];
    n = len(ar);

    # Create and fill mul and div Array
    mul = [0] * (n + 1);
    div = [0] * (n + 1);

    for i in range(n + 1):
        mul[i] = div[i] = 1;

    update(0, 1, 10, mul, div);
    update(1, 3, 20, mul, div);
    update(2, 2, 2, mul, div);

    initialize(mul, div, n + 1);

    printArray(ar, mul, div, n);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Creates a mul[] array for A[] and returns
// it after filling initial values.
static void initialize(int []mul,
                       int []div, int size)
{

    for (int i = 1; i < size; i++)
    {
        mul[i] = (mul[i] * mul[i - 1]) / div[i];
    }
}

// Does range update
static void update(int l, int r, int x,
                   int []mul, int []div)
{
    mul[l] *= x;
    div[r + 1] *= x;
}

// Prints updated Array
static void printArray(int []ar, int []mul,
                       int []div, int n)
{
    for (int i = 0; i < n; i++)
    {
        ar[i] = ar[i] * mul[i];
        Console.Write(ar[i] + " ");
    }
}

// Driver code;
public static void Main(String[] args)
{
    // Array to be updated
    int []ar = { 10, 5, 20, 40 };
    int n = ar.Length;

    // Create and fill mul and div Array
    int []mul = new int[n + 1];
    int []div = new int[n + 1];

    for (int i = 0; i < n + 1; i++)
    {
        mul[i] = div[i] = 1;
    }

    update(0, 1, 10, mul, div);
    update(1, 3, 20, mul, div);
    update(2, 2, 2, mul, div);

    initialize(mul, div, n + 1);

    printArray(ar, mul, div, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach   

// Creates a mul array for A and returns
    // it after filling initial values.
    function initialize(mul , div , size)
    {

        for (i = 1; i < size; i++) {
            mul[i] = (mul[i] * mul[i - 1]) / div[i];
        }
    }

    // Does range update
    function update(l , r , x , mul , div) {
        mul[l] *= x;
        div[r + 1] *= x;
    }

    // Prints updated Array
    function printArray(ar , mul , div , n)
    {
        for (i = 0; i < n; i++) {
            ar[i] = ar[i] * mul[i];
            document.write(ar[i] + " ");
        }
    }

    // Driver code;

        // Array to be updated
        var ar = [ 10, 5, 20, 40 ];
        var n = ar.length;

        // Create and fill mul and div Array
        var mul = Array(n + 1).fill(0);
        var div = Array(n + 1).fill(0);

        for (i = 0; i < n + 1; i++) {
            mul[i] = div[i] = 1;
        }

        update(0, 1, 10, mul, div);
        update(1, 3, 20, mul, div);
        update(2, 2, 2, mul, div);

        initialize(mul, div, n + 1);

        printArray(ar, mul, div, n);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
100 1000 800 800
```