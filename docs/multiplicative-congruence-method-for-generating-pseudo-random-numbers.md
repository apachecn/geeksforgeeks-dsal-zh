# 生成伪随机数的乘法同余法

> 原文:[https://www . geeksforgeeks . org/乘法同余生成伪随机数的方法/](https://www.geeksforgeeks.org/multiplicative-congruence-method-for-generating-pseudo-random-numbers/)

**乘法同余法** (Lehmer 法)是一种产生特定范围内伪随机数的线性同余发生器。这种方法可以定义为:

> ![\[X_{i + 1} = aX_{i} \hspace{0.2cm} mod \hspace{0.2cm} m\]   ](img/8c3c41f9b95e8b92c5f303fc8d99d946.png "Rendered by QuickLaTeX.com")
> 
> 其中，
> **X** ，伪随机数序列
> **m** ( > 0)，模数
> **a** (0，m)，乘数
> **X<sub>0</sub>**<sub>【0，m)，序列初始值–称为**种子**</sub>
> 
> 应适当选择 m、a 和 X <sub>0</sub> ，以获得几乎等于 m 的周期。

**进场:**

*   选择种子值(X <sub>0</sub> )、模量参数(m)和乘数项(a)。
*   初始化需要生成的随机数数量(比如，一个整数变量*nofrandomnums*)。
*   定义存储以保持生成的随机数(这里考虑的是*向量*的大小*无随机数*。
*   用种子值初始化向量的第 0 <sup>个</sup>索引。
*   对于其余的索引，遵循乘法同余法来生成随机数。

> randomNums[i] = （randomNums[i – 1] * a） % m

最后，返回随机数。
下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate random numbers
void multiplicativeCongruentialMethod(
    int Xo, int m, int a,
    vector<int>& randomNums,
    int noOfRandomNums)
{

    // Initialize the seed state
    randomNums[0] = Xo;

    // Traverse to generate required
    // numbers of random numbers
    for (int i = 1; i < noOfRandomNums; i++) {

        // Follow the multiplicative
        // congruential method
        randomNums[i]
            = (randomNums[i - 1] * a) % m;
    }
}

// Driver Code
int main()
{
    int Xo = 3; // seed value
    int m = 15; // modulus parameter
    int a = 7; // multiplier term

    // Number of Random numbers
    // to be generated
    int noOfRandomNums = 10;

    // To store random numbers
    vector<int> randomNums(noOfRandomNums);

    // Function Call
    multiplicativeCongruentialMethod(
        Xo, m, a, randomNums,
        noOfRandomNums);

    // Print the generated random numbers
    for (int i = 0; i < noOfRandomNums; i++) {
        cout << randomNums[i] << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to generate random numbers
static void multiplicativeCongruentialMethod(
    int Xo, int m, int a,
    int[] randomNums,
    int noOfRandomNums)
{

    // Initialize the seed state
    randomNums[0] = Xo;

    // Traverse to generate required
    // numbers of random numbers
    for(int i = 1; i < noOfRandomNums; i++)
    {

        // Follow the multiplicative
        // congruential method
        randomNums[i] = (randomNums[i - 1] * a) % m;
    }
}

// Driver code
public static void main(String[] args)
{

    // Seed value
    int Xo = 3;

    // Modulus parameter
    int m = 15;

    // Multiplier term
    int a = 7;

    // Number of Random numbers
    // to be generated
    int noOfRandomNums = 10;

    // To store random numbers
    int[] randomNums = new int[noOfRandomNums];

    // Function Call
    multiplicativeCongruentialMethod(Xo, m, a,
                                     randomNums,
                                     noOfRandomNums);

    // Print the generated random numbers
    for(int i = 0; i < noOfRandomNums; i++)
    {
        System.out.print(randomNums[i] + " ");
    }
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to generate random numbers
def multiplicativeCongruentialMethod(Xo, m, a,
                                     randomNums,
                                     noOfRandomNums):

    # Initialize the seed state
    randomNums[0] = Xo

    # Traverse to generate required
    # numbers of random numbers
    for i in range(1, noOfRandomNums):

        # Follow the linear congruential method
        randomNums[i] = (randomNums[i - 1] * a) % m

# Driver Code
if __name__ == '__main__':

    # Seed value
    Xo = 3

    # Modulus parameter
    m = 15

    # Multiplier term
    a = 7

    # Number of Random numbers
    # to be generated
    noOfRandomNums = 10

    # To store random numbers
    randomNums = [0] * (noOfRandomNums)

    # Function Call
    multiplicativeCongruentialMethod(Xo, m, a,
                                     randomNums,
                                     noOfRandomNums)

    # Print the generated random numbers
    for i in randomNums:
        print(i, end = " ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to generate random numbers
static void multiplicativeCongruentialMethod(
    int Xo, int m, int a,
    int[] randomNums,
    int noOfRandomNums)
{

    // Initialize the seed state
    randomNums[0] = Xo;

    // Traverse to generate required
    // numbers of random numbers
    for(int i = 1; i < noOfRandomNums; i++)
    {

        // Follow the multiplicative
        // congruential method
        randomNums[i] = (randomNums[i - 1] * a) % m;
    }
}

// Driver code
public static void Main(String[] args)
{

    // Seed value
    int Xo = 3;

    // Modulus parameter
    int m = 15;

    // Multiplier term
    int a = 7;

    // Number of Random numbers
    // to be generated
    int noOfRandomNums = 10;

    // To store random numbers
    int[] randomNums = new int[noOfRandomNums];

    // Function call
    multiplicativeCongruentialMethod(Xo, m, a,
                                     randomNums,
                                     noOfRandomNums);

    // Print the generated random numbers
    for(int i = 0; i < noOfRandomNums; i++)
    {
        Console.Write(randomNums[i] + " ");
    }
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to generate random numbers
function multiplicativeCongruentialMethod(
    Xo, m, a,
    randomNums, noOfRandomNums)
{

    // Initialize the seed state
    randomNums[0] = Xo;

    // Traverse to generate required
    // numbers of random numbers
    for(let i = 1; i < noOfRandomNums; i++)
    {

        // Follow the multiplicative
        // congruential method
        randomNums[i] = (randomNums[i - 1] * a) % m;
    }
}

    // Driver Code

    // Seed value
    let Xo = 3;

    // Modulus parameter
    let m = 15;

    // Multiplier term
    let a = 7;

    // Number of Random numbers
    // to be generated
    let noOfRandomNums = 10;

    // To store random numbers
    let randomNums = new Array(noOfRandomNums).fill(0);

    // Function Call
    multiplicativeCongruentialMethod(Xo, m, a,
                                     randomNums,
                                     noOfRandomNums);

    // Prlet the generated random numbers
    for(let i = 0; i < noOfRandomNums; i++)
    {
        document.write(randomNums[i] + " ");
    }

</script>
```

**Output:** 

```
3 6 12 9 3 6 12 9 3 6
```

**时间复杂度:** O(N)，其中 N 是我们需要生成的随机数总数。
**辅助空间** : O(1)
伪的字面意思是**假**。这些随机数被称为伪随机数，因为使用了一些已知的算术过程来生成。即使生成的序列形成一个模式，因此 ***生成的数字似乎是随机的，但可能不是真正随机的*** 。