# 根据给定条件

找到二进制字符串中最后剩余的字符

> 原文:[https://www . geesforgeks . org/根据给定条件查找二进制字符串中最后剩余的字符/](https://www.geeksforgeeks.org/find-the-last-remaining-character-in-the-binary-string-according-to-the-given-conditions/)

给定一个只有 0 和 1 的二进制字符串 **str** ，可以对其执行以下两个操作:

1.  一个数字可以删除另一个数字，即 0 可以删除 1，反之亦然。
2.  如果在任何时候，整个字符串只包含 0 或 1，则打印相应的数字。

任务是打印最后剩下的数字。
**例:**

> **输入:** str = "100"
> **输出:** 0
> **说明:**
> 第一位数字为 1，删除下一位数字 0。
> 第二位数字 0 被删除，现在不存在。
> 现在，第三位数字 0 删除第一位数字 1。
> 由于现在只剩下 0，输出为 0。
> **输入:** str = "10"
> **输出:** 1

**方法:**为此使用[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)。可以按照以下步骤计算答案:

1.  所有数字都被添加到队列中。
2.  两个计数器被保持为大小为 2**del【2】**的数组，这将表示每个数字存在的浮动删除数。
3.  遍历队列，直到这两种类型中至少有一个数字存在。
4.  那么对于队列中的每个数字，如果该数字的**删除**计数器不是 0，则删除该数字。
5.  否则，相反数字的**删除**计数器递增并放回队列。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

string remainingDigit(string S, int N)
{

    // Delete counters for each to
    // count the deletes
    int del[] = { 0, 0 };

    // Counters to keep track
    // of characters left from each type
    int count[] = { 0, 0 };

    // Queue to simulate the process
    queue<int> q;

    // Initializing the queue
    for (int i = 0; i < N; i++)
    {
        int x = S[i] == '1' ? 1 : 0;
        count[x]++;
        q.push(x);
    }

    // Looping till at least 1 digit is
    // left from both the type
    while (count[0] > 0 && count[1] > 0)
    {
        int t = q.front();
        q.pop();

        // If there is a floating delete for
        // current character we will
        // delete it and move forward otherwise
        // we will increase delete counter for
        // opposite digit
        if (del[t] > 0)
        {
            del[t]--;
            count[t]--;
        }
        else
        {
            del[t ^ 1]++;
            q.push(t);
        }
    }

    // If 0 are left
    // then answer is 0 else
    // answer is 1
    if (count[0] > 0)
        return "0";
    return "1";
}

// Driver Code
int main()
{

    // Input String
    string S = "1010100100000";

    // Length of String
    int N = S.length();

    // Printing answer
    cout << remainingDigit(S, N);
}

// This code is contributed by tufan_gupta2000
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;

public class GfG {
    private static String remainingDigit(String S, int N)
    {
        // Converting string to array
        char c[] = S.toCharArray();

        // Delete counters for each to
        // count the deletes
        int del[] = { 0, 0 };

        // Counters to keep track
        // of characters left from each type
        int count[] = { 0, 0 };

        // Queue to simulate the process
        Queue<Integer> q = new LinkedList<>();

        // Initializing the queue
        for (int i = 0; i < N; i++) {
            int x = c[i] == '1' ? 1 : 0;
            count[x]++;
            q.add(x);
        }

        // Looping till at least 1 digit is
        // left from both the type
        while (count[0] > 0 && count[1] > 0) {
            int t = q.poll();

            // If there is a floating delete for
            // current character we will
            // delete it and move forward otherwise
            // we will increase delete counter for
            // opposite digit
            if (del[t] > 0) {
                del[t]--;
                count[t]--;
            }
            else {
                del[t ^ 1]++;
                q.add(t);
            }
        }

        // If 0 are left
        // then answer is 0 else
        // answer is 1
        if (count[0] > 0)
            return "0";
        return "1";
    }

    // Driver Code
    public static void main(String args[])
    {

        // Input String
        String S = "1010100100000";

        // Length of String
        int N = S.length();

        // Printing answer
        System.out.print(remainingDigit(S, N));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from collections import deque;

def remainingDigit(S, N):

    # Converting string to array
    c = [i for i in S]

    # Delete counters for each to
    # count the deletes
    de = [0, 0]

    # Counters to keep track
    # of characters left from each type
    count = [0, 0]

    # Queue to simulate the process
    q = deque()

    # Initializing the queue
    for i in c:
        x = 0
        if i == '1':
            x = 1
        count[x] += 1
        q.append(x)

    # Looping till at least 1 digit is
    # left from both the type
    while (count[0] > 0 and count[1] > 0):
        t = q.popleft()

        # If there is a floating delete for
        # current character we will
        # delete it and move forward otherwise
        # we will increase delete counter for
        # opposite digit
        if (de[t] > 0):
            de[t] -= 1
            count[t] -= 1
        else:
            de[t ^ 1] += 1
            q.append(t)

    # If 0 are left
    # then answer is 0 else
    # answer is 1
    if (count[0] > 0):
        return "0"
    return "1"

# Driver Code
if __name__ == '__main__':

    # Input String
    S = "1010100100000"

    # Length of String
    N = len(S)

    # Printing answer
    print(remainingDigit(S, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

public class GfG
{
    private static String remainingDigit(String S, int N)
    {
        // Converting string to array
        char []c = S.ToCharArray();

        // Delete counters for each to
        // count the deletes
        int []del = { 0, 0 };

        // Counters to keep track
        // of characters left from each type
        int []count = { 0, 0 };

        // Queue to simulate the process
        List<int> q = new List<int>();

        // Initializing the queue
        for (int i = 0; i < N; i++)
        {
            int x = c[i] == '1' ? 1 : 0;
            count[x]++;
            q.Add(x);
        }

        // Looping till at least 1 digit is
        // left from both the type
        while (count[0] > 0 && count[1] > 0)
        {
            int t = q[0];
            q.RemoveAt(0);

            // If there is a floating delete for
            // current character we will
            // delete it and move forward otherwise
            // we will increase delete counter for
            // opposite digit
            if (del[t] > 0)
            {
                del[t]--;
                count[t]--;
            }
            else
            {
                del[t ^ 1]++;
                q.Add(t);
            }
        }

        // If 0 are left
        // then answer is 0 else
        // answer is 1
        if (count[0] > 0)
            return "0";
        return "1";
    }

    // Driver Code
    public static void Main(String []args)
    {

        // Input String
        String S = "1010100100000";

        // Length of String
        int N = S.Length;

        // Printing answer
        Console.Write(remainingDigit(S, N));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

function remainingDigit(S,N)
{
     // Converting string to array
        let c = S.split("");

        // Delete counters for each to
        // count the deletes
        let del = [ 0, 0 ];

        // Counters to keep track
        // of characters left from each type
        let count = [ 0, 0 ];

        // Queue to simulate the process
        let q = [];

        // Initializing the queue
        for (let i = 0; i < N; i++) {
            let x = (c[i] == '1' ? 1 : 0);
            count[x]++;
            q.push(x);
        }   

        // Looping till at least 1 digit is
        // left from both the type
        while (count[0] > 0 && count[1] > 0) {
            let t = q.shift();

            // If there is a floating delete for
            // current character we will
            // delete it and move forward otherwise
            // we will increase delete counter for
            // opposite digit
            if (del[t] > 0) {
                del[t]--;
                count[t]--;
            }
            else {
                del[t ^ 1]++;
                q.push(t);
            }
        }

        // If 0 are left
        // then answer is 0 else
        // answer is 1
        if (count[0] > 0)
            return "0";
        return "1";
}

// Driver Code

let S = "1010100100000";

// Length of String
let N = S.length;

// Printing answer
document.write(remainingDigit(S, N));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(N)