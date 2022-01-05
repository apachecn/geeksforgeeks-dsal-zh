# 最长正确括号子序列集的范围查询| 2

> 原文:[https://www . geesforgeks . org/range-query-最长-正确-括号-子序列-set-2/](https://www.geeksforgeeks.org/range-queries-longest-correct-bracket-subsequence-set-2/)

给定一个括号序列，或者换句话说，一个长度为 n 的字符串，由字符“(”和“)”组成。为给定的查询范围找到序列的最大正确括号子序列的长度。注意:正确的括号序列是指具有匹配的括号对或包含另一个嵌套的正确括号序列的序列。例如()、(())、()()都是一些正确的括号顺序。
示例:

```
Input : S = ())(())(())(
        Start Index of Range = 0, 
        End Index of Range = 11
Output : 10
Explanation:  Longest Correct Bracket Subsequence is ()(())(())

Input : S = ())(())(())(
        Start Index of Range = 1, 
        End Index of Range = 2
Output : 0
```

**方法:**在上一篇帖子( [SET 1](https://www.geeksforgeeks.org/range-queries-longest-correct-bracket-subsequence/) )中我们讨论了一个对每个查询都适用于 O(long)的解决方案，现在是这篇帖子我们将去看一个对每个查询都适用于 O(1)的解决方案。
这个想法基于最长有效平衡子串的 Post [长度如果我们在一个临时数组中标记所有平衡括号/括号的索引(这里我们将其命名为 BCP[]，BOP[])，那么我们在 O(1)时间内回答每个查询。
**算法:**](https://www.geeksforgeeks.org/length-of-the-longest-valid-substring/)

```
stack is used to get the index of balance bracket.
Traverse a string from 0 ..to n
IF we seen a closing bracket, 
      ( i.e., str[i] = ')' && stack is not empty )

Then mark both "open & close" bracket indexes as 1.
BCP[i] = 1; 
BOP[stk.top()] = 1;

And At last, stored cumulative sum of BCP[] & BOP[] 
Run a loop from 1 to n
BOP[i] +=BOP[i-1], BCP[i] +=BCP[i-1]
```

现在，您可以在 O(1)时间内回答每个查询

```
(BCP[e] - BOP[s-1]])*2;
```

以下是上述想法的实现。

## C++

```
// CPP code to answer the query in constant time
#include <bits/stdc++.h>
using namespace std;

/*
BOP[] stands for "Balanced open parentheses"
BCP[] stands for "Balanced close parentheses"

*/

// function for precomputation
void constructBlanceArray(int BOP[], int BCP[],
                          char* str, int n)
{

    // Create a stack and push -1 as initial index to it.
    stack<int> stk;

    // Initialize result
    int result = 0;

    // Traverse all characters of given string
    for (int i = 0; i < n; i++) {
        // If opening bracket, push index of it
        if (str[i] == '(')
            stk.push(i);

        else // If closing bracket, i.e., str[i] = ')'
        {
            // If closing bracket, i.e., str[i] = ')'
            // && stack is not empty then mark both
            // "open & close" bracket indexs as 1 .
            // Pop the previous opening bracket's index
            if (!stk.empty()) {
                BCP[i] = 1;
                BOP[stk.top()] = 1;
                stk.pop();
            }

            // If stack is empty.
            else
                BCP[i] = 0;
        }
    }

    for (int i = 1; i < n; i++) {
        BCP[i] += BCP[i - 1];
        BOP[i] += BOP[i - 1];
    }
}

// Function return output of each query in O(1)
int query(int BOP[], int BCP[],
          int s, int e)
{
    if (BOP[s - 1] == BOP[s]) {
        return (BCP[e] - BOP[s]) * 2;
    }

    else {
        return (BCP[e] - BOP[s] + 1) * 2;
    }
}

// Driver program to test above function
int main()
{

    char str[] = "())(())(())(";
    int n = strlen(str);

    int BCP[n + 1] = { 0 };
    int BOP[n + 1] = { 0 };

    constructBlanceArray(BOP, BCP, str, n);

    int startIndex = 5, endIndex = 11;

    cout << "Maximum Length Correct Bracket"
            " Subsequence between "
         << startIndex << " and " << endIndex << " = "
         << query(BOP, BCP, startIndex, endIndex) << endl;

    startIndex = 4, endIndex = 5;
    cout << "Maximum Length Correct Bracket"
            " Subsequence between "
         << startIndex << " and " << endIndex << " = "
         << query(BOP, BCP, startIndex, endIndex) << endl;

    startIndex = 1, endIndex = 5;
    cout << "Maximum Length Correct Bracket"
            " Subsequence between "
         << startIndex << " and " << endIndex << " = "
         << query(BOP, BCP, startIndex, endIndex) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to answer the query in constant time
import java.util.*;

class GFG{

/*
BOP[] stands for "Balanced open parentheses"
BCP[] stands for "Balanced close parentheses"

*/

// Function for precomputation
static void constructBlanceArray(int BOP[], int BCP[],
                                String str, int n)
{

    // Create a stack and push -1
    // as initial index to it.
    Stack<Integer> stk = new Stack<>();;

    // Traverse all characters of given String
    for(int i = 0; i < n; i++)
    {

        // If opening bracket, push index of it
        if (str.charAt(i) == '(')
            stk.add(i);

        // If closing bracket, i.e., str[i] = ')'
        else
        {

            // If closing bracket, i.e., str[i] = ')'
            // && stack is not empty then mark both
            // "open & close" bracket indexs as 1 .
            // Pop the previous opening bracket's index
            if (!stk.isEmpty())
            {
                BCP[i] = 1;
                BOP[stk.peek()] = 1;
                stk.pop();
            }

            // If stack is empty.
            else
                BCP[i] = 0;
        }
    }

    for(int i = 1; i < n; i++)
    {
        BCP[i] += BCP[i - 1];
        BOP[i] += BOP[i - 1];
    }
}

// Function return output of each query in O(1)
static int query(int BOP[], int BCP[],
                 int s, int e)
{
    if (BOP[s - 1] == BOP[s])
    {
        return (BCP[e] - BOP[s]) * 2;
    }
    else
    {
        return (BCP[e] - BOP[s] + 1) * 2;
    }
}

// Driver code
public static void main(String[] args)
{

    String str = "())(())(())(";
    int n = str.length();

    int BCP[] = new int[n + 1];
    int BOP[] = new int[n + 1];

    constructBlanceArray(BOP, BCP, str, n);

    int startIndex = 5, endIndex = 11;
    System.out.print("Maximum Length Correct " +
                     "Bracket Subsequence between " +
                     startIndex + " and " + endIndex +
                     " = " + query(BOP, BCP, startIndex,
                                   endIndex) + "\n");

    startIndex = 4;
    endIndex = 5;
    System.out.print("Maximum Length Correct " + 
                     "Bracket Subsequence between " +
                     startIndex + " and " + endIndex +
                     " = " + query(BOP, BCP, startIndex,
                                   endIndex) + "\n");

    startIndex = 1;
    endIndex = 5;
    System.out.print("Maximum Length Correct " +
                     "Bracket Subsequence between " +
                     startIndex + " and " + endIndex +
                     " = " + query(BOP, BCP, startIndex,
                                   endIndex) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to answer the query in constant time

'''
BOP[] stands for "Balanced open parentheses"
BCP[] stands for "Balanced close parentheses"

'''
# Function for precomputation
def constructBlanceArray(BOP, BCP, str, n):

    # Create a stack and push -1
    # as initial index to it.
    stk = []

    # Traverse all characters of given String
    for i in range(n):

        # If opening bracket, push index of it
        if (str[i] == '('):
            stk.append(i);

        # If closing bracket, i.e., str[i] = ')'
        else:

            # If closing bracket, i.e., str[i] = ')'
            # && stack is not empty then mark both
            # "open & close" bracket indexs as 1 .
            # Pop the previous opening bracket's index
            if (len(stk) != 0):
                BCP[i] = 1;
                BOP[stk[-1]] = 1;
                stk.pop();

            # If stack is empty.
            else:
                BCP[i] = 0;

    for i in range(1, n):

        BCP[i] += BCP[i - 1];
        BOP[i] += BOP[i - 1];

# Function return output of each query in O(1)
def query(BOP, BCP, s, e):

    if (BOP[s - 1] == BOP[s]):
        return (BCP[e] - BOP[s]) * 2;

    else:
        return (BCP[e] - BOP[s] + 1) * 2;

# Driver code
if __name__=='__main__':

    string = "())(())(())(";
    n = len(string)

    BCP = [0 for i in range(n + 1)];
    BOP = [0 for i in range(n + 1)];

    constructBlanceArray(BOP, BCP, string, n);
    startIndex = 5
    endIndex = 11;
    print("Maximum Length Correct " +
                     "Bracket Subsequence between " +
                     str(startIndex) + " and " + str(endIndex) +
                     " = " + str(query(BOP, BCP, startIndex,
                                   endIndex)));
    startIndex = 4;
    endIndex = 5;
    print("Maximum Length Correct " + 
                     "Bracket Subsequence between " +
                     str(startIndex) + " and " + str(endIndex) +
                     " = " + str(query(BOP, BCP, startIndex,
                                   endIndex)))
    startIndex = 1;
    endIndex = 5;
    print("Maximum Length Correct " +
                     "Bracket Subsequence between " +
                     str(startIndex) + " and " + str(endIndex) +
                     " = " + str(query(BOP, BCP, startIndex,
                                   endIndex)));

# This code is contributed by rutvik_56.
```

## C#

```
// C# code to answer the query
// in constant time
using System;
using System.Collections.Generic;
class GFG{

    /*
    BOP[] stands for "Balanced open parentheses"
    BCP[] stands for "Balanced close parentheses"
    */

    // Function for precomputation
    static void constructBlanceArray(int[] BOP, int[] BCP,
                                     String str, int n)
    {

        // Create a stack and push -1
        // as initial index to it.
        Stack<int> stk = new Stack<int>();;

        // Traverse all characters of given String
        for (int i = 0; i < n; i++)
        {

            // If opening bracket, push index of it
            if (str[i] == '(')
                stk.Push(i);

            // If closing bracket, i.e., str[i] = ')'
            else
            {

                // If closing bracket, i.e., str[i] = ')'
                // && stack is not empty then mark both
                // "open & close" bracket indexs as 1 .
                // Pop the previous opening bracket's index
                if (stk.Count != 0)
                {
                    BCP[i] = 1;
                    BOP[stk.Peek()] = 1;
                    stk.Pop();
                }

                // If stack is empty.
                else
                    BCP[i] = 0;
            }
        }

        for (int i = 1; i < n; i++)
        {
            BCP[i] += BCP[i - 1];
            BOP[i] += BOP[i - 1];
        }
    }

    // Function return output of each query in O(1)
    static int query(int[] BOP, int[] BCP, int s, int e)
    {
        if (BOP[s - 1] == BOP[s])
        {
            return (BCP[e] - BOP[s]) * 2;
        }
        else
        {
            return (BCP[e] - BOP[s] + 1) * 2;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "())(())(())(";
        int n = str.Length;
        int[] BCP = new int[n + 1];
        int[] BOP = new int[n + 1];
        constructBlanceArray(BOP, BCP, str, n);
        int startIndex = 5, endIndex = 11;
        Console.Write("Maximum Length Correct " +
                      "Bracket Subsequence between " +
                       startIndex + " and " + endIndex + " = " +
                       query(BOP, BCP, startIndex, endIndex) + "\n");

        startIndex = 4;
        endIndex = 5;
        Console.Write("Maximum Length Correct " +
                      "Bracket Subsequence between " +
                       startIndex + " and " + endIndex + " = " +
                       query(BOP, BCP, startIndex, endIndex) + "\n");

        startIndex = 1;
        endIndex = 5;
        Console.Write("Maximum Length Correct " +
                      "Bracket Subsequence between " +
                       startIndex + " and " + endIndex + " = " +
                       query(BOP, BCP, startIndex, endIndex) + "\n");
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript code to answer the query in constant time

/*
BOP[] stands for "Balanced open parentheses"
BCP[] stands for "Balanced close parentheses"

*/

// function for precomputation
function constructBlanceArray(BOP, BCP, str, n)
{

    // Create a stack and push -1 as initial index to it.
    var stk = [];

    // Initialize result
    var result = 0;

    // Traverse all characters of given string
    for (var i = 0; i < n; i++) {
        // If opening bracket, push index of it
        if (str[i] == '(')
            stk.push(i);

        else // If closing bracket, i.e., str[i] = ')'
        {
            // If closing bracket, i.e., str[i] = ')'
            // && stack is not empty then mark both
            // "open & close" bracket indexs as 1 .
            // Pop the previous opening bracket's index
            if (stk.length!=0) {
                BCP[i] = 1;
                BOP[stk[stk.length-1]] = 1;
                stk.pop();
            }

            // If stack is empty.
            else
                BCP[i] = 0;
        }
    }

    for (var i = 1; i < n; i++) {
        BCP[i] += BCP[i - 1];
        BOP[i] += BOP[i - 1];
    }
}

// Function return output of each query in O(1)
function query(BOP, BCP, s, e)
{
    if (BOP[s - 1] == BOP[s]) {
        return (BCP[e] - BOP[s]) * 2;
    }

    else {
        return (BCP[e] - BOP[s] + 1) * 2;
    }
}

// Driver program to test above function
var str = "())(())(())(";
var n = str.length;
var BCP = Array(n+1).fill(0);
var BOP = Array(n+1).fill(0);
constructBlanceArray(BOP, BCP, str, n);
var startIndex = 5, endIndex = 11;

document.write( "Maximum Length Correct Bracket"+
        " Subsequence between "
     + startIndex + " and " + endIndex + " = "
     + query(BOP, BCP, startIndex, endIndex) + "<br>");;
startIndex = 4, endIndex = 5;

document.write( "Maximum Length Correct Bracket"+
        " Subsequence between "
     + startIndex + " and " + endIndex + " = "
     + query(BOP, BCP, startIndex, endIndex) + "<br>");;
startIndex = 1, endIndex = 5;

document.write( "Maximum Length Correct Bracket"+
        " Subsequence between "
     + startIndex + " and " + endIndex + " = "
     + query(BOP, BCP, startIndex, endIndex) + "<br>");;

</script>
```

**Output:** 

```
Maximum Length Correct Bracket Subsequence between 5 and 11 = 4
Maximum Length Correct Bracket Subsequence between 4 and 5 = 0
Maximum Length Correct Bracket Subsequence between 1 and 5 = 2
```

**每个查询的时间复杂度为 O(1)。**