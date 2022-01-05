# 求数列第 n 项的程序-1，2，11，26，47……

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-1-2-11-26-47/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-series-1-2-11-26-47/)

给定一个数字 N，任务是找到这个数列的第 N 项:

```
-1, 2, 11, 26, 47, 74, .....
```

**例:**

```
Input: 3
Output: 11
Explanation:
when N = 3
Nth term = ( (3 * N * N) - (6 * N) + 2 )
         = ( (3 * 3 * 3) - (6 * 3) + 2 )
         = 11

Input: 9
Output: 191
```

**方法:**
给定序列的第 n 项可以概括为:

```
Nth term of the series : ( (3 * N * N) - (6 * N) + 2 )
```

下面是上面问题的实现:
**程序:**

## C++

```
// CPP program to find N-th term of the series:       
// 9, 23, 45, 75, 113, 159......         

#include <iostream>;
using namespace std;   
// calculate Nth term of series   
int nthTerm(int N)   
{   
    return ((3 * N * N) - (6 * N) + 2);   
}   

// Driver Function   
int main()   
{   

    // Get the value of N   
    int N = 3;   

    // Find the Nth term   
    // and print it   
    cout << nthTerm(N);   

    return 0;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th term of the series:
// 9, 23, 45, 75, 113, 159......
 class GFG {

    // calculate Nth term of series
    static int nthTerm(int N)
    {
        return ((3 * N * N) - (6 * N) + 2);
    }

    // Driver code
    public static void main(String[] args) {
        int N = 3;

        // Find the Nth term
        // and print it
        System.out.println(nthTerm(N));
    }
}

// This code is contributed by bilal-hungund
```

## 蟒蛇 3

```
# Python3 program to find N-th term
# of the series:
# 9, 23, 45, 75, 113, 159......

def nthTerm(N):

    #calculate Nth term of series
    return ((3 * N * N) - (6 * N) + 2);

# Driver Code
if __name__=='__main__':
    n = 3

    #Find the Nth term
    # and print it
    print(nthTerm(n))

# this code is contributed by bilal-hungund
```

## C#

```
// C# program to find N-th term of the series:
// 9, 23, 45, 75, 113, 159......
using System;
class GFG
{

// calculate Nth term of series
static int nthTerm(int N)
{
    return ((3 * N * N) - (6 * N) + 2);
}

// Driver code
public static void Main()
{
    int N = 3;

    // Find the Nth term
    // and print it
    Console.WriteLine(nthTerm(N));
}
}

// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find N-th term of
// the series: 9, 23, 45, 75, 113, 159......

// calculate Nth term of series
function nthTerm($N)
{
    return ((3 * $N * $N) -
            (6 * $N) + 2);
}

// Driver Code

// Get the value of N
$N = 3;

// Find the Nth term
// and print it
echo nthTerm($N);

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term of the series:
// 9, 23, 45, 75, 113, 159......

    // calculate Nth term of series
    function nthTerm(N)
    {
        return ((3 * N * N) - (6 * N) + 2);
    }

    // Driver Function

    // Get the value of N
    let N = 3;

    // Find the Nth term
    // and print it
    document.write(nthTerm(N)); 

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
11
```

**时间复杂度:** O(1)