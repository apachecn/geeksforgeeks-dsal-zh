# 生成一个整数的所有唯一分区|集合 2

> 原文:[https://www . geesforgeks . org/generate-all-unique-partitions-of-integer-set-2/](https://www.geeksforgeeks.org/generate-all-unique-partitions-of-an-integer-set-2/)

给定一个正整数 **n** ，任务是生成所有可能的唯一方式来将 **n** 表示为正整数之和。
**例:**

> **输入:**4
> T3】输出:T5】4
> 3 1
> 2 2
> 2 1 1
> 1 1 1
> 1**输入:**3
> T14】输出:T16】3
> 2 1
> 1 1

**方法:**我们已经在[这篇](https://www.geeksforgeeks.org/generate-unique-partitions-of-an-integer/)帖子中讨论了生成唯一分区的实现。这篇文章包含了使用[递归](https://www.geeksforgeeks.org/recursion/)对上述问题的另一个更直观的实现。
这个想法很简单，和这里使用的方法差不多。我们必须递归地从 n 移动到 1，并继续在数组中追加用于形成 sum 的数字。当总和等于 n 时，我们打印数组并返回。实现中考虑的基本情况是: **remSum == 0:** 形成所需的 n，因此打印数组。
然后我们开始使用前一个分区中使用的最大值数来形成所需的和。如果这个数变得大于 n，我们忽略它，否则我们将这个数附加到数组中，并递归地移动到下一次迭代，以形成**sum =(remSum–I)**，其中可以使用的最大值
是 I 或小于 I。这样，我们可以生成所需的唯一分区。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Array to store the numbers used
// to form the required sum
int dp[200];
int count = 0;

// Function to print the array which contains
// the unique partitions which are used
// to form the required sum
void print(int idx)
{
    for (int i = 1; i < idx; i++) {
        cout << dp[i] << " ";
    }
    cout << endl;
}

// Function to find all the unique partitions
// remSum = remaining sum to form
// maxVal is the maximum number that
// can be used to make the partition
void solve(int remSum, int maxVal, int idx, int& count)
{

    // If remSum == 0 that means the sum
    // is achieved so print the array
    if (remSum == 0) {
        print(idx);
        count++;
        return;
    }

    // i will begin from maxVal which is the
    // maximum value which can be used to form the sum
    for (int i = maxVal; i >= 1; i--) {
        if (i > remSum) {
            continue;
        }
        else if (i <= remSum) {

            // Store the number used in forming
            // sum gradually in the array
            dp[idx] = i;

            // Since i used the rest of partition
            // cant have any number greater than i
            // hence second parameter is i
            solve(remSum - i, i, idx + 1, count);
        }
    }
}

// Driver code
int main()
{
    int n = 4, count = 0;

    solve(n, n, 1, count);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Array to store the numbers used
    // to form the required sum
    static int[] dp = new int[200];
    static int count = 0;

    // Function to print the array which contains
    // the unique partitions which are used
    // to form the required sum
    static void print(int idx)
    {
        for (int i = 1; i < idx; i++)
        {
            System.out.print(dp[i] + " ");
        }
        System.out.println("");
    }

    // Function to find all the unique partitions
    // remSum = remaining sum to form
    // maxVal is the maximum number that
    // can be used to make the partition
    static void solve(int remSum, int maxVal,
                        int idx, int count)
    {

        // If remSum == 0 that means the sum
        // is achieved so print the array
        if (remSum == 0)
        {
            print(idx);
            count++;
            return;
        }

        // i will begin from maxVal which is the
        // maximum value which can be used to form the sum
        for (int i = maxVal; i >= 1; i--)
        {
            if (i > remSum)
            {
                continue;
            }
            else if (i <= remSum)
            {

                // Store the number used in forming
                // sum gradually in the array
                dp[idx] = i;

                // Since i used the rest of partition
                // cant have any number greater than i
                // hence second parameter is i
                solve(remSum - i, i, idx + 1, count);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, count = 0;

        solve(n, n, 1, count);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Array to store the numbers used
# to form the required sum
dp = [0 for i in range(200)]
count = 0

# Function to print the array which contains
# the unique partitions which are used
# to form the required sum
def print1(idx):
    for i in range(1,idx,1):
        print(dp[i],end = " ")
    print("\n",end = "")

# Function to find all the unique partitions
# remSum = remaining sum to form
# maxVal is the maximum number that
# can be used to make the partition
def solve(remSum,maxVal,idx,count):
    # If remSum == 0 that means the sum
    # is achieved so print the array
    if (remSum == 0):
        print1(idx)
        count += 1
        return
    # i will begin from maxVal which is the
    # maximum value which can be used to form the sum
    i = maxVal
    while(i >= 1):
        if (i > remSum):
            i -= 1
            continue
        elif (i <= remSum):
            # Store the number used in forming
            # sum gradually in the array
            dp[idx] = i

            # Since i used the rest of partition
            # cant have any number greater than i
            # hence second parameter is i
            solve(remSum - i, i, idx + 1, count)
            i -= 1

# Driver code
if __name__ == '__main__':
    n = 4
    count = 0

    solve(n, n, 1, count)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Array to store the numbers used
    // to form the required sum
    static int[] dp = new int[200];

    // Function to print the array which contains
    // the unique partitions which are used
    // to form the required sum
    static void print(int idx)
    {
        for (int i = 1; i < idx; i++)
        {
            Console.Write(dp[i] + " ");
        }
        Console.WriteLine("");
    }

    // Function to find all the unique partitions
    // remSum = remaining sum to form
    // maxVal is the maximum number that
    // can be used to make the partition
    static void solve(int remSum, int maxVal,
                        int idx, int count)
    {

        // If remSum == 0 that means the sum
        // is achieved so print the array
        if (remSum == 0)
        {
            print(idx);
            count++;
            return;
        }

        // i will begin from maxVal which is the
        // maximum value which can be used to form the sum
        for (int i = maxVal; i >= 1; i--)
        {
            if (i > remSum)
            {
                continue;
            }
            else if (i <= remSum)
            {

                // Store the number used in forming
                // sum gradually in the array
                dp[idx] = i;

                // Since i used the rest of partition
                // cant have any number greater than i
                // hence second parameter is i
                solve(remSum - i, i, idx + 1, count);
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 4, count = 0;

        solve(n, n, 1, count);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Array to store the numbers used
// to form the required sum
var dp = Array.from({length: 200}, (_, i) => 0);
var count = 0;

// Function to print the array which contains
// the unique partitions which are used
// to form the required sum
function print(idx)
{
    for (var i = 1; i < idx; i++)
    {
        document.write(dp[i] + " ");
    }
    document.write('<br>');
}

// Function to find all the unique partitions
// remSum = remaining sum to form
// maxVal is the maximum number that
// can be used to make the partition
function solve(remSum , maxVal,idx , count)
{

    // If remSum == 0 that means the sum
    // is achieved so print the array
    if (remSum == 0)
    {
        print(idx);
        count++;
        return;
    }

    // i will begin from maxVal which is the
    // maximum value which can be used to form the sum
    for (var i = maxVal; i >= 1; i--)
    {
        if (i > remSum)
        {
            continue;
        }
        else if (i <= remSum)
        {

            // Store the number used in forming
            // sum gradually in the array
            dp[idx] = i;

            // Since i used the rest of partition
            // cant have any number greater than i
            // hence second parameter is i
            solve(remSum - i, i, idx + 1, count);
        }
    }
}

// Driver code
var n = 4, count = 0;

solve(n, n, 1, count);

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
4 
3 1 
2 2 
2 1 1 
1 1 1 1
```