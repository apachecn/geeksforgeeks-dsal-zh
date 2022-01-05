# 加 K 后检查号码是否可以回文

> 原文:[https://www . geesforgeks . org/check-number-can-make-添加-k 后回文/](https://www.geeksforgeeks.org/check-whether-the-number-can-be-made-palindromic-after-adding-k/)

给定两个数字 **N** 和 **K** ，任务是检查给定的数字 **N** 添加 **K** 后是否可以做回文。
**例:**

> **输入:** N = 19，K = 3
> **输出:**是
> **说明:**
> 19 + 3 = 22 和 22 是回文。
> **输入:** N = 15，K = 3
> **输出:**否
> **说明:**
> 15 + 3 = 18 且 18 不是回文。

**方法:**思路是先给定数字加 K，然后[检查得到的数字是否是回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。
以下是上述方法的实施:

## C++

```
// C++ program to check whether the number
// can be made palindrome number after adding K
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a number
// is a palindrome or not
void checkPalindrome(int num)
{

    // Convert num to string
    string str = to_string(num);

    int l = 0, r = str.length() - 1;

    // Comparing kth character from the
    // beginning and N - kth character
    // from the end. If all the characters
    // match, then the number is a palindrome
    while (l < r) {

        if (str[l] != str[r]) {
            cout << "No";
            return;
        }
        l++;
        r--;
    }

    // If all the above conditions satisfy,
    // it means that the number is a palindrome
    cout << "Yes";
    return;
}

// Driver code
int main()
{
    int n = 19, k = 3;

    checkPalindrome(n + k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
class GFG{
// Java program to check whether the number
// can be made palindrome number after adding K

// Function to check whether a number
// is a palindrome or not
static void checkPalindrome(int num)
{

    // Convert num to string
    String str = Integer.toString(num);

    int l = 0, r = str.length() - 1;

    // Comparing kth character from the
    // beginning and N - kth character
    // from the end. If all the characters
    // match, then the number is a palindrome
    while (l < r) {

        if (str.charAt(l) != str.charAt(r)) {
            System.out.print("No");
            return;
        }
        l++;
        r--;
    }

    // If all the above conditions satisfy,
    // it means that the number is a palindrome
    System.out.print("Yes");
    return;
}

// Driver code
public static void main(String args[])
{
    int n = 19, k = 3;

    checkPalindrome(n + k);
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to check whether the number
# can be made palindrome number after adding K

# Function to check whether a number
# is a palindrome or not
def checkPalindrome(num):

    # Convert num to stringing
    string = str(num)

    l = 0
    r = len(string) - 1;

    # Comparing kth character from the
    # beginning and N - kth character
    # from the end. If all the characters
    # match, then the number is a palindrome
    while (l < r):

        if (string[l] != string[r]) :
            print("No")
            return;

        l = l + 1;
        r = r - 1;

    # If all the above conditions satisfy,
    # it means that the number is a palindrome
    print("Yes")
    return;

# Driver code
if __name__=='__main__':

    n = 19
    k = 3

    checkPalindrome(n + k);

# This code is contributed by Princi Singh
```

## C#

```
using System;

class GFG{
// C# program to check whether the number
// can be made palindrome number after adding K

// Function to check whether a number
// is a palindrome or not
static void checkPalindrome(int num)
{

    // Convert num to string
    String str = num.ToString();

    int l = 0, r = str.Length - 1;

    // Comparing kth character from the
    // beginning and N - kth character
    // from the end. If all the characters
    // match, then the number is a palindrome
    while (l < r) {

        if (str[l] != str[r]) {
            Console.Write("No");
            return;
        }
        l++;
        r--;
    }

    // If all the above conditions satisfy,
    // it means that the number is a palindrome
    Console.Write("Yes");
    return;
}

// Driver code
public static void Main(String []args)
{
    int n = 19, k = 3;

    checkPalindrome(n + k);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to check whether the number
// can be made palindrome number after adding K

// Function to check whether a number
// is a palindrome or not
function checkPalindrome(num)
{

    // Convert num to string
    let str = num.toString();

    let l = 0, r = str.length - 1;

    // Comparing kth character from the
    // beginning and N - kth character
    // from the end. If all the characters
    // match, then the number is a palindrome
    while (l < r) {

        if (str[l] != str[r]) {
            document.write("No");
            return;
        }
        l++;
        r--;
    }

    // If all the above conditions satisfy,
    // it means that the number is a palindrome
    document.write("Yes");
    return;
}

// Driver Code

    let n = 19, k = 3;

    checkPalindrome(n + k);

</script>
```

**Output:** 

```
Yes
```

时间复杂度:0(n)

辅助空间:0(1)