# 清空给定字符串所需的不同连续字符子序列的最小删除量

> 原文:[https://www . geeksforgeeks . org/给定字符串需要清空的不同连续字符子序列的最小移除数/](https://www.geeksforgeeks.org/minimum-removal-of-subsequences-of-distinct-consecutive-characters-required-to-empty-a-given-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)、**字符串**，任务是按照单个字符或包含与**字符串**不同的连续字符的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)的最小删除次数清空给定的字符串。

**示例:**

> **输入:** str = "0100100111"
> **输出:** 3
> **解释:**
> 从字符串中删除子序列“010101”将 str 修改为“0011”。
> 从字符串中删除子序列“01”会将字符串修改为“01”。
> 从字符串中删除子序列“01”会将字符串修改为空字符串。
> 因此，要求输出为 3。
> 
> **输入:**str = " 010110 "
> T3】输出: 2

**简单方法:**解决这个问题最简单的方法是[重复遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，从字符串中删除最长的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)，每次删除后增加计数。最后，打印计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效途径:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化两个变量，比如 **cntOne** 和 **cntZero** ，存储 **1** s 和 **0** s 的计数。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，并检查以下条件:
    *   如果 **str[i] == '0'** ，则增加 **cntZero** 的值，并检查 **cntOne** 的值是否大于 **0** 。如果发现为真，则递减 **cntOne** 的值。
    *   如果 **str[i] == '1'** ，则增加 **cntOne** 的值，检查 **cntZero** 的值是否大于 **0** 。如果发现为真，则递减 **cntZero** 的值。
*   最后打印 **(cntZero + cntOne)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

//Function to count minimum operations required
// to make the string an empty string
int findMinOperationsReqEmpStr(string str)
{
    // Stores count of 1s by removing
    // consecutive distinct subsequence
    int cntOne = 0;

    // Stores count of 0s by removing
    // consecutive distinct subsequence
    int cntZero = 0 ;

    // Stores length of str
    int N = str.length();

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // If current character
        // is 0
        if(str[i] == '0'){
            if (cntOne) {

                // Update cntOne
                cntOne--;
            }

            // Update cntZero
            cntZero++;
        }

        // If current character
        // is 1
        else{

            //Update cntZero
            if (cntZero) {
                cntZero--;
            }

            // Update cntOne
            cntOne++;
        }
    }

    return (cntOne + cntZero);
}

// Driver Code
int main()
{
    string str = "0100100111";
    cout<< findMinOperationsReqEmpStr(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG{

//Function to count minimum operations required
// to make the string an empty string
static int findMinOperationsReqEmpStr(String str)
{

    // Stores count of 1s by removing
    // consecutive distinct subsequence
    int cntOne = 0;

    // Stores count of 0s by removing
    // consecutive distinct subsequence
    int cntZero = 0;

    // Stores length of str
    int N = str.length();

    // Traverse the string
    for(int i = 0; i < N; i++)
    {

        // If current character
        // is 0
        if(str.charAt(i) == '0')
        {
            if (cntOne != 0)
            {

                // Update cntOne
                cntOne--;
            }

            // Update cntZero
            cntZero++;
        }

        // If current character
        // is 1
        else
        {

            // Update cntZero
            if (cntZero != 0)
            {
                cntZero--;
            }

            // Update cntOne
            cntOne++;
        }
    }
    return (cntOne + cntZero);
}

// Driver code
public static void main(String[] args)
{
    String str = "0100100111";

    System.out.print(findMinOperationsReqEmpStr(str));
}
}

// This code is contributed by ajaykr00kj
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count minimum operations
# required to make the string an empty
# string
def findMinOperationsReqEmpStr(str):

    # Stores count of 1s by removing
    # consecutive distinct subsequence
    cntOne = 0

    # Stores count of 0s by removing
    # consecutive distinct subsequence
    cntZero = 0

    # Traverse the string
    for element in str:

        # If current character
        # is 0
        if element == '0':
            if cntOne > 0: 

                # Update cntOne
                cntOne = cntOne - 1

            # Update cntZero
            cntZero = cntZero + 1

        # If current character
        # is 1
        else:

            # Update cntZero
            if cntZero > 0:
                cntZero = cntZero - 1

            # Update cntOne
            cntOne = cntOne + 1

    return cntOne + cntZero  

# Driver code
if __name__ == "__main__":

    str = "0100100111"

    print(findMinOperationsReqEmpStr(str))

# This code is contributed by ajaykr00kj
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to count minimum operations required
// to make the string an empty string
static int findMinOperationsReqEmpStr(String str)
{

    // Stores count of 1s by removing
    // consecutive distinct subsequence
    int cntOne = 0;

    // Stores count of 0s by removing
    // consecutive distinct subsequence
    int cntZero = 0;

    // Stores length of str
    int N = str.Length;

    // Traverse the string
    for(int i = 0; i < N; i++)
    {

        // If current character
        // is 0
        if(str[i] == '0')
        {
            if (cntOne != 0)
            {

                // Update cntOne
                cntOne--;
            }

            // Update cntZero
            cntZero++;
        }

        // If current character
        // is 1
        else
        {

            // Update cntZero
            if (cntZero != 0)
            {
                cntZero--;
            }

            // Update cntOne
            cntOne++;
        }
    }
    return (cntOne + cntZero);
}

// Driver code
public static void Main(String[] args)
{
    String str = "0100100111";

    Console.Write(findMinOperationsReqEmpStr(str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count minimum operations required
// to make the string an empty string
function findMinOperationsReqEmpStr(str)
{

    // Stores count of 1s by removing
    // consecutive distinct subsequence
    let cntOne = 0;

    // Stores count of 0s by removing
    // consecutive distinct subsequence
    let cntZero = 0;

    // Stores length of str
    let N = str.length;

    // Traverse the string
    for(let i = 0; i < N; i++)
    {

        // If current character
        // is 0
        if (str[i] == '0')
        {
            if (cntOne != 0)
            {

                // Update cntOne
                cntOne--;
            }

            // Update cntZero
            cntZero++;
        }

        // If current character
        // is 1
        else
        {

            // Update cntZero
            if (cntZero != 0)
            {
                cntZero--;
            }

            // Update cntOne
            cntOne++;
        }
    }
    return (cntOne + cntZero);
}

// Driver code
let str = "0100100111";

document.write(findMinOperationsReqEmpStr(str));

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)