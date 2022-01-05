# 检查给定的硬币是否可以用来支付 S 值

> 原文:[https://www . geesforgeks . org/check-if-given-coins-can-to-pay-a-value-of-s/](https://www.geeksforgeeks.org/check-if-given-coins-can-be-used-to-pay-a-value-of-s/)

给定价值为 **A** 的硬币 **N** 和 **B** 的硬币 **M** ，任务是检查给定的硬币是否可以用来支付价值为 **S** 的硬币。

**示例:**

> **输入:** A = 1，B = 2，N = 3，S = 4，M = 1
> **输出:** YES
> **解释:**
> 在这种情况下，如果选择 1 枚价值 3 的硬币和 2 枚价值 1 的硬币，那么有可能支付价值 S 的硬币
> 
> **输入:** A = 1，B = 2，N = 3，S = 6，M = 1
> **输出:**否
> 在这种情况下，不可能支付 S 的值

**进场:**
思路是用贪心进场。

*   继续从要求的总和 s 中减去 N 值的硬币。
*   在每一步，当减去价值为 N 的硬币时，检查剩余的总和是否是价值为 M 的硬币的倍数，并且我们有足够的价值为 M 的硬币来获得这个剩余的总和。
*   如果在任何步骤中，上述两个条件都满足，则返回“是”。

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// if it is possible to pay a value

#include <bits/stdc++.h>
using namespace std;

// Function to check if it
// is possible to pay a value
void knowPair(int a, int b,
        int n, int s, int m){

    int i = 0, rem = 0;
    int count_b = 0, flag = 0;

    // Loop to add the value of coin A
    while (i <= a) {
        rem = s - (n * i);
        count_b = rem / m;
        if (rem % m == 0 && count_b <= b){
            flag = 1;
        }
        i++;
    }

    // Condition to check if it is
    // possible to pay a value of S
    if (flag == 1) {
        cout << "YES" << endl;
    }else{
        cout << "NO" << endl;
    }
}

// Driver Code
int main()
{
    int A = 1;
    int B = 2;
    int n = 3;
    int S = 4;
    int m = 2;

    knowPair(A, B, n, S, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if it is possible to pay a value
class GFG{

// Function to check if it
// is possible to pay a value
static void knowPair(int a, int b,
        int n, int s, int m){

    int i = 0, rem = 0;
    int count_b = 0, flag = 0;

    // Loop to add the value of coin A
    while (i <= a) {
        rem = s - (n * i);
        count_b = rem / m;
        if (rem % m == 0 && count_b <= b){
            flag = 1;
        }
        i++;
    }

    // Condition to check if it is
    // possible to pay a value of S
    if (flag == 1) {
        System.out.print("YES" +"\n");
    }else{
        System.out.print("NO" +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A = 1;
    int B = 2;
    int n = 3;
    int S = 4;
    int m = 2;

    knowPair(A, B, n, S, m);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to check
# if it is possible to pay a value

# Function to check if it
# is possible to pay a value
def knowPair(a,b,n,s,m):
    i = 0
    rem = 0
    count_b = 0
    flag = 0

    # Loop to add the value of coin A
    while (i <= a):
        rem = s - (n * i)
        count_b = rem // m
        if (rem % m == 0 and count_b <= b):
            flag = 1
        i += 1

    # Condition to check if it is
    # possible to pay a value of S
    if (flag == 1):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':
    A = 1
    B = 2
    n = 3
    S = 4
    m = 2

    knowPair(A, B, n, S, m)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to check
// if it is possible to pay a value
using System;

class GFG{

// Function to check if it
// is possible to pay a value
static void knowPair(int a, int b,
        int n, int s, int m){

    int i = 0, rem = 0;
    int count_b = 0, flag = 0;

    // Loop to add the value of coin A
    while (i <= a) {
        rem = s - (n * i);
        count_b = rem / m;
        if (rem % m == 0 && count_b <= b){
            flag = 1;
        }
        i++;
    }

    // Condition to check if it is
    // possible to pay a value of S
    if (flag == 1) {
        Console.Write("YES" + "\n");
    }else{
        Console.Write("NO" + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int A = 1;
    int B = 2;
    int n = 3;
    int S = 4;
    int m = 2;

    knowPair(A, B, n, S, m);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation to check
// if it is possible to pay a value

// Function to check if it
// is possible to pay a value
function knowPair(a, b, n, s, m)
{
    var i = 0, rem = 0;
    var count_b = 0, flag = 0;

    // Loop to add the value of coin A
    while (i <= a)
    {
        rem = s - (n * i);
        count_b = parseInt(rem / m);

        if (rem % m == 0 && count_b <= b)
        {
            flag = 1;
        }
        i++;
    }

    // Condition to check if it is
    // possible to pay a value of S
    if (flag == 1)
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }
}

// Driver Code
var A = 1;
var B = 2;
var n = 3;
var S = 4;
var m = 2;

knowPair(A, B, n, S, m);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
YES
```