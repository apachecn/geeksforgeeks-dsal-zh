# 打印前 N 个马赛克号

> 原文:[https://www.geeksforgeeks.org/print-first-n-mosaic-numbers/](https://www.geeksforgeeks.org/print-first-n-mosaic-numbers/)

给定一个整数 N，任务是打印前 N 个马赛克数字。马赛克数可以表示如下:

> 如果 N = p<sub>1</sub>T2【aT4<sup>1</sup>T7【p<sub>2</sub>T10【aT12<sup>2</sup>T15】…p<sub>k</sub>T18】aT20<sup>k</sup>T23】在 N 的素因式分解中其中 p
> 1，p <sub>2</sub> … p
> 那么第 N <sup>个</sup>镶嵌数等于((p<sub>1</sub>)*(a<sub>1</sub>)*((p<sub>2</sub>)*(a<sub>2</sub>)*……*((p<sub>k</sub>)*(a<sub>k</sub>)

**示例:**

> **输入:**N = 10
> T3】输出:1 2 3 4 5 6 7 6 10
> 对于 N = 4，N = 2 <sup>2</sup> 。
> 4 <sup>第</sup>镶嵌编号= 2*2 = 4
> 对于 N=8，N = 2<sup>3</sup>T14】8<sup>第</sup>镶嵌编号= 2*3 = 6
> 同样打印前 N 个镶嵌编号
> 
> **输入:**N = 5
> T3】输出: 1 2 3 4 5

**逼近** :
运行一个从 1 到 N 的循环，对于每一个 I，我们必须通过将数除以因子直到因子除以数来找到所有的质因数以及数中因子的幂。然后，第 I 个马赛克数将是已发现的质因数及其幂的乘积。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth mosaic number
int mosaic(int n)
{
    int i, ans = 1;

    // Iterate from 2 to the number
    for (i = 2; i <= n; i++) {

        // If i is the factor of n
        if (n % i == 0 && n > 0) {
            int count = 0;

            // Find the count where i^count
            // is a factor of n
            while (n % i == 0) {

                // Divide the number by i
                n /= i;

                // Increase the count
                count++;
            }

            // Multiply the answer with
            // count and i
            ans *= count * i;
        }
    }

    // Return the answer
    return ans;
}

// Function to print first N Mosaic numbers
void nMosaicNumbers(int n)
{
    for (int i = 1; i <= n; i++)
        cout << mosaic(i) << " ";
}

// Driver code
int main()
{
    int n = 10;
    nMosaicNumbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the nth mosaic number
    static int mosaic(int n)
    {
        int i, ans = 1;

        // Iterate from 2 to the number
        for (i = 2; i <= n; i++)
        {

            // If i is the factor of n
            if (n % i == 0 && n > 0)
            {
                int count = 0;

                // Find the count where i^count
                // is a factor of n
                while (n % i == 0)
                {

                    // Divide the number by i
                    n /= i;

                    // Increase the count
                    count++;
                }

                // Multiply the answer with
                // count and i
                ans *= count * i;
            }
        }

        // Return the answer
        return ans;
    }

    // Function to print first N Mosaic numbers
    static void nMosaicNumbers(int n)
    {
        for (int i = 1; i <= n; i++)
            System.out.print( mosaic(i)+ " ");
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 10;
        nMosaicNumbers(n);
    }
}

// This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the nth mosaic number
    static int mosaic(int n)
    {
        int i, ans = 1;

        // Iterate from 2 to the number
        for (i = 2; i <= n; i++)
        {

            // If i is the factor of n
            if (n % i == 0 && n > 0)
            {
                int count = 0;

                // Find the count where i^count
                // is a factor of n
                while (n % i == 0)
                {

                    // Divide the number by i
                    n /= i;

                    // Increase the count
                    count++;
                }

                // Multiply the answer with
                // count and i
                ans *= count * i;
            }
        }

        // Return the answer
        return ans;
    }

    // Function to print first N Mosaic numbers
    static void nMosaicNumbers(int n)
    {
        for (int i = 1; i <= n; i++)
            Console.Write( mosaic(i)+ " ");
    }

    // Driver code
    public static void Main()
    {

        int n = 10;
        nMosaicNumbers(n);
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python implementation of the approach

# Function to return the nth mosaic number
def mosaic( n):
    ans = 1

    # Iterate from 2 to the number
    for i in range(2,n+1):

        # If i is the factor of n
        if (n % i == 0 and n > 0):
            count = 0;

            # Find the count where i^count
            # is a factor of n
            while (n % i == 0):

                # Divide the number by i
                n = n// i

                # Increase the count
                count+=1;

            # Multiply the answer with
            # count and i
            ans *= count * i;

    # Return the answer
    return ans;

# Function to print first N Mosaic numbers
def nMosaicNumbers(n):
    for i in range(1,n+1):
        print mosaic(i),

# Driver code
n = 10;
nMosaicNumbers(n);

# This code is contributed by CrazyPro
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the nth mosaic number
function mosaic(n)
{
    var i, ans = 1;

    // Iterate from 2 to the number
    for (i = 2; i <= n; i++) {

        // If i is the factor of n
        if (n % i == 0 && n > 0) {
            var count = 0;

            // Find the count where i^count
            // is a factor of n
            while (n % i == 0) {

                // Divide the number by i
                n /= i;

                // Increase the count
                count++;
            }

            // Multiply the answer with
            // count and i
            ans *= count * i;
        }
    }

    // Return the answer
    return ans;
}

// Function to print first N Mosaic numbers
function nMosaicNumbers(n)
{
    for (var i = 1; i <= n; i++)
        document.write( mosaic(i) + " ");
}

// Driver code
var n = 10;
nMosaicNumbers(n);

</script>
```

**Output:** 

```
1 2 3 4 5 6 7 6 6 10
```