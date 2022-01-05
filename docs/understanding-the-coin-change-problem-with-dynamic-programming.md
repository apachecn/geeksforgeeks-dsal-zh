# 用动态编程理解硬币兑换问题

> 原文:[https://www . geesforgeks . org/了解动态编程的硬币变化问题/](https://www.geeksforgeeks.org/understanding-the-coin-change-problem-with-dynamic-programming/)

许多人认为**硬币兑换问题**对于理解被称为 [**动态编程**](https://en.wikipedia.org/wiki/Dynamic_programming) 的编程范式至关重要。这两者通常总是成对出现，因为硬币兑换问题包含动态规划的概念。根据维基百科，对于那些不了解动态编程的人来说，

> “数学优化方法和计算机编程方法……都是指通过将一个复杂的问题分解成更简单的子问题来简化它”。

换句话说，动态问题是一种编程方法，用于将问题简化为更小的部分。例如，如果简单地问你 3 * 89 是多少？你可能不会马上知道答案，因为你可能知道什么是 2 * 2。然而，如果你知道 3 * 88 (264)是什么，那么你当然可以推导出 3 * 89。你所要做的就是把 3 加到前面的倍数上，你就会得到 267 的答案。因此，这是对什么是动态编程的一个非常简单的解释，也许你现在可以看到它如何被用来有效地解决大时间复杂度的问题。
牢记动态规划的上述定义，我们现在可以进入**硬币兑换问题**。以下是硬币兑换问题的众多变体之一的例子。给定一份硬币清单，即 **1 分、5 分和 10 分**，你能确定给定清单中硬币的组合总数来组成数字 **N** 吗？
**例 1** :假设给你 1 分钱、5 分钱、10 分钱的硬币，N = 8 分钱，你能安排获得 8 分钱的硬币组合总数是多少。

```
Input: N=8
        Coins : 1, 5, 10
Output: 2

Explanation: 
1 way: 
      1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 = 8 cents.
2 way:
      1 + 1 + 1 + 5 = 8 cents.
```

你所做的就是确定所有你能想出 8 美分面额的方法。八个 1 分加起来等于 8 分。三个 1 分加一个 5 分等于 8 分。因此，给定硬币 1、5 和 10 的列表，总共有 2 种方法可以获得 8 美分。
**例 2** :假设给你 1 美分、5 美分、10 美分的硬币，N = 10 美分，你能安排获得 10 美分的硬币组合总数是多少。

```
Input : N=10
        Coins : 1, 5, 10
Output : 4
Explanation: 
1 way: 
   1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 = 10 cents.
2 way: 
   1 + 1 + 1 + 1 + 1 + 5 = 10 cents.
3 way: 
   5 + 5 = 10 cents.
4 way: 
   10 cents = 10 cents.
```

现在我们已经知道了问题陈述，以及如何找到较小值的解决方案，我们将如何确定添加到**较大值**的硬币组合总数？我们写一个程序。我们如何编写程序来计算获得更大 N 值的所有方法？简单我们用**动态编程**。请记住动态编程背后的思想是将问题的每个部分切割成更小的部分。类似于页面顶部的示例。如果我们不知道 4 * 36 的值，但知道 4 * 35 (140)的值，我们可以把 4 加到那个值上，得到 4 * 36 的答案，顺便说一下，它是 144。
好的，我们明白我们必须做什么，但是一个程序如何确定硬币列表可以输出 N 的方式？让我们看看这个例子。

```
N = 12         
Index of Array: [0, 1,  2]
Array of coins: [1, 5, 10]
```

这是一组硬币，1 分、5 分和 10 分。N 是 12 美分。因此，我们需要想出一个方法，可以使用这些硬币的价值，并确定我们可以赚 12 美分的方式的数量。
动态思考，需要弄清楚如何添加到之前的数据中。这意味着我们必须添加到以前的解决方案中，而不是重新计算相同的值。显然，我们必须遍历整个硬币数组。我们还需要一种方法来查看一枚硬币是否大于 N 值。
实现这一点的一种方法是拥有一个一直计数到**第 n 个值**的数组。
所以……
**阵仗:**

```
 [0, 0, 0 ..... Nth value] in our case it would be up to 12.
```

之所以有第 n 个值的数组，是因为我们可以在**路数组**的索引处确定硬币组成值的路数。我们这样做是因为如果我们能确定一枚硬币大于指数上的那个值，那么显然我们不能用那枚硬币来确定硬币的组合，因为那枚硬币大于那个值。这可以通过一个例子更好地理解。
以上述数字为例。

```
N = 12         
Index of Array of Coins:    
  [0, 1,  2]     
Array of coins:
  [1, 5, 10]

Index of Array of ways:   
  [0,  1,  2,  3,  4,  5,  6,  7,  8,  9,  10,  11,  12]
Array of  ways:            
  [0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,   0,    0]
```

在开始迭代之前，我们必须给 way 数组一个预定义的值。我们必须将 way 数组索引 0 处的第一个元素设置为 1。这是因为有 1 种方法可以使数字为 0，使用 0 个硬币。
因此，如果我们开始遍历所有硬币数组，并将元素与路数组进行比较，我们将确定一枚硬币可以使用多少次来产生路数组索引处的值。
例如……
第一套方式[0] = 1。
我们来比较一下第一枚硬币，1 分。

```
N = 12         
Index of Array of Coins:    
  [0, 1,  2]     
Array of coins:             
  [1, 5, 10]

Index of Array of ways:    
  [0,  1,  2,  3,  4,  5,  6,  7,  8,  9,  10,  11,  12]
Array of  ways:            
  [0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,   0,    0]

Then compare coins[0] to all of the index's 
of ways array. If the value of the coin is less 
than or equal to the ways index, then
ways[j-coins[i]]+ways[j] is the new value of 
ways[j]. We do this because we are 
trying to break each part down into smaller 
pieces. You will see what is happening as 
you continue to read. So comparing each value of the 
ways index to the first coin, we get the following.

Index of Array of ways:    
  [0,  1,  2,  3,  4,  5,  6,  7,  8,  9,  10,  11,  12]
Array of  ways:            
  [1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,   1,    1]
```

现在让我们比较第二枚硬币，5 美分。

```
N = 12         
Index of Array of Coins:    
  [0, 1,  2]     
Array of coins:             
  [1, 5, 10]

Index of Array of ways:    
  [0,  1,  2,  3,  4,  5,  6,  7,  8,  9,  10,  11,  12]
Array of  ways:            
  [1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,   1,    1]

Comparing 5 cents to each of the index and
making that same comparison, if the value 
of the coin is smaller than the value of 
the index at the ways array then ways[j-coins[i]]+ways[j] 
is the new value of ways[j]. Thus we
get the following.

Index of Array of ways:    
  [0,  1,  2,  3,  4,  5,  6,  7,  8,  9,  10,  11,  12]
Array of  ways:            
  [1,  1,  1,  1,  1,  2,  2,  2,  2,  2,  3,   3,    3]

We are determining how many times the second
coin goes into all of the values leading up the
Nth coin. Why are we using all 
of the coins? It is to check our previous 
result dynamically and update our answer 
instead of recalculating all over again. 
For example take the element at index 10 
the answer is 3 so far. But how did we get 3? 
We know that the value of 10-5 is 5 so that
is our j-coins[i] value, that is the 
difference of what needs to be made up to 
make the amount 10\. So we look at index 5 of the
ways array and see it has the value 2, for
the same reason as above, there are so far 2 
ways to obtain the value 5\. So if there are 
2 ways to obtain the value 5 then those ways
plus the current number of ways is the new
updated value of the TOTAL 
ways to get the value at index 10\.                                    
```

现在让我们比较第三枚硬币，10 美分。

```
N = 12         
Index of Array of Coins:    
  [0, 1,  2]     
Array of coins:             
  [1, 5, 10]

Comparing 10 cents to each of the index
and making that same comparison, if the 
value of the coin is smaller than the value of the 
index at the ways array then 
ways[j-coins[i]]+ways[j] is the new value of ways[j]. 
Thus we get the following.

Index of Array of ways:    
  [0,  1,  2,  3,  4,  5,  6,  7,  8,  9,  10,  11,  12]
Array of  ways:            
  [1,  1,  1,  1,  1,  2,  2,  2,  2,  2,  4,   4,    4]

So the answer to our example is ways[12] which is 4.
```

考虑到以上所有内容，让我们来看看下面的程序。

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* We have input values of N and an array Coins
  that holds all of the coins. We use data type
  of long because we want to be able to test
  large values
without integer overflow*/
long getNumberOfWays(long N, vector<long> Coins)
{

    // Create the ways array to 1 plus the amount
    // to stop overflow
    vector<long> ways(N + 1);

    // Set the first way to 1 because its 0 and
    // there is 1 way to make 0 with 0 coins
    ways[0] = 1;

     // Go through all of the coins
    for(int i = 0; i < Coins.size(); i++)
    {

        // Make a comparison to each index value
        // of ways with the coin value.
        for(int j = 0; j < ways.size(); j++)
        {
            if (Coins[i] <= j)
            {

                // Update the ways array
                ways[j] += ways[(j - Coins[i])];
            }
        }
    }

    // Return the value at the Nth position
    // of the ways array.
    return ways[N];
}

void printArray(vector<long> coins)
{
    for(long i : coins)
        cout << i << "\n";
}

// Driver Code
int main()
{
    vector<long> Coins = { 1, 5, 10 };

    cout << "The Coins Array:" << endl;
    printArray(Coins);

    cout << "Solution:" << endl;
    cout << getNumberOfWays(12, Coins) << endl;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* We have input values of N and an array Coins 
  that holds all of the coins. We use data type
  of long because we want to be able to test
  large values
without integer overflow*/

class getWays {

    static long getNumberOfWays(long N, long[] Coins)
    {
        // Create the ways array to 1 plus the amount
        // to stop overflow
        long[] ways = new long[(int)N + 1];

        // Set the first way to 1 because its 0 and
        // there is 1 way to make 0 with 0 coins
        ways[0] = 1;

         // Go through all of the coins
        for (int i = 0; i < Coins.length; i++) {

            // Make a comparison to each index value
            // of ways with the coin value.
            for (int j = 0; j < ways.length; j++) {
                if (Coins[i] <= j) {

                    // Update the ways array
                    ways[j] += ways[(int)(j - Coins[i])];
                }
            }
        }

        // return the value at the Nth position
        // of the ways array.   
        return ways[(int)N];
    }

    static void printArray(long[] coins)
    {
        for (long i : coins)
            System.out.println(i);
    }

    public static void main(String args[])
    {
        long Coins[] = { 1, 5, 10 };

        System.out.println("The Coins Array:");
        printArray(Coins);

        System.out.println("Solution:");
        System.out.println(getNumberOfWays(12, Coins));
    }
}
```

## 蟒蛇 3

```
''' We have input values of N and an array Coins
that holds all of the coins. We use data type
of because long we want to be able to test
large values
without integer overflow'''

def getNumberOfWays(N, Coins):

    # Create the ways array to 1 plus the amount
    # to stop overflow
    ways = [0] * (N + 1);

    # Set the first way to 1 because its 0 and
    # there is 1 way to make 0 with 0 coins
    ways[0] = 1;

    # Go through all of the coins
    for i in range(len(Coins)):

        # Make a comparison to each index value
        # of ways with the coin value.
        for j in range(len(ways)):
            if (Coins[i] <= j):

                # Update the ways array
                ways[j] += ways[(int)(j - Coins[i])];

    # return the value at the Nth position
    # of the ways array.
    return ways[N];

def printArray(coins):
    for i in coins:
        print(i);

if __name__ == '__main__':
    Coins = [1, 5, 10];

    print("The Coins Array:");
    printArray(Coins);

    print("Solution:",end="");
    print(getNumberOfWays(12, Coins));

# This code is contributed by 29AjayKumar
```

## C#

```
/* We have input values of N and
an array Coins that holds all of
the coins. We use data type of
long because we want to be able
to test large values without
integer overflow*/
using System;

public class getWays
{

    static long getNumberOfWays(long N, long[] Coins)
    {
        // Create the ways array to 1 plus the amount
        // to stop overflow
        long[] ways = new long[(int)N + 1];

        // Set the first way to 1 because its 0 and
        // there is 1 way to make 0 with 0 coins
        ways[0] = 1;

        // Go through all of the coins
        for (int i = 0; i < Coins.Length; i++)
        {

            // Make a comparison to each index value
            // of ways with the coin value.
            for (int j = 0; j < ways.Length; j++)
            {
                if (Coins[i] <= j)
                {

                    // Update the ways array
                    ways[j] += ways[(int)(j - Coins[i])];
                }
            }
        }

        // return the value at the Nth position
        // of the ways array.
        return ways[(int)N];
    }

    static void printArray(long[] coins)
    {
        foreach (long i in coins)
            Console.WriteLine(i);
    }

    // Driver code
    public static void Main(String []args)
    {
        long []Coins = { 1, 5, 10 };

        Console.WriteLine("The Coins Array:");
        printArray(Coins);

        Console.WriteLine("Solution:");
        Console.WriteLine(getNumberOfWays(12, Coins));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
/* We have input values of N and an array Coins
  that holds all of the coins. We use data type
  of long because we want to be able to test
  large values
without integer overflow*/

function getNumberOfWays(N,Coins)
{
    // Create the ways array to 1 plus the amount
        // to stop overflow
        let ways = new Array(N + 1);
         for(let i=0;i<N+1;i++)
        {
            ways[i]=0;
        }
        // Set the first way to 1 because its 0 and
        // there is 1 way to make 0 with 0 coins
        ways[0] = 1;

         // Go through all of the coins
        for (let i = 0; i < Coins.length; i++) {

            // Make a comparison to each index value
            // of ways with the coin value.
            for (let j = 0; j < ways.length; j++) {
                if (Coins[i] <= j) {

                    // Update the ways array
                    ways[j] += ways[(j - Coins[i])];
                }
            }
        }

        // return the value at the Nth position
        // of the ways array.  
        return ways[N];
}

function printArray(coins)
{
    for(let i=0;i<coins.length;i++)
    {
        document.write(coins[i]+"<br>");
    }
}

let Coins=[1, 5, 10];
document.write("The Coins Array:<br>");
printArray(Coins);

document.write("Solution:<br>");
document.write(getNumberOfWays(12, Coins)+"<br>");

// This code is contributed by patel2127
</script>
```

**Output:** 

```
The Coins Array:
1
5
10
Solution:
4
```