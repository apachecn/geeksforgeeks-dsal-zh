# 检查给定号码是否断电

> 原文:[https://www . geeksforgeeks . org/check-给定号码是否电源隔离/](https://www.geeksforgeeks.org/check-whether-a-given-number-is-power-isolated-or-not/)

给定一个整数 N，用质因数 n1 <sup>p1</sup> * n2 <sup>p2</sup> ……任务是检查整数 N 是否电源隔离。

> 如果 **n1 * p1 * n2 * p2 …..= N** 。

**示例**:

```
Input: N = 12
Output: Power-isolated Integer.

Input: N = 18
Output: Not a power-isolated integer.
```

**方法:**对于一个被幂隔离的整数，它的素因子和它们的幂的乘积等于整数本身。因此，为了计算相同的，你必须找到给定整数的所有质因数以及它们各自的幂。之后，计算它们的乘积，检查乘积是否等于整数。
**算法:**

> *   Find prime factors with their factors and store them in key-value pairs.
> *   Then calculate the product of all factors and their forces.
> *   If the product is equal to an integer, print true or print false.

下面是上述算法的实现:

## C++

```
// C++ program to find whether a number
// is power-isolated or not
#include <bits/stdc++.h>
using namespace std;

void checkIfPowerIsolated(int num)
{
    int input = num;
    int count = 0;
    int factor[num + 1]={0};

    // for 2 as prime factor
    if(num % 2 == 0)
    {
        while(num % 2 == 0)
        {
            ++count;
            num/=2;
        }
        factor[2] = count;
    }

    // for odd prime factor
    for (int i = 3; i*i <= num; i += 2)
    {
        count = 0;
        while(num % i == 0)
        {
            ++count;
            num /= i;
        }
        if(count > 0)
            factor[i] = count;
    }

    if(num > 1)
        factor[num] = 1;

    // calculate product of powers and prime factors
    int product = 1;
    for(int i = 0; i < num + 1; i++)
    {
        if(factor[i] > 0)
            product = product * factor[i] * i;
    }

    // check result for power-isolation
    if (product == input)
        cout << "Power-isolated Integer\n";
    else
        cout << "Not a Power-isolated Integer\n";
}

// Driver code
int main()
{
    checkIfPowerIsolated(12);
    checkIfPowerIsolated(18);
    checkIfPowerIsolated(35);
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find whether a number
// is power-isolated or not
class GFG
{

static void checkIfPowerIsolated(int num)
{
    int input = num;
    int count = 0;
    int[] factor= new int[num+1];

    // for 2 as prime factor
    if(num % 2 == 0)
    {
        while(num % 2 == 0)
        {
            ++count;
            num/=2;
        }
        factor[2] = count;
    }

    // for odd prime factor
    for (int i = 3; i*i <= num; i += 2)
    {
        count = 0;
        while(num % i == 0)
        {
            ++count;
            num /= i;
        }
        if(count > 0)
            factor[i] = count;
    }

    if(num > 1)
        factor[num] = 1;

    // calculate product of powers and prime factors
    int product = 1;
    for(int i = 0; i < num + 1; i++)
    {
        if(factor[i] > 0)
            product = product * factor[i] * i;
    }

    // check result for power-isolation
    if (product == input)
        System.out.print("Power-isolated Integer\n");
    else
        System.out.print("Not a Power-isolated Integer\n");
}

// Driver code
public static void main(String[] args)
{
    checkIfPowerIsolated(12);
    checkIfPowerIsolated(18);
    checkIfPowerIsolated(35);
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 program to find whether a number
# is power-isolated or not

def checkIfPowerIsolated(num):

    input1 = num;
    count = 0;
    factor = [0] * (num + 1);

    # for 2 as prime factor
    if(num % 2 == 0):
        while(num % 2 == 0):
            count += 1;
            num //= 2;
        factor[2] = count;

    # for odd prime factor
    i = 3;
    while(i * i <= num):
        count = 0;
        while(num % i == 0):
            count += 1;
            num //= i;
        if(count > 0):
            factor[i] = count;
        i += 2;

    if(num > 1):
        factor[num] = 1;

    # calculate product of powers and prime factors
    product = 1;
    for i in range(0, len(factor)):
        if(factor[i] > 0):
            product = product * factor[i] * i;

    # check result for power-isolation
    if (product == input1):
        print("Power-isolated Integer");
    else:
        print("Not a Power-isolated Integer");

# Driver code
checkIfPowerIsolated(12);
checkIfPowerIsolated(18);
checkIfPowerIsolated(35);

# This code is contributed by mits
```

## C#

```
// C# program to find whether a number
// is power-isolated or not
using System;

class GFG
{
static void checkIfPowerIsolated(int num)
{
    int input = num;
    int count = 0;
    int[] factor= new int[num+1];

    // for 2 as prime factor
    if(num % 2 == 0)
    {
        while(num % 2 == 0)
        {
            ++count;
            num/=2;
        }
        factor[2] = count;
    }

    // for odd prime factor
    for (int i = 3; i*i <= num; i += 2)
    {
        count = 0;
        while(num % i == 0)
        {
            ++count;
            num /= i;
        }
        if(count > 0)
            factor[i] = count;
    }

    if(num > 1)
        factor[num] = 1;

    // calculate product of powers and prime factors
    int product = 1;
    for(int i = 0; i < num + 1; i++)
    {
        if(factor[i] > 0)
            product = product * factor[i] * i;
    }

    // check result for power-isolation
    if (product == input)
        Console.Write("Power-isolated Integer\n");
    else
        Console.Write("Not a Power-isolated Integer\n");
}

// Driver code
static void Main()
{
    checkIfPowerIsolated(12);
    checkIfPowerIsolated(18);
    checkIfPowerIsolated(35);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find whether a number
// is power-isolated or not

function checkIfPowerIsolated($num)
{
        $input = $num;
        $count = 0;
        $factor= array();

        // for 2 as prime factor
        if($num%2==0)
        {
            while($num%2==0)
            {
                ++$count;
                $num/=2;
            }   
            $factor[2] = $count;
        }

        // for odd prime factor
        for ($i=3; $i*$i <= $num; $i+=2)
        {
            $count = 0;
            while($num%$i==0)
            {   
                ++$count;
                $num /= $i;
            }
            if($count)
            $factor[$i] = $count;
        }

        if($num>1)
           $factor[$num] = 1;
        // calculate product of powers and prime factors 
        $product  = 1;
        foreach ($factor as $primefactor => $power) {
            $product = $product * $primefactor * $power;
        }

        // check result for power-isolation
        if ($product ==  $input)
            print_r("Power-isolated Integer\n");
        else
            print_r("Not a Power-isolated Integer\n");
}

// driver code
checkIfPowerIsolated(12);
checkIfPowerIsolated(18);
checkIfPowerIsolated(35);

?>
```

## java 描述语言

```
<script>

// Javascript program to find whether a number
// is power-isolated or not

function checkIfPowerIsolated(num)
{
    let input = num;
    let count = 0;
    let factor = new Array(0);

    // for 2 as prime factor
    if(num % 2 == 0)
    {
        while(num % 2 == 0)
        {
            ++count;
            num/=2;
        }
        factor[2] = count;
    }

    // for odd prime factor
    for (let i = 3; i*i <= num; i += 2)
    {
        count = 0;
        while(num % i == 0)
        {
            ++count;
            num /= i;
        }
        if(count > 0)
            factor[i] = count;
    }

    if(num > 1)
        factor[num] = 1;

    // calculate product of powers and prime factors
    let product = 1;
    for(let i = 0; i < num + 1; i++)
    {
        if(factor[i] > 0)
            product = product * factor[i] * i;
    }

    // check result for power-isolation
    if (product == input)
        document.write("Power-isolated Integer" + "<br>");
    else
        document.write("Not a Power-isolated Integer" + "<br>");
}

// Driver code

    checkIfPowerIsolated(12);
    checkIfPowerIsolated(18);
    checkIfPowerIsolated(35);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Power-isolated Integer
Not a Power-isolated Integer
Power-isolated Integer
```

***时间复杂度:** O(num)*

***辅助空间:** O(num)*