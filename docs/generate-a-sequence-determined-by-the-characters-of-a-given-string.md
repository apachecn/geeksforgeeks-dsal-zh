# 生成由给定字符串的字符确定的序列

> 原文:[https://www . geesforgeks . org/generate-a-sequence-由给定字符串的字符决定/](https://www.geeksforgeeks.org/generate-a-sequence-determined-by-the-characters-of-a-given-string/)

给定一个长度为**N**(*1≤N≤10<sup>5</sup>*)的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是打印一个由满足以下条件的整数 **0** 到 **N** 组成的排列 **A** :

*   如果 **S[i] = 1** ，那么 **A[i] < A[i + 1]** 。
*   如果 **S[i] = 0** ，则 **A[i] > A[i + 1]** 。

**例:**

> ***输入:**S =【001】*
> T5】**输出:**【3、2、0、1】
> **解释:**
> S[0] = 0 和 A[0](= 3)>A[1](= 2)
> S[1]= 0 和 A[1](= 2)>A[2](= 0)
> S[2]= 0
> 
> ***输入:** S = "1010"*
> ***输出:**【0，4，1，3，2】*

**方法:**按照以下步骤解决问题:

*   如果字符串中遇到的字符是**‘1’**，则分配可能的最低数字。
*   如果字符串中遇到的字符是**‘0’**，则分配可能的最高数字。
*   设置两个指针 **lo (= 0)** ，存储当前最低可能值， **hi (= N)** ，存储当前最高可能值。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并将值附加到结果数组中，例如 **re** s，相应地使用两个指针。
*   在字符串完全遍历之后，只剩下一个值需要追加。将 **lo** 追加到最后一个索引。
*   [打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **res** 作为所需结果。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the
// required sequence
void StringPattern(string S)
{
    // Length of the string
    int n = (int)S.size();

    // Pointers to store lowest and
    // highest possible values
    int l = 0, r = n;

    // Stores the required answer
    vector<int> res(n + 1, 0);

    for (int i = 0; i < n; i++) {

        switch (S[i]) {

        // If current character is '1'
        case '1':

            // Assign smallest
            // possible value
            res[i] = l++;
            break;

        // If current character is '0'
        case '0':

            // Assign largest
            // possible value
            res[i] = r--;
            break;
        }
    }

    // At this point, l == r ，
    // only one value is not assigned yet.
    res[n] = l;
    for (int el : res) {
        cout << el << " ";
    }
}

// Driver Code
int main()
{
    string s = "001";
    StringPattern(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above approach
import java.util.*;
class GFG
{

// function to find minimum required permutation
static void StringPattern(String s)
{
    int n = s.length();
    int l = 0, r = n; 
    int [] res = new int[n + 1];
    for (int x = 0; x < n; x++)
    {
        if (s.charAt(x) == '1')
        {
            res[x] = l++;
        }
        else if(s.charAt(x) == '0')
        {
            res[x] = r--;
        }
    }    
    res[n] = l;
    for(int i = 0; i < n+1; i++)
    {
        System.out.print(res[i]+" ");
    }
}

// Driver code
public static void main(String[] args)
{
    String s = "001";
    StringPattern(s);
}
}

// This code is contributed by mohit kumar 29.
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to print the
# required sequence
def StringPattern(S):

    # Stores the lowest, highest
    # possible values that can be
    # appended, size of the string
    lo, hi = 0, len(S)

    # Stores the required result
    ans = []

    # Traverse the string
    for x in S:

        # If current character is '1'
        if x == '1':

            # Append lowest
            # possible value
            ans.append(lo)

            lo += 1

        # If current character is '0'
        else:

            # Append highest
            # possible value
            ans.append(hi)

            hi -= 1

    return ans + [lo]

# Driver Code
if __name__ == "__main__":
        # Input
    s = '001'
    print(StringPattern(s))
```

## C#

```
// C# Implementation of above approach
using System;
class GFG
{

// function to find minimum required permutation
static void StringPattern(String s)
{
    int n = s.Length;
    int l = 0, r = n; 
    int [] res = new int[n + 1];
    for (int x = 0; x < n; x++)
    {
        if (s[x] == '1')
        {
            res[x] = l++;
        }
        else if(s[x] == '0')
        {
            res[x] = r--;
        }
    }    
    res[n] = l;
    for(int i = 0; i < n + 1; i++)
    {
        Console.Write(res[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    String s = "001";
    StringPattern(s);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program of
// the above approach

 // function to find minimum
 // required permutation
function StringPattern(s)
{
    let n = s.length;
    let l = 0, r = n;
    let res = new Array(n+1).fill(0);
    for (let x = 0; x < n; x++)
    {
        if (s[x] == '1')
        {
            res[x] = l++;
        }
        else if(s[x] == '0')
        {
            res[x] = r--;
        }
    }   
    res[n] = l;
    for(let i = 0; i < n+1; i++)
    {
        document.write(res[i]+" ");
    }
}

    // Driver Code

    let s = "001";
    StringPattern(s);

</script>
```

**Output:** 

```
3 2 0 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)