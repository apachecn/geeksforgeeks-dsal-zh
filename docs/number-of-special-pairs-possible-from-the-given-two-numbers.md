# 给定两个数字中可能的特殊对的数量

> 原文:[https://www . geeksforgeeks . org/特殊对数-从给定的两个数字中可能得到的数/](https://www.geeksforgeeks.org/number-of-special-pairs-possible-from-the-given-two-numbers/)

给定两个数字 A，B，任务是找出 A，B 的特殊对的数字，两个数字 A，B 的特殊对是满足两个给定条件的一对数字 X，Y–**A = X | Y，B = X & Y.**
**示例:**

```
Input: A = 3, B = 0
Output: 2
(0, 3), (1, 2) will satisfy the conditions

Input:  A = 5, B = 7
Output: 0
```

**方法:**这里的关键观察是，如果我们希望两个数字 X，Y 的 or 等于 A，那么 X，Y 都必须小于或等于 A，如果有人大于 A，那么 OR 就不会等于 A，这将给出我们的循环将终止的极限，剩下的我们将尝试检查两对是否满足给定的条件，然后我们将递增计数器。
以下是所需的实现:

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Function to count the pairs
int countPairs(int A, int B)
{

    // Variable to store a number of special pairs
    int cnt = 0;

    for (int i = 0; i <= A; ++i) {
        for (int j = i; j <= A; ++j) {
            // Calculating AND of i, j
            int AND = i & j;

            // Calculating OR of i, j
            int OR = i | j;

            // If the conditions are met,
            // then increment the count of special pairs
            if (OR == A and AND == B) {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver code
int main()
{
    int A = 3, B = 0;
    cout << countPairs(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to count the pairs
static int countPairs(int A, int B)
{

    // Variable to store a number
    // of special pairs
    int cnt = 0;

    for (int i = 0; i <= A; ++i)
    {
        for (int j = i; j <= A; ++j)
        {
            // Calculating AND of i, j
            int AND = i & j;

            // Calculating OR of i, j
            int OR = i | j;

            // If the conditions are met,
            // then increment the count
            // of special pairs
            if (OR == A && AND == B)
            {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver code
public static void main(String [] args)
{
    int A = 3, B = 0;
    System.out.println(countPairs(A, B));
}
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above
# approach

# Function to count the pairs
def countPairs(A,B):

    # Variable to store a number
    # of special pairs
    cnt=0
    for i in range(0,A+1):
        for j in range(i,A+1):

            # Calculating AND of i, j
            AND = i&j
            OR = i|j

            # If the conditions are met,
            # then increment the count of
            # special pairs
            if(OR==A and AND==B):
                cnt +=1
    return cnt

if __name__=='__main__':
    A = 3
    B = 0
    print(countPairs(A,B))

# This code is contributed by
# Shrikant13
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to count the pairs
static int countPairs(int A, int B)
{

    // Variable to store a number
    // of special pairs
    int cnt = 0;

    for (int i = 0; i <= A; ++i)
    {
        for (int j = i; j <= A; ++j)
        {
            // Calculating AND of i, j
            int AND = i & j;

            // Calculating OR of i, j
            int OR = i | j;

            // If the conditions are met,
            // then increment the count
            // of special pairs
            if (OR == A && AND == B)
            {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver code
public static void Main()
{
    int A = 3, B = 0;
    Console.WriteLine(countPairs(A, B));
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to count the pairs
function countPairs($A, $B)
{

    // Variable to store a number
    // of special pairs
    $cnt = 0;

    for ($i = 0; $i <= $A; ++$i)
    {
        for ($j = $i; $j <= $A; ++$j)
        {
            // Calculating AND of i, j
            $AND = $i & $j;

            // Calculating OR of i, j
            $OR = $i | $j;

            // If the conditions are met,
            // then increment the count
            // of special pairs
            if ($OR == $A && $AND == $B)
            {
                $cnt++;
            }
        }
    }
    return $cnt;
}

// Driver code
$A = 3;
$B = 0;
echo countPairs($A, $B);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to count the pairs
function countPairs(A, B) {

    // Variable to store a number of special pairs
    let cnt = 0;

    for (let i = 0; i <= A; ++i) {
        for (let j = i; j <= A; ++j) {
            // Calculating AND of i, j
            let AND = i & j;

            // Calculating OR of i, j
            let OR = i | j;

            // If the conditions are met,
            // then increment the count of special pairs
            if (OR == A && AND == B) {
                cnt++;
            }
        }
    }
    return cnt;
}

// Driver code

let A = 3, B = 0;
document.write(countPairs(A, B));

// This code is contributed by _saurabh_jaiswal
<script>
```

**Output:** 

```
2
```