# 范围[L，R]

内所有可能的同素不同元素对

> 原文:[https://www . geesforgeks . org/all-可能性-co-prime-distinct-element-pairs-in-a-range-l-r/](https://www.geeksforgeeks.org/all-possible-co-prime-distinct-element-pairs-within-a-range-l-r/)

给定一个范围[L，R]，任务是从这个范围中找到所有可能的同素对，这样一个元素不会出现在一个以上的对中。
**例:**

```
Input : L=1 ; R=6
Output : 3
The answer is 3 [(1, 2) (3, 4) (5, 6)], 
all these pairs have GCD 1.

Input : L=2 ; R=4
Output : 1
The answer is 1 [(2, 3) or (3, 4)] 
as '3' can only be chosen for a single pair.
```

**方法:**对问题的关键观察是，差为‘1’的数总是彼此相对素数，即同素数。
这一对的 GCD 始终为‘1’。因此，答案将是(R-L+1)/2 [(范围内的总数)/ 2 ]

*   如果 R-L+1 是奇数，那么剩下的一个元素不能成对。
*   如果 R-L+1 是偶数，那么所有元素都可以成对。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to count possible pairs
void CountPair(int L, int R)
{

    // total count of numbers in range
    int x = (R - L + 1);

    // Note that if 'x' is odd then
    // there will be '1' element left
    // which can't form a pair

    // printing count of pairs
    cout << x / 2 << "\n";
}

// Driver code
int main()
{

    int L, R;

    L = 1, R = 8;
    CountPair(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java implementation of the approach
import java.util.*;
class solution
{

// Function to count possible pairs
static void CountPair(int L, int R)
{

    // total count of numbers in range
    int x = (R - L + 1);

    // Note that if 'x' is odd then
    // there will be '1' element left
    // which can't form a pair

    // printing count of pairs
    System.out.println(x / 2 + "\n");
}

// Driver code
public static void main(String args[])
{

    int L, R;

    L = 1; R = 8;
    CountPair(L, R);

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach

# Function to count possible
# pairs
def CountPair(L,R):

    # total count of numbers
    # in range
    x=(R-L+1)

    # Note that if 'x' is odd then
    # there will be '1' element left
    # which can't form a pair
    # printing count of pairs
    print(x//2)

# Driver code
if __name__=='__main__':
    L,R=1,8
    CountPair(L,R)

# This code is contributed by
# Indrajit Sinha.
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to count possible pairs
static void CountPair(int L, int R)
{

    // total count of numbers in range
    int x = (R - L + 1);

    // Note that if 'x' is odd then
    // there will be '1' element left
    // which can't form a pair

    // printing count of pairs
    Console.WriteLine(x / 2 + "\n");
}

// Driver code
public static void Main()
{
    int L, R;

    L = 1; R = 8;
    CountPair(L, R);
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count possible pairs
function CountPair($L, $R)
{

    // total count of numbers in range
    $x = ($R - $L + 1);

    // Note that if 'x' is odd then
    // there will be '1' element left
    // which can't form a pair

    // printing count of pairs
    echo $x / 2, "\n";
}

// Driver code
$L = 1;
$R = 8;
CountPair($L, $R);

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to count possible pairs
function CountPair(L, R)
{

    // total count of numbers in range
    let x = (R - L + 1);

    // Note that if 'x' is odd then
    // there will be '1' element left
    // which can't form a pair

    // printing count of pairs
   document.write(x / 2 + "<br/>");
}

// driver code

    let L, R;

    L = 1; R = 8;
    CountPair(L, R);

</script>
```

**Output:** 

```
4
```

**复杂度:O(1)**