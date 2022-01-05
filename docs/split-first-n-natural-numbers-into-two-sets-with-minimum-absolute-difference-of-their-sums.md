# 将前 N 个自然数拆分为两个集合，其和的绝对差最小

> 原文:[https://www . geeksforgeeks . org/将第一个 n 个自然数拆分为两个具有最小绝对和差的集合/](https://www.geeksforgeeks.org/split-first-n-natural-numbers-into-two-sets-with-minimum-absolute-difference-of-their-sums/)

给定一个整数 **N** ，将第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)分成两组，使它们之和的绝对差最小。任务是打印可以获得的最小绝对差值。

**示例**:

> **输入:** N = 5
> **输出:** 1
> **解释:**
> 将前 N (= 5)个自然数拆分成集合{1，2，5}(和= 8)和{3，4}(和= 7)。
> 因此，要求的输出为 1。
> 
> **输入:**N = 6
> T3】输出: 1

**天真方法**:这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

*   初始化两个变量，比如 **sumSet1** 和 **sumSet2** 来存储两个集合的元素之和。
*   先遍历 **N** 个自然数，从 **N** 到 **1** 。对于每个数字，检查 set1 中元素的当前总和是否小于或等于 set2 中元素的总和。如果发现为真，将当前遍历的号码加入**集合 1** 并更新**集合 1** 。
*   否则，将当前自然数的值加到**集合 2** 并更新**集合 2** 。
*   最后，打印**ABS(sumset 1–sumset 2)**作为所需答案。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
int minAbsDiff(int N)
{
    // Stores the sum of
    // elements of set1
    int sumSet1 = 0;

    // Stores the sum of
    // elements of set2
    int sumSet2 = 0;

    // Traverse first N
    // natural numbers
    for (int i = N; i > 0; i--) {

        // Check if sum of elements of
        // set1 is less than or equal
        // to sum of elements of set2
        if (sumSet1 <= sumSet2) {
            sumSet1 += i;
        }
        else {
            sumSet2 += i;
        }
    }
    return abs(sumSet1 - sumSet2);
}

// Driver Code
int main()
{
    int N = 6;
    cout << minAbsDiff(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
static int minAbsDiff(int N)
{

    // Stores the sum of
    // elements of set1
    int sumSet1 = 0;

    // Stores the sum of
    // elements of set2
    int sumSet2 = 0;

    // Traverse first N
    // natural numbers
    for(int i = N; i > 0; i--)
    {

        // Check if sum of elements of
        // set1 is less than or equal
        // to sum of elements of set2
        if (sumSet1 <= sumSet2)
        {
            sumSet1 += i;
        }
        else
        {
            sumSet2 += i;
        }
    }
    return Math.abs(sumSet1 - sumSet2);
}

// Driver code
public static void main (String[] args)
{
    int N = 6;

    System.out.println(minAbsDiff(N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to split the first N
# natural numbers into two sets
# having minimum absolute
# difference of their sums
def minAbsDiff(N):

    # Stores the sum of
    # elements of set1
    sumSet1 = 0

    # Stores the sum of
    # elements of set2
    sumSet2 = 0

    # Traverse first N
    # natural numbers
    for i in reversed(range(N + 1)):

        # Check if sum of elements of
        # set1 is less than or equal
        # to sum of elements of set2
        if sumSet1 <= sumSet2:
           sumSet1 = sumSet1 + i
        else:
           sumSet2 = sumSet2 + i

    return abs(sumSet1 - sumSet2)

# Driver Code
N = 6

print(minAbsDiff(N))

# This code is contributed by sallagondaavinashreddy7
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
static int minAbsDiff(int N)
{

    // Stores the sum of
    // elements of set1
    int sumSet1 = 0;

    // Stores the sum of
    // elements of set2
    int sumSet2 = 0;

    // Traverse first N
    // natural numbers
    for(int i = N; i > 0; i--)
    {

        // Check if sum of elements of
        // set1 is less than or equal
        // to sum of elements of set2
        if (sumSet1 <= sumSet2)
        {
            sumSet1 += i;
        }
        else
        {
            sumSet2 += i;
        }
    }
    return Math.Abs(sumSet1 - sumSet2);
}

// Driver code
static void Main()
{
    int N = 6;

    Console.Write(minAbsDiff(N));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
function minAbsDiff(N)
{

    // Stores the sum of
    // elements of set1
    var sumSet1 = 0;

    // Stores the sum of
    // elements of set2
    var sumSet2 = 0;

    // Traverse first N
    // natural numbers
    for(i = N; i > 0; i--)
    {

        // Check if sum of elements of
        // set1 is less than or equal
        // to sum of elements of set2
        if (sumSet1 <= sumSet2)
        {
            sumSet1 += i;
        }
        else
        {
            sumSet2 += i;
        }
    }
    return Math.abs(sumSet1 - sumSet2);
}

// Driver code
var N = 6;

document.write(minAbsDiff(N));

// This code is contributed by umadevi9616

</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法**:优化上述方法的想法基于以下观察:

> 将任意 4 个连续整数拆分成 2 个集合，它们的和的最小绝对差等于 0。
> 
> 数学证明:
> 考虑 4 个连续整数{a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> ， a<sub>4</sub>}
> a<sub>4</sub>= a<sub>3</sub>+1
> a<sub>1</sub>= a<sub>2</sub>–1
> =>a<sub>4</sub>+<sub>T23】a<sub>1</sub>= a<sub>3</sub>+1+a<sub>2</sub>–1</sub>

按照以下步骤解决问题:

*   如果 **N % 4 == 0** 或 **N % 4 == 3** ，则打印 **0** 。
*   否则，打印 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
int minAbsDiff(int N)
{
    if (N % 4 == 0 || N % 4 == 3) {
        return 0;
    }
    return 1;
}

// Driver Code
int main()
{
    int N = 6;
    cout << minAbsDiff(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
static int minAbsDiff(int N)
{
    if (N % 4 == 0 || N % 4 == 3)
    {
        return 0;
    }
    return 1;
}

// Driver Code
public static void main (String[] args)
{
    int N = 6;

    System.out.println(minAbsDiff(N));
}
}

// This code is contributed by sallagondaavinashreddy7
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to split the first N
# natural numbers into two sets
# having minimum absolute
# difference of their sums
def minAbsDiff(N):

    if (N % 4 == 0 or N % 4 == 3):
        return 0

    return 1

# Driver Code
N = 6

print(minAbsDiff(N))

# This code is contributed by sallagondaavinashreddy7
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to split the first N
// natural numbers into two sets
// having minimum absolute
// difference of their sums
static int minAbsDiff(int N)
{
  if (N % 4 == 0 ||
      N % 4 == 3)
  {
    return 0;
  }
  return 1;
}

// Driver Code
public static void Main(String[] args)
{
  int N = 6;
  Console.WriteLine(minAbsDiff(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach   
// Function to split the first N
    // natural numbers into two sets
    // having minimum absolute
    // difference of their sums
    function minAbsDiff(N) {
        if (N % 4 == 0 || N % 4 == 3) {
            return 0;
        }
        return 1;
    }

    // Driver Code

        var N = 6;

        document.write(minAbsDiff(N));

// This code contributed by gauravrajput1
</script>
```

**Output**

```
1
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)