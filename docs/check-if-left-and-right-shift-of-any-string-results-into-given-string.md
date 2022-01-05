# 检查任何字符串的左右移动是否导致给定的字符串

> 原文:[https://www . geesforgeks . org/check-if-左移和右移-将任意字符串结果转换为给定字符串/](https://www.geeksforgeeks.org/check-if-left-and-right-shift-of-any-string-results-into-given-string/)

给定仅由小写英文字母组成的字符串。任务是查找是否存在左移位和右移位都等于字符串 s 的字符串。如果存在任何字符串，则打印“是”，否则打印“否”

**示例:**

> **输入:** S = "abcd"
> **输出:**否
> **说明:**
> 没有左移和右移都等于字符串“abcd”的字符串。
> 
> **输入:**帕帕
> T3】输出:是
> **说明:**
> 字符串“apap”的左移和右移都等于字符串“papa”。

**进场:**

1.  主要目标是检查任意字符串的左移位和右移位是否等于给定字符串。
2.  为此，我们只需**检查给定字符串的每个字符**是否等于其下一个字符(即位于(i) <sup>第</sup>位置的字符必须等于位于(i+2) <sup>第</sup>位置的字符)。
3.  如果给定字符串上的每个位置都是真的，那么我们可以说存在左移和右移等于给定字符串的任何字符串，否则不是。

下面是上述方法的实现:

## C++

```
// C++ program to check if left
// and right shift of any string
// results into the given string

#include <bits/stdc++.h>
using namespace std;

// Function to check string exist
// or not as per above approach
void check_string_exist(string S)
{
    int size = S.length();

    bool check = true;

    for (int i = 0; i < size; i++) {

        // Check if any character
        // at position i and i+2
        // are not equal
        // then string doesnot exist
        if (S[i] != S[(i + 2) % size]) {
            check = false;
            break;
        }
    }

    if (check)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver code
int main()
{
    string S = "papa";

    check_string_exist(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if left
// and right shift of any string
// results into the given string
class GFG{

// Function to check string exist
// or not as per above approach
public static void check_string_exist(String S)
{
    int size = S.length();
    boolean check = true;

    for(int i = 0; i < size; i++)
    {

       // Check if any character
       // at position i and i+2
       // are not equal
       // then string doesnot exist
       if (S.charAt(i) != S.charAt((i + 2) % size))
       {
           check = false;
           break;
       }
    }

    if (check)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String[] args)
{
    String S = "papa";

    check_string_exist(S);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to check if left
# and right shift of any string
# results into the given string

# Function to check string exist
# or not as per above approach
def check_string_exist(S):

    size = len(S)
    check = True

    for i in range(size):

        # Check if any character
        # at position i and i+2
        # are not equal, then 
        # string doesnot exist
        if S[i] != S[(i + 2) % size]:
            check = False
            break

    if check :
        print("Yes")
    else:
        print("No")

# Driver Code
S = "papa"

check_string_exist(S)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to check if left
// and right shift of any string
// results into the given string
using System;

class GFG{

// Function to check string exist
// or not as per above approach
public static void check_string_exist(String S)
{
    int size = S.Length;
    bool check = true;

    for(int i = 0; i < size; i++)
    {

       // Check if any character
       // at position i and i+2
       // are not equal
       // then string doesnot exist
       if (S[i] != S[(i + 2) % size])
       {
           check = false;
           break;
       }
    }
    if (check)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main(String[] args)
{
    String S = "papa";

    check_string_exist(S);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to check if left
// and right shift of any string
// results into the given string

// Function to check string exist
// or not as per above approach
function check_string_exist(S)
{
    var size = S.length;

    var check = true;

    for (var i = 0; i < size; i++) {

        // Check if any character
        // at position i and i+2
        // are not equal
        // then string doesnot exist
        if (S[i] != S[(i + 2) % size]) {
            check = false;
            break;
        }
    }

    if (check)
        document.write( "Yes" );
    else
        document.write( "No" );
}

// Driver code
var S = "papa";
check_string_exist(S);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)* 其中 N 是字符串 s 的大小
***辅助空间复杂度:** O(1)*