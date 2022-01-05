# 通过将范围[a，b]和[b，c]

中的任意两个数字相加，获得范围[1，b+c]中每个数字的方法数

> 原文:[https://www . geeksforgeeks . org/通过添加任意两个范围内的数字 a-B-和 b-c 获得每个范围内的数字的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-obtain-each-numbers-in-range-1-bc-by-adding-any-two-numbers-in-range-a-b-and-b-c/)

给定三个整数 **a** 、 **b** 和 **c** 。您需要从范围[a，b]中选择一个整数，从范围[b，c]中选择一个整数并相加。计算获得[1，b+c]范围内所有数字之和的方法数的任务。

**示例:**

> **输入:** a = 1，b = 2，c = 2
> **输出:** 0，0，1，1
> **说明:**
> 需要得到的数是【1，b+ c】=【1，4】= { 1，2，3，4}
> 因此，每一个的获取方式数是:
> 1–无法得到
> 2–无法得到
> 3–只有一种方式。从范围[a，b]中选择{1}和从范围[b，c]中选择{ 2 }–1+2 = 3
> 4–只有一种方式。从范围[a，b]中选择{2}，从范围[b，c]中选择{ 2 }–2+2 = 4
> 
> **输入:** a = 1，b = 3，c = 4
> **输出:** 0，0，0，1，2，2，1

**简单方法:**

*   一个简单的强力解决方案是使用[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)，其中外部循环从 i = a 遍历到 i = b，内部循环从 j = b 遍历到 j = c。
*   我们将用零初始化大小为 **b + c + 1** 的数组 a。现在在循环中，我们将在 i+j 处增加索引，即 **(a[i+j]++)** 。
*   我们将在最后简单地打印数组。

下面是上述方法的实现。

## C++

```
// C++ program to calculate
// the number of ways

#include <bits/stdc++.h>
using namespace std;

void CountWays(int a, int b, int c)
{
    int x = b + c + 1;
    int arr[x] = { 0 };

    // Initialising the array with zeros.
    // You can do using memset too.
    for (int i = a; i <= b; i++) {
        for (int j = b; j <= c; j++) {
            arr[i + j]++;
        }
    }
    // Printing the array
    for (int i = 1; i < x; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}
// Driver code
int main()
{
    int a = 1;
    int b = 2;
    int c = 2;

    CountWays(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the number of ways
class GFG{

public static void CountWays(int a, int b,
                                    int c)
{
    int x = b + c + 1;
    int[] arr = new int[x];

    // Initialising the array with zeros.
    // You can do using memset too.
    for(int i = a; i <= b; i++)
    {
       for(int j = b; j <= c; j++)
       {
          arr[i + j]++;
       }
    }

    // Printing the array
    for(int i = 1; i < x; i++)
    {
       System.out.print(arr[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int a = 1;
    int b = 2;
    int c = 2;

    CountWays(a, b, c);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to calculate
# the number of ways
def CountWays(a, b, c):

    x = b + c + 1;
    arr = [0] * x;

    # Initialising the array with zeros.
    # You can do using memset too.
    for i in range(a, b + 1):
        for j in range(b, c + 1):
            arr[i + j] += 1;

    # Printing the array
    for i in range(1, x):
        print(arr[i], end = " ");

# Driver code
if __name__ == '__main__':

    a = 1;
    b = 2;
    c = 2;

    CountWays(a, b, c);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to calculate
// the number of ways
using System;
class GFG{

public static void CountWays(int a, int b,
                                    int c)
{
    int x = b + c + 1;
    int[] arr = new int[x];

    // Initialising the array with zeros.
    // You can do using memset too.
    for(int i = a; i <= b; i++)
    {
        for(int j = b; j <= c; j++)
        {
            arr[i + j]++;
        }
    }

    // Printing the array
    for(int i = 1; i < x; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main()
{
    int a = 1;
    int b = 2;
    int c = 2;

    CountWays(a, b, c);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // Javascript program to calculate
    // the number of ways

    function CountWays(a, b, c)
    {
        let x = b + c + 1;
        let arr = new Array(x);
        arr.fill(0);

        // Initialising the array with zeros.
        // You can do using memset too.
        for (let i = a; i <= b; i++) {
            for (let j = b; j <= c; j++) {
                arr[i + j]++;
            }
        }
        // Printing the array
        for (let i = 1; i < x; i++) {
            document.write(arr[i] + " ");
        }
        document.write("</br>");
    }

    // Driver code

    let a = 1;
    let b = 2;
    let c = 2;

    CountWays(a, b, c);

</script>
```

**Output:** 

```
0 0 1 1
```

**时间复杂度:** O((b-a)*(c-b))，最坏的情况是 O(c <sup>2</sup> )

**高效途径:**思路是用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)逻辑来解决这个问题。

1.  我们将从[a，b]遍历 I，对于每个 I，我们将简单地将起始区间 arr[i + b]的值增加 1，并将结束区间 arr[i + c + 1]的值减少 1。
2.  现在我们需要做的就是计算数组的前缀和(arr[i]+ = arr[i-1])并打印数组。

让我们借助一个例子来看看这个方法。
这为什么管用？

> 比如:a = 1，b = 2，c = 2，我们只会遇到 I
> I = 1 =>arr[1+2]+++的两个值；arr[1+2+1]–；
> I = 2 =>arr[2+2]++；arr[2+2+1]–；
> arr = {0，0，0，1，0，-1 }；
> 前缀和:
> arr = {0，0，0，1，1，0 }；
> 现在仔细看，意识到这是我们的答案。
> 所以我们在特定索引 I 上做的是 arr[I+b]+++和 arr[I+c+1]–；
> 现在我们使用前缀和，所以所有的值将在 i+b 和无穷大之间增加 1(我们不会去那里，但是将导致前缀和增加 1，并且一旦我们在 i+c+1 进行减量，i+c+1 和无穷大之间的所有值将减少 1。
> 因此有效地，范围[i+b，i+c]中的所有值都增加 1，其余所有值都将不受影响。

下面是上述方法的实现。

## C++

```
// C++ program to calculate
// the number of ways

#include <bits/stdc++.h>
using namespace std;

void CountWays(int a, int b, int c)
{
    // 2 is added because sometimes
    // we will decrease the
    // value out of bounds.
    int x = b + c + 2;

    // Initialising the array with zeros.
    // You can do using memset too.
    int arr[x] = { 0 };

    for (int i = 1; i <= b; i++) {
        arr[i + b]++;
        arr[i + c + 1]--;
    }

    // Printing the array
    for (int i = 1; i < x - 1; i++) {
        arr[i] += arr[i - 1];
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    int a = 1;
    int b = 2;
    int c = 2;

    CountWays(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the number of ways
import java.util.*;

class GFG{

static void CountWays(int a, int b, int c)
{

    // 2 is added because sometimes
    // we will decrease the
    // value out of bounds.
    int x = b + c + 2;

    // Initialising the array with zeros.
    int arr[] = new int[x];

    for(int i = 1; i <= b; i++)
    {
       arr[i + b]++;
       arr[i + c + 1]--;
    }

    // Printing the array
    for(int i = 1; i < x - 1; i++)
    {
       arr[i] += arr[i - 1];
       System.out.print(arr[i] + " ");
    }
    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    int a = 1;
    int b = 2;
    int c = 2;

    CountWays(a, b, c);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to calculate
# the number of ways
def CountWays(a, b, c):

    # 2 is added because sometimes
    # we will decrease the
    # value out of bounds.
    x = b + c + 2;

    # Initialising the array with zeros.
    arr = [0] * x;

    for i in range(1, b+1):
       arr[i + b] = arr[i + b] + 1;
       arr[i + c + 1] = arr[i + c + 1] -1;

    # Printing the array
    for i in range(1, x-1):

       arr[i] += arr[i - 1];
       print(arr[i], end = " ");

# Driver code
if __name__ == '__main__':

    a = 1;
    b = 2;
    c = 2;

    CountWays(a, b, c);

# This code is contributed by rock_cool
```

## C#

```
// C# program to calculate
// the number of ways
using System;
class GFG{

static void CountWays(int a, int b, int c)
{

    // 2 is added because sometimes
    // we will decrease the
    // value out of bounds.
    int x = b + c + 2;

    // Initialising the array with zeros.
    int []arr = new int[x];

    for(int i = 1; i <= b; i++)
    {
        arr[i + b]++;
        arr[i + c + 1]--;
    }

    // Printing the array
    for(int i = 1; i < x - 1; i++)
    {
        arr[i] += arr[i - 1];
        Console.Write(arr[i] + " ");
    }
    Console.WriteLine();
}

// Driver code
public static void Main()
{
    int a = 1;
    int b = 2;
    int c = 2;

    CountWays(a, b, c);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to calculate
// the number of ways
function CountWays(a, b, c)
{

    // 2 is added because sometimes
    // we will decrease the
    // value out of bounds.
    let x = b + c + 2;

    // Initialising the array with zeros.
    // You can do using memset too.
    let arr = new Array(x);
    arr.fill(0);

    for(let i = 1; i <= b; i++)
    {
        arr[i + b]++;
        arr[i + c + 1]--;
    }

    // Printing the array
    for(let i = 1; i < x - 1; i++)
    {
        arr[i] += arr[i - 1];
        document.write(arr[i] + " ");
    }
    document.write("</br>");
}

// Driver code
let a = 1;
let b = 2;
let c = 2;

CountWays(a, b, c);

// This code is contributed by rameshtravel07 

</script>
```

**Output:** 

```
0 0 1 1
```

**时间复杂度:** O(C)