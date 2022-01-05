# 一个人最多只能和一个人成对时的配对数

> 原文:[https://www . geesforgeks . org/counting-pairs-person-can-form-pair-one/](https://www.geeksforgeeks.org/counting-pairs-person-can-form-pair-one/)

考虑一下[极客练习](https://practice.geeksforgeeks.org/)上的编码竞赛。现在他们是参加比赛的不同参与者**。一个参与者最多可以与一个其他参与者配对。我们需要计算 **n** 参与者参与编码竞赛的方式数量。
**举例:**** 

```
Input : n = 2
Output : 2
2 shows that either both participant 
can pair themselves in one way or both 
of them can remain single.

Input : n = 3 
Output : 4
One way : Three participants remain single
Three More Ways : [(1, 2)(3)], [(1), (2,3)]
and [(1,3)(2)]
```

**1)每个参与者可以与另一个参与者配对，也可以保持单身。
2)让我们考虑 **X-th** 参与者，他可以保持单身或者
他可以与来自**【1，X-1】**的人配对。** 

## **C++**

```
// Number of ways in which participant can take part.
#include<iostream>
using namespace std;

int numberOfWays(int x)
{
    // Base condition
    if (x==0 || x==1)    
        return 1;

    // A participant can choose to consider
    // (1) Remains single. Number of people
    //     reduce to (x-1)
    // (2) Pairs with one of the (x-1) others.
    //     For every pairing, number of people
    //     reduce to (x-2).
    else
        return numberOfWays(x-1) +
               (x-1)*numberOfWays(x-2);
}

// Driver code
int main()
{
    int x = 3;
    cout << numberOfWays(x) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Number of ways in which
// participant can take part.
import java.io.*;

class GFG {

static int numberOfWays(int x)
{
    // Base condition
    if (x==0 || x==1)    
        return 1;

    // A participant can choose to consider
    // (1) Remains single. Number of people
    //     reduce to (x-1)
    // (2) Pairs with one of the (x-1) others.
    //     For every pairing, number of people
    //     reduce to (x-2).
    else
        return numberOfWays(x-1) +
            (x-1)*numberOfWays(x-2);
}

// Driver code
public static void main (String[] args) {
int x = 3;
System.out.println( numberOfWays(x));

    }
}

// This code is contributed by vt_m.
```

## **蟒蛇 3**

```
# Python program to find Number of ways
# in which participant can take part.

# Function to calculate number of ways.
def numberOfWays (x):

    # Base condition
    if x == 0 or x == 1:
        return 1

    # A participant can choose to consider
    # (1) Remains single. Number of people
    # reduce to (x-1)
    # (2) Pairs with one of the (x-1) others.
    # For every pairing, number of people
    # reduce to (x-2).
    else:
        return (numberOfWays(x-1) +
              (x-1) * numberOfWays(x-2))

# Driver code
x = 3
print (numberOfWays(x))

# This code is contributed by "Sharad_Bhardwaj"
```

## **C#**

```
// Number of ways in which
// participant can take part.
using System;

class GFG {

    static int numberOfWays(int x)
    {

        // Base condition
        if (x == 0 || x == 1)
            return 1;

        // A participant can choose to
        // consider (1) Remains single.
        // Number of people reduce to
        // (x-1) (2) Pairs with one of
        // the (x-1) others. For every
        // pairing, number of people
        // reduce to (x-2).
        else
            return numberOfWays(x - 1) +
            (x - 1) * numberOfWays(x - 2);
    }

    // Driver code
    public static void Main ()
    {
        int x = 3;

        Console.WriteLine(numberOfWays(x));
    }
}

// This code is contributed by vt_m.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// Number of ways in which
// participant can take part.

function numberOfWays($x)
{
    // Base condition
    if ($x == 0 || $x == 1)    
        return 1;

    // A participant can choose
    // to consider (1) Remains single.
    // Number of people reduce to (x-1)
    // (2) Pairs with one of the (x-1)
    // others. For every pairing, number
    // of peopl reduce to (x-2).
    else
        return numberOfWays($x - 1) +
            ($x - 1) * numberOfWays($x - 2);
}

// Driver code
$x = 3;
echo numberOfWays($x);

// This code is contributed by Sam007
?>
```

## **java 描述语言**

```
<script>
// Number of ways in which
// participant can take part.

    function numberOfWays(x)
    {

        // Base condition
        if (x == 0 || x == 1)
            return 1;

        // A participant can choose to consider
        // (1) Remains single. Number of people
        // reduce to (x-1)
        // (2) Pairs with one of the (x-1) others.
        // For every pairing, number of people
        // reduce to (x-2).
        else
            return numberOfWays(x - 1) + (x - 1) * numberOfWays(x - 2);
    }

    // Driver code
    var x = 3;
    document.write(numberOfWays(x));

// This code is contributed by gauravrajput1
</script>
```

****输出:**** 

```
4
```

**由于存在重叠子问题，我们可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。** 

## **C++**

```
// Number of ways in which participant can take part.
#include<iostream>
using namespace std;

int numberOfWays(int x)
{
    int dp[x+1];
    dp[0] = dp[1] = 1;

    for (int i=2; i<=x; i++)
       dp[i] = dp[i-1] + (i-1)*dp[i-2];

    return dp[x];
}

// Driver code
int main()
{
    int x = 3;
    cout << numberOfWays(x) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Number of ways in which
// participant can take part.
import java.io.*;
class GFG {

static int numberOfWays(int x)
{
    int dp[] = new int[x+1];
    dp[0] = dp[1] = 1;

    for (int i=2; i<=x; i++)
    dp[i] = dp[i-1] + (i-1)*dp[i-2];

    return dp[x];
}

// Driver code
public static void main (String[] args) {
int x = 3;
System.out.println(numberOfWays(x));

    }
}
// This code is contributed by vipinyadav15799
```

## **蟒蛇 3**

```
# Python program to find Number of ways
# in which participant can take part.

# Function to calculate number of ways.
def numberOfWays (x):

    dp=[]
    dp.append(1)
    dp.append(1)
    for i in range(2,x+1):
        dp.append(dp[i-1]+(i-1)*dp[i-2])
    return(dp[x])

# Driver code
x = 3
print (numberOfWays(x))

# This code is contributed by "Sharad_Bhardwaj"
```

## **C#**

```
// Number of ways in which
// participant can take part.
using System;

class GFG {

    static int numberOfWays(int x)
    {
        int []dp = new int[x+1];
        dp[0] = dp[1] = 1;

        for (int i = 2; i <= x; i++)
            dp[i] = dp[i - 1] +
                 (i - 1) * dp[i - 2];

        return dp[x];
    }

    // Driver code
    public static void Main ()
    {
        int x = 3;

        Console.WriteLine(numberOfWays(x));
    }
}

// This code is contributed by vt_m. 
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program for Number of ways
// in which participant can take part.

function numberOfWays($x)
{

    $dp[0] = 1;
    $dp[1] = 1;
    for ($i = 2; $i <= $x; $i++)
    $dp[$i] = $dp[$i - 1] + ($i - 1) *
                         $dp[$i - 2];

    return $dp[$x];
}

    // Driver code
    $x = 3;
    echo numberOfWays($x) ;

// This code is contributed by Sam007
?>
```

## **java 描述语言**

```
<script>
// Number of ways in which
// participant can take part.

    function numberOfWays( x)
    {
        let dp = Array(x + 1).fill(0);
        dp[0] = dp[1] = 1;

        for ( i = 2; i <= x; i++)
            dp[i] = dp[i - 1] + (i - 1) * dp[i - 2];

        return dp[x];
    }

    // Driver code
    let x = 3;
    document.write(numberOfWays(x));

// This code is contributed by gauravrajput1
</script>
```

**输出:** 

```
4
```

**本文由[**nikun Ji _ Agarwal**](https://auth.geeksforgeeks.org/profile.php?user=nikunj_agarwal&list=practice)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**