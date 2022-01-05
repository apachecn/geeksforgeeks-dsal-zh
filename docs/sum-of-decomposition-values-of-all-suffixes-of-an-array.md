# 数组所有后缀的分解值之和

> 原文:[https://www . geesforgeks . org/数组所有后缀的分解值之和/](https://www.geeksforgeeks.org/sum-of-decomposition-values-of-all-suffixes-of-an-array/)

给定一个数组 **arr[]** ，任务是找到后缀子数组的分解值之和。
**分解值:**子阵列的分解值是子阵列中可能的分区数。只有当数组的元素小于当前索引时，才能在索引![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")处对数组进行分区。即 A[k] < A[i]，其中 k ≤ i.
**例:**

> **输入:** arr[] = {2，8，4}
> **输出:** 4
> **解释:**
> arr[]的所有后缀子数组都是【2，8，4】，【8，4】，【4】
> 后缀【4】=>只有 1 个分解 **{4}**
> 后缀【8，4】=>只有 1 个分解 **{8，4 }**T15 分解值之和= 1 + 1 + 2 = 4
> **输入:** arr[] = {9，6，9，35}
> **输出:** 8
> **解释:**
> arr 的所有后缀都是[9，6，9，35]，[6，9，35]，[35]
> 后缀[35] = >只有 1 个分解 **{35 35}
> 后缀[9，6，9，35] = > 2 分解{9，6，9} {35}
> 因此，分解值之和= 1 + 2 + 3 + 2 = 8**

**做法:**思路是用[栈](https://www.geeksforgeeks.org/stack-data-structure/)解决这个问题。下面是方法的图解

*   从头到尾遍历数组。
*   保持最小变量和答案变量。
*   如果堆栈为空或当前元素小于堆栈顶部–
    *   将 S[i]推到堆栈上。
    *   将答案增加堆栈的大小。
    *   另外，保持最小值到现在。
*   否则，
    *   只要栈顶小于当前元素，就继续弹出块。
    *   用当前元素更新最小值。
    *   将最小值推送到堆栈上。因为，我们希望子阵列的最小值代表该子阵列
    *   将答案增加堆栈的大小。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// sum of Decomposition values of
// all suffixes of an array

#include <bits/stdc++.h>
using namespace std;
#define int long long int

// Function to find the decomposition
// values of the array
int decompose(vector<int> S)
{
    // Stack
    stack<int> s;
    int N = S.size();
    int ans = 0;

    // Variable to maintain
    // min value in stack
    int nix = INT_MAX;

    // Loop to iterate over the array
    for (int i = N - 1; i >= 0; i--) {

        // Condition to check if the
        // stack is empty
        if (s.empty()) {
            s.push(S[i]);
            nix = S[i];
        }
        else {

            // Condition to check if the
            // top of the stack is greater
            // than the current element
            if (S[i] < s.top()) {
                s.push(S[i]);
                nix = min(nix, S[i]);
            }
            else {
                int val = S[i];

                // Loop to pop the element out
                while (!s.empty() &&
                       val >= s.top()) {
                    s.pop();
                }
                nix = min(nix, S[i]);
                s.push(nix);
            }
        }

        // the size of the stack is the
        // max no of subarrays for
        // suffix till index i
        // from the right
        ans += s.size();
    }

    return ans;
}

// Driver Code
signed main()
{
    vector<int> S = { 9, 6, 9, 35 };
    cout << decompose(S) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// sum of Decomposition values of
// all suffixes of an array
import java.util.*;

class GFG{

// Function to find the decomposition
// values of the array
static int decompose(Vector<Integer> S)
{

    // Stack
    Stack<Integer> s = new Stack<Integer>();
    int N = S.size();
    int ans = 0;

    // Variable to maintain
    // min value in stack
    int nix = Integer.MAX_VALUE;

    // Loop to iterate over the array
    for(int i = N - 1; i >= 0; i--)
    {

       // Condition to check if the
       // stack is empty
       if (s.isEmpty())
       {
           s.add(S.get(i));
           nix = S.get(i);
       }
       else
       {

           // Condition to check if the
           // top of the stack is greater
           // than the current element
           if (S.get(i) < s.peek())
           {
               s.add(S.get(i));
               nix = Math.min(nix, S.get(i));
           }
           else
           {
               int val = S.get(i);

               // Loop to pop the element out
               while (!s.isEmpty() && val >= s.peek())
               {
                   s.pop();
               }
               nix = Math.min(nix, S.get(i));
               s.add(nix);
           }
       }

       // The size of the stack is the
       // max no of subarrays for
       // suffix till index i
       // from the right
       ans += s.size();
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    Vector<Integer> S = new Vector<Integer>();
    S.add(9);
    S.add(6);
    S.add(9);
    S.add(35);

    System.out.println(decompose(S));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# sum of Decomposition values of
# all suffixes of an array
import sys

# Function to find the decomposition
# values of the array
def decompose(S):

    # Stack
    s = []
    N = len(S)
    ans = 0

    # Variable to maintain
    # min value in stack
    nix = sys.maxsize

    # Loop to iterate over the array
    for i in range(N - 1, -1, -1):

        # Condition to check if the
        # stack is empty
        if (len(s) == 0):
            s.append(S[i])
            nix = S[i]

        else:

            # Condition to check if the
            # top of the stack is greater
            # than the current element
            if (S[i] < s[-1]):
                s.append(S[i])
                nix = min(nix, S[i])

            else:
                val = S[i]

                # Loop to pop the element out
                while (len(s) != 0 and
                          val >= s[-1]):
                    s.pop()

                nix = min(nix, S[i]);
                s.append(nix)

        # The size of the stack is the
        # max no of subarrays for
        # suffix till index i
        # from the right
        ans += len(s)

    return ans

# Driver Code
if __name__ =="__main__":

    S = [ 9, 6, 9, 35 ]

    print(decompose(S))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the
// sum of Decomposition values of
// all suffixes of an array
using System;
using System.Collections.Generic;

class GFG{

// Function to find the decomposition
// values of the array
static int decompose(List<int> S)
{

    // Stack
    Stack<int> s = new Stack<int>();

    int N = S.Count;
    int ans = 0;

    // Variable to maintain
    // min value in stack
    int nix = Int32.MaxValue;

    // Loop to iterate over the array
    for(int i = N - 1; i >= 0; i--)
    {

        // Condition to check if the
        // stack is empty
        if (s.Count == 0)
        {
            s.Push(S[i]);
            nix = S[i];
        }
        else
        {

            // Condition to check if the
            // top of the stack is greater
            // than the current element
            if (S[i] < s.Peek())
            {
                s.Push(S[i]);
                nix = Math.Min(nix, S[i]);
            }
            else
            {
                int val = S[i];

                // Loop to pop the element out
                while (s.Count != 0 && val >= s.Peek())
                {
                    s.Pop();
                }
                nix = Math.Min(nix, S[i]);
                s.Push(nix);
            }
        }

        // The size of the stack is the
        // max no of subarrays for
        // suffix till index i
        // from the right
        ans += s.Count;
    }
    return ans;
}

// Driver code
static void Main()
{
    List<int> S = new List<int>();
    S.Add(9);
    S.Add(6);
    S.Add(9);
    S.Add(35);

    Console.WriteLine(decompose(S));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// sum of Decomposition values of
// all suffixes of an array

// Function to find the decomposition
// values of the array
function decompose(S)
{

    // Stack
    let s = [];
    let N = S.length;
    let ans = 0;

    // Variable to maintain
    // min value in stack
    let nix = Number.MAX_VALUE;

    // Loop to iterate over the array
    for(let i = N - 1; i >= 0; i--)
    {

       // Condition to check if the
       // stack is empty
       if (s.length==0)
       {
           s.push(S[i]);
           nix = S[i];
       }
       else
       {

           // Condition to check if the
           // top of the stack is greater
           // than the current element
           if (S[i] < s[s.length-1])
           {
               s.push(S[i]);
               nix = Math.min(nix, S[i]);
           }
           else
           {
               let val = S[i];

               // Loop to pop the element out
               while (s.length!=0 && val >= s[s.length-1])
               {
                   s.pop();
               }
               nix = Math.min(nix, S[i]);
               s.push(nix);
           }
       }

       // The size of the stack is the
       // max no of subarrays for
       // suffix till index i
       // from the right
       ans += s.length;
    }
    return ans;
}

// Driver Code
let S = [];
S.push(9);
S.push(6);
S.push(9);
S.push(35);

document.write(decompose(S));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
8
```