# 使用对数函数

找出两个数的差

> 原文:[https://www . geesforgeks . org/find-两个数差-使用-log-function/](https://www.geeksforgeeks.org/find-the-difference-between-two-numbers-using-log-function/)

给定两个整数 **a** 和 **b** ，任务是使用[日志功能](https://www.geeksforgeeks.org/log-function-cpp/)找到 **a** 和 **b** 的减法，即 **(a-b)** 。

> **注意:**我们不能使用**–**运算符。

**示例:**

> **输入:** a = 4，b = 81
> **输出:** -77
> 
> **输入:** a = -3，b = 16
> **输出:** -19
> 
> **输入:** a = -3，b =-13
> T3】输出: 10

**方法:**要编写此问题的解决方案，请使用日志的以下三个属性

> *   对数(a/b)=对数(a)–对数(b)
> *   log <sub>a</sub> (a)= 1
> *   原木(a <sup>b</sup> )= b 原木(a)

结合这三个属性，写。

> log<sub>e</sub>(e<sup>a</sup>/e<sup>b</sup>)
> =>log<sub>e</sub>(e<sup>a</sup>)–log<sub>e</sub>(e<sup>b</sup>){使用属性 1 }
> =>log<sub>e</sub>(e)–blog<sub>e</sub>(e){使用属性 2 }>

> **注:**T2 e 为**欧拉数**即 **2.71828**

按照以下步骤解决问题:

*   **a-b** 的减法将**对数(exp(a) / exp(b))** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the subtraction
// of two number a and b i.e, (a-b)
int subtract(int a, int b)
{
    return log(exp(a) / exp(b));
}

// Driver Code
int main()
{
    int a = -15;
    int b = 7;

    cout << subtract(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the subtraction
    // of two number a and b i.e, (a-b)
    static int subtract(int a, int b) {
        return (int) Math.log(Math.exp(a) / Math.exp(b));
    }

    // Driver Code
    public static void main(String[] args) {
        int a = -15;
        int b = 7;

        System.out.print(subtract(a, b));

    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the subtraction
# of two number a and b i.e, (a-b)
def subtract(a, b) :
    return math.log(math.exp(a) / math.exp(b));

# Driver Code
if __name__ == "__main__" :

    a = -15;
    b = 7;

    print(subtract(a, b));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to find the subtraction
    // of two number a and b i.e, (a-b)
    static int subtract(int a, int b)
    {
        return (int)Math.Log(Math.Exp(a) / Math.Exp(b));
    }

    // Driver Code
    public static void Main(string[] args) {
        int a = -15;
        int b = 7;

        Console.Write(subtract(a, b));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the subtraction
        // of two number a and b i.e, (a-b)
        function subtract(a, b) {
            return Math.log(Math.exp(a) / Math.exp(b));
        }

        // Driver Code

        let a = -15;
        let b = 7;

        document.write(subtract(a, b));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
-22
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)