# N 次转身后，球会以多少种方式回到第一个男孩身边

> 原文:[https://www . geesforgeks . org/in-how-how-the-ball-to-return-to-first-boy-on-turns/](https://www.geeksforgeeks.org/in-how-many-ways-the-ball-will-come-back-to-the-first-boy-after-n-turns/)

四个男孩正在玩球游戏。在每一回合中，玩家(当前拥有球)随机将球传给不同的**玩家。鲍勃总是开始游戏。任务是找出在 **N** 传球后，球会以多少种方式回到鲍勃手中。
**例:**** 

> ****输入:** N = 3
> **输出:** 6
> 以下是所有可能的方式:
> Bob->boy 1->boy 2->Bob
> Bob->boy 1->boy 3->Bob
> Bob->boy 2->boy 1->Bob
> Bob->boy 2->boy 3-【T36**

****进场:**让 **N** 传球后回到鲍勃的序列数为 **P(N)** 。这是两种情况，要么通过**N–2**是鲍勃，要么不是。注意鲍勃不能在**(N–1)**传球时拿球，因为那样他就不会在**N**传球时拿球。** 

1.  ****情况 1:** 如果传球**N–2**给鲍勃，那么传球**N–1**可以给其他 3 个男孩中的任何一个。因此，此类序列的数量为**3 * P(N–2)**。**
2.  ****情况 2:** 如果传球**N–2**不是传给鲍勃，那么传球**N–1**就是传给除了鲍勃之外的两个男孩中的一个，以及那个拿到球的男孩。所以，用 Bob 代替接收方通过**N–1**，得到一个唯一的**N–1**序列。所以，这样的序列数是**2 * P(N–1)**。**

**因此递归关系为**P(N)= 2 * P(N–1)+3 * P(N–2)**，其中 **P(0) = 1** 和 **P(1) = 0** 。
求解递归关系后，**P(N)=(3<sup>N</sup>+3 *(1<sup>N</sup>)/4**
以下是上述方法的实现:** 

## **C++**

```
// Function to return the number of
// sequences that get back to Bob
#include <bits/stdc++.h>
using namespace std;

int numSeq(int n)
{
    return (pow(3, n) + 3 * pow(-1, n)) / 4;
}

// Driver code
int main()
{
    int N = 10;
    printf("%d", numSeq(N));
    return 0;
}

// This code is contributed by Mohit kumar
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Function to return the number of
// sequences that get back to Bob
import java.util.*;

class GFG
{

static int numSeq(int n)
{
    return (int) ((Math.pow(3, n) + 3 *
                    Math.pow(-1, n)) / 4);
}

// Driver code
public static void main(String[] args)
{
    int N = 10;
    System.out.printf("%d", numSeq(N));
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Function to return the number of
# sequences that get back to Bob
def numSeq(n):
    return (pow(3, n) + 3 * pow(-1, n))//4

# Driver code
N = 10
print(numSeq(N))
```

## **C#**

```
// C# implementation of the above approach
using System;

// Function to return the number of
// sequences that get back to Bob
class GFG
{

    static int numSeq(int n)
    {
        return (int) ((Math.Pow(3, n) + 3 *
                       Math.Pow(-1, n)) / 4);
    }

    // Driver code
    public static void Main()
    {
        int N = 10;
        Console.WriteLine(numSeq(N));
    }
}

// This code is contributed by AnkitRai01
```

## **java 描述语言**

```
<script>

// Function to return the number of
// sequences that get back to Bob
function numSeq(n)
{
    return  Math.floor((Math.pow(3, n) + 3 * Math.pow(-1, n)) / 4);
}

// Driver code

    let N = 10;
    document.write(numSeq(N));

// This code is contributed by Surbhi Tyagi.

</script>
```

****Output:** 

```
14763
```**