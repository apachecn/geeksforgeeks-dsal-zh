# 检查一个字符串是否是另一个

的后缀

> 原文:[https://www . geesforgeks . org/check-if-a-string-is-后缀-of-other/](https://www.geeksforgeeks.org/check-if-a-string-is-suffix-of-another/)

给定两个字符串 s1 和 s2，检查 s1 是否是 s2 的后缀。或者简单的说，我们需要找到字符串 s2 是否以字符串 s1 结尾。

**例:**

```
Input : s1 = "geeks" and s2 = "geeksforgeeks"
Output : Yes

Input : s1 = "world", s2 = "my first code is hello world"
Output : Yes

Input : s1 = "geeks" and s2 = "geeksforGeek"
Output : No
```

**方法 1(编写我们自己的代码)**

## c++

```
// CPP program to find if a string is
// suffix of another
#include <iostream>
#include <string>
using namespace std;

bool isSuffix(string s1, string s2)
{
    int n1 = s1.length(), n2 = s2.length();
    if (n1 > n2)
      return false;
    for (int i=0; i<n1; i++)
       if (s1[n1 - i - 1] != s2[n2 - i - 1])
           return false;
    return true;
}

int main()
{
    string s1 = "geeks", s2 = "geeksforgeeks";

    // Test case-sensitive implementation
    // of endsWith function
    bool result = isSuffix(s1, s2);

    if (result)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java

```
// Java program to find if a string is
// suffix of another

class GFG
{
    static boolean isSuffix(String s1, String s2)
    {
        int n1 = s1.length(), n2 = s2.length();
        if (n1 > n2)
        return false;
        for (int i=0; i<n1; i++)
        if (s1.charAt(n1 - i - 1) != s2.charAt(n2 - i - 1))
            return false;
        return true;
    }

    public static void main(String []args)
    {
        String s1 = "geeks", s2 = "geeksforgeeks";

        // Test case-sensitive implementation
        // of endsWith function
        boolean result = isSuffix(s1, s2);

        if (result)
            System.out.println( "Yes");
        else
            System.out.println("No");

    }

}

// This code is contributed by iAyushRaj
```

## python 3

T2

## c#

T3

## PHP

T4

## Javascript

T31

```
<script>

// Javascript program to find if
// a string is suffix of another
function isSuffix(s1, s2)
{
    let n1 = s1.length, n2 = s2.length;
    if (n1 > n2)
        return false;

    for(let i = 0; i < n1; i++)
        if (s1[n1 - i - 1] != s2[n2 - i - 1])
            return false;

    return true;
}

// Driver code
let s1 = "geeks", s2 = "geeksforgeeks";

// Test case-sensitive implementation
// of endsWith function
let result = isSuffix(s1, s2);

if (result)
    document.write( "Yes");
else
    document.write("No");

// This code is contributed by decode2207

</script>
```

T34

```
Yes
```