# 进行字符串回文的逆时针移位数

给定一串小写英语字母，找到使该字符串回文所需的字符的逆时针移位数。 据认为，移弦总是会导致回文。
**范例：**

> **输入：** str =“ baabbccb”
> **输出：** 2
> 逆时针移动字符串 2 次，
> 将使字符串回文。
> 第一班：aabbccbb
> 第二班：abbccbba
> 
> **输入：** bbaabbcc
> **输出**：3
> 逆时针移动字符串
> 3 次将使字符串回文。
> 第一班：baabbccb
> 第二班：aabbccbb
> 第三班：abbccbba

**天真的方法**：天真的方法是逆时针周期性地对给定的字符串逐个移位字符，并检查字符串是否是回文。

**更好的方法**：更好的方法是将字符串与字符串一起附加，并从给定字符串的第一个字符到最后一个字符进行迭代。 附加字符串中从 i 到 i + n（其中 i 在[0，n-1]范围内）的子字符串将是每次逆时针移动后获得的字符串。 检查子字符串是否为回文。 移位操作的数量为 i。

下面是上述方法的实现：

## C ++

```

// C++ program to find counter clockwise
// shifts to make string palindrome.
#include <bits/stdc++.h>
using namespace std;

// Function to check if given string is
// palindrome or not.
bool isPalindrome(string str, int l, int r)
{
    while (l < r) {
        if (str[l] != str[r])
            return false;

        l++;
        r--;
    }

    return true;
}

// Function to find counter clockwise shifts
// to make string palindrome.
int CyclicShifts(string str)
{

    int n = str.length();

    // Pointer to starting of current
    // shifted string.
    int left = 0;

    // Pointer to ending of current
    // shifted string.
    int right = n - 1;

    // Concatenate string with itself
    str = str + str;

    // To store counterclockwise shifts
    int cnt = 0;

    // Move left and right pointers one
    // step at a time.
    while (right < 2 * n - 1) {

        // Check if current shifted string
        // is palindrome or not
        if (isPalindrome(str, left, right))
            break;

        // If string is not palindrome
        // then increase count of number
        // of shifts by 1.
        cnt++;

        left++;
        right++;
    }

    return cnt;
}

// Driver code.
int main()
{
    string str = "bccbbaab";

    cout << CyclicShifts(str);
    return 0;
}

```

## 爪哇

```

// Java program to find counter clockwise
// shifts to make string palindrome.
class GFG {

    // Function to check if given string is
    // palindrome or not.
    static boolean isPalindrome(String str, int l, int r)
    {
        while (l < r) {
            if (str.charAt(l) != str.charAt(r))
                return false;

            l++;
            r--;
        }
        return true;
    }

    // Function to find counter clockwise shifts
    // to make string palindrome.
    static int CyclicShifts(String str)
    {

        int n = str.length();

        // Pointer to starting of current
        // shifted string.
        int left = 0;

        // Pointer to ending of current
        // shifted string.
        int right = n - 1;

        // Concatenate string with itself
        str = str + str;

        // To store counterclockwise shifts
        int cnt = 0;

        // Move left and right pointers one
        // step at a time.
        while (right < 2 * n - 1) {

            // Check if current shifted string
            // is palindrome or not
            if (isPalindrome(str, left, right))
                break;

            // If string is not palindrome
            // then increase count of number
            // of shifts by 1.
            cnt++;

            left++;
            right++;
        }
        return cnt;
    }

    // Driver code.
    public static void main(String[] args)
    {
        String str = "bccbbaab";

        System.out.println(CyclicShifts(str));
    }
}

// This code is contributed by Rajput-Ji

```

## Python3

```

# Python3 program to find counter clockwise
# shifts to make string palindrome.

# Function to check if given string 
# is palindrome or not.
def isPalindrome(str, l, r):

    while (l < r) :
        if (str[l] != str[r]):
            return False

        l += 1
        r -= 1

    return True

# Function to find counter clockwise 
# shifts to make string palindrome.
def CyclicShifts(str):

    n = len(str)

    # Pointer to starting of current
    # shifted string.
    left = 0

    # Pointer to ending of current
    # shifted string.
    right = n - 1

    # Concatenate string with itself
    str = str + str

    # To store counterclockwise shifts
    cnt = 0

    # Move left and right pointers 
    # one step at a time.
    while (right < 2 * n - 1) :

        # Check if current shifted string
        # is palindrome or not
        if (isPalindrome(str, left, right)):
            break

        # If string is not palindrome
        # then increase count of number
        # of shifts by 1.
        cnt += 1

        left += 1
        right += 1

    return cnt

# Driver code.
if __name__ == "__main__":

    str = "bccbbaab";

    print(CyclicShifts(str))

# This code is contributed by ita_c

```

## C＃

```

// C# program to find counter clockwise
// shifts to make string palindrome.
using System;

class GFG
{

    // Function to check if given string is
    // palindrome or not.
    static bool isPalindrome(String str, int l, int r)
    {
        while (l < r)
        {
            if (str[l] != str[r])
                return false;

            l++;
            r--;
        }
        return true;
    }

    // Function to find counter clockwise shifts
    // to make string palindrome.
    static int CyclicShifts(String str)
    {

        int n = str.Length;

        // Pointer to starting of current
        // shifted string.
        int left = 0;

        // Pointer to ending of current
        // shifted string.
        int right = n - 1;

        // Concatenate string with itself
        str = str + str;

        // To store counterclockwise shifts
        int cnt = 0;

        // Move left and right pointers one
        // step at a time.
        while (right < 2 * n - 1) 
        {

            // Check if current shifted string
            // is palindrome or not
            if (isPalindrome(str, left, right))
                break;

            // If string is not palindrome
            // then increase count of number
            // of shifts by 1.
            cnt++;

            left++;
            right++;
        }
        return cnt;
    }

    // Driver code.
    public static void Main(String[] args)
    {
        String str = "bccbbaab";

        Console.WriteLine(CyclicShifts(str));
    }
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
2

```

**时间复杂度：** O（N <sup>2</sup> ）
**辅助空间：** O（N）

**有效方法**：一种有效方法是使用[累积哈希](https://www.geeksforgeeks.org/palindrome-substring-queries/)。 根据上述方法对字符串进行循环移位，并将该字符串的哈希值与反向字符串的哈希值进行比较。 如果两个值相同，则当前移位的字符串是回文，否则字符串再次移位。 班次的计数在任何一步都是 i。 要使用哈希函数计算两个字符串的值：

> H（s）= ∑（31 <sup>i</sup> *（S <sub>i</sub> –'a'））％mod，0≤i≤（字符串的长度– 1）。
> 其中， H（x）=哈希函数
> s =给定字符串
> mod = 10 <sup>9</sup> + 7

使用上述哈希函数和[累积哈希技术，对所有子字符串进行迭代，并检查它是否是回文。](https://www.geeksforgeeks.org/palindrome-substring-queries/)

下面是上述方法的实现：

## C ++

```

// CPP program to find counter clockwise
// shifts to make string palindrome.
#include <bits/stdc++.h>

#define mod 1000000007
using namespace std;

// Function that returns true
// if str is palindrome
bool isPalindrome(string str, int n)
{
    int i = 0, j = n - 1;
    while (i < j) {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
    }
    return true;
}

// Function to find counter clockwise shifts
// to make string palindrome.
int CyclicShifts(string str)
{

    int n = str.length(), i;

    // If the string is already a palindrome
    if (isPalindrome(str, n))
        return 0;

    // To store power of 31.
    // po[i] = 31^i;
    long long int po[2 * n + 2];

    // To store hash value of string.
    long long int preval[2 * n + 2];

    // To store hash value of reversed
    // string.
    long long int suffval[2 * n + 2];

    // To find hash value of string str[i..j]
    long long int val1;

    // To store hash value of reversed string
    // str[j..i]
    long long int val2;

    // To store number of counter clockwise
    // shifts.
    int cnt = 0;

    // Concatenate string with itself to shift
    // it cyclically.
    str = str + str;

    // Calculate powers of 31 upto 2*n which
    // will be used in hash function.
    po[0] = 1;
    for (i = 1; i <= 2 * n; i++) {
        po[i] = (po[i - 1] * 31) % mod;
    }

    // Hash value of string str[0..i] is stored in
    // preval[i].
    for (i = 1; i <= 2 * n; i++) {
        preval[i] = ((preval[i - 1] * 31) % mod + (str[i - 1] - 'a')) % mod;
    }

    // Hash value of string str[i..n-1] is stored
    // in suffval[i].
    for (i = 2 * n; i > 0; i--) {
        suffval[i] = ((suffval[i + 1] * 31) % mod + (str[i - 1] - 'a')) % mod;
    }

    // Characters in string str[0..i] is present
    // at position [(n-1-i)..(n-1)] in reversed
    // string. If hash value of both are same
    // then string is palindrome else not.
    for (i = 1; i <= n; i++) {

        // Hash value of shifted string starting at
        // index i and ending at index i+n-1.
        val1 = (preval[i + n - 1] - ((po[n] * preval[i - 1]) % mod)) % mod;
        if (val1 < 0)
            val1 += mod;

        // Hash value of corresponding string when
        // reversed starting at index i+n-1 and
        // ending at index i.
        val2 = (suffval[i] - ((po[n] * suffval[i + n])
                              % mod))
               % mod;
        if (val2 < 0)
            val2 += mod;

        // If both hash value are same then current
        // string str[i..(i+n-1)] is palindrome.
        // Else increase the shift count.
        if (val1 != val2)
            cnt++;
        else
            break;
    }

    return cnt;
}

// Driver code.
int main()
{
    string str = "bccbbaab";

    cout << CyclicShifts(str);
    return 0;
}

```

## 爪哇

```

// Java program to find counter clockwise 
// shifts to make string palindrome. 
class GFG{

static int mod = 1000000007; 

// Function that returns true 
// if str is palindrome 
public static boolean isPalindrome(String str, int n) 
{ 
    int i = 0, j = n - 1; 

    while (i < j) 
    { 
        if (str.charAt(i) != str.charAt(j)) 
            return false; 

        i++; 
        j--; 
    } 
    return true; 
} 

// Function to find counter clockwise shifts 
// to make string palindrome. 
public static int CyclicShifts(String str) 
{ 
    int n = str.length(), i; 

    // If the string is already a palindrome 
    if (isPalindrome(str, n)) 
        return 0; 

    // To store power of 31\. 
    // po[i] = 31^i; 
    long[] po = new long[2 * n + 2]; 

    // To store hash value of string. 
    long[] preval = new long[2 * n + 2]; 

    // To store hash value of reversed 
    // string. 
    long[] suffval = new long[2 * n + 2]; 

    // To find hash value of string str[i..j] 
    long val1; 

    // To store hash value of reversed string 
    // str[j..i] 
    long val2; 

    // To store number of counter clockwise 
    // shifts. 
    int cnt = 0; 

    // Concatenate string with itself to shift 
    // it cyclically. 
    str = str + str; 

    // Calculate powers of 31 upto 2*n which 
    // will be used in hash function. 
    po[0] = 1;

    for(i = 1; i <= 2 * n; i++)
    { 
        po[i] = (po[i - 1] * 31) % mod; 
    } 

    // Hash value of string str[0..i] is stored in 
    // preval[i]. 
    for(i = 1; i <= 2 * n; i++) 
    { 
        preval[i] = ((preval[i - 1] * 31) % mod +
                 (str.charAt(i - 1) - 'a')) % mod; 
    } 

    // Hash value of string str[i..n-1] is stored 
    // in suffval[i]. 
    for(i = 2 * n; i > 0; i--) 
    { 
        suffval[i] = ((suffval[i + 1] * 31) % mod + 
                   (str.charAt(i - 1) - 'a')) % mod; 
    } 

    // Characters in string str[0..i] is present 
    // at position [(n-1-i)..(n-1)] in reversed 
    // string. If hash value of both are same 
    // then string is palindrome else not. 
    for(i = 1; i <= n; i++)
    { 

        // Hash value of shifted string starting at 
        // index i and ending at index i+n-1\. 
        val1 = (preval[i + n - 1] - 
                  ((po[n] * 
                preval[i - 1]) % mod)) % mod; 

        if (val1 < 0) 
            val1 += mod; 

        // Hash value of corresponding string when 
        // reversed starting at index i+n-1 and 
        // ending at index i. 
        val2 = (suffval[i] - 
                   ((po[n] * 
                suffval[i + n]) % mod)) % mod;

        if (val2 < 0) 
            val2 += mod; 

        // If both hash value are same then current 
        // string str[i..(i+n-1)] is palindrome. 
        // Else increase the shift count. 
        if (val1 != val2) 
            cnt++; 
        else
            break; 
    } 
    return cnt; 
} 

// Driver code
public static void main(String[] args)
{
    String str = "bccbbaab"; 

    System.out.println(CyclicShifts(str));
}
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```

# Python3 program to find counter clockwise
# shifts to make string palindrome.
mod = 1000000007

# Function to find counter clockwise shifts
# to make string palindrome.
def CyclicShifts(str1):

    n = len(str1)
    i = 0

    # To store power of 31.
    # po[i] = 31 ^ i;
    po = [0 for i in range(2 * n + 2)]

    # To store hash value of string.
    preval = [0 for i in range(2 * n + 2)]

    # To store hash value of reversed
    # string.
    suffval = [0 for i in range(2 * n + 2)]

    # To find hash value of string str[i..j]
    val1 = 0

    # To store hash value of reversed string
    # str[j..i]
    val2 = 0

    # To store number of counter clockwise
    # shifts.
    cnt = 0

    # Concatenate string with itself to shift
    # it cyclically.
    str1 = str1 + str1

    # Calculate powers of 31 upto 2 * n which
    # will be used in hash function.
    po[0] = 1
    for i in range(1, 2 * n + 1):
        po[i] = (po[i - 1] * 31) % mod

    # Hash value of string str[0..i] 
    # is stored in preval[i].
    for i in range(1, 2 * n + 1):
        preval[i] = ((preval[i - 1] * 31) % mod +
                        (ord(str1[i - 1]) -
                         ord('a'))) % mod

    # Hash value of string str[i..n-1] is stored
    # in suffval[i].
    for i in range(2 * n, -1, -1):
        suffval[i] = ((suffval[i + 1] * 31) % mod +
                      (ord(str1[i - 1]) -
                       ord('a'))) % mod

    # Characters in string str[0..i] is present
    # at position [(n-1-i)..(n-1)] in reversed
    # string. If hash value of both are same
    # then string is palindrome else not.
    for i in range(1, n + 1):

        # Hash value of shifted string starting at
        # index i and ending at index i + n-1.
        val1 = (preval[i + n - 1] - ((po[n] *
                preval[i - 1]) % mod)) % mod
        if (val1 < 0):
            val1 += mod

        # Hash value of corresponding string when
        # reversed starting at index i + n-1 and
        # ending at index i.
        val2 = (suffval[i] - ((po[n] *
                suffval[i + n])% mod)) % mod;
        if (val2 < 0):
            val2 += mod

        # If both hash value are same then current
        # string str[i..(i + n-1)] is palindrome.
        # Else increase the shift count.
        if (val1 != val2):
            cnt += 1
        else:
            break

    return cnt

# Driver code
str1 = "bccbbaab"

print(CyclicShifts(str1))

# This code is contributed by mohit kumar

```

## C＃

```

// C# program to find counter clockwise
// shifts to make string palindrome.
using System;
using System.Collections.Generic;

class GFG 
{

static int mod= 1000000007;

// Function that returns true
// if str is palindrome
static bool isPalindrome(string str, int n)
{
    int i = 0, j = n - 1;
    while (i < j) {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
    }
    return true;
}

// Function to find counter clockwise shifts
// to make string palindrome.
static int CyclicShifts(string str)
{

    int n = str.Length, i;

    // If the string is already a palindrome
    if (isPalindrome(str, n))
        return 0;

    // To store power of 31.
    // po[i] = 31^i;
    long []po=new long[2 * n + 2];

    // To store hash value of string.
    long []preval=new long[2 * n + 2];

    // To store hash value of reversed
    // string.
    long []suffval=new long[2 * n + 2];

    // To find hash value of string str[i..j]
    long val1;

    // To store hash value of reversed string
    // str[j..i]
    long val2;

    // To store number of counter clockwise
    // shifts.
    int cnt = 0;

    // Concatenate string with itself to shift
    // it cyclically.
    str = str + str;

    // Calculate powers of 31 upto 2*n which
    // will be used in hash function.
    po[0] = 1;
    for (i = 1; i <= 2 * n; i++) {
        po[i] = (po[i - 1] * 31) % mod;
    }

    // Hash value of string str[0..i] is stored in
    // preval[i].
    for (i = 1; i <= 2 * n; i++) {
        preval[i] = ((preval[i - 1] * 31) % mod + (str[i - 1] - 'a')) % mod;
    }

    // Hash value of string str[i..n-1] is stored
    // in suffval[i].
    for (i = 2 * n; i > 0; i--) {
        suffval[i] = ((suffval[i + 1] * 31) % mod + (str[i - 1] - 'a')) % mod;
    }

    // Characters in string str[0..i] is present
    // at position [(n-1-i)..(n-1)] in reversed
    // string. If hash value of both are same
    // then string is palindrome else not.
    for (i = 1; i <= n; i++) {

        // Hash value of shifted string starting at
        // index i and ending at index i+n-1.
        val1 = (preval[i + n - 1] - ((po[n] * preval[i - 1]) % mod)) % mod;
        if (val1 < 0)
            val1 += mod;

        // Hash value of corresponding string when
        // reversed starting at index i+n-1 and
        // ending at index i.
        val2 = (suffval[i] - ((po[n] * suffval[i + n])
                              % mod))
               % mod;
        if (val2 < 0)
            val2 += mod;

        // If both hash value are same then current
        // string str[i..(i+n-1)] is palindrome.
        // Else increase the shift count.
        if (val1 != val2)
            cnt++;
        else
            break;
    }

    return cnt;
}

    // Driver Code
    public static void Main(string []args)
    {
         string str = "bccbbaab";

        Console.Write(CyclicShifts(str));
    }
}

```

**Output:** 

```
2

```

**时间复杂度：** O（N）
**辅助空间：** O（N）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。