# 第 N 个智能号码

> 原文:[https://www.geeksforgeeks.org/nth-smart-number/](https://www.geeksforgeeks.org/nth-smart-number/)

给定一个数字 n，找到第 n 个智能数字(1<=n<=1000)。智能数是一个至少有三个不同质因数的数。我们给出了一个最大结果值的上限

例如，30 是第一个智能数字，因为它有 2、3、5 个不同的质因数。42 是第二个聪明的数字，因为它有 2，3，7 个不同的质因数。
**例:**

```
Input : n = 1
Output: 30
// three distinct prime factors 2, 3, 5

Input : n = 50
Output: 273
// three distinct prime factors 3, 7, 13

Input : n = 1000
Output: 2664
// three distinct prime factors 2, 3, 37

```

这个想法是基于厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。我们使用数组来使用数组质数[]来跟踪质数。我们还使用相同的数组来记录到目前为止看到的质因数的计数。每当计数达到 3，我们就把数字加到结果上。

*   取一个数组 primes[]并用 0 初始化它。
*   现在我们知道第一个质数是 i = 2，所以标记质数[2] = 1，即；素数[i] = 1 表示‘I’是素数。
*   现在遍历 primes[]数组，并通过条件 primes[j] -= 1 标记所有 I 的倍数，其中 j 是 I 的倍数，并检查条件 primes[j]+3 = 0，因为每当 primes[j]变成-3 时，它表明以前它是三个不同的 prime 因子的倍数。如果条件**质数【j】+3 = 0**变为真，这意味着‘j’是一个智能数字，因此将其存储在数组结果[]中。
*   现在对数组结果[]进行排序，并返回结果[n-1]。

以下是上述想法的实现。

## C++

```
// C++ implementation to find n'th smart number
#include<bits/stdc++.h>
using namespace std;

// Limit on result
const int MAX = 3000;

// Function to calculate n'th smart number
int smartNumber(int n)
{
    // Initialize all numbers as not prime
    int primes[MAX] = {0};

    // iterate to mark all primes and smart number
    vector<int> result;

    // Traverse all numbers till maximum limit
    for (int i=2; i<MAX; i++)
    {
        // 'i' is maked as prime number because
        // it is not multiple of any other prime
        if (primes[i] == 0)
        {
            primes[i] = 1;

            // mark all multiples of 'i' as non prime
            for (int j=i*2; j<MAX; j=j+i)
            {
                primes[j] -= 1;

                // If i is the third prime factor of j
                // then add it to result as it has at
                // least three prime factors.
                if ( (primes[j] + 3) == 0)
                    result.push_back(j);
            }
        }
    }

    // Sort all smart numbers
    sort(result.begin(), result.end());

    // return n'th smart number
    return result[n-1];
}

// Driver program to run the case
int main()
{
    int n = 50;
    cout << smartNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find n'th smart number
import java.util.*;
import java.lang.*;

class GFG {

    // Limit on result
    static int MAX = 3000;

    // Function to calculate n'th smart number
    public static int smartNumber(int n)
    {

        // Initialize all numbers as not prime
        Integer[] primes = new Integer[MAX];
        Arrays.fill(primes, new Integer(0));

        // iterate to mark all primes and smart
        // number
        Vector<Integer> result = new Vector<>();

        // Traverse all numbers till maximum
        // limit
        for (int i = 2; i < MAX; i++)
        {

            // 'i' is maked as prime number
            // because it is not multiple of
            // any other prime
            if (primes[i] == 0)
            {
                primes[i] = 1;

                // mark all multiples of 'i' 
                // as non prime
                for (int j = i*2; j < MAX; j = j+i)
                {
                    primes[j] -= 1;

                    // If i is the third prime
                    // factor of j then add it
                    // to result as it has at
                    // least three prime factors.
                    if ( (primes[j] + 3) == 0)
                        result.add(j);
                }
            }
        }

        // Sort all smart numbers
        Collections.sort(result);

        // return n'th smart number
        return result.get(n-1);

    }

    // Driver program to run the case
    public static void main(String[] args)
    {
        int n = 50;
        System.out.println(smartNumber(n));

    }
}

// This code is contributed by Prasad Kshirsagar
```

## 蟒蛇 3

```
# Python3 implementation to find
# n'th smart number 

# Limit on result 
MAX = 3000; 

# Function to calculate n'th
# smart number 
def smartNumber(n): 

    # Initialize all numbers as not prime 
    primes = [0] * MAX; 

    # iterate to mark all primes 
    # and smart number 
    result = []; 

    # Traverse all numbers till maximum limit 
    for i in range(2, MAX): 

        # 'i' is maked as prime number because 
        # it is not multiple of any other prime 
        if (primes[i] == 0): 
            primes[i] = 1; 

            # mark all multiples of 'i' as non prime
            j = i * 2;
            while (j < MAX): 
                primes[j] -= 1; 

                # If i is the third prime factor of j 
                # then add it to result as it has at 
                # least three prime factors. 
                if ( (primes[j] + 3) == 0): 
                    result.append(j);
                j = j + i;

    # Sort all smart numbers 
    result.sort(); 

    # return n'th smart number 
    return result[n - 1]; 

# Driver Code
n = 50; 
print(smartNumber(n)); 

# This code is contributed by mits 
```

## C#

```
// C# implementation to find n'th smart number
using System.Collections.Generic;

class GFG {

    // Limit on result
    static int MAX = 3000;

    // Function to calculate n'th smart number
    public static int smartNumber(int n)
    {

        // Initialize all numbers as not prime
        int[] primes = new int[MAX];

        // iterate to mark all primes and smart
        // number
        List<int> result = new List<int>();

        // Traverse all numbers till maximum
        // limit
        for (int i = 2; i < MAX; i++)
        {

            // 'i' is maked as prime number
            // because it is not multiple of
            // any other prime
            if (primes[i] == 0)
            {
                primes[i] = 1;

                // mark all multiples of 'i' 
                // as non prime
                for (int j = i*2; j < MAX; j = j+i)
                {
                    primes[j] -= 1;

                    // If i is the third prime
                    // factor of j then add it
                    // to result as it has at
                    // least three prime factors.
                    if ( (primes[j] + 3) == 0)
                        result.Add(j);
                }
            }
        }

        // Sort all smart numbers
        result.Sort();

        // return n'th smart number
        return result[n-1];

    }

    // Driver program to run the case
    public static void Main()
    {
        int n = 50;
        System.Console.WriteLine(smartNumber(n));

    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find n'th smart number 

// Limit on result 
$MAX = 3000; 

// Function to calculate n'th smart number 
function smartNumber($n) 
{
    global $MAX;
    // Initialize all numbers as not prime 
    $primes=array_fill(0,$MAX,0); 

    // iterate to mark all primes and smart number 
    $result=array(); 

    // Traverse all numbers till maximum limit 
    for ($i=2; $i<$MAX; $i++) 
    { 
        // 'i' is maked as prime number because 
        // it is not multiple of any other prime 
        if ($primes[$i] == 0) 
        { 
            $primes[$i] = 1; 

            // mark all multiples of 'i' as non prime 
            for ($j=$i*2; $j<$MAX; $j=$j+$i) 
            { 
                $primes[$j] -= 1; 

                // If i is the third prime factor of j 
                // then add it to result as it has at 
                // least three prime factors. 
                if ( ($primes[$j] + 3) == 0) 
                    array_push($result,$j); 
            } 
        } 
    } 

    // Sort all smart numbers 
    sort($result); 

    // return n'th smart number 
    return $result[$n-1]; 
} 

// Driver program to run the case 

    $n = 50; 
    echo smartNumber($n); 

// This code is contributed by mits 
?>
```

**输出:**

```
273

```

本文由 **[沙沙克·米什拉(古卢)](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。