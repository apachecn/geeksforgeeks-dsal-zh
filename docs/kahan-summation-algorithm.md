# 卡汉求和算法

> 原文:[https://www.geeksforgeeks.org/kahan-summation-algorithm/](https://www.geeksforgeeks.org/kahan-summation-algorithm/)

**先决条件:** [舍入误差](https://www.geeksforgeeks.org/rounding-off-errors-java/)、[浮点表示介绍](https://www.geeksforgeeks.org/introduction-of-floating-point-representation/)
卡涵求和算法，也称为带进位算法的补偿求和和求和，用于**最小化通过添加有限精度浮点数序列获得的总结果中的显著性损失**。这是通过保持一个单独的运行补偿(一个积累小误差的变量)来实现的。

**失去意义的原因:**

*   正如我们在 Java 语言中所知道的，我们有两种原始浮点类型， **float** 和 **double** ，其中**单精度 32 位**和**双精度 64 位**格式值和操作由 IEEE 754 指定。也就是说，它们以如下形式表示:

```
SIGN FRACTION * 2EXP
```

*   例如 0.15625 = (0.00101) <sub>2</sub> ，浮点格式表示为:1.01 * 2 <sup>-3</sup> 。然而，并不是所有的分数都可以精确地表示为 2 的幂的分数。例如，0.1 =(0.000110011001100110011001100110011001100110011001100110011001……)<sub>2</sub>因此不能存储在浮点变量中。
*   因此，浮点错误/显著性损失是指当一个数字不能按其在 IEEE 浮点表示中的原样存储并且重复对其执行一些算术运算时。这会导致一些意外的值，预期值和获得值之间的差异就是误差。

下面是一个模拟重要性错误的实现:

## C++

```
// C++ program to illustrate the
// floating-point error
#include<bits/stdc++.h>
using namespace std;

double floatError(double no)
{
    double sum = 0.0;
    for(int i = 0; i < 10; i++)
    {
        sum = sum + no;
    }
    return sum;
}

// Driver code
int main()
{
    cout << setprecision(16);
    cout << floatError(0.1);
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate the
// floating-point error

public class GFG {

    public static double floatError(double no)
    {
        double sum = 0.0;
        for (int i = 0; i < 10; i++) {
            sum = sum + no;
        }
        return sum;
    }

    public static void main(String[] args)
    {

        System.out.println(floatError(0.1));
    }
}
```

## 蟒蛇 3

```
# Python3 program to illustrate the
# floating-point error

def floatError(no):
    sum = 0.0
    for i in range(10):
        sum = sum + no
    return sum

if __name__ == '__main__':
    print(floatError(0.1))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program to illustrate the
// floating-point error

function floatError(no)
{
    let sum = 0.0;
        for (let i = 0; i < 10; i++) {
            sum = sum + no;
        }
        return sum;
}

document.write(floatError(0.1));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
0.9999999999999999
```