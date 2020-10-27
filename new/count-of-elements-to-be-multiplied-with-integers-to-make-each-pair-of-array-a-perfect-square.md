# 要与整数相乘的元素计数，以使每对 Array 成为一个完美的正方形

给定包含正整数的数组 **arr []** ，任务是找到要在数组上执行的最小操作数，以使数组的每个数成为超能力。
在每个操作中，我们可以将数组的任何元素乘以整数。

> 超级能力定义为数组中的一个数字，当乘以数组中除自身以外的任何其他数字时，就形成一个完美的平方。

**示例：**

> **输入：** arr [] = {2，2，2}
> **输出：** 0
> **说明：**
> 我们不需要 在数组上执行任何操作，因为选择任何元素（2）并将其与其他索引（2）中的任何元素相乘，我们得到一个完美的平方（4）。
> **输入：** arr [] = {2，4，6}
> **输出：** 2
> **说明：**
> 我们需要 执行以下两个操作：
> 首先，我们将索引 1 处的元素与整数 2 相乘。数组变为{2,8,6}。
> 其次，我们将索引 2 的元素与整数 3 相乘。数组变为{2，8，18}。
> 现在，所有要素都已成为超级大国。 数组中任何两个数字相乘得到一个完美的平方。
> 即 2 * 8 = 16、2 * 16 = 36 和 8 * 18 = 144。

**方法：**由于我们需要检查所有数字的素因数，所以我们的想法是首先预先计算所有数字的[唯一素因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)并将其存储在[哈希图中](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 。 然后，我们创建一个变量来存储[主因子](https://www.geeksforgeeks.org/prime-factor/)在数组的每个元素中出现的次数。 我们还需要观察到，我们需要找到转换数组的最小步骤数。 因此，我们计算向量中的奇数个数和偶数素数的个数，取最小者为准。 可以计算以下步骤来找到答案：

1.  我们首先需要计算 spf []数组。 这是存储所有元素的最小素因数的数组。
2.  然后，我们需要找到唯一的主要因素并将其存储在哈希图中。
3.  现在，遍历哈希图以找到一个数的唯一素数，然后遍历给定数组中的元素以计算素数的频率。
4.  现在，初始化两个变量，它们存储出现次数为偶数的质数的频率，另一个变量存储为奇数的质数的频率。
5.  现在，我们需要在最终变量中添加两个变量中的最小值，这是为该素数获得超能力的最小运算。
6.  对数组中的所有数字重复上述步骤。

下面是上述方法的实现：

## C ++

```

// C++ program to find the minimum 
// number of steps to modify the 
// array such that the product 
// of any two numbers in the 
// array is a perfect square 

#include <iostream> 
#include <unordered_map> 
#include <vector> 
using namespace std; 

// Function to find the smallest 
// prime factor of the elements 
void spf_array(int spf[]) 
{ 

    // Initializing the first element 
    // of the array 
    spf[1] = 1; 

    // Loop to add the remaining 
    // elements to the array 
    for (int i = 2; i < 1000; i++) 

        // Marking the smallest prime 
        // factor for every 
        // number to be itself 
        spf[i] = i; 

    // Separately marking spf for 
    // every even number as 2 
    for (int i = 4; i < 1000; i += 2) 
        spf[i] = 2; 

    for (int i = 3; i * i < 1000; i++) { 

        // Checking if i is prime 
        if (spf[i] == i) { 

            // Marking SPF for all the 
            // numbers divisible by i 
            for (int j = i * i; j < 1000; j += i) 

                // Marking spf[j] if it is not 
                // previously marked 
                if (spf[j] == j) 
                    spf[j] = i; 
        } 
    } 
} 

// Function to find the minimum 
// number of steps to modify the 
// array such that the product 
// of any two numbers in the 
// array is a perfect square 
int minimum_operation(int b[], int d, 
                    int spf[]) 
{ 

    // Map created to store 
    // the unique prime numbers 
    unordered_map<int, int> m; 
    int i = 0; 

    // Variable to store the 
    // minimum number of operations 
    int c = 0; 

    // Loop to store every 
    // unique prime number 
    for (i = 0; i < d; i++) { 
        int x = b[i]; 
        while (x != 1) { 
            x = x / spf[x]; 
            if (m[spf[x]] == 0) { 
                m[spf[x]] = 1; 
            } 
        } 
    } 

    // Erasing 1 as a key because 
    // it is not a prime number 
    m.erase(1); 

    // Iterating through the hash 
    for (auto x : m) { 

        // Two variables used for 
        // counting the frequency 
        // of prime is even or odd 
        int e = 0, o = 0; 

        // First prime number 
        int j = x.first; 

        // Iterating the number D 
        for (i = 0; i < d; i++) { 

            // check if prime is a 
            // factor of the element 
            // in the array 
            if (b[i] % j == 0) { 
                int h = 0; 
                int g = b[i]; 

                // Loop for calculating the 
                // frequency of the element 
                while (g != 0) { 
                    if (g % j != 0) { 
                        break; 
                    } 
                    g = g / j; 
                    h = h + 1; 
                } 

                // Check for frequency 
                // odd or even 
                if (h % 2 == 0) { 
                    e = e + 1; 
                } 
                else { 
                    o = o + 1; 
                } 
            } 
            else { 

                // If it is not a factor of the 
                // element, then it is automatically 
                // even 
                e = e + 1; 
            } 
        } 

        // Storing the minimum of two variable 
        // even or odd 
        c = c + min(o, e); 
    } 
    return c; 
} 

// Driver code 
int main() 
{ 
    int spf[1001]; 

    // Input array 
    int b[] = { 1, 4, 6 }; 

    // Creating shortest prime 
    // factorisation array 
    int d = sizeof(b) / sizeof(b[0]); 
    spf_array(spf); 

    cout << minimum_operation(b, d, spf) 
        << endl; 
} 

```

## 爪哇

```

// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the smallest
// prime factor of the elements
static void spf_array(int spf[])
{

    // Initializing the first element
    // of the array
    spf[1] = 1;

    // Loop to add the remaining
    // elements to the array
    for(int i = 2; i < 1000; i++)

        // Marking the smallest prime
        // factor for every
        // number to be itself
        spf[i] = i;

    // Separately marking spf for
    // every even number as 2
    for(int i = 4; i < 1000; i += 2)
        spf[i] = 2;

    for(int i = 3; i * i < 1000; i++) 
    {

        // Checking if i is prime
        if (spf[i] == i)
        {

            // Marking SPF for all the
            // numbers divisible by i
            for(int j = i * i; j < 1000; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to find the minimum
// number of steps to modify the
// array such that the product
// of any two numbers in the
// array is a perfect square
static int minimum_operation(int b[], int d,
                             int spf[])
{

    // Map created to store
    // the unique prime numbers
    Map<Integer, Integer> m=new HashMap<>();
    int i = 0;

    // Variable to store the
    // minimum number of operations
    int c = 0;

    // Loop to store every
    // unique prime number
    for(i = 0; i < d; i++)
    {
        int x = b[i];
        while (x != 1) 
        {
            x = x / spf[x];
            if (m.get(spf[x]) == null)
            {
                m.put(spf[x],1); 
            }
        }
    }

    // Erasing 1 as a key because
    // it is not a prime number
    m.remove(1);

    // Iterating through the hash
    for(Map.Entry<Integer,
                  Integer> x : m.entrySet()) 
    {

        // Two variables used for
        // counting the frequency
        // of prime is even or odd
        int e = 0, o = 0;

        // First prime number
        int j = x.getKey();

        // Iterating the number D
        for(i = 0; i < d; i++)
        {

            // Check if prime is a
            // factor of the element
            // in the array
            if (b[i] % j == 0)
            {
                int h = 0;
                int g = b[i];

                // Loop for calculating the
                // frequency of the element
                while (g != 0) 
                {
                    if (g % j != 0)
                    {
                        break;
                    }
                    g = g / j;
                    h = h + 1;
                }

                // Check for frequency
                // odd or even
                if (h % 2 == 0) 
                {
                    e = e + 1;
                }
                else
                {
                    o = o + 1;
                }
            }
            else
            {

                // If it is not a factor of the
                // element, then it is automatically
                // even
                e = e + 1;
            }
        }

        // Storing the minimum of two variable
        // even or odd
        c = c + Math.min(o, e);
    }
    return c;
}

// Driver Code
public static void main (String[] args)
{
    int[] spf = new int[1001];

    // Input array
    int b[] = { 1, 4, 6 };

    // Creating shortest prime
    // factorisation array
    int d = b.length;
    spf_array(spf);

    System.out.print(minimum_operation(b, d, spf));
}
}

// This code is contributed by offbeat

```

## C＃

```

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the smallest
// prime factor of the elements
static void spf_array(int []spf)
{
  // Initializing the first element
  // of the array
  spf[1] = 1;

  // Loop to add the remaining
  // elements to the array
  for(int i = 2; i < 1000; i++)

    // Marking the smallest prime
    // factor for every
    // number to be itself
    spf[i] = i;

  // Separately marking spf for
  // every even number as 2
  for(int i = 4; i < 1000; i += 2)
    spf[i] = 2;

  for(int i = 3; i * i < 1000; i++) 
  {
    // Checking if i is prime
    if (spf[i] == i)
    {
      // Marking SPF for all the
      // numbers divisible by i
      for(int j = i * i; j < 1000; j += i)

        // Marking spf[j] if it is not
        // previously marked
        if (spf[j] == j)
          spf[j] = i;
    }
  }
}

// Function to find the minimum
// number of steps to modify the
// array such that the product
// of any two numbers in the
// array is a perfect square
static int minimum_operation(int []b, 
                             int d, int []spf)
{
  // Map created to store
  // the unique prime numbers
  Dictionary<int, 
             int> m = new Dictionary<int, 
                                   int>();
  int i = 0;

  // Variable to store the
  // minimum number of operations
  int c = 0;

  // Loop to store every
  // unique prime number
  for(i = 0; i < d; i++)
  {
    int x = b[i];
    while (x != 1) 
    {
      x = x / spf[x];
      if (!m.ContainsKey(spf[x]))
      {
        m.Add(spf[x], 1); 
      }
    }
  }

  // Erasing 1 as a key because
  // it is not a prime number
  m.Remove(1);

  // Iterating through the hash
  foreach(KeyValuePair<int,
                       int> x in m) 
  {
    // Two variables used for
    // counting the frequency
    // of prime is even or odd
    int e = 0, o = 0;

    // First prime number
    int j = x.Key;

    // Iterating the number D
    for(i = 0; i < d; i++)
    {
      // Check if prime is a
      // factor of the element
      // in the array
      if (b[i] % j == 0)
      {
        int h = 0;
        int g = b[i];

        // Loop for calculating the
        // frequency of the element
        while (g != 0) 
        {
          if (g % j != 0)
          {
            break;
          }
          g = g / j;
          h = h + 1;
        }

        // Check for frequency
        // odd or even
        if (h % 2 == 0) 
        {
          e = e + 1;
        }
        else
        {
          o = o + 1;
        }
      }
      else
      {
        // If it is not a factor of the
        // element, then it is automatically
        // even
        e = e + 1;
      }
    }

    // Storing the minimum of two variable
    // even or odd
    c = c + Math.Min(o, e);
  }
  return c;
}

// Driver Code
public static void Main(String[] args)
{
  int[] spf = new int[1001];

  // Input array
  int []b = {1, 4, 6};

  // Creating shortest prime
  // factorisation array
  int d = b.Length;
  spf_array(spf);

  Console.Write(minimum_operation(b, d, spf));
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
2

```

**时间复杂度：** *O（N * log（N））*，其中 N 是输入数组的大小。

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。