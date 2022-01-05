# 通过反转由偶数个 1 组成的子串来检查二进制字符串是否可以转换成另一个

> 原文:[https://www . geeksforgeeks . org/check-if-一个二进制字符串可以通过反转子字符串转换为另一个二进制字符串-由偶数个 1 组成/](https://www.geeksforgeeks.org/check-if-a-binary-string-can-be-converted-to-another-by-reversing-substrings-consisting-of-even-number-of-1s/)

给定两个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **A** 和 **B** ，任务是通过反转包含偶数个 **1** s 的 **A** 的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)来检查字符串 **A** 是否可以转换为 **B** 。

**示例:**

> **输入:**A =“10011”，B =“11100”
> **输出:**是
> **说明:**反转子串 A[2，5]，1 **0011** → 11100。
> 完成上述步骤后，字符串 A 和 B 相同。
> 
> **输入:**A = " 10011 " B = " 00111 "
> T3】输出:否

**方法:**该想法基于以下观察:

*   如果弦 **A** 可以转换成弦 **B** ，那么反过来也成立，因为转换 **A** 到 **B** 的操作可以反过来转换 **B** 到 **A** 。
*   **A** 只能等于 **B** 当:
    *   **长度(A) =长度(B)****A**和 **B** 中 **1s** 的数量相同
    *   **CNT<sub>A</sub>= CNT<sub>B</sub>**<sub>其中 **cnt <sub>S</sub>** 是 **i** 的位置号其中 **1 ≤ i ≤长度(S)** 和**(∑<sup>I</sup><sub>j = 1</sub>(S<sub>j</sub>)mod 2 = 1【T23**</sub>

按照以下步骤解决问题:

1.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **A** 和 **B** 和[在变量中存储 1](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/) 的频率，分别说 **count1A** 和 **count1B** 。
2.  初始化一个变量，比如**温度**，来存储 **1s** 的临时计数。
3.  使用变量 **i** 遍历字符串 **A** ，并执行以下步骤:
    *   如果当前字符是 **1** ，那么将**温度**增加 **1** 。
    *   否则，[如果**温度**的值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将变量 **odd1A** 增加 **1** 。否则，将变量 **even1A** 增加 1。
4.  重复上述步骤 **2** 至 **3** 进行串 **B** 也。
5.  完成上述步骤后，如果 **count1A** 和 **count1B** 的值相同， **odd1A** 和 **odd1B** 的值相同， **even1A** 和 **even1B** 的值相同，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if string A can be
// transformed to string B by reversing
// substrings of A having even number of 1s
void canTransformStrings(string A, string B)
{
    // Store the size of string A
    int n1 = A.size();

    // Store the size of string B
    int n2 = B.size();

    // Store the count of 1s in A and B
    int count1A = 0, count1B = 0;

    // Stores cntA for string A
    // and cntB for string B
    int odd1A = 0, odd1B = 0;
    int even1A = 0, even1B = 0;

    // Traverse the string A
    for (int i = 0; i < n1; i++) {

        // If current character is 1
        if (A[i] == '1')

            // Increment 1s count
            count1A++;

        // Otherwise, update odd1A or
        // even1A depending whether
        // count1A is odd or even
        else {
            if (count1A & 1)
                odd1A++;
            else
                even1A++;
        }
    }

    // Traverse the string B
    for (int i = 0; i < n2; i++) {

        // If current character is 1
        if (B[i] == '1')

            // Increment 1s count
            count1B++;

        // Otherwise, update odd1B or
        // even1B depending whether
        // count1B is odd or even
        else {
            if (count1B & 1)
                odd1B++;
            else
                even1B++;
        }
    }

    // If the condition is satisfied
    if (count1A == count1B
        && odd1A == odd1B
        && even1A == even1B) {

        // If true, print Yes
        cout << "Yes";
    }

    // Otherwise, print No
    else
        cout << "No";
}

// Driver Code
int main()
{
    string A = "10011", B = "11100";

    // Function Call
    canTransformStrings(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if string A can be
// transformed to string B by reversing
// substrings of A having even number of 1s
public static void canTransformStrings(String A,
                                       String B)
{

    // Store the size of string A
    int n1 = A.length();

    // Store the size of string B
    int n2 = B.length();

    // Store the count of 1s in A and B
    int count1A = 0, count1B = 0;

    // Stores cntA for string A
    // and cntB for string B
    int odd1A = 0, odd1B = 0;
    int even1A = 0, even1B = 0;

    // Traverse the string A
    for(int i = 0; i < n1; i++)
    {

        // If current character is 1
        if (A.charAt(i) == '1')

            // Increment 1s count
            count1A++;

        // Otherwise, update odd1A or
        // even1A depending whether
        // count1A is odd or even
        else
        {
            if ((count1A & 1) == 1)
                odd1A++;
            else
                even1A++;
        }
    }

    // Traverse the string B
    for(int i = 0; i < n2; i++)
    {

        // If current character is 1
        if (B.charAt(i) == '1')

            // Increment 1s count
            count1B++;

        // Otherwise, update odd1B or
        // even1B depending whether
        // count1B is odd or even
        else
        {
            if ((count1B & 1) == 1)
                odd1B++;
            else
                even1B++;
        }
    }

    // If the condition is satisfied
    if (count1A == count1B &&
          odd1A == odd1B &&
         even1A == even1B)
    {

        // If true, print Yes
        System.out.print("Yes");
    }

    // Otherwise, print No
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    String A = "10011", B = "11100";

    // Function Call
    canTransformStrings(A, B);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if string A can be
# transformed to string B by reversing
# substrings of A having even number of 1s
def canTransformStrings(A, B):

    # Store the size of string A
    n1 = len(A);

    # Store the size of string B
    n2 = len(B);

    # Store the count of 1s in A and B
    count1A = 0;
    count1B = 0;

    # Stores cntA for string A
    # and cntB for string B
    odd1A = 0; odd1B = 0;
    even1A = 0; even1B = 0;

    # Traverse the string A
    for i in range(n1):

        # If current character is 1
        if (A[i] == '1'):

            # Increment 1s count
            count1A += 1;

        # Otherwise, update odd1A or
        # even1A depending whether
        # count1A is odd or even
        else:
            if ((count1A & 1) == 1):
                odd1A += 1;
            else:
                even1A += 1;

    # Traverse the string B
    for i in range(n2):

        # If current character is 1
        if (B[i] == '1'):

            # Increment 1s count
            count1B += 1;

        # Otherwise, update odd1B or
        # even1B depending whether
        # count1B is odd or even
        else:
            if ((count1B & 1) == 1):
                odd1B += 1;
            else:
                even1B += 1;

    # If the condition is satisfied
    if (count1A == count1B and odd1A == odd1B and even1A == even1B):

        # If True, prYes
        print("Yes");

    # Otherwise, prNo
    else:
        print("No");

# Driver Code
if __name__ == '__main__':
    A = "10011";
    B = "11100";

    # Function Call
    canTransformStrings(A, B);

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Function to check if string A can be
    // transformed to string B by reversing
    // substrings of A having even number of 1s
    static void canTransformStrings(string A, string B)
    {

        // Store the size of string A
        int n1 = A.Length;

        // Store the size of string B
        int n2 = B.Length;

        // Store the count of 1s in A and B
        int count1A = 0, count1B = 0;

        // Stores cntA for string A
        // and cntB for string B
        int odd1A = 0, odd1B = 0;
        int even1A = 0, even1B = 0;

        // Traverse the string A
        for(int i = 0; i < n1; i++)
        {

            // If current character is 1
            if (A[i] == '1')

                // Increment 1s count
                count1A++;

            // Otherwise, update odd1A or
            // even1A depending whether
            // count1A is odd or even
            else
            {
                if ((count1A & 1) == 1)
                    odd1A++;
                else
                    even1A++;
            }
        }

        // Traverse the string B
        for(int i = 0; i < n2; i++)
        {

            // If current character is 1
            if (B[i] == '1')

                // Increment 1s count
                count1B++;

            // Otherwise, update odd1B or
            // even1B depending whether
            // count1B is odd or even
            else
            {
                if ((count1B & 1) == 1)
                    odd1B++;
                else
                    even1B++;
            }
        }

        // If the condition is satisfied
        if (count1A == count1B &&
              odd1A == odd1B &&
             even1A == even1B)
        {

            // If true, print Yes
            Console.Write("Yes");
        }

        // Otherwise, print No
        else
            Console.Write("No");
    } 

  static void Main()
  {
    string A = "10011", B = "11100";

    // Function Call
    canTransformStrings(A, B);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program for above approach

    // Function to check if string A can be
    // transformed to string B by reversing
    // substrings of A having even number of 1s
    function canTransformStrings(A, B)
    {

        // Store the size of string A
        let n1 = A.length;

        // Store the size of string B
        let n2 = B.length;

        // Store the count of 1s in A and B
        let count1A = 0, count1B = 0;

        // Stores cntA for string A
        // and cntB for string B
        let odd1A = 0, odd1B = 0;
        let even1A = 0, even1B = 0;

        // Traverse the string A
        for(let i = 0; i < n1; i++)
        {

            // If current character is 1
            if (A[i] == '1')

                // Increment 1s count
                count1A++;

            // Otherwise, update odd1A or
            // even1A depending whether
            // count1A is odd or even
            else
            {
                if ((count1A & 1) == 1)
                    odd1A++;
                else
                    even1A++;
            }
        }

        // Traverse the string B
        for(let i = 0; i < n2; i++)
        {

            // If current character is 1
            if (B[i] == '1')

                // Increment 1s count
                count1B++;

            // Otherwise, update odd1B or
            // even1B depending whether
            // count1B is odd or even
            else
            {
                if ((count1B & 1) == 1)
                    odd1B++;
                else
                    even1B++;
            }
        }

        // If the condition is satisfied
        if (count1A == count1B &&
              odd1A == odd1B &&
             even1A == even1B)
        {

            // If true, print Yes
            document.write("Yes");
        }

        // Otherwise, print No
        else
            document.write("No");
    }

// Driver Code

    let A = "10011", B = "11100";

    // Function Call
    canTransformStrings(A, B);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)