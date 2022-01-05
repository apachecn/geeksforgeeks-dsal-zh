# 使用堆栈

以递减顺序打印给定整数的质因数

> 原文:[https://www . geesforgeks . org/print-给定整数的质因数递减顺序使用堆栈/](https://www.geeksforgeeks.org/print-prime-factors-of-a-given-integer-in-decreasing-order-using-stack/)

给定一个整数 **N** ，任务是使用[堆栈数据结构以降序打印 **N** 的](https://www.geeksforgeeks.org/stack-data-structure/)[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。

**示例:**

> **输入:** N = 34
> **输出:**
> 17 2
> **说明:**
> 数字 34 的质因数是 2 和 17。
> 
> **输入:**N = 8
> T3】输出: 2

**方式:**思路是使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)存储**N**T7】的所有[质因数，最后打印](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)[栈](https://www.geeksforgeeks.org/stack-data-structure/)中的所有值。按照以下步骤解决问题:

1.  初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)，比如 **st** 。
2.  [跑一圈](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)同时 **N！= 1** 。从 **i = 2、**开始，对于 **i** 的每个值，运行一个循环，直到 **N % i == 0** 和[将 **i** 推入堆栈](https://www.geeksforgeeks.org/stack-push-method-in-java/) **st** 并将 **N** 更新为 **N/i.**
3.  最后，[从栈顶到底打印所有值](https://www.geeksforgeeks.org/print-stack-elements-from-top-to-bottom/) **st** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print prime factors
// of N in decreasing order
void PrimeFactors(int N)
{
    // Stores prime factors of N
    // in decreasing order
    stack<int> st;

    int i = 2;
    while (N != 1) {

        if (N % i == 0) {

            // Insert i into stack
            st.push(i);

            while (N % i == 0) {

                // Update N
                N = N / i;
            }
        }

        // Update i
        i++;
    }

    // Print value of stack st
    while (!st.empty()) {

        printf("%d ", st.top());
        st.pop();
    }
}

// Driver Code
int main()
{
    int N = 8;

    // function Call
    PrimeFactors(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
import java.util.*;

class GFG{

// Function to print prime factors
// of N in decreasing order
static void PrimeFactors(int N)
{

    // Stores prime factors of N
    // in decreasing order
    Stack<Integer> st = new Stack<>();

    int i = 2;

    while (N != 1)
    {
        if (N % i == 0)
        {

            // Insert i into stack
            st.push(i);

            while (N % i == 0)
            {

                // Update N
                N = N / i;
            }
        }

        // Update i
        i++;
    }

    // Print value of stack st
    while (!st.isEmpty())
    {
        System.out.println(st.peek());
        st.pop();
    }
}

// Driver Code   
public static void main (String[] args)   
{   
    int N = 8;

    // Function Call
    PrimeFactors(N);;
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print prime factors
# of N in decreasing order
def PrimeFactors(N):

    # Stores prime factors of N
    # in decreasing order
    st = []
    i = 2
    while (N != 1):
        if (N % i == 0):

            # Insert i into stack
            st.append(i)
            while (N % i == 0):

                # Update N
                N = N // i

        # Update i
        i += 1

    # Print value of stack st
    while (len(st) != 0):
        print(st[-1])
        st.pop()

# Driver Code
if __name__ == "__main__":
    N = 8

    # function Call
    PrimeFactors(N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print prime factors
// of N in decreasing order
static void PrimeFactors(int N)
{

    // Stores prime factors of N
    // in decreasing order
    Stack<int> st = new Stack<int>();

    int i = 2;

    while (N != 1)
    {
        if (N % i == 0)
        {

            // Insert i into stack
            st.Push(i);

            while (N % i == 0)
            {

                // Update N
                N = N / i;
            }
        }

        // Update i
        i++;
    }

    // Print value of stack st
    while (st.Count != 0)
    {
        Console.Write(st.Peek());
        st.Pop();
    }
}

// Driver Code   
public static void Main ()   
{  
    int N = 8;

    // Function Call
    PrimeFactors(N);;
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print prime factors
// of N in decreasing order
function PrimeFactors(N)
{
    // Stores prime factors of N
    // in decreasing order
    let st = [];

    let i = 2;

    while (N != 1)
    {
        if (N % i == 0)
        {

            // Insert i into stack
            st.push(i);

            while (N % i == 0)
            {

                // Update N
                N = Math.floor(N / i);
            }
        }

        // Update i
        i++;
    }

    // Print value of stack st
    while (st.length!=0)
    {
        document.write(st.pop());

    }
}
// Driver Code  
let N = 8;

// Function Call
PrimeFactors(N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(sqrt(N))
**辅助空间:** O(1)