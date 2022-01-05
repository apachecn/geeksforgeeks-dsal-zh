# O(1)复杂度中前 n 个奇数的和

> 原文:[https://www . geesforgeks . org/sum-first-n-奇数-o1-complexity/](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)

给定奇数序列
1，3，5，7，9，11，13，15，17，19，21，23，…
求前 n 个奇数的和
例:

```
Input : n = 2
Output : 4
Sum of first two odd numbers is 1 + 3 = 4.

Input : 5
Output : 25
Sum of first 5 odd numbers is 1 + 3 + 5 +
7 + 9 = 25
```

一个**简单的解决方案**是迭代所有奇数。

## C++

```
// A naive CPP program to find sum of
// first n odd numbers
#include <iostream>
using namespace std;

// Returns the sum of first
// n odd numbers
int oddSum(int n)
{
    int sum = 0, curr = 1;
    for (int i = 0; i < n; i++) {
        sum += curr;
        curr += 2;
    }
    return sum;
}

// Driver function
int main()
{
    int n = 20;
    cout << " Sum of first " << n
         << " Odd Numbers is: " << oddSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// first n odd numbers
import java.util.*;

class Odd
{  
    // Returns the sum of first
    // n odd numbers
    public static int oddSum(int n)
    {
        int sum = 0, curr = 1;
        for (int i = 0; i < n; i++) {
            sum += curr;
            curr += 2;
        }
        return sum;
    }

    // driver function
    public static void main(String[] args)
    {
        int n = 20;
        System.out.println(" Sum of first "+ n
        +" Odd Numbers is: "+oddSum(n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program to find sum
# of first n odd numbers

def oddSum(n) :
    sum = 0
    curr = 1
    i = 0
    while i < n:
        sum = sum + curr
        curr = curr + 2
        i = i + 1
    return sum

# Driver Code
n = 20
print (" Sum of first" , n, "Odd Numbers is: ",
                                oddSum(n) )

# This code is contributed by rishabh_jain
```

## C#

```
// C# program to find sum of
// first n odd numbers
using System;

class GFG {

    // Returns the sum of first
    // n odd numbers
    public static int oddSum(int n)
    {
        int sum = 0, curr = 1;
        for (int i = 0; i < n; i++) {
            sum += curr;
            curr += 2;
        }

        return sum;
    }

    // driver function
    public static void Main()
    {
        int n = 20;
        Console.WriteLine(" Sum of first " + n
            + " Odd Numbers is: " + oddSum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive PHP program to find sum of
// first n odd numbers

// Returns the sum of first
// n odd numbers
function oddSum($n)
{
    $sum = 0; $curr = 1;
    for ($i = 0; $i < $n; $i++)
    {
        $sum += $curr;
        $curr += 2;
    }
    return $sum;
}

// Driver Code
$n = 20;
echo " Sum of first ", $n
     , " Odd Numbers is: ", oddSum($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// A naive Javascript program to find sum of
// first n odd numbers

// Returns the sum of first
// n odd numbers
function oddSum(n)
{
    let sum = 0; curr = 1;
    for (let i = 0; i < n; i++)
    {
        sum += curr;
        curr += 2;
    }
    return sum;
}

// Driver Code
let n = 20;
document.write(" Sum of first " + n
     + " Odd Numbers is: " + oddSum(n));

// This code is contributed by gfgking.
</script>
```

输出:

```
Sum of first 20 odd numbers is 400
```

时间复杂度:O(n)
辅助空间:O(1)

一个**高效的解决方案**就是用直接公式。为了求前 n 个奇数的和，我们可以应用奇数定理，它规定前 n 个奇数的和等于 n 的平方

> ∑(2i–1)= n<sup>2</sup>其中 I 从 1 到 n 变化

**设 n = 10，因此前 10 个奇数之和为**
1+3+5+7+9+11+13+15+17+19 = 100
**如果我们应用奇数定理:**
前 10 个奇数之和= n * n = 10 * 10 = 100。
以下是上述方法的实施:

## C++

```
// Efficient program to find sum of
// first n odd numbers
#include <iostream>
using namespace std;

// Returns the sum of first
// n odd numbers
int oddSum(int n)
{
    return (n * n);
}

// Driver function
int main()
{
    int n = 20;
    cout << " Sum of first " << n
         << " Odd Numbers is: " << oddSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// first n odd numbers
import java.util.*;

class Odd
{  
    // Returns the sum of first
    // n odd numbers
    public static int oddSum(int n)
    {
        return (n * n);
    }

    // driver function
    public static void main(String[] args)
    {
        int n = 20;
        System.out.println(" Sum of first "+ n
        +" Odd Numbers is: "+oddSum(n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program to find sum
# of first n odd numbers

def oddSum(n) :
    return (n * n);

# Driver Code
n = 20
print (" Sum of first" , n, "Odd Numbers is: ",
                               oddSum(n) )

# This code is contributed by rishabh_jain
```

## C#

```
// C# program to find sum of
// first n odd numbers
using System;

class GFG {

    // Returns the sum of first
    // n odd numbers
    public static int oddSum(int n)
    {
        return (n * n);
    }

    // driver function
    public static void Main()
    {
        int n = 20;
        Console.WriteLine(" Sum of first " + n
            + " Odd Numbers is: " + oddSum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient program to find sum of
// first n odd numbers

// Returns the sum of first
// n odd numbers
function oddSum($n)
{
    return ($n * $n);
}

// Driver Code
$n = 20;
echo " Sum of first " , $n,
     " Odd Numbers is: ", oddSum($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find sum of first n odd numbers

    // Returns the sum of first
    // n odd numbers
    function oddSum(n)
    {
        return (n * n);
    }

    let n = 20;
    document.write(" Sum of first " + n
                      + " Odd Numbers is: " + oddSum(n));

    // This code is contributed by divyesh072019.
</script>
```

输出:

```
Sum of first 20 odd numbers is 400
```

时间复杂度:O(1)
辅助空间:O(1)
**如何工作？**
我们可以用数学归纳法来证明。我们知道 n = 1 和 n = 2 是真的，因为和分别是 1 和 4 (1 + 3)。

```
Let it be true for n = k-1.

Sum of first k odd numbers = 
  Sum of first k-1 odd numbers + k'th odd number
= (k-1)*(k-1) + (2k - 1)
= k*k
```