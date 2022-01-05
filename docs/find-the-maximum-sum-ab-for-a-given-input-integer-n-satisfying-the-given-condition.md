# 求满足给定条件的给定输入整数 N 的最大和(a+b)

> 原文:[https://www . geesforgeks . org/find-给定输入的最大和-ab-for-给定条件的整数-n/](https://www.geeksforgeeks.org/find-the-maximum-sum-ab-for-a-given-input-integer-n-satisfying-the-given-condition/)

给定一个整数 **N** ，任务是求最大和( **a + b** ) {1 ≤ a ≤ N，1 ≤ b ≤ N}使得 **a * b/(a + b)** 为整数(即 a + b 除 a * b)和 a！= b。

**示例:**

> **输入:** N = 10
> **输出:** 9
> **解释:**数字 a = 3 和 b = 6 导致和= 9 也是 6 * 3 = 18，它可被 6 + 3 = 9
> 整除
> 
> **输入:**N = 20
> T3】输出: 27

**天真方法:**用天真方法解决这个问题的思路是使用[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)的概念。可以按照以下步骤计算结果:

1.  运行从 1 到 n 的嵌套循环
2.  对于[1，N]范围内的每个数字 **a** ，再找一个整数 **b** ，这样 **a！= b**(**a+b**)除 **a * b** 。
3.  如果满足条件，将( **a + b** )的值存储在变量中，以跟踪获得的最大值。
4.  最后返回最大值( **a + b** )。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the largest value
// of a + b satisfying the given condition
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum of
// a + b satisfying the given condition
int getLargestSum(int N)
{
    // Initialize max_sum
    int max_sum = 0;

    // Consider all the possible pairs
    for (int i = 1; i <= N; i++) {
        for (int j = i + 1; j <= N; j++) {

            // Check if the product is
            // divisible by the sum
            if (i * j % (i + j) == 0)

                // Storing the maximum sum
                // in the max_sum variable
                max_sum = max(max_sum, i + j);
        }
    }

    // Return the max_sum value
    return max_sum;
}

// Driver code
int main()
{
    int N = 25;

    int max_sum = getLargestSum(N);

    cout << max_sum << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the largest value
// of a + b satisfying the given condition
import java.util.*;

class GFG{

// Function to return the maximum sum of
// a + b satisfying the given condition
static int getLargestSum(int N)
{
    // Initialize max_sum
    int max_sum = 0;

    // Consider all the possible pairs
    for (int i = 1; i <= N; i++) {
        for (int j = i + 1; j <= N; j++) {

            // Check if the product is
            // divisible by the sum
            if (i * j % (i + j) == 0)

                // Storing the maximum sum
                // in the max_sum variable
                max_sum = Math.max(max_sum, i + j);
        }
    }

    // Return the max_sum value
    return max_sum;
}

// Driver code
public static void main(String[] args)
{
    int N = 25;

    int max_sum = getLargestSum(N);

    System.out.print(max_sum );
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation to find the largest value
# of a + b satisfying the given condition

# Function to return the maximum sum of
# a + b satisfying the given condition
def getLargestSum(N):
    # Initialize max_sum
    max_sum = 0

    # Consider all the possible pairs
    for i in range(1,N+1):
        for j in range(i + 1, N + 1, 1):

            # Check if the product is
            # divisible by the sum
            if (i * j % (i + j) == 0):

                # Storing the maximum sum
                # in the max_sum variable
                max_sum = max(max_sum, i + j)

    # Return the max_sum value
    return max_sum

# Driver code
if __name__ == '__main__':
    N = 25

    max_sum = getLargestSum(N)
    print(max_sum)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to find the largest value
// of a + b satisfying the given condition
using System;

class GFG{

    // Function to return the maximum sum of
    // a + b satisfying the given condition
    static int getLargestSum(int N)
    {
        // Initialize max_sum
        int max_sum = 0;

        // Consider all the possible pairs
        for (int i = 1; i <= N; i++) {
            for (int j = i + 1; j <= N; j++) {

                // Check if the product is
                // divisible by the sum
                if (i * j % (i + j) == 0)

                    // Storing the maximum sum
                    // in the max_sum variable
                    max_sum = Math.Max(max_sum, i + j);
            }
        }

        // Return the max_sum value
        return max_sum;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int N = 25;

        int max_sum = getLargestSum(N);

        Console.WriteLine(max_sum );
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation to find the largest value
// of a + b satisfying the given condition

    // Function to return the maximum sum of
    // a + b satisfying the given condition
    function getLargestSum(N) {
        // Initialize max_sum
        var max_sum = 0;

        // Consider all the possible pairs
        for (i = 1; i <= N; i++) {
            for (j = i + 1; j <= N; j++) {

                // Check if the product is
                // divisible by the sum
                if (i * j % (i + j) == 0)

                    // Storing the maximum sum
                    // in the max_sum variable
                    max_sum = Math.max(max_sum, i + j);
            }
        }

        // Return the max_sum value
        return max_sum;
    }

    // Driver code

        var N = 25;

        var max_sum = getLargestSum(N);

        document.write(max_sum);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
36
```

**时间复杂度:**由于嵌套 for 循环运行了(N * (N + 1)) / 2 次，上述解的时间复杂度为 **O(N <sup>2</sup> )** 。

**辅助空间:** O(1)
**有效途径:**可以做的一个观察是，如果两个数 **a** 和 **b** 存在，使得它们的乘积可被它们的和整除，那么它们不是相对素数，即它们的 GCD 不是一。这可以用[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)来证明。
因此，通过使用上述观察，可以遵循以下步骤来计算结果:

1.如果 **a** 可以表示为 **k * x** 而 **b** 可以表示为 **k * y** 使得 **x** 和 **y** 为[共形](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)，那么:

```
a + b = k(x + y)
a * b = k2
```

2.现在，在划分上述值时:

```
(a * b) /(a + b) = k * ((x * y)/(x + y)). 
```

3.既然知道 x 和 y 是互素，( **x * y** )就不能被( **x + y** 整除。这意味着 **k** 必须能被 x + y 整除。

4.因此， **k** 是( **k * x** )和( **k * y** )保持小于 **N** 的最大可能因素。

5.显然， **k** 可被(x + y)整除的最小值是( **x + y** )。这意味着(x+y)* y&leq；n 和(x+y)* x&leq；名词（noun 的缩写）

6.因此，从 **1 到 N <sup>0.5</sup>** 检查所有因素。

以下是上述方法的实现:

## C++

```
// C++ implementation to  find the largest value
// of a + b satisfying the given condition
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum of
// a + b satisfying the given condition
int getLargestSum(int N)
{
    int max_sum = 0; // Initialize max_sum

    // Consider all possible pairs and check
    // the sum divides product property
    for (int i = 1; i * i <= N; i++) {
        for (int j = i + 1; j * j <= N; j++) {

            // To find the largest factor k
            int k = N / j;
            int a = k * i;
            int b = k * j;

            // Check if the product is
            // divisible by the sum
            if (a <= N && b <= N
                && a * b % (a + b) == 0)

                // Storing the maximum sum
                // in the max_sum variable
                max_sum = max(max_sum, a + b);
        }
    }

    // Return the max_sum value
    return max_sum;
}

// Driver code
int main()
{
    int N = 25;
    int max_sum = getLargestSum(N);

    cout << max_sum << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the largest value
// of a + b satisfying the given condition

class GFG{

// Function to return the maximum sum of
// a + b satisfying the given condition
static int getLargestSum(int N)
{
    // Initialize max_sum
    int max_sum = 0;

    // Consider all possible pairs and check
    // the sum divides product property
    for (int i = 1; i * i <= N; i++) {
         for (int j = i + 1; j * j <= N; j++) {

              // To find the largest factor k
              int k = N / j;
              int a = k * i;
              int b = k * j;

               // Check if the product is
               // divisible by the sum
               if (a <= N && b <= N &&
                   a * b % (a + b) == 0)

                   // Storing the maximum sum
                   // in the max_sum variable
                   max_sum = Math.max(max_sum, a + b);
        }
    }

    // Return the max_sum value
    return max_sum;
}

// Driver code
public static void main(String[] args)
{
    int N = 25;
    int max_sum = getLargestSum(N);
    System.out.print(max_sum + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the largest value
# of a + b satisfying the given condition

# Function to return the maximum sum of
# a + b satisfying the given condition
def getLargestSum(N) :

    max_sum = 0; # Initialize max_sum

    # Consider all possible pairs and check
    # the sum divides product property
    for i in range(1, int(N ** (1/2))+1) :
        for j in range(i + 1, int(N ** (1/2)) + 1) :

            # To find the largest factor k
            k = N // j;
            a = k * i;
            b = k * j;

            # Check if the product is
            # divisible by the sum
            if (a <= N and b <= N and a * b % (a + b) == 0) :
                # Storing the maximum sum
                # in the max_sum variable
                max_sum = max(max_sum, a + b);

    # Return the max_sum value
    return max_sum;

# Driver code
if __name__ == "__main__" :
    N = 25;
    max_sum = getLargestSum(N);
    print(max_sum);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the largest value
// of a + b satisfying the given condition
using System;

class GFG{

// Function to return the maximum sum of
// a + b satisfying the given condition
static int getLargestSum(int N)
{

    // Initialize max_sum
    int max_sum = 0;

    // Consider all possible pairs and check
    // the sum divides product property
    for(int i = 1; i * i <= N; i++)
    {
       for(int j = i + 1; j * j <= N; j++)
       {
          // To find the largest factor k
          int k = N / j;
          int a = k * i;
          int b = k * j;

          // Check if the product is
          // divisible by the sum
          if (a <= N && b <= N &&
              a * b % (a + b) == 0)

              // Storing the maximum sum
              // in the max_sum variable
              max_sum = Math.Max(max_sum, a + b);
        }
    }

    // Return the max_sum value
    return max_sum;
}

// Driver code
static public void Main(String[] args)
{
    int N = 25;
    int max_sum = getLargestSum(N);

    Console.Write(max_sum + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
    // Javascript implementation to find the largest value
    // of a + b satisfying the given condition

    // Function to return the maximum sum of
    // a + b satisfying the given condition
    function getLargestSum(N)
    {

        // Initialize max_sum
        let max_sum = 0;

        // Consider all possible pairs and check
        // the sum divides product property
        for(let i = 1; i * i <= N; i++)
        {
           for(let j = i + 1; j * j <= N; j++)
           {
              // To find the largest factor k
              let k = parseInt(N / j, 10);
              let a = k * i;
              let b = k * j;

              // Check if the product is
              // divisible by the sum
              if (a <= N && b <= N &&
                  a * b % (a + b) == 0)

                  // Storing the maximum sum
                  // in the max_sum variable
                  max_sum = Math.max(max_sum, a + b);
            }
        }

        // Return the max_sum value
        return max_sum;
    }

    let N = 25;
    let max_sum = getLargestSum(N);

    document.write(max_sum + "</br>");

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
36
```

**时间复杂度:**虽然有两个循环，但每个循环最多运行 sqrt(N)次。因此，整体时间复杂度 **O(N)** 。

**辅助空间:** O(1)