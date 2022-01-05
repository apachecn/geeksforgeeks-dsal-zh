# 通过删除不相邻的字符检查二进制字符串是否可以按降序排序

> 原文:[https://www . geeksforgeeks . org/check-if-a-binary-string-可通过移除非相邻字符按降序排序/](https://www.geeksforgeeks.org/check-if-a-binary-string-can-be-sorted-in-decreasing-order-by-removing-non-adjacent-characters/)

给定大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过移除任意数量的不相邻字符来检查二进制字符串 **S** 是否可以按[降序排序](https://www.geeksforgeeks.org/sort-string-characters/)。如果可以[对字符串](https://www.geeksforgeeks.org/program-sort-string-descending-order/)进行降序排序，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**S**=“10101011011”
> **输出:**是
> **说明:**
> 在去除索引 1、3、5、8 处的不相邻字符后，将字符串修改为“1111111”，按降序排序。因此，打印“是”。**
> 
> ****输入:**S = " 0011 "
> T3】输出:否**

****方法:**给定的问题可以基于这样的观察来解决:如果存在两个具有 **1s** 的相邻字符，然后存在具有 **0s** 的相邻字符，则不可能通过[移除非相邻字符](https://www.geeksforgeeks.org/rearrange-characters-string-no-two-adjacent/)来对字符串进行排序。按照以下步骤解决问题:**

*   **初始化一个布尔变量，说**标志**为**真**，存储给定字符串是否可以排序的状态。**
*   **[从末尾遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果存在任何具有值 **1s** 的相邻字符对，则将第二个索引 **1** 存储在变量中，比如 **idx** 和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。**
*   **[再次从后面遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 越过范围**【idx，0】**，如果存在任何具有值 **0s** 的相邻字符对，则将**标志**的值更新为**假**和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。**
*   **完成上述步骤后，如果**标志**的值为**真**，则打印**“是”**。否则，打印**“否”**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the given string in
// decreasing order by removing the non
// adjacent characters
string canSortString(string S, int N)
{
    // Keeps the track whether the
    // string can be sorted or not
    int flag = 1;

    int i, j;

    // Traverse the given string S
    for (i = N - 2; i >= 0; i--) {

        // Check if S[i] and
        // S[i + 1] are both '1'
        if (S[i] == '1'
            && S[i + 1] == '1') {
            break;
        }
    }

    // Traverse the string S from
    // the indices i to 0
    for (int j = i; j >= 0; j--) {

        // If S[j] and S[j + 1] is
        // equal to 0
        if (S[j] == '0'
            && S[j + 1] == '0') {

            // Mark flag false
            flag = 0;
            break;
        }
    }

    // If flag is 0, then it is not
    // possible to sort the string
    if (flag == 0) {
        return "No";
    }

    // Otherwise
    else {
        return "Yes";
    }
}

// Driver Code
int main()
{
    string S = "10101011011";
    int N = S.length();
    cout << canSortString(S, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to sort the given string in
// decreasing order by removing the non
// adjacent characters
static String canSortString(String S, int N)
{

    // Keeps the track whether the
    // string can be sorted or not
    int flag = 1;

    int i, j;

    // Traverse the given string S
    for (i = N - 2; i >= 0; i--) {

        // Check if S[i] and
        // S[i + 1] are both '1'
        if (S.charAt(i) == '1'
            && S.charAt(i + 1) == '1') {
            break;
        }
    }

    // Traverse the string S from
    // the indices i to 0
    for ( j = i; j >= 0; j--) {

        // If S[j] and S[j + 1] is
        // equal to 0
        if (S.charAt(j) == '0'
            && S.charAt(j + 1) == '0') {

            // Mark flag false
            flag = 0;
            break;
        }
    }

    // If flag is 0, then it is not
    // possible to sort the string
    if (flag == 0) {
        return "No";
    }

    // Otherwise
    else {
        return "Yes";
    }
}

    public static void main (String[] args) {
      String S = "10101011011";
    int N = S.length();
    System.out.println(canSortString(S, N));

    }
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to sort the given string in
# decreasing order by removing the non
# adjacent characters
def canSortString(S, N):

    # Keeps the track whether the
    # string can be sorted or not
    flag = 1

    # Traverse the given string S
    i = N - 2

    while(i >= 0):

        # Check if S[i] and
        # S[i + 1] are both '1'
        if (S[i] == '1' and S[i + 1] == '1'):
            break

        i -= 1

    # Traverse the string S from
    # the indices i to 0
    j = i

    while(j >= 0):

        # If S[j] and S[j + 1] is
        # equal to 0
        if (S[j] == '0' and S[j + 1] == '0'):

            # Mark flag false
            flag = 0
            break

        j -= 1

    # If flag is 0, then it is not
    # possible to sort the string
    if (flag == 0):
        return "No"

    # Otherwise
    else:
        return "Yes"

# Driver Code
if __name__ == '__main__':

    S = "10101011011"
    N = len(S)

    print(canSortString(S, N))

# This code is contributed by ipg2016107
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to sort the given string in
// decreasing order by removing the non
// adjacent characters
static string canSortString(string S, int N)
{

    // Keeps the track whether the
    // string can be sorted or not
    int flag = 1;

    int i, j;

    // Traverse the given string S
    for(i = N - 2; i >= 0; i--)
    {

        // Check if S[i] and
        // S[i + 1] are both '1'
        if (S[i] == '1' && S[i + 1] == '1')
        {
            break;
        }
    }

    // Traverse the string S from
    // the indices i to 0
    for(j = i; j >= 0; j--)
    {

        // If S[j] and S[j + 1] is
        // equal to 0
        if (S[j] == '0' && S[j + 1] == '0')
        {

            // Mark flag false
            flag = 0;
            break;
        }
    }

    // If flag is 0, then it is not
    // possible to sort the string
    if (flag == 0)
    {
        return "No";
    }

    // Otherwise
    else
    {
        return "Yes";
    }
}

// Driver code
public static void Main(string[] args)
{
    string S = "10101011011";
    int N = S.Length;

    Console.WriteLine(canSortString(S, N));
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to sort the given string in
// decreasing order by removing the non
// adjacent characters
function canSortString(S, N)
{
    // Keeps the track whether the
    // string can be sorted or not
    let flag = 1;

    let i, j;

    // Traverse the given string S
    for (let i = N - 2; i >= 0; i--) {

        // Check if S[i] and
        // S[i + 1] are both '1'
        if (S[i] == '1'
            && S[i + 1] == '1') {
            break;
        }
    }

    // Traverse the string S from
    // the indices i to 0
    for (let j = i; j >= 0; j--) {

        // If S[j] and S[j + 1] is
        // equal to 0
        if (S[j] == '0'
            && S[j + 1] == '0') {

            // Mark flag false
            flag = 0;
            break;
        }
    }

    // If flag is 0, then it is not
    // possible to sort the string
    if (flag == 0) {
        return "No";
    }

    // Otherwise
    else {
        return "Yes";
    }
}

// Driver Code
    let S = "10101011011";
    let N = S.length;
    document.write(canSortString(S, N));

// This code is contributed by gfgking
</script>
```

****Output:** 

```
Yes
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**