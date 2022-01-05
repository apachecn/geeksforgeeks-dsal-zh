# 从给定的序列 Y 生成序列 X，使得 Yi = gcd(X1，，…，)

> 原文:[https://www . geesforgeks . org/generate-a-sequence-x-from-给定-sequence-y-so-yi-gcdx1-x2-Xi/](https://www.geeksforgeeks.org/generate-a-sequence-x-from-given-sequence-y-such-that-yi-gcdx1-x2-xi/)

给定大小为 **N** 的序列 **Y** ，其中:

> Y <sub>i</sub> = gcd(X <sub>1</sub> ，X <sub>2</sub> ，X <sub>3</sub> ，。。。某序列 X 的 X <sub>i</sub> )

任务是找到这样一个序列 **X** 如果任何这样的 X 是可能的话。

**注意:**如果 X 存在，那么 X 可以有多个值，生成任意一个就足够了。

**示例:**

> **输入:** N = 2，Y =【4，2】
> **输出:**【4，2】
> **解释:**Y<sub>0</sub>= gcd(X<sub>0</sub>)= X<sub>0</sub>= 4。和 gcd(4，2) = 2 = Y <sub>1</sub> 。
> 
> **输入:**【1，3】
> **输出:** -1
> **说明:**不能形成这样的序列。

**方法:**根据以下观察可以解决问题:

*   **用**的**元素 Y** = gcd(X <sub>1</sub> ，X <sub>2</sub> ，X <sub>3</sub> 。。。，X <sub>i</sub> )和 Y = gcd 的第(i+1)个元素(X <sub>1</sub> ，X <sub>2</sub> ，X <sub>3</sub> ，。。。，X <sub>i，</sub> X <sub>i+1</sub> 。
*   所以 Y 的第(i+1)个元素可以写成 gcd(gcd(X <sub>1</sub> 、X <sub>2</sub> 、X <sub>3</sub> ，。。。，X <sub>i</sub> ，X<sub>I+1</sub>)—-(1)即 gcd(a，b，c) = gcd( gcd(a，b，c))。
*   所以 Y 的第(i+1)个元素是公式 1 中的**gcd(Y 的第(i+1)个元素)。**
*   因此 Y 的第 **(i+1)个元素**必须是 Y 的第个元素的**因子，因为两个元素的 gcd 是两个元素的除数。**
*   由于 Y 的第(i+1)个元素除以 Y 的第(I)个元素， **gcd(第(i+1)个元素)**总是**等于第(i+1)个**元素。

遵循下图:

> 插图:
> 
> 例如:N = 2，Y = {4，2}
> 
> *   X[0] = Y[0] = 4，因为任何数字都是自身的 GCD。
> *   Y[1] = GCD(X[0]，X[1])。现在 GCD(X[0]) = Y[0]。所以 Y[1] = GCD(Y[0]，X[1])。因此，Y[1]应该是 Y[0]的因子。
> *   在给定的示例中，2 是 4 的因子。所以形成序列 X 是可能的，X[1]可以和 Y[1]相同。
>     赋值 X[1] = 2 满足 GCD (X[0，X[1]) = Y[1] = 2。
> *   所以最后的序列 X 是{4，2}。

因此，根据上面的观察，按照下面提到的步骤来解决问题:

1.  从序列开始处开始**穿越 Y** 。
2.  如果在给定的序列 Y 中有任何第 **(i+1)个元素**，而**没有将**与元素分开，那么序列 X **就不能生成**。
3.  如果第(i+1)个元素除以第(i+1)个元素，则存在一个序列 X，通过以上结论可以发现 Y 的第(i+1)个元素
    是 gcd(Y 的第(i+1)个元素，X <sub>i+1</sub> )和**X<sub>I+1</sub>= Y<sub>I+1</sub>**是 **X <sub>i+1</sub>** 的一个**可能值**。

以下是该方法的实施情况:

## C++

```
// C++ Program to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Euclidean theorem to find gcd
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check if it is possible
// to generate lost sequence X
void checkforX(int Y[], int N)
{
    int cur_gcd = Y[0];
    bool Xexist = true;

    // Loop to check existence of X
    for (int i = 1; i < N; i++) {
        cur_gcd = gcd(cur_gcd, Y[i]);
        if (cur_gcd != Y[i]) {
            Xexist = false;
            break;
        }
    }

    // Sequence X is found
    if (Xexist) {

        // Loop to generate X
        for (int i = 0; i < N; i++)
            cout << Y[i] << ' ';
    }

    // Sequence X can't be generated
    else {
        cout << -1 << endl;
    }
}

// Driver code
int main()
{
    int N = 2;

    // Sequence Y of size 2
    int Y[] = { 4, 2 };
    checkforX(Y, N);
    return 0;
}
```

## C

```
// C program to implement above approach
#include <stdio.h>

// Euclidean theorem to calculate gcd
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check if it is possible
// to generate lost sequence X
void checkforX(int Y[], int N)
{
    int cur_gcd = Y[0];
    int Xexist = 1;

    // Loop to check existence of X
    for (int i = 1; i < N; i++) {
        cur_gcd = gcd(cur_gcd, Y[i]);
        if (cur_gcd != Y[i]) {
            Xexist = 0;
            break;
        }
    }

    // Sequence X is found
    if (Xexist) {

        // Loop to generate X
        for (int i = 0; i < N; i++)
            printf("%d ", Y[i]);
    }

    // Sequence X can't be generated
    else {
        printf("-1");
    }
}

// Driver code
int main()
{
    int N = 2;

    // Sequence Y of size 2
    int Y[] = { 4, 2 };
    checkforX(Y, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement above approach
import java.util.*;

class GFG{

// Euclidean theorem to find gcd
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check if it is possible
// to generate lost sequence X
static void checkforX(int Y[], int N)
{
    int cur_gcd = Y[0];
    boolean Xexist = true;

    // Loop to check existence of X
    for (int i = 1; i < N; i++) {
        cur_gcd = gcd(cur_gcd, Y[i]);
        if (cur_gcd != Y[i]) {
            Xexist = false;
            break;
        }
    }

    // Sequence X is found
    if (Xexist) {

        // Loop to generate X
        for (int i = 0; i < N; i++)
            System.out.print(Y[i] +" ");
    }

    // Sequence X can't be generated
    else {
        System.out.print(-1 +"\n");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 2;

    // Sequence Y of size 2
    int Y[] = { 4, 2 };
    checkforX(Y, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Euclidean theorem to find gcd
def gcd(a, b):
    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to check if it is possible
# to generate lost sequence X
def checkforX(Y, N):
    cur_gcd = Y[0]
    Xexist = True

    # Loop to check existence of X
    for i in range(1, N):
        cur_gcd = gcd(cur_gcd, Y[i])
        if (cur_gcd != Y[i]):
            Xexist = False
            break

    # Sequence X is found
    if (Xexist):

        # Loop to generate X
        for i in range(N):
            print(Y[i], end=' ')

    # Sequence X can't be generated
    else:
        print(-1)

# Driver code
N = 2

# Sequence Y of size 2
Y = [4, 2]
checkforX(Y, N)

# This code is contributed by gfgking
```

## C#

```
// C# Program to implement above approach
using System;
class GFG
{

// Euclidean theorem to find gcd
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check if it is possible
// to generate lost sequence X
static void checkforX(int []Y, int N)
{
    int cur_gcd = Y[0];
    bool Xexist = true;

    // Loop to check existence of X
    for (int i = 1; i < N; i++) {
        cur_gcd = gcd(cur_gcd, Y[i]);
        if (cur_gcd != Y[i]) {
            Xexist = false;
            break;
        }
    }

    // Sequence X is found
    if (Xexist) {

        // Loop to generate X
        for (int i = 0; i < N; i++)
            Console.Write(Y[i] + " ");
    }

    // Sequence X can't be generated
    else {
        Console.Write(-1);
    }
}

// Driver code
public static void Main()
{
    int N = 2;

    // Sequence Y of size 2
    int []Y = { 4, 2 };
    checkforX(Y, N);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach

        // Euclidean theorem to find gcd
        function gcd(a, b) {
            if (b == 0)
                return a;
            return gcd(b, a % b);
        }

        // Function to check if it is possible
        // to generate lost sequence X
        function checkforX(Y, N) {
            let cur_gcd = Y[0];
            let Xexist = true;

            // Loop to check existence of X
            for (let i = 1; i < N; i++) {
                cur_gcd = gcd(cur_gcd, Y[i]);
                if (cur_gcd != Y[i]) {
                    Xexist = false;
                    break;
                }
            }

            // Sequence X is found
            if (Xexist) {

                // Loop to generate X
                for (let i = 0; i < N; i++)
                    document.write(Y[i] + ' ');
            }

            // Sequence X can't be generated
            else {
                document.write(-1 + '<br>');
            }
        }

        // Driver code
        let N = 2;

        // Sequence Y of size 2
        let Y = [4, 2];
        checkforX(Y, N);

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4 2 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)