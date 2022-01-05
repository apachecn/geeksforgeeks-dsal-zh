# 步数

> 原文:[https://www.geeksforgeeks.org/stepping-numbers/](https://www.geeksforgeeks.org/stepping-numbers/)

给定两个整数“n”和“m”，找出[n，m]范围内的所有步进数。如果所有相邻数字的绝对差值为 1，则一个数字称为**步进数**。321 是步进数，而 421 不是。

**示例:**

```
Input : n = 0, m = 21
Output : 0 1 2 3 4 5 6 7 8 9 10 12 21

Input : n = 10, m = 15
Output : 10, 12
```

**方法 1:蛮力法**
在该方法中，使用蛮力法来迭代从 n 到 m 的所有整数，并检查它是否是步进数。

## C++

```
// A C++ program to find all the Stepping Number in [n, m]
#include<bits/stdc++.h>
using namespace std;

// This function checks if an integer n is a Stepping Number
bool isStepNum(int n)
{
    // Initialize prevDigit with -1
    int prevDigit = -1;

    // Iterate through all digits of n and compare difference
    // between value of previous and current digits
    while (n)
    {
        // Get Current digit
        int curDigit = n % 10;

        // Single digit is consider as a
        // Stepping Number
        if (prevDigit == -1)
            prevDigit = curDigit;
        else
        {
            // Check if absolute difference between
            // prev digit and current digit is 1
            if (abs(prevDigit - curDigit) != 1)
                 return false;
        }
        prevDigit = curDigit;
        n /= 10;
    }

    return true;
}

// A brute force approach based function to find all
// stepping numbers.
void displaySteppingNumbers(int n, int m)
{
    // Iterate through all the numbers from [N,M]
    // and check if it’s a stepping number.
    for (int i=n; i<=m; i++)
        if (isStepNum(i))
            cout << i << " ";
}

// Driver program to test above function
int main()
{
    int n = 0, m = 21;

    // Display Stepping Numbers in
    // the range [n, m]
    displaySteppingNumbers(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find all the Stepping Number in [n, m]
class Main
{
    // This Method checks if an integer n
    // is a Stepping Number
    public static boolean isStepNum(int n)
    {
        // Initialize prevDigit with -1
        int prevDigit = -1;

        // Iterate through all digits of n and compare
        // difference between value of previous and
        // current digits
        while (n > 0)
        {
            // Get Current digit
            int curDigit = n % 10;

            // Single digit is consider as a
            // Stepping Number
            if (prevDigit != -1)
            {
                // Check if absolute difference between
                // prev digit and current digit is 1
                if (Math.abs(curDigit-prevDigit) != 1)
                    return false;
            }
            n /= 10;
            prevDigit = curDigit;
        }
        return true;
    }

    // A brute force approach based function to find all
    // stepping numbers.
    public static void displaySteppingNumbers(int n,int m)
    {
        // Iterate through all the numbers from [N,M]
        // and check if it is a stepping number.
        for (int i = n; i <= m; i++)
            if (isStepNum(i))
                System.out.print(i+ " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 0, m = 21;

        // Display Stepping Numbers in the range [n,m]
        displaySteppingNumbers(n,m);
    }
}
```

## 蟒蛇 3

```
# A Python3 program to find all the Stepping Number in [n, m]

# This function checks if an integer n is a Stepping Number
def isStepNum(n):

    # Initialize prevDigit with -1
    prevDigit = -1

    # Iterate through all digits of n and compare difference
    # between value of previous and current digits
    while (n):

        # Get Current digit
        curDigit = n % 10

        # Single digit is consider as a
        # Stepping Number
        if (prevDigit == -1):
            prevDigit = curDigit
        else:

            # Check if absolute difference between
            # prev digit and current digit is 1
            if (abs(prevDigit - curDigit) != 1):
                return False
        prevDigit = curDigit
        n //= 10
    return True

# A brute force approach based function to find all
# stepping numbers.
def displaySteppingNumbers(n, m):

    # Iterate through all the numbers from [N,M]
    # and check if it’s a stepping number.
    for i in range(n, m + 1):
        if (isStepNum(i)):
            print(i, end = " ")

# Driver code
if __name__ == '__main__':
    n, m = 0, 21

    # Display Stepping Numbers in
    # the range [n, m]
    displaySteppingNumbers(n, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// A C# program to find all
// the Stepping Number in [n, m]
using System;

class GFG
{
    // This Method checks if an
    // integer n is a Stepping Number
    public static bool isStepNum(int n)
    {
        // Initialize prevDigit with -1
        int prevDigit = -1;

        // Iterate through all digits
        // of n and compare difference
        // between value of previous
        // and current digits
        while (n > 0)
        {
            // Get Current digit
            int curDigit = n % 10;

            // Single digit is considered
            // as a Stepping Number
            if (prevDigit != -1)
            {
                // Check if absolute difference
                // between prev digit and current
                // digit is 1
                if (Math.Abs(curDigit -
                             prevDigit) != 1)
                    return false;
            }
            n /= 10;
            prevDigit = curDigit;
        }
        return true;
    }

    // A brute force approach based
    // function to find all stepping numbers.
    public static void displaySteppingNumbers(int n,
                                              int m)
    {
        // Iterate through all the numbers
        // from [N,M] and check if it is
        // a stepping number.
        for (int i = n; i <= m; i++)
            if (isStepNum(i))
                Console.Write(i+ " ");
    }

    // Driver code
    public static void Main()
    {
        int n = 0, m = 21;

        // Display Stepping Numbers
        // in the range [n,m]
        displaySteppingNumbers(n, m);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>
    // A Javascript program to find all the Stepping Number in [n, m]

    // This function checks if an integer n is a Stepping Number
    function isStepNum(n)
    {
        // Initialize prevDigit with -1
        let prevDigit = -1;

        // Iterate through all digits of n and compare difference
        // between value of previous and current digits
        while (n > 0)
        {
            // Get Current digit
            let curDigit = n % 10;

            // Single digit is consider as a
            // Stepping Number
            if (prevDigit == -1)
                prevDigit = curDigit;
            else
            {
                // Check if absolute difference between
                // prev digit and current digit is 1
                if (Math.abs(prevDigit - curDigit) != 1)
                     return false;
            }
            prevDigit = curDigit;
            n = parseInt(n / 10, 10);
        }

        return true;
    }

    // A brute force approach based function to find all
    // stepping numbers.
    function displaySteppingNumbers(n, m)
    {
        // Iterate through all the numbers from [N,M]
        // and check if it’s a stepping number.
        for (let i = n; i <= m; i++)
            if (isStepNum(i))
                document.write(i + " ");
    }

    let n = 0, m = 21;

    // Display Stepping Numbers in
    // the range [n, m]
    displaySteppingNumbers(n, m);

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
0 1 2 3 4 5 6 7 8 9 10 12 21 
```

**方法二:使用 BFS/DFS**

想法是使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) / [深度优先搜索](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)遍历。

**如何构建图形？**
图中每个节点代表一个步数；如果 V 可以从 U 变换(U 和 V 是步进数)，那么从节点 U 到 V 会有一条有向边。
**最后一位数字**是指 U(即 U % 10)
的最后一位数字，相邻的数字 **V** 可以是:

*   U*10 +最后一位数字+ 1(邻居 A)
*   U*10 +最后一位数字–1(邻居 B)

通过应用上述操作，一个新的数字被附加到 U 上，它或者是 lastDigit-1，或者是 lastDigit+1，因此由 U 形成的新数字 V 也是一个步进数。
因此，每个节点最多有 2 个相邻节点。
**边例:**当 U 的最后一位数字为 **0** 或 **9** 时

*   **情况 1:** 最后一位数字为 0:在这种情况下，只能追加数字‘1’。
*   **情况 2:** 最后一位数字是 9:在这种情况下，只能追加数字‘8’。

**什么是源/起始节点？**

*   每个数字都被认为是一个步进数，所以 bfs 遍历每个数字会给出从那个数字开始的所有步进数。
*   对[0，9]中的所有数字进行 bfs/dfs 遍历。

**注意:**对于节点 0，在 BFS 遍历期间不需要探索邻居，因为它将导致 01、012、010，并且这些将被从节点 1 开始的 BFS 遍历覆盖。
**示例查找从 0 到 21 的所有步进号**

```
-> 0 is a stepping Number and it is in the range
   so display it.
-> 1 is a Stepping Number, find neighbors of 1 i.e.,
   10 and 12 and push them into the queue

How to get 10 and 12?
Here U is 1 and last Digit is also 1 
V = 10 + 0 = 10 ( Adding lastDigit - 1 )
V = 10 + 2 = 12 ( Adding lastDigit + 1 )

Then do the same for 10 and 12 this will result into
101, 123, 121 but these Numbers are out of range. 
Now any number transformed from 10 and 12 will result
into a number greater than 21 so no need to explore 
their neighbors.

-> 2 is a Stepping Number, find neighbors of 2 i.e. 
   21, 23.
-> 23 is out of range so it is not considered as a 
   Stepping Number (Or a neighbor of 2)

The other stepping numbers will be 3, 4, 5, 6, 7, 8, 9.
```

**基于 BFS 的解决方案:**

## C++

```
// A C++ program to find all the Stepping Number from N=n
// to m using BFS Approach
#include<bits/stdc++.h>
using namespace std;

// Prints all stepping numbers reachable from num
// and in range [n, m]
void bfs(int n, int m, int num)
{
    // Queue will contain all the stepping Numbers
    queue<int> q;

    q.push(num);

    while (!q.empty())
    {
        // Get the front element and pop from the queue
        int stepNum = q.front();
        q.pop();

        // If the Stepping Number is in the range
        // [n, m] then display
        if (stepNum <= m && stepNum >= n)
            cout << stepNum << " ";

        // If Stepping Number is 0 or greater than m,
        // no need to explore the neighbors
        if (num == 0 || stepNum > m)
            continue;

        // Get the last digit of the currently visited
        // Stepping Number
        int lastDigit = stepNum % 10;

        // There can be 2 cases either digit to be
        // appended is lastDigit + 1 or lastDigit - 1
        int stepNumA = stepNum * 10 + (lastDigit- 1);
        int stepNumB = stepNum * 10 + (lastDigit + 1);

        // If lastDigit is 0 then only possible digit
        // after 0 can be 1 for a Stepping Number
        if (lastDigit == 0)
            q.push(stepNumB);

        //If lastDigit is 9 then only possible
        //digit after 9 can be 8 for a Stepping
        //Number
        else if (lastDigit == 9)
            q.push(stepNumA);

        else
        {
            q.push(stepNumA);
            q.push(stepNumB);
        }
    }
}

// Prints all stepping numbers in range [n, m]
// using BFS.
void displaySteppingNumbers(int n, int m)
{
    // For every single digit Number 'i'
    // find all the Stepping Numbers
    // starting with i
    for (int i = 0 ; i <= 9 ; i++)
        bfs(n, m, i);
}

//Driver program to test above function
int main()
{
    int n = 0, m = 21;

    // Display Stepping Numbers in the
    // range [n,m]
    displaySteppingNumbers(n,m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find all the Stepping Number in
// range [n, m]
import java.util.*;

class Main
{
    // Prints all stepping numbers reachable from num
    // and in range [n, m]
    public static void bfs(int n,int m,int num)
    {
        // Queue will contain all the stepping Numbers
        Queue<Integer> q = new LinkedList<Integer> ();

        q.add(num);

        while (!q.isEmpty())
        {
            // Get the front element and pop from
            // the queue
            int stepNum = q.poll();

            // If the Stepping Number is in
            // the range [n,m] then display
            if (stepNum <= m && stepNum >= n)
            {
                System.out.print(stepNum + " ");
            }

            // If Stepping Number is 0 or greater
            // then m, no need to explore the neighbors
            if (stepNum == 0 || stepNum > m)
                continue;

            // Get the last digit of the currently
            // visited Stepping Number
            int lastDigit = stepNum % 10;

            // There can be 2 cases either digit
            // to be appended is lastDigit + 1 or
            // lastDigit - 1
            int stepNumA = stepNum * 10 + (lastDigit- 1);
            int stepNumB = stepNum * 10 + (lastDigit + 1);

            // If lastDigit is 0 then only possible
            // digit after 0 can be 1 for a Stepping
            // Number
            if (lastDigit == 0)
                q.add(stepNumB);

            // If lastDigit is 9 then only possible
            // digit after 9 can be 8 for a Stepping
            // Number
            else if (lastDigit == 9)
                q.add(stepNumA);

            else
            {
                q.add(stepNumA);
                q.add(stepNumB);
            }
        }
    }

    // Prints all stepping numbers in range [n, m]
    // using BFS.
    public static void displaySteppingNumbers(int n,int m)
    {
        // For every single digit Number 'i'
        // find all the Stepping Numbers
        // starting with i
        for (int i = 0 ; i <= 9 ; i++)
            bfs(n, m, i);
    }

    //Driver code
    public static void main(String args[])
    {
        int n = 0, m = 21;

        // Display Stepping Numbers in
        // the range [n,m]
        displaySteppingNumbers(n,m);
    }
}
```

## 蟒蛇 3

```
# A Python3 program to find all the Stepping Number from N=n
# to m using BFS Approach

# Prints all stepping numbers reachable from num
# and in range [n, m]
def bfs(n, m, num) :

    # Queue will contain all the stepping Numbers
    q = []
    q.append(num)
    while len(q) > 0 :

        # Get the front element and pop from the queue
        stepNum = q[0]
        q.pop(0);

        # If the Stepping Number is in the range
        # [n, m] then display
        if (stepNum <= m and stepNum >= n) :
            print(stepNum, end = " ")

        # If Stepping Number is 0 or greater than m,
        # no need to explore the neighbors
        if (num == 0 or stepNum > m) :
            continue

        # Get the last digit of the currently visited
        # Stepping Number
        lastDigit = stepNum % 10

        # There can be 2 cases either digit to be
        # appended is lastDigit + 1 or lastDigit - 1
        stepNumA = stepNum * 10 + (lastDigit- 1)
        stepNumB = stepNum * 10 + (lastDigit + 1)

        # If lastDigit is 0 then only possible digit
        # after 0 can be 1 for a Stepping Number
        if (lastDigit == 0) :
            q.append(stepNumB)

        #If lastDigit is 9 then only possible
        #digit after 9 can be 8 for a Stepping
        #Number
        elif (lastDigit == 9) :
            q.append(stepNumA)

        else :
            q.append(stepNumA)
            q.append(stepNumB)

# Prints all stepping numbers in range [n, m]
# using BFS.
def displaySteppingNumbers(n, m) :

    # For every single digit Number 'i'
    # find all the Stepping Numbers
    # starting with i
    for i in range(10) :
        bfs(n, m, i)

        # Driver code
n, m = 0, 21

# Display Stepping Numbers in the
# range [n,m]
displaySteppingNumbers(n, m)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// A C# program to find all the Stepping Number in
// range [n, m]
using System;
using System.Collections.Generic;
public class GFG
{

    // Prints all stepping numbers reachable from num
    // and in range [n, m]
    static void bfs(int n, int m, int num)
    {

        // Queue will contain all the stepping Numbers
        Queue<int> q = new Queue<int>();
        q.Enqueue(num);
        while(q.Count != 0)
        {

            // Get the front element and pop from
            // the queue
            int stepNum = q.Dequeue();

            // If the Stepping Number is in
            // the range [n,m] then display
            if (stepNum <= m && stepNum >= n)
            {
                Console.Write(stepNum + " ");
            }

            // If Stepping Number is 0 or greater
            // then m, no need to explore the neighbors
            if (stepNum == 0 || stepNum > m)
                continue;

            // Get the last digit of the currently
            // visited Stepping Number
            int lastDigit = stepNum % 10;

            // There can be 2 cases either digit
            // to be appended is lastDigit + 1 or
            // lastDigit - 1
            int stepNumA = stepNum * 10 + (lastDigit- 1);
            int stepNumB = stepNum * 10 + (lastDigit + 1);

            // If lastDigit is 0 then only possible
            // digit after 0 can be 1 for a Stepping
            // Number
            if (lastDigit == 0)
                q.Enqueue(stepNumB);

            // If lastDigit is 9 then only possible
            // digit after 9 can be 8 for a Stepping
            // Number
            else if (lastDigit == 9)
                q.Enqueue(stepNumA);
            else
            {
                q.Enqueue(stepNumA);
                q.Enqueue(stepNumB);
            }
        }
    }

    // Prints all stepping numbers in range [n, m]
    // using BFS.
    static void displaySteppingNumbers(int n,int m)
    {
        // For every single digit Number 'i'
        // find all the Stepping Numbers
        // starting with i
        for (int i = 0 ; i <= 9 ; i++)
            bfs(n, m, i);
    }

    // Driver code
    static public void Main ()
    {
        int n = 0, m = 21;

        // Display Stepping Numbers in
        // the range [n,m]
        displaySteppingNumbers(n,m);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// A Javascript program to find all
// the Stepping Number in
// range [n, m]

    // Prints all stepping numbers
    // reachable from num
    // and in range [n, m]
    function bfs(n,m,num)
    {
        // Queue will contain all the
        // stepping Numbers
        let q = [];

        q.push(num);

        while (q.length!=0)
        {
            // Get the front element and pop from
            // the queue
            let stepNum = q.shift();

            // If the Stepping Number is in
            // the range [n,m] then display
            if (stepNum <= m && stepNum >= n)
            {
                document.write(stepNum + " ");
            }

            // If Stepping Number is 0 or greater
            // then m, no need to explore the neighbors
            if (stepNum == 0 || stepNum > m)
                continue;

            // Get the last digit of the currently
            // visited Stepping Number
            let lastDigit = stepNum % 10;

            // There can be 2 cases either digit
            // to be appended is lastDigit + 1 or
            // lastDigit - 1
            let stepNumA = stepNum * 10 + (lastDigit- 1);
            let stepNumB = stepNum * 10 + (lastDigit + 1);

            // If lastDigit is 0 then only possible
            // digit after 0 can be 1 for a Stepping
            // Number
            if (lastDigit == 0)
                q.push(stepNumB);

            // If lastDigit is 9 then only possible
            // digit after 9 can be 8 for a Stepping
            // Number
            else if (lastDigit == 9)
                q.push(stepNumA);

            else
            {
                q.push(stepNumA);
                q.push(stepNumB);
            }
        }
    }

    // Prints all stepping numbers in range [n, m]
    // using BFS.
    function displaySteppingNumbers(n,m)
    {
        // For every single digit Number 'i'
        // find all the Stepping Numbers
        // starting with i
        for (let i = 0 ; i <= 9 ; i++)
            bfs(n, m, i);
    }

    // Driver code
    let n = 0, m = 21;

    // Display Stepping Numbers in
    // the range [n,m]
    displaySteppingNumbers(n,m);

    // This code is contributed by unknown2108

</script>
```

**输出**:

```
0 1 10 12 2 21 3 4 5 6 7 8 9 
```

**基于 DFS 的解决方案**

## C++

```
// A C++ program to find all the Stepping Numbers
// in range [n, m] using DFS Approach
#include<bits/stdc++.h>
using namespace std;

// Prints all stepping numbers reachable from num
// and in range [n, m]
void dfs(int n, int m, int stepNum)
{
    // If Stepping Number is in the
    // range [n,m] then display
    if (stepNum <= m && stepNum >= n)
        cout << stepNum << " ";

    // If Stepping Number is 0 or greater
    // than m, then return
    if (stepNum == 0 || stepNum > m)
        return ;

    // Get the last digit of the currently
    // visited Stepping Number
    int lastDigit = stepNum % 10;

    // There can be 2 cases either digit
    // to be appended is lastDigit + 1 or
    // lastDigit - 1
    int stepNumA = stepNum*10 + (lastDigit-1);
    int stepNumB = stepNum*10 + (lastDigit+1);

    // If lastDigit is 0 then only possible
    // digit after 0 can be 1 for a Stepping
    // Number
    if (lastDigit == 0)
        dfs(n, m, stepNumB);

    // If lastDigit is 9 then only possible
    // digit after 9 can be 8 for a Stepping
    // Number
    else if(lastDigit == 9)
        dfs(n, m, stepNumA);
    else
    {
        dfs(n, m, stepNumA);
        dfs(n, m, stepNumB);
    }
}

// Method displays all the stepping
// numbers in range [n, m]
void displaySteppingNumbers(int n, int m)
{
    // For every single digit Number 'i'
    // find all the Stepping Numbers
    // starting with i
    for (int i = 0 ; i <= 9 ; i++)
        dfs(n, m, i);
}

//Driver program to test above function
int main()
{
    int n = 0, m = 21;

    // Display Stepping Numbers in
    // the range [n,m]
    displaySteppingNumbers(n,m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find all the Stepping Numbers
// in range [n, m] using DFS Approach
import java.util.*;

class Main
{
    // Method display's all the stepping numbers
    // in range [n, m]
    public static void dfs(int n,int m,int stepNum)
    {
        // If Stepping Number is in the
        // range [n,m] then display
        if (stepNum <= m && stepNum >= n)
            System.out.print(stepNum + " ");

        // If Stepping Number is 0 or greater
        // than m then return
        if (stepNum == 0 || stepNum > m)
            return ;

        // Get the last digit of the currently
        // visited Stepping Number
        int lastDigit = stepNum % 10;

        // There can be 2 cases either digit
        // to be appended is lastDigit + 1 or
        // lastDigit - 1
        int stepNumA = stepNum*10 + (lastDigit-1);
        int stepNumB = stepNum*10 + (lastDigit+1);

        // If lastDigit is 0 then only possible
        // digit after 0 can be 1 for a Stepping
        // Number
        if (lastDigit == 0)
            dfs(n, m, stepNumB);

        // If lastDigit is 9 then only possible
        // digit after 9 can be 8 for a Stepping
        // Number
        else if(lastDigit == 9)
            dfs(n, m, stepNumA);
        else
        {
            dfs(n, m, stepNumA);
            dfs(n, m, stepNumB);
        }
    }

    // Prints all stepping numbers in range [n, m]
    // using DFS.
    public static void displaySteppingNumbers(int n, int m)
    {
        // For every single digit Number 'i'
        // find all the Stepping Numbers
        // starting with i
        for (int i = 0 ; i <= 9 ; i++)
            dfs(n, m, i);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 0, m = 21;

        // Display Stepping Numbers in
        // the range [n,m]
        displaySteppingNumbers(n,m);
    }
}
```

## 蟒蛇 3

```
# A Python3 program to find all the Stepping Numbers
# in range [n, m] using DFS Approach

# Prints all stepping numbers reachable from num
# and in range [n, m]
def dfs(n, m, stepNum) :

    # If Stepping Number is in the
    # range [n,m] then display
    if (stepNum <= m and stepNum >= n) :
        print(stepNum, end = " ")

    # If Stepping Number is 0 or greater
    # than m, then return
    if (stepNum == 0 or stepNum > m) :
        return

    # Get the last digit of the currently
    # visited Stepping Number
    lastDigit = stepNum % 10

    # There can be 2 cases either digit
    # to be appended is lastDigit + 1 or
    # lastDigit - 1
    stepNumA = stepNum * 10 + (lastDigit - 1)
    stepNumB = stepNum * 10 + (lastDigit + 1)

    # If lastDigit is 0 then only possible
    # digit after 0 can be 1 for a Stepping
    # Number
    if (lastDigit == 0) :
        dfs(n, m, stepNumB)

    # If lastDigit is 9 then only possible
    # digit after 9 can be 8 for a Stepping
    # Number
    elif(lastDigit == 9) :
        dfs(n, m, stepNumA)
    else :

        dfs(n, m, stepNumA)
        dfs(n, m, stepNumB)

# Method displays all the stepping
# numbers in range [n, m]
def displaySteppingNumbers(n, m) :

    # For every single digit Number 'i'
    # find all the Stepping Numbers
    # starting with i
    for i in range(10) :
        dfs(n, m, i)

n, m = 0, 21

# Display Stepping Numbers in
# the range [n,m]
displaySteppingNumbers(n, m)

# This code is contributed by divyesh072019.
```

## C#

```
// A C# program to find all the Stepping Numbers
// in range [n, m] using DFS Approach
using System;
public class GFG
{

  // Method display's all the stepping numbers
  // in range [n, m]
  static void dfs(int n, int m, int stepNum)
  {

    // If Stepping Number is in the
    // range [n,m] then display
    if (stepNum <= m && stepNum >= n)
      Console.Write(stepNum + " ");

    // If Stepping Number is 0 or greater
    // than m then return
    if (stepNum == 0 || stepNum > m)
      return ;

    // Get the last digit of the currently
    // visited Stepping Number
    int lastDigit = stepNum % 10;

    // There can be 2 cases either digit
    // to be appended is lastDigit + 1 or
    // lastDigit - 1
    int stepNumA = stepNum*10 + (lastDigit - 1);
    int stepNumB = stepNum*10 + (lastDigit + 1);

    // If lastDigit is 0 then only possible
    // digit after 0 can be 1 for a Stepping
    // Number
    if (lastDigit == 0)
      dfs(n, m, stepNumB);

    // If lastDigit is 9 then only possible
    // digit after 9 can be 8 for a Stepping
    // Number
    else if(lastDigit == 9)
      dfs(n, m, stepNumA);
    else
    {
      dfs(n, m, stepNumA);
      dfs(n, m, stepNumB);
    }
  }

  // Prints all stepping numbers in range [n, m]
  // using DFS.
  public static void displaySteppingNumbers(int n, int m)
  {

    // For every single digit Number 'i'
    // find all the Stepping Numbers
    // starting with i
    for (int i = 0 ; i <= 9 ; i++)
      dfs(n, m, i);
  }

  // Driver code
  static public void Main ()
  {
    int n = 0, m = 21;

    // Display Stepping Numbers in
    // the range [n,m]
    displaySteppingNumbers(n,m);
  }
}

// This code is contributed by rag2127.
```

## java 描述语言

```
<script>

// A Javascript program to find all the Stepping Numbers
// in range [n, m] using DFS Approach

// Method display's all the stepping numbers
    // in range [n, m]
function dfs(n, m, stepNum)
{
    // If Stepping Number is in the
        // range [n,m] then display
        if (stepNum <= m && stepNum >= n)
            document.write(stepNum + " ");

        // If Stepping Number is 0 or greater
        // than m then return
        if (stepNum == 0 || stepNum > m)
            return ;

        // Get the last digit of the currently
        // visited Stepping Number
        let lastDigit = stepNum % 10;

        // There can be 2 cases either digit
        // to be appended is lastDigit + 1 or
        // lastDigit - 1
        let stepNumA = stepNum*10 + (lastDigit-1);
        let stepNumB = stepNum*10 + (lastDigit+1);

        // If lastDigit is 0 then only possible
        // digit after 0 can be 1 for a Stepping
        // Number
        if (lastDigit == 0)
            dfs(n, m, stepNumB);

        // If lastDigit is 9 then only possible
        // digit after 9 can be 8 for a Stepping
        // Number
        else if(lastDigit == 9)
            dfs(n, m, stepNumA);
        else
        {
            dfs(n, m, stepNumA);
            dfs(n, m, stepNumB);
        }
}

// Prints all stepping numbers in range [n, m]
    // using DFS.
function displaySteppingNumbers(n, m)
{

    // For every single digit Number 'i'
        // find all the Stepping Numbers
        // starting with i
        for (let i = 0 ; i <= 9 ; i++)
            dfs(n, m, i);
}

// Driver code
let n = 0, m = 21;

// Display Stepping Numbers in
// the range [n,m]
displaySteppingNumbers(n,m);

// This code is contributed by ab2127
</script>
```

**输出:**

```
0 1 10 12 2 21 3 4 5 6 7 8 9 
```

本文由 **Chirag Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。