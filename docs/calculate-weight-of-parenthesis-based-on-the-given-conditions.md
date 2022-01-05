# 根据给定条件

计算括号的权重

> 原文:[https://www . geesforgeks . org/基于给定条件计算括号权重/](https://www.geeksforgeeks.org/calculate-weight-of-parenthesis-based-on-the-given-conditions/)

给定一个有效的括号字符串 **S** ，任务是根据以下条件找到括号的权重:

1.  “()”的权重为 1
2.  “AB”的重量= A 的重量+B 的重量(其中，A 和 B 都是独立的有效括号)。例如“()()”的重量=“()”的重量+“()”的重量
3.  “(A)”的重量= 2 倍于“A”的重量(其中 A 是独立的有效括号)。例如，“()”的重量是“()”重量的 2 倍

**示例:**

> **输入:**S =()(())”
> **输出:** 3
> **说明:**
> 的重量()= 1
> 的重量(())= 2
> 因此，重量()(())= 1 + 2 = 3
> 
> **输入:**S =(()((())))
> **输出:** 6
> **说明:**
> 重量为()(())= 3
> 重量为(()(())))= 2 * 3 = 6

**方式:**
这个问题可以用[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)的方式解决。按照以下步骤解决问题:

*   假设输入括号字符串始终有效，即平衡。所以，任何 ***的左括号“(‘***都有对应的 ***的右括号“)”*** 。
*   考虑输入字符串开头的左括号(左括号不能是右括号，否则无效)。现在，对于这个左括号，对应的右括号可以有以下两个可能的索引。
    1.  在最末端，即 **(n-1) <sup>第</sup>指数**
    2.  介于**开始**和**结束**之间，即**【1，n-2】**
*   如果右括号的末尾有一个索引，那么根据约束 3，括号的总重量将是字符串[1，n-2] 重量的两倍 ***。***

*   如果右括号在开始和结束之间，比如中间，那么根据约束 2，括号的**总重量将是弦【开始，中间】**重量的**总和和弦【中间+1，结束】**重量的**总和。** 
*   递归的基本情况是，当字符串中只有两个括号时，它们的权重为 1，因为它们本质上是有效的。

*   现在，问题是我们如何找到一个左括号对应的右括号的索引。这个想法类似于[有效括号检查](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)。我们将使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)检查并在[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中存储相应左括号的右括号索引。

*   请执行以下步骤:
    *   遍历字符串。
    *   如果字符是左括号，将其索引推入**堆栈**。
    *   如果是右括号，从**栈**弹出其索引，将 ***(弹出 _ 索引，当前 _ 索引)*** 配对插入 **HashMap** 。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// HashMap to store the ending
// index of every opening bracket
unordered_map<int, int> endIndex;

// Function to calculate and store
// the closing index of each opening
// bracket in the parenthesis
void getClosingIndex(string s)
{
    int n = s.length();

    stack<int> st;

    for(int i = 0; i < n; i++)
    {
        if (s[i] == ')')
        {

            // If it's a closing bracket,
            // pop index of it's corresponding
            // opening bracket
            int startIndex = st.top();
            st.pop();

            // Insert the index of opening
            // bracket and closing bracket
            // as key-value pair in the
            // hashmap
            endIndex[startIndex] = i;
        }
        else
        {

            // If it's an opening bracket,
            // push it's index into the stack
            st.push(i);
        }
    }
}

// Function to return the weight of
// parenthesis
int calcWeight(string s, int low, int high)
{

    // Base case
    if (low + 1 == high)
    {
        return 1;
    }

    else
    {

        // Mid refers to ending index of
        // opening bracket at index low
        int mid = endIndex[low];

        if (mid == high)
        {
            return 2 * calcWeight(s, low + 1,
                                    high - 1);
        }
        else
        {
            return calcWeight(s, low, mid) +
                   calcWeight(s, mid + 1,
                              high);
        }
    }
}

// Driver Code
int main()
{
    string input = "(()(()))";
    int n = input.length();

    // Update the closing Index
    getClosingIndex(input);

    cout << (calcWeight(input, 0, n - 1)) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

public class GFG {

    // HashMap to store the ending
    // index of every opening bracket
    static HashMap<Integer, Integer> endIndex
        = new HashMap<Integer, Integer>();

    // Function to calculate and store
    // the closing index of each opening
    // bracket in the parenthesis
    public static void getClosingIndex(String s)
    {

        int n = s.length();

        Stack<Integer> st = new Stack<Integer>();

        for (int i = 0; i < n; i++) {

            if (s.charAt(i) == ')') {

                // If it's a closing bracket,
                // pop index of it's corresponding
                // opening bracket
                int startIndex = st.pop();

                // Insert the index of opening
                // bracket and closing bracket
                // as key-value pair in the
                // hashmap
                endIndex.put(startIndex, i);
            }
            else {

                // If it's an opening bracket,
                // push it's index into the stack
                st.push(i);
            }
        }
    }

    // Function to return the weight of
    // parenthesis
    public static int calcWeight(String s,
                                int low,
                                int high)
    {

        // Base case
        if (low + 1 == high) {
            return 1;
        }

        else {

            // Mid refers to ending index of
            // opening bracket at index low
            int mid = endIndex.get(low);
            if (mid == high) {
                return 2 * calcWeight(s, low + 1,
                                    high - 1);
            }
            else {
                return calcWeight(s, low, mid)
                    + calcWeight(s, mid + 1,
                                high);
            }
        }
    }

    public static void main(String[] args)
    {
        String input = "(()(()))";
        int n = input.length();

        // Update the closing Index
        getClosingIndex(input);

        System.out.println(calcWeight(input,
                                    0, n - 1));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to calculate and store
# the closing index of each opening
# bracket in the parenthesis
def getClosingIndex(string):

    # Dictionary to store
    # the ending index of
    # each opening bracket
    endIndex = dict()

    n = len(string)

    stack = []
    for i in range(n):
        if (string[i]==')'):

            # If it's a closing bracket,
            # pop index of it's
            # corresponding
            # opening bracket
            startIndex = stack.pop()

            # Put the index of opening
            # bracket and closing
            # bracket as key value
            # pair in the Dictionary
            endIndex[startIndex] = i

        else:

            # If it's an opening bracket,
            # push it's index into
            # the stack
            stack.append(i)
    return endIndex

# Function to return the weight
# of parenthesis
def calcWeight(s, low,
                high, endIndex):

    # Base case
    if (low + 1 == high):
        return 1
    else:

        # Mid refers to ending index of
        # opening bracket at index low
        mid = endIndex[low]
        if (mid == high):
            return 2*(calcWeight(s, low + 1,
            high-1, endIndex))

        else:
            return calcWeight(s, low,
            mid, endIndex) + calcWeight(s,
            mid + 1, high, endIndex)

if __name__ == "__main__":
    string = "(()(()))"
    n = len(string)
    endIndex = getClosingIndex(string)
    print(calcWeight(string, 0,
    n-1, endIndex))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// HashMap to store the ending
// index of every opening bracket
static Dictionary<int,
                  int> endIndex = new Dictionary<int,
                                                 int>();

// Function to calculate and store
// the closing index of each opening
// bracket in the parenthesis
public static void getClosingIndex(string s)
{
    int n = s.Length;

    Stack<int> st = new Stack<int>();

    for(int i = 0; i < n; i++)
    {
        if (s[i] == ')')
        {

            // If it's a closing bracket,
            // pop index of it's corresponding
            // opening bracket
            int startIndex = st.Pop();

            // Insert the index of opening
            // bracket and closing bracket
            // as key-value pair in the
            // hashmap
            endIndex.Add(startIndex, i);
        }
        else
        {

            // If it's an opening bracket,
            // push it's index into the stack
            st.Push(i);
        }
    }
}

// Function to return the weight of
// parenthesis
public static int calcWeight(string s, int low,
                                       int high)
{

    // Base case
    if (low + 1 == high)
    {
        return 1;
    }
    else
    {

        // Mid refers to ending index of
        // opening bracket at index low
        int mid = endIndex[low];
        if (mid == high)
        {
            return 2 * calcWeight(s, low + 1,
                                    high - 1);
        }
        else
        {
            return calcWeight(s, low, mid) +
                   calcWeight(s, mid + 1, high);
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    string input = "(()(()))";
    int n = input.Length;

    // Update the closing Index
    getClosingIndex(input);

    Console.Write(calcWeight(input, 0, n - 1));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// HashMap to store the ending
// index of every opening bracket
var endIndex = new Map();

// Function to calculate and store
// the closing index of each opening
// bracket in the parenthesis
function getClosingIndex(s)
{
    var n = s.length;

    var st = [];

    for(var i = 0; i < n; i++)
    {
        if (s[i] == ')')
        {

            // If it's a closing bracket,
            // pop index of it's corresponding
            // opening bracket
            var startIndex = st[st.length-1];
            st.pop();

            // Insert the index of opening
            // bracket and closing bracket
            // as key-value pair in the
            // hashmap
            endIndex[startIndex] = i;
        }
        else
        {

            // If it's an opening bracket,
            // push it's index into the stack
            st.push(i);
        }
    }
}

// Function to return the weight of
// parenthesis
function calcWeight(s, low, high)
{

    // Base case
    if (low + 1 == high)
    {
        return 1;
    }

    else
    {

        // Mid refers to ending index of
        // opening bracket at index low
        var mid = endIndex[low];

        if (mid == high)
        {
            return 2 * calcWeight(s, low + 1,
                                    high - 1);
        }
        else
        {
            return calcWeight(s, low, mid) +
                   calcWeight(s, mid + 1,
                              high);
        }
    }
}

// Driver Code
var input = "(()(()))";
var n = input.length;
// Update the closing Index
getClosingIndex(input);
document.write((calcWeight(input, 0, n - 1)));

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)，其中 N 为字符串的长度。*