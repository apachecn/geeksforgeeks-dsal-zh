# 寻找范埃克序列第 n 项的程序

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-of-van-ecks-sequence/](https://www.geeksforgeeks.org/program-to-find-nth-term-of-the-van-ecks-sequence/)

给定一个正整数 **N** ，任务是打印*范埃克序列*的第**N**T4 项。
在数学中，范埃克序列是一个整数序列，其递归定义如下:

*   设第一项为 0，即 a <sub>0</sub> = 0。
*   那么对于 n >= 0，如果存在 m < n

```
am = an
```

*   取最大的 m，设置一个<sub>n+1</sub>= n-m；
*   否则 a <sub>n+1</sub> = 0。
*   以 a(1)=0 开始。

范埃克序列的前几个术语如下:

> 0，0，1，0，2，0，2，2，2，1，6，0，5，0，2，6，5，4，0，5……

**例:**

```
Input: N = 5
Output: 2

Input: N = 10
Output: 6 
```

**方法:**
如上所述，我们可以按照以下步骤生成范埃克的序列:

*   将序列的第一项设置为 0。
*   然后重复应用:
    *   如果最后一项还没有出现，并且到目前为止是新的，那么将下一项设置为零。
    *   否则，下一个术语就是上一个术语出现的时间。
*   一旦序列生成，我们就可以很容易地得到我们的第**n**T2 项。

以下是上述方法的实现:

## C++

```
// C++ program to print Nth
// term of Van Eck's sequence

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000
int sequence[MAX];

// Utility function to compute
// Van Eck's sequence
void vanEckSequence()
{

    // Initialize sequence array
    for (int i = 0; i < MAX; i++) {
        sequence[i] = 0;
    }

    // Loop to generate sequence
    for (int i = 0; i < MAX; i++) {

        // Check if sequence[i] has occurred
        // previously or is new to sequence
        for (int j = i - 1; j >= 0; j--) {
            if (sequence[j] == sequence[i]) {

                // If occurrence found
                // then the next term will be
                // how far back this last term
                // occurred previously
                sequence[i + 1] = i - j;
                break;
            }
        }
    }
}

// Utility function to return
// Nth term of sequence
int getNthTerm(int n)
{

    return sequence[n];
}

// Driver code
int main()
{

    // Pre-compute Van Eck's sequence
    vanEckSequence();

    int n = 6;

    // Print nth term of the sequence
    cout << getNthTerm(n) << endl;

    n = 100;

    // Print nth term of the sequence
    cout << getNthTerm(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Nth
// term of Van Eck's sequence

class GFG {

    static int MAX = 1000;

    // Array to store terms of sequence
    static int sequence[] = new int[MAX];

    // Utility function to compute
    // Van Eck's sequence
    static void vanEckSequence()
    {

        // Initialize sequence array
        for (int i = 0; i < MAX - 1; i++) {
            sequence[i] = 0;
        }

        // Loop to generate sequence
        for (int i = 0; i < MAX - 1; i++) {

            // Check if sequence[i] has occurred
            // previously or is new to sequence
            for (int j = i - 1; j >= 0; j--) {
                if (sequence[j] == sequence[i]) {

                    // If occurrence found
                    // then the next term will be
                    // how far back this last term
                    // occurred previously
                    sequence[i + 1] = i - j;
                    break;
                }
            }
        }
    }

    // Utility function to return
    // Nth term of sequence
    static int getNthTerm(int n)
    {

        return sequence[n];
    }

    // Driver code
    public static void main(String[] args)
    {

        // Pre-compute Van Eck's sequence
        vanEckSequence();

        int n = 6;

        // Print nth term of the sequence
        System.out.println(getNthTerm(n));

        n = 100;

        // Print nth term of the sequence
        System.out.println(getNthTerm(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to print Nth
# term of Van Eck's sequence
MAX = 1000
sequence = [0] * (MAX + 1);

# Utility function to compute
# Van Eck's sequence
def vanEckSequence() :

    # Initialize sequence array
    for i in range(MAX) :
        sequence[i] = 0;

    # Loop to generate sequence
    for i in range(MAX) :

        # Check if sequence[i] has occurred
        # previously or is new to sequence
        for j in range(i - 1 , -1, -1) :
            if (sequence[j] == sequence[i]) :

                # If occurrence found
                # then the next term will be
                # how far back this last term
                # occurred previously
                sequence[i + 1] = i - j;
                break;

# Utility function to return
# Nth term of sequence
def getNthTerm(n) :

    return sequence[n];

# Driver code
if __name__ == "__main__" :

    # Pre-compute Van Eck's sequence
    vanEckSequence();

    n = 6;

    # Print nth term of the sequence
    print(getNthTerm(n));

    n = 100;

    # Print nth term of the sequence
    print(getNthTerm(n));

# This code is contributed by kanugargng
```

## C#

```
// C# program to print Nth
// term of Van Eck's sequence

using System;
class GFG {

    static int MAX = 1000;

    // Array to store terms of sequence
    static int[] sequence = new int[MAX];

    // Utility function to compute
    // Van Eck's sequence
    static void vanEckSequence()
    {

        // Initialize sequence array
        for (int i = 0; i < MAX - 1; i++) {
            sequence[i] = 0;
        }

        // Loop to generate sequence
        for (int i = 0; i < MAX - 1; i++) {

            // Check if sequence[i] has occurred
            // previously or is new to sequence
            for (int j = i - 1; j >= 0; j--) {
                if (sequence[j] == sequence[i]) {

                    // If occurrence found
                    // then the next term will be
                    // how far back this last term
                    // occurred previously
                    sequence[i + 1] = i - j;
                    break;
                }
            }
        }
    }

    // Utility function to return
    // Nth term of sequence
    static int getNthTerm(int n)
    {

        return sequence[n];
    }

    // Driver code
    public static void Main()
    {

        // Pre-compute Van Eck's sequence
        vanEckSequence();

        int n = 6;

        // Print nth term of the sequence
        Console.WriteLine(getNthTerm(n));

        n = 100;

        // Print nth term of the sequence
        Console.WriteLine(getNthTerm(n));
    }
}
```

## java 描述语言

```
<script>

// Javascript program to print Nth
// term of Van Eck's sequence

var MAX = 1000;
var sequence = Array(MAX).fill(0);

// Utility function to compute
// Van Eck's sequence
function vanEckSequence()
{

    // Initialize sequence array
    for (var i = 0; i < MAX; i++) {
        sequence[i] = 0;
    }

    // Loop to generate sequence
    for (var i = 0; i < MAX; i++) {

        // Check if sequence[i] has occurred
        // previously or is new to sequence
        for (var j = i - 1; j >= 0; j--) {
            if (sequence[j] == sequence[i]) {

                // If occurrence found
                // then the next term will be
                // how far back this last term
                // occurred previously
                sequence[i + 1] = i - j;
                break;
            }
        }
    }
}

// Utility function to return
// Nth term of sequence
function getNthTerm(n)
{

    return sequence[n];
}

// Driver code
// Pre-compute Van Eck's sequence
vanEckSequence();
var n = 6;

// Print nth term of the sequence
document.write( getNthTerm(n) + "<br>");
n = 100;

// Print nth term of the sequence
document.write( getNthTerm(n) + "<br>");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
2
23
```

**方法 2:使用 lambda 函数**
不需要存储整个序列来获取**n**T5 项的值。我们可以递归地构建直到第 n 项的系列，并使用[λ表达式](https://www.geeksforgeeks.org/lambda-expressions-java-8/)只找到第 n 个**项的值。
下面是使用 lambda 函数实现上述方法:** 

## 蟒蛇 3

```
# Python3 program to find
# Nth term of Van Eck's sequence
# using the lambda expression

# Lambda function 
f = lambda n, l = 0, *s : f(n-1, l in s and ~s.index(l), l, *s) \
if n else -l

# The above lambda function recursively
# build the sequence and store it in tuple s

# The expression l in s and ~s.index(l)
# returns False if l is not present in tuple s
# otherwise, returns the negation of the value of
# the index of l in tuple s
# and is appended to tuple s
# Thus, tuple s store negation of all the elements
# of the sequence in reverse order

# At the end, when n reaches 0, function converts
# the nth term back to its actual value
# and returns it.

# Driver code
n = 6

# Get Nth term of the sequence
print(f(n))

n = 100
# Get Nth term of the sequence
print(f(n))
```

**Output:** 

```
2
23
```

**参考:**[https://codegolf . stackexchange . com/questions/186654/n-term-of-van-eck-sequence](https://codegolf.stackexchange.com/questions/186654/nth-term-of-van-eck-sequence)