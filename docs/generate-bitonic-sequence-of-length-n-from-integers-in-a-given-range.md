# 从给定范围内的整数生成长度为 N 的双调和序列

> 原文:[https://www . geesforgeks . org/generate-bit onic-sequence-n-from-in-a-给定范围内的整数/](https://www.geeksforgeeks.org/generate-bitonic-sequence-of-length-n-from-integers-in-a-given-range/)

给定整数 **N** 、 **L** 和 **R** ，任务是从范围**【L，R】**中的整数生成长度为 **N** 的 [**双音素序列**](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/) ，使得第一个元素最大。如果无法创建这样的序列，则打印**-1”**。

> 一个**双音素序列**是一个必须先严格递增再严格递减的序列。

**示例:**

> **输入:** N = 5，L = 3，R = 10
> **输出:** 9，10，9，8，7
> **说明:**序列{9，10，9，8，7}先严格递增后严格递减。
> 
> **输入:** N = 5，L = 2，R = 5
> **输出:** 4，5，4，3，2
> **解释:**
> 【顺序{4，5，4，3，2}先严格递增后严格递减。

**做法:**思路是用一个[德格](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)**T5【这样元素就可以从头到尾加了。按照以下步骤解决问题:**

*   初始化一个[德格](https://www.geeksforgeeks.org/deque-cpp-stl/)来存储结果[双音素序列](https://www.geeksforgeeks.org/bitonic-sort/)的元素。
*   将变量 **i** 初始化为 **0** ，并从**(R–I)**开始在结果列表中添加元素，直到 **i** 小于**(R–L+1)**和**(N–1)**的最小值。
*   在上述步骤之后，如果结果列表的大小小于 **N** ，则从列表的开始向 **L** 添加来自**(R–1)**的添加元素，直到结果列表的大小不变为 **N** 。
*   经过上述步骤后，如果 **N** 大于**(R–L)* 2+1**，则无法构建这样的序列，然后打印**-1”**否则打印存储在**德清**中的序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct bitonic
// sequence of length N from
// integers in the range [L, R]
void bitonicSequence(int num, int lower,
                     int upper)
{

    // If sequence is not possible
    if (num > (upper - lower) * 2 + 1)
    {
        cout << -1;
        return;
    }

    // Store the resultant list
    deque<int> ans;
    deque<int>::iterator j = ans.begin();

    for(int i = 0;
            i < min(upper - lower + 1, num - 1);
            i++)
        ans.push_back(upper - i);

    // If size of deque < n
    for(int i = 0;
            i < num - ans.size();
            i++)

    // Add elements from start
    ans.push_front(upper - i - 1);

    // Print the stored in the list
    cout << '[';
    for(j = ans.begin(); j != ans.end(); ++j)
        cout << ' ' << *j;

    cout << ' ' << ']';
}

// Driver Code
int main()
{
    int N = 5, L = 3, R = 10;

    // Function Call
    bitonicSequence(N, L, R);

    return 0;
}

// This code is contributed by jana_sayantan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to construct bitonic
    // sequence of length N from
    // integers in the range [L, R]
    public static void bitonicSequence(
        int num, int lower, int upper)
    {
        // If sequence is not possible
        if (num > (upper - lower) * 2 + 1) {
            System.out.println(-1);
            return;
        }

        // Store the resultant list
        Deque<Integer> ans
            = new ArrayDeque<>();

        for (int i = 0;
             i < Math.min(upper - lower + 1,
                          num - 1);
             i++)
            ans.add(upper - i);

        // If size of deque < n
        for (int i = 0;
             i < num - ans.size(); i++)

            // Add elements from start
            ans.addFirst(upper - i - 1);

        // Print the stored in the list
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5, L = 3, R = 10;

        // Function Call
        bitonicSequence(N, L, R);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to construct bitonic
# sequence of length N from
# integers in the range [L, R]
def bitonicSequence(num, lower, upper):

    # If sequence is not possible
    if (num > (upper - lower) * 2 + 1):
        print(-1)
        return

    # Store the resultant list
    ans = deque()

    for i in range(min(upper - lower + 1,
                                 num - 1)):
        ans.append(upper - i)

    # If size of deque < n
    for i in range(num - len(ans)):

        # Add elements from start
        ans.appendleft(upper - i - 1)

    # Print the stored in the list
    print(list(ans))

# Driver Code
if __name__ == '__main__':

    N = 5
    L = 3
    R = 10

    # Function Call
    bitonicSequence(N, L, R)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to construct bitonic
// sequence of length N from
// integers in the range [L, R]
public static void bitonicSequence(int num,
                                   int lower,
                                   int upper)
{

    // If sequence is not possible
    if (num > (upper - lower) * 2 + 1)
    {
        Console.WriteLine(-1);
        return;
    }

    // Store the resultant list
    List<int> ans = new List<int>();

    for(int i = 0;
            i < Math.Min(upper - lower + 1,
                           num - 1); i++)
        ans.Add(upper - i);

    // If size of deque < n
    for(int i = 0;
            i < num - ans.Count; i++)

        // Add elements from start
        ans.Insert(0,upper - i - 1);

    // Print the stored in the list
    Console.Write("[");
    foreach(int x in ans)
        Console.Write(x + ", ");

    Console.Write("]");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5, L = 3, R = 10;

    // Function Call
    bitonicSequence(N, L, R);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to construct bitonic
// sequence of length N from
// integers in the range [L, R]
function bitonicSequence(num, lower, upper)
{

    // If sequence is not possible
    if (num > (upper - lower) * 2 + 1)
    {
        document.write( -1);
        return;
    }

    // Store the resultant list
    var ans = [];

    for(var i = 0;
            i < Math.min(upper - lower + 1, num - 1);
            i++)
        ans.push(upper - i);

    // If size of deque < n
    for(var i = 0;
            i < num - ans.length;
            i++)
    {

            // Add elements from start
            ans.splice(0, 0, upper -i - 1)
    }

    // Print the stored in the list
    document.write( '[');

    ans.forEach(element => {
        document.write(" "+element);
    });

    document.write( ' ' + ']');
}

// Driver Code
var N = 5, L = 3, R = 10;
// Function Call
bitonicSequence(N, L, R);

</script>
```

**Output:** 

```
[9, 10, 9, 8, 7]
```

***时间复杂度** : O(N)*
***辅助空间:** O(1)*