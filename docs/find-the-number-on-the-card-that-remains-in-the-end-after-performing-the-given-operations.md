# 在卡片上找到执行给定操作后剩余的号码

> 原文:[https://www . geeksforgeeks . org/find-执行给定操作后卡上剩余的号码/](https://www.geeksforgeeks.org/find-the-number-on-the-card-that-remains-in-the-end-after-performing-the-given-operations/)

给定一个整数 **N** ，代表一副牌中的牌数。从 **1** 到 **N** 点一副牌，其中 **1** 是最上面的牌， **N** 是最下面的牌。你从一副牌中取出最上面的一张牌，并将其插入底部，然后抛出出现在一副牌顶部的下一张牌。你再次做同样的事情，直到剩下一张卡。任务是找到最后剩下的卡的号码。
**举例:**

```
Input: N = 4 
Output: 1
1 2 3 4
^     ^
Top   Bottom

Operation 1: 3 4 1 (1 got shifted to the bottom and 2 got removed)
Operation 2: 1 3 (3 got shifted and 4 got removed)
Operation 3: 1 (3 got removed after shifting 1)

Input: N = 10
Output: 5
```

**进场:**

1.  首先在[队列](https://www.geeksforgeeks.org/queue-data-structure/)中插入从 **1** 到 **N** 的数字。
2.  现在，将前面的元素从队列中出列，并在最后将其入队。
3.  最后，弹出前面的元素。
4.  打印队列中剩余的最后一个元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that will find the
// card number which is remaining
int remainingCard(int n)
{
    queue<int> queCards;

    // Inserting all the numbers from 1 to n
    for (int i = 1; i <= n; i++)
        queCards.push(i);

    // While there are atleast two
    // elements in the queue
    while (((int)queCards.size()) >= 2) {

        // Push the front element at the back
        queCards.push(queCards.front());

        // Remove the front element
        queCards.pop();

        // Remove another element
        queCards.pop();
    }

    // Return the only element
    // left in the queue
    return queCards.front();
}

// Driver code
int main()
{
    int n = 10;

    cout << remainingCard(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that will find the
// card number which is remaining
static int remainingCard(int n)
{
    Queue<Integer> queCards = new LinkedList<>();

    // Inserting all the numbers from 1 to n
    for (int i = 1; i <= n; i++)
    {
        queCards.add(i);
    }

    // While there are atleast two
    // elements in the queue
    while (((int) queCards.size()) >= 2)
    {

        // Push the front element at the back
        queCards.add(queCards.peek());

        // Remove the front element
        queCards.remove();

        // Remove another element
        queCards.remove();
    }

    // Return the only element
    // left in the queue
    return queCards.peek();
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    System.out.println(remainingCard(n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that will find the
# card number which is remaining
def remainingCard(n):

    queCards = []

    # Inserting all the numbers from 1 to n
    for i in range(1, n + 1):
        queCards.append(i)

    # While there are atleast two
    # elements in the queue
    while (len(queCards) >= 2):

        # Push the front element at the back
        queCards.append(queCards[0]);

        # Remove the front element
        queCards.pop(0);

        # Remove another element
        queCards.pop(0);

    # Return the only element
    # left in the queue
    return queCards[0]

# Driver code
n = 10
print(remainingCard(n))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that will find the
// card number which is remaining
static int remainingCard(int n)
{
    Queue<int> queCards = new Queue<int>();

    // Inserting all the numbers from 1 to n
    for (int i = 1; i <= n; i++)
    {
        queCards.Enqueue(i);
    }

    // While there are atleast two
    // elements in the queue
    while (((int) queCards.Count) >= 2)
    {

        // Push the front element at the back
        queCards.Enqueue(queCards.Peek());

        // Remove the front element
        queCards.Dequeue();

        // Remove another element
        queCards.Dequeue();
    }

    // Return the only element
    // left in the queue
    return queCards.Peek();
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;

    Console.WriteLine(remainingCard(n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that will find the
// card number which is remaining
function remainingCard(n)
{
    queCards = [];

    // Inserting all the numbers from 1 to n
    for (var i = 1; i <= n; i++)
        queCards.push(i);

    // While there are atleast two
    // elements in the queue
    while ((queCards.length) >= 2) {

        // Push the front element at the back
        queCards.push(queCards[0]);

        // Remove the front element
        queCards.shift();

        // Remove another element
        queCards.shift();
    }

    // Return the only element
    // left in the queue
    return queCards[0];
}

// Driver code
var n = 10;
document.write( remainingCard(n));

</script>
```

**Output:** 

```
5
```