# 求数列 2、3、10、15、26 的第 n 项。

> 原文:[https://www . geesforgeks . org/find-n 系列术语-2-3-10-15-26/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-2-3-10-15-26/)

给定一个数字 **N** ，任务是找到系列 **2，3，10，15，26 中的**N**项。**
**例:**

```
Input: N = 2
Output: 3
2nd term = (2*2)-1
         = 3

Input: N = 5
Output: 26
5th term = (5*5)+1
         = 26
```

**进场:**

*   级数的第 n 个数由下式得到
    1.  对数字本身求平方。
    2.  如果这个数是奇数，在这个数的平方上加 1。如果数字是偶数，则减去 1
*   由于数列的起始数为 2
    第一项= 2
    第二项=(2 * 2)–1 = 3
    第三项= (3 * 3) + 1 = 10
    第四项=(4 * 4)–1 = 15
    第五项= (5 * 5) + 1 = 26
    以此类推。

*   一般来说，第 n 个数字由公式获得:

![](img/fe7dc8ecff9ac1aab64f40d743a36be1.png)

以下是上述方法的实现:

## C++

```
// C++ program to find Nth term
// of the series 2, 3, 10, 15, 26....

#include <bits/stdc++.h>
using namespace std;

// Function to find Nth term
int nthTerm(int N)
{
    int nth = 0;

    // Nth term
    if (N % 2 == 1)
        nth = (N * N) + 1;
    else
        nth = (N * N) - 1;

    return nth;
}

// Driver Method
int main()
{
    int N = 5;

    cout << nthTerm(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Nth term
// of the series 2, 3, 10, 15, 26....
class GFG
{

// Function to find Nth term
static int nthTerm(int N)
{
    int nth = 0;

    // Nth term
    if (N % 2 == 1)
        nth = (N * N) + 1;
    else
        nth = (N * N) - 1;

    return nth;
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    System.out.print(nthTerm(N) +"\n");

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find Nth term
# of the series 2, 3, 10, 15, 26....

# Function to find Nth term
def nthTerm(N) :
    nth = 0;

    # Nth term
    if (N % 2 == 1) :
        nth = (N * N) + 1;
    else :
        nth = (N * N) - 1;

    return nth;

# Driver Method
if __name__ == "__main__" :
    N = 5;
    print(nthTerm(N)) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find Nth term
// of the series 2, 3, 10, 15, 26....
using System;

class GFG
{

// Function to find Nth term
static int nthTerm(int N)
{
    int nth = 0;

    // Nth term
    if (N % 2 == 1)
        nth = (N * N) + 1;
    else
        nth = (N * N) - 1;

    return nth;
}

// Driver code
public static void Main(String[] args)
{
    int N = 5;

    Console.Write(nthTerm(N) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to find Nth term
    // of the series 2, 3, 10, 15, 26....

    // Function to find Nth term
    function nthTerm(N)
    {
        let nth = 0;

        // Nth term 
        if (N % 2 == 1)
            nth = (N * N) + 1;
        else
            nth = (N * N) - 1;

        return nth;
    }

    let N = 5;
    document.write(nthTerm(N));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
26
```