# 爬第 n 级楼梯，允许从 1 到 n 的所有跳跃(三种不同的方法)

> 原文:[https://www . geeksforgeeks . org/爬升-n-th-楼梯-全跳-从 1 到 n-允许-三种不同的方法/](https://www.geeksforgeeks.org/climb-n-th-stair-with-all-jumps-from-1-to-n-allowed-three-different-approaches/)

一只猴子站在下面有 N 级台阶的楼梯上。考虑到它一次可以跨越 1 到 N 级台阶，计算一下它能有多少种方式到达楼梯顶端？

**示例:**

```
Input : 2
Output : 2
It can either take (1, 1) or (2) to
reach the top. So, total 2 ways

Input : 3
Output : 4
Possibilities : (1, 1, 1), (1, 2), (2, 1),
(3). So, total 4 ways 
```

**思考问题有 3 种不同的方式。**

1.  在所有可能的解决方案中，一个步骤要么被猴子踩到，要么可以跳过。所以利用[基本计数原理](https://people.richland.edu/james/lecture/m116/sequences/counting.html)，第一步有 2 种方式参与，对于每一种方式，第二步也有 2 种方式，以此类推。但是最后一步总是要踩的。

```
  2 x 2 x 2 x .... x 2(N-1 th step) x 1(Nth step) 
  = 2(N-1) different ways. 
```

1.  让我们为用例定义一个函数 F(n)。F(n)表示从楼梯底部到顶部有 N 级台阶的所有可能到达方式，其中最小跳跃为 1 级台阶，最大跳跃为 N 级台阶。现在，对于猴子来说，它能做的第一个动作有 N 种不同的方式(1 步，2 步，3 步..n 步)。如果把第一次飞跃当成 1 步，那还剩下 N-1 步需要攻克，可以用 F(N-1)种方式实现。而如果把第一次飞跃当成 2 步，那就要多覆盖 N-2 步，可以用 F(N-2)的方式来实现。放在一起，

```
F(N) = F(N-1) + F(N-2) + F(N-3) + ... + 
                      F(2) + F(1) + F(0) 
Now, 
F(0) = 1
F(1) = 1
F(2) = 2
F(3) = 4

Hence,
F(N) = 1 + 1 + 2 + 4 + ... + F(n-1)
     = 1 + 2^0 + 2^1 + 2^2 + ... + 2^(n-2)
     = 1 + [2^(n-1) - 1]
```

## C++

```
// C++ program to count total number of ways
// to reach n-th stair with all jumps allowed
#include <iostream>

int calculateLeaps(int n)
{
    if (n == 0 || n == 1) {
        return 1;
    }
    else {
        int leaps = 0;
        for (int i = 0; i < n; i++)
            leaps += calculateLeaps(i);
        return leaps;
    }
}

// Driver code
int main()
{
    int calculateLeaps(int);
    std::cout << calculateLeaps(4) << std::endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total number of ways
// to reach n-th stair with all jumps allowed
class GFG {
    static int calculateLeaps(int n)
    {
        if (n == 0 || n == 1) {
            return 1;
        }
        else {
            int leaps = 0;
            for (int i = 0; i < n; i++)
                leaps += calculateLeaps(i);
            return leaps;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(calculateLeaps(4));
    }
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count
# total number of ways
# to reach n-th stair with
# all jumps allowed

def calculateLeaps(n):
    if n == 0 or n == 1:
        return 1;
    else:
        leaps = 0;
        for i in range(0,n):
            leaps = leaps + calculateLeaps(i);
        return leaps;

# Driver code
print(calculateLeaps(4));

# This code is contributed by mits
```

## C#

```
// C# program to count total number of ways
// to reach n-th stair with all jumps allowed
using System;

class GFG {

    // Function to calculate leaps
    static int calculateLeaps(int n)
    {
        if (n == 0 || n == 1) {
            return 1;
        }
        else {
            int leaps = 0;
            for (int i = 0; i < n; i++)
                leaps += calculateLeaps(i);
            return leaps;
        }
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(calculateLeaps(4));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count total
// number of ways to reach
// n-th stair with all
// jumps allowed

// function return the
// number of ways
function calculateLeaps($n)
{
    if ($n == 0 || $n == 1)
    {
        return 1;
    }
    else
    {
        $leaps = 0;
        for ($i = 0; $i < $n; $i++)
            $leaps += calculateLeaps($i);
        return $leaps;
    }
}

    // Driver Code
    echo calculateLeaps(4), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to count total number of ways
    // to reach n-th stair with all jumps allowed

    // Function to calculate leaps
    function calculateLeaps(n)
    {
        if (n == 0 || n == 1) {
            return 1;
        }
        else {
            let leaps = 0;
            for (let i = 0; i < n; i++)
                leaps += calculateLeaps(i);
            return leaps;
        }
    }

    document.write(calculateLeaps(4));

</script>
```

1.  **输出:**

```
8
```

2.上述解决方案可以通过使用动态编程(自底向上方法)来改进

```
                              Leaps(3)
                         3/      2|         1\
                     Leaps(0)   Leaps(1)            Leaps(2)
                    /   |   \                   3/       2|     1\
          Leaps(-3) Leaps(-2)  Leaps(-1)   Lepas(-1) Leaps(0) Leaps(1)
```

## C++

```
// C++ program to count total number of ways
// to reach n-th stair with all jumps allowed

#include <iostream>
using namespace std;

int calculateLeaps(int n, int dp[]){
    if(n == 0){
        return 1 ;
    }else if(n < 0){
        return 0 ;
    }

    if(dp[n] != 0 ){
       return dp[n] ;
    }

    int count = 0;
    for(int i = 0 ; i < n ; i++ ){
        count += calculateLeaps(i, dp)  ;
    }

    dp[n] = count ;
    return count ;

}
int main() {
    int n = 4 ;

    int dp[n+1] = {0} ;

    cout<<calculateLeaps(n,dp) ;

    return 0;

}
```

3.让我们把这个问题分成几个小的子问题。猴子必须踩最后一步，前 N-1 步是可选的。猴子在到达顶阶之前可以踩 0 级台阶，这是最大的一次登顶。或者可以决定中间只踩一次，可以通过 n-1 种方式[ <sup>(N-1)</sup> C <sub>1</sub> ]实现。依此类推，在 <sup>(N-1)</sup> C <sub>2</sub> 方式中，只需踩 2 级台阶就能登顶。放在一起..
F(N)=<sup>(N-1)</sup>C<sub>0</sub>+<sup>(N-1)</sup>C<sub>1</sub>+<sup>(N-1)</sup>C<sub>2</sub>+…+<sup>(N-1)</sup>C<sub>(N-2)</sub>+<sup>(N-1)</sup>C【T27
= 2^(n-1)

## C++

```
// C++ program to count total number of ways
// to reach n-th stair with all jumps allowed
#include <bits/stdc++.h>
using namespace std;

     int calculateLeaps(int n)
    {
        if (n == 0)
            return 1;
        return (1 << (n - 1));
    }

// Driver code
int main()
{
    int calculateLeaps(int);
    std::cout << calculateLeaps(4) << std::endl;
    return 0;
}

// This code is contributed by shivanisinghss2110.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total number of ways
// to reach n-th stair with all jumps allowed
class GFG {
    static int calculateLeaps(int n)
    {
        if (n == 0)
            return 1;
        return (1 << (n - 1));
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(calculateLeaps(4));
    }
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python3 program to count
# total number of ways
# to reach n-th stair with
# all jumps allowed

def calculateLeaps(n):
    if (n == 0):
        return 1;
    return (1 << (n - 1));

# Driver code
print(calculateLeaps(4));

# This code is contributed
# by mits
```

## C#

```
// C# program to count total number of ways
// to reach n-th stair with all jumps allowed
using System;

class GFG {

    // Function to calculate leaps
    static int calculateLeaps(int n)
    {
        if (n == 0)
            return 1;
        return (1 << (n - 1));
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(calculateLeaps(4));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count total
// number of ways to reach n-th
// stair with all jumps allowed

// Function to calculate leaps
function calculateLeaps($n)
{
    if ($n == 0)
        return 1;
    return (1 << ($n - 1));
}

// Driver code
echo calculateLeaps(4);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// javascript program to count total number of ways
// to reach n-th stair with all jumps allowed

function calculateLeaps(n)
{
    if (n == 0)
        return 1;
    return (1 << (n - 1));
}

// Driver code
document.write(calculateLeaps(4));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
8
```

本文由 **Partha Pratim Mallik** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。