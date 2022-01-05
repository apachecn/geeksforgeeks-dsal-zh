# 检查一个数的奇数和偶数因子的计数是否相等

> 原文:[https://www . geeksforgeeks . org/check-count-count-of-of-of-单数和双数因子是否相等/](https://www.geeksforgeeks.org/check-whether-count-of-odd-and-even-factors-of-a-number-are-equal/)

给定一个数字 **N** ，任务是找出 N 是否有相等数量的奇偶因子。
**例:**

> **输入:** N = 10
> **输出:** YES
> **解释:** 10 有两个奇数因子(1 和 5)和两个偶数因子(2 和 10)
> **输入:** N = 24
> **输出:** NO
> **解释:** 24 有两个奇数因子(1 和 3)和六个偶数因子(2、4、6、8、12 和 24

**天真的做法:** [找出所有的除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)检查奇数除数和偶数除数的计数是否相同。
以下是上述办法的实施情况

## C++

```
// C++ solution for the above approach
#include <bits/stdc++.h>
using namespace std;
#define lli long long int

// Function to check condition
void isEqualFactors(lli N)
{
    // Initialize even_count
    // and od_count
    lli ev_count = 0, od_count = 0;

    // loop runs till square root
    for (lli i = 1;
         i <= sqrt(N) + 1; i++) {

        if (N % i == 0) {
            if (i == N / i) {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }

            else {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;

                if ((N / i) % 2 == 0)
                    ev_count += 1;

                else
                    od_count += 1;
            }
        }
    }

    if (ev_count == od_count)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

// Driver Code
int main()
{
    lli N = 10;
    isEqualFactors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java solution for the above approach
class GFG{

// Function to check condition
static void isEqualFactors(int N)
{

    // Initialize even_count
    // and od_count
    int ev_count = 0, od_count = 0;

    // Loop runs till square root
    for(int i = 1;
            i <= Math.sqrt(N) + 1; i++)
    {
       if (N % i == 0)
       {
           if (i == N / i)
           {
               if (i % 2 == 0)
                   ev_count += 1;
               else
                   od_count += 1;
           }
           else
           {
               if (i % 2 == 0)
                   ev_count += 1;
               else
                   od_count += 1;

               if ((N / i) % 2 == 0)
                   ev_count += 1;
               else
                   od_count += 1;
           }
       }
    }

    if (ev_count == od_count)
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    isEqualFactors(N);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 code for the naive approach
import math

# Function to check condition
def isEqualFactors(N):

# Initialize even_count
# and od_count
    ev_count = 0
    od_count = 0

# loop runs till square root
    for i in range(1, (int)(math.sqrt(N)) + 2) :
        if (N % i == 0):
            if(i == N // i):
                if(i % 2 == 0):
                    ev_count += 1
                else:
                    od_count += 1

            else:
                if(i % 2 == 0):
                    ev_count += 1
                else:
                    od_count += 1

                if((N // i) % 2 == 0):
                    ev_count += 1;
                else:
                    od_count += 1;

    if (ev_count == od_count):
        print("YES")
    else:
        print("NO")

# Driver Code
N = 10
isEqualFactors(N)
```

## C#

```
// C# solution for the above approach
using System;

class GFG{

// Function to check condition
static void isEqualFactors(int N)
{

    // Initialize even_count
    // and od_count
    int ev_count = 0, od_count = 0;

    // Loop runs till square root
    for(int i = 1;
            i <= Math.Sqrt(N) + 1; i++)
    {
        if (N % i == 0)
        {
            if (i == N / i)
            {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
            else
            {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;

                if ((N / i) % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
        }
    }

    if (ev_count == od_count)
        Console.Write("YES" + "\n");
    else
        Console.Write("NO" + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 10;

    isEqualFactors(N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check condition
function isEqualFactors(N)
{

    // Initialize even_count
    // and od_count
    let ev_count = 0, od_count = 0;

    // Loop runs till square root
    for(let i = 1;
            i <= Math.sqrt(N) + 1; i++)
    {
       if (N % i == 0)
       {
           if (i == N / i)
           {
               if (i % 2 == 0)
                   ev_count += 1;
               else
                   od_count += 1;
           }
           else
           {
               if (i % 2 == 0)
                   ev_count += 1;
               else
                   od_count += 1;

               if ((N / i) % 2 == 0)
                   ev_count += 1;
               else
                   od_count += 1;
           }
       }
    }

    if (ev_count == od_count)
        document.write("YES" + "\n");
    else
        document.write("NO" + "\n");
}

    // Driver Code

    let N = 10;

    isEqualFactors(N);

</script>
```

**Output:** 

```
YES
```