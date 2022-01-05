# 检查一个字符串的排列是否会破坏另一个字符串的排列

> 原文:[https://www . geeksforgeeks . org/check-如果一个字符串的排列可以打破另一个字符串的排列/](https://www.geeksforgeeks.org/check-if-permutation-of-one-string-can-break-permutation-of-another/)

给定两个字符串 **str1** 和 **str2** ，任务是检查给定字符串 **str1** 和 **str2** 的任何排列是否可能使得一个字符串的每个索引处的字符大于或等于另一个字符串。

**示例:**

> **输入:**A =“abc”，B =“xya”
> **输出:**是
> **说明:**
> “ayx”是 B =“xya”的一个排列，可以断成串“abc”，串“ABC”是 A =“ABC”的一个排列。
> 
> **输入:** A = "abe "，B = "acd"
> **输出:**【否】

**天真方法:**想法是[生成一个字符串的所有排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)并检查任何排列的每个字符是否大于另一个字符串，然后打印“是”，否则打印“否”。

***时间复杂度:** O(N^2)*
***辅助空间:** O(1)*

**有效方法:**因为我们必须检查一个字符串的置换的每个字符是否大于或等于另一个字符串的置换。这个想法是[按照字母顺序对两个字符串进行排序](https://www.geeksforgeeks.org/sort-string-characters/)。现在，如果字符串 str1 的所有字符串都小于 str2 或者字符串 str2 的所有字符都小于 str1，则在字符串的所有字符上循环，然后打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if permutation of
// one string can break permutation of
// another string or not
bool CanBreak(string A, string B)
{
    // Sort both the strings
    // in alphabetical order
    sort(A.begin(), A.end());
    sort(B.begin(), B.end());

    bool ans1 = true, ans2 = true;

    // Iterate over the strings
    for (int i = 0; i < A.length(); i++) {

        // If any of the string can break
        // other then mark ans as false;
        if (A[i] < B[i])
            ans1 = false;
        if (B[i] < A[i])
            ans2 = false;
    }

    // If any of the string can break
    return ans1 || ans2;
}

// Driver Code
int main()
{
    // Given string A and B
    string A = "abc", B = "xya";

    // Function Call
    if (CanBreak(A, B))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if permutation of
// one String can break permutation of
// another String or not
static boolean CanBreak(String A, String B)
{

    // Sort both the Strings
    // in alphabetical order
    A = sortString(A);
    B = sortString(B);

    boolean ans1 = true, ans2 = true;

    // Iterate over the Strings
    for(int i = 0; i < A.length(); i++)
    {

        // If any of the String can break
        // other then mark ans as false;
        if (A.charAt(i) < B.charAt(i))
            ans1 = false;
        if (B.charAt(i) < A.charAt(i))
            ans2 = false;
    }

    // If any of the String can break
    return ans1 || ans2;
}

static String sortString(String inputString) 
{ 

    // Convert input string to char array 
    char tempArray[] = inputString.toCharArray(); 

    // Sort tempArray 
    Arrays.sort(tempArray); 

    // Return new sorted string 
    return new String(tempArray); 
} 

// Driver Code
public static void main(String[] args)
{

    // Given String A and B
    String A = "abc", B = "xya";

    // Function call
    if (CanBreak(A, B))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for 
# the above approach

# Function to check if 
# permutation of one string 
# can break permutation of
# another string or not
def CanBreak(A, B):

    # Sort both the strings
    # in alphabetical order
    A = "".join(sorted(A))
    B = "".join(sorted(B))
    ans1 = True
    ans2 = True

    # Iterate over the strings
    for i in range(len(A)):

        # If any of the string 
        # can break other then 
        # mark ans as false;
        if(A[i] < B[i]):
            ans1 = False
        if(B[i] < A[i]):
            ans2 = False

    # If any of the string 
    # can break
    return (ans1 or ans2)

# Driver Code

# Given string A and B
A = "abc"
B = "xya"

# Function Call
if(CanBreak(A, B)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if permutation of
// one String can break permutation of
// another String or not
static bool CanBreak(String A, String B)
{

    // Sort both the Strings
    // in alphabetical order
    A = sortString(A);
    B = sortString(B);

    bool ans1 = true, ans2 = true;

    // Iterate over the Strings
    for(int i = 0; i < A.Length; i++)
    {

        // If any of the String can break
        // other then mark ans as false;
        if (A[i] < B[i])
            ans1 = false;
        if (B[i] < A[i])
            ans2 = false;
    }

    // If any of the String can break
    return ans1 || ans2;
}

static String sortString(String inputString) 
{ 

    // Convert input string to char array 
    char []tempArray = inputString.ToCharArray(); 

    // Sort tempArray 
    Array.Sort(tempArray); 

    // Return new sorted string 
    return new String(tempArray); 
} 

// Driver Code
public static void Main(String[] args)
{

    // Given String A and B
    String A = "abc", B = "xya";

    // Function call
    if (CanBreak(A, B))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to check if permutation of
// one String can break permutation of
// another String or not
function CanBreak(A, B)
{

    // Sort both the Strings
    // in alphabetical order
    A = sortString(A);
    B = sortString(B);

    let ans1 = true, ans2 = true;

    // Iterate over the Strings
    for(let i = 0; i < A.length; i++)
    {

        // If any of the String can break
        // other then mark ans as false;
        if (A[i] < B[i])
            ans1 = false;
        if (B[i] < A[i])
            ans2 = false;
    }

    // If any of the String can break
    return ans1 || ans2;
}

function sortString(inputString)
{

    // Convert input string to char array
    let tempArray = inputString.split('');

    // Sort tempArray
    tempArray.sort();

    // Return new sorted string
    return new String(tempArray);
}

// Driver Code    

    // Given String A and B
    let A = "abc", B = "xya";

    // Function call
    if (CanBreak(A, B))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*