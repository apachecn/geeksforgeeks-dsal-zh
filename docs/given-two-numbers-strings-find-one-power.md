# 给定两个数字作为字符串，找出其中一个是否是另一个的幂

> 原文:[https://www . geesforgeks . org/给定-两个数-字符串-查找-一次幂/](https://www.geeksforgeeks.org/given-two-numbers-strings-find-one-power/)

给定两个大数字作为字符串，找出其中一个是否是另一个的幂。例如:

**示例:**

```
Input : a = "374747", b = "52627712618930723"
Output : YES 
Explanation : 374747^3 = 52627712618930723

Input : a = "2", b = "4099"
Output : NO

```

先决条件:[将两个表示为字符串](https://www.geeksforgeeks.org/multiply-large-numbers-represented-as-strings/) 
的大数相乘，方法很简单。首先，找到两个字符串中较小的一个，然后将其与自身相乘，直到它等于或大于较大的字符串。如果它们相等，则返回真，否则返回假。

下面是上述方法的实现

## C++

```
// CPP program to check if one number is
// power of other
#include <bits/stdc++.h>
using namespace std;

bool isGreaterThanEqualTo(string s1, string s2)
{
    if (s1.size() > s2.size())
        return true;

    return (s1 == s2);
}

string multiply(string s1, string s2)
{
    int n = s1.size();
    int m = s2.size();

    vector<int> result(n + m, 0);

    // Multiply the numbers. It multiplies 
    // each digit of second string to each
    // digit of first and stores the result.
    for (int i = n - 1; i >= 0; i--) 
        for (int j = m - 1; j >= 0; j--) 
            result[i + j + 1] += 
               (s1[i] - '0') * (s2[j] - '0');

    // If the digit exceeds 9, add the 
    // cumulative carry to previous digit.
    int size = result.size();
    for (int i = size - 1; i > 0; i--) {
        if (result[i] >= 10) {
            result[i - 1] += result[i] / 10;
            result[i] = result[i] % 10;
        }
    }

    int i = 0;
    while (i < size && result[i] == 0)
        i++;

    // if all zeroes, return "0".
    if (i == size)
        return "0";

    string temp;

    // Remove starting zeroes.
    while (i < size) {
        temp += (result[i] + '0');
        i++;
    }
    return temp;
}

// Removes Extra zeroes from front of a string.
string removeLeadingZeores(string s)
{
    int n = s.size();

    int i = 0;
    while (i < n && s[i] == '0')
        i++;

    if (i == n)
        return "0";

    string temp;
    while (i < n)
        temp += s[i++];

    return temp;
}

bool isPower(string s1, string s2)
{
    // Make sure there are no leading zeroes 
    // in the string.
    s1 = removeLeadingZeores(s1);
    s2 = removeLeadingZeores(s2);

    if (s1 == "0" || s2 == "0")
        return false;

    if (s1 == "1" && s2 == "1")
        return true;

    if (s1 == "1" || s2 == "1")
        return true;

    // Making sure that s1 is smaller.
    // If it is greater, we recur we
    // reversed parameters.
    if (s1.size() > s2.size())
        return isPower(s2, s1);

    string temp = s1;
    while (!isGreaterThanEqualTo(s1, s2))
        s1 = multiply(s1, temp);

    return s1 == s2;
}

int main()
{
    string s1 = "374747", s2 = "52627712618930723";
    cout << (isPower(s1, s2) ? "YES\n" : "NO\n");

    s1 = "4099", s2 = "2";
    cout << (isPower(s1, s2) ? "YES\n" : "NO\n");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if one number is 
// power of other 
import java.util.*;

class new_file
{
    static boolean isGreaterThanEqual(String s1, 
                                      String s2) 
    {
        if (s1.length() > s2.length())
            return true;
        if (s1.compareTo(s2) == 0)
            return true;
        return false;
    }

    static String multiply(String s1, String s2) 
    {
        int n = s1.length();
        int m = s2.length();

        int[] result = new int[n + m];

        // Multiply the numbers. It multiplies
        // each digit of second string to each
        // digit of first and stores the result.
        for (int i = n - 1; i >= 0; i--)
            for (int j = m - 1; j >= 0; j--)
                result[i + j + 1] += (s1.charAt(i) - '0') *
                                     (s2.charAt(j) - '0');

        // If the digit exceeds 9, add the
        // cumulative carry to previous digit.
        int size = result.length;
        for (int i = size - 1; i > 0; i--) 
        {
            if (result[i] >= 10)
            {
                result[i - 1] += result[i] / 10;
                result[i] = result[i] % 10;
            }
        }

        int i = 0;
        while (i < size && result[i] == 0)
            i++;

        // if all zeroes, return "0".
        if (i == size)
            return "0";

        String temp = "";

        // Remove starting zeroes.
        while (i < size)
        {
            temp += Integer.toString(result[i]);
            i++;
        }
        return temp;
    }

    // Removes Extra zeroes from front of a string.
    static String removeLeadingZeores(String s) 
    {
        int n = s.length();
        int i = 0;
        while (i < n && s.charAt(i) == '0')
            i++;
        if (i == n)
            return "0";
        String temp = "";
        while (i < n) 
        {
            temp += s.charAt(i);
            i++;
        }

        return temp;
    }

    static boolean isPower(String s1, String s2) 
    {

        // Make sure there are no leading zeroes
        // in the string.
        s1 = removeLeadingZeores(s1);
        s2 = removeLeadingZeores(s2);
        if (s1 == "0" || s2 == "0")
            return false;
        if (s1 == "1" && s2 == "1")
            return true;
        if (s1 == "1" || s2 == "1")
            return true;

        // Making sure that s1 is smaller.
        // If it is greater, we recur we
        // reversed parameters.
        if (s1.length() > s2.length())
            return isPower(s2, s1);

        String temp = new String(s1);
        while (!isGreaterThanEqual(s1, s2))
            s1 = multiply(s1, temp);

        if (s1.compareTo(s2) == 0)
            return true;
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s1 = "374747", s2 = "52627712618930723";
        if (isPower(s1, s2))
            System.out.println("Yes");
        else
            System.out.println("No");

        s1 = "4099";
        s2 = "2";

        if (isPower(s1, s2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if one 
# number is a power of other 
def isGreaterThanEqualTo(s1, s2): 

    if len(s1) > len(s2): 
        return True

    return s1 == s2 

def multiply(s1, s2): 

    n, m = len(s1), len(s2)
    result = [0] * (n + m) 

    # Multiply the numbers. It multiplies 
    # each digit of second string to each 
    # digit of first and stores the result. 
    for i in range(n - 1, -1, -1): 
        for j in range(m - 1, -1, -1): 
            result[i + j + 1] += (int(s1[i]) * 
                                  int(s2[j]))

    # If the digit exceeds 9, add the 
    # cumulative carry to previous digit. 
    size = len(result) 
    for i in range(size - 1, 0, -1): 
        if result[i] >= 10: 
            result[i - 1] += result[i] // 10
            result[i] = result[i] % 10

    i = 0
    while i < size and result[i] == 0: 
        i += 1

    # If all zeroes, return "0". 
    if i == size: 
        return "0"

    temp = "" 

    # Remove starting zeroes. 
    while i < size: 
        temp += str(result[i]) 
        i += 1

    return temp 

# Removes Extra zeroes from front of a string. 
def removeLeadingZeores(s): 

    n, i = len(s), 0

    while i < n and s[i] == '0': 
        i += 1

    if i == n: 
        return "0"

    temp = "" 
    while i < n: 
        temp += s[i]
        i += 1

    return temp 

def isPower(s1, s2): 

    # Make sure there are no leading 
    # zeroes in the string. 
    s1 = removeLeadingZeores(s1) 
    s2 = removeLeadingZeores(s2) 

    if s1 == "0" or s2 == "0": 
        return False

    if s1 == "1" and s2 == "1": 
        return True

    if s1 == "1" and s2 == "1": 
        return True

    # Making sure that s1 is smaller. 
    # If it is greater, we recur we 
    # reversed parameters. 
    if len(s1) > len(s2): 
        return isPower(s2, s1) 

    temp = s1 
    while not isGreaterThanEqualTo(s1, s2): 
        s1 = multiply(s1, temp) 

    return s1 == s2 

# Driver Code
if __name__ == "__main__":

    s1, s2 = "374747", "52627712618930723"
    if isPower(s1, s2):
        print("YES")
    else:
        print("NO")

    s1, s2 = "4099", "2"
    if isPower(s1, s2):
        print("YES")
    else:
        print("NO")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to check if one number is 
// power of other 
using System;

public class new_file
{
    static bool isGreaterThanEqual(String s1, 
                                    String s2) 
    {
        if (s1.Length > s2.Length)
            return true;
        if (s1.CompareTo(s2) == 0)
            return true;
        return false;
    }

    static String multiply(String s1, String s2) 
    {
        int n = s1.Length;
        int m = s2.Length;
        int i = 0;
        int[] result = new int[n + m];

        // Multiply the numbers. It multiplies
        // each digit of second string to each
        // digit of first and stores the result.
        for (i = n - 1; i >= 0; i--)
            for (int j = m - 1; j >= 0; j--)
                result[i + j + 1] += (s1[i] - '0') *
                                    (s2[j] - '0');

        // If the digit exceeds 9, add the
        // cumulative carry to previous digit.
        int size = result.Length;
        for (i = size - 1; i > 0; i--) 
        {
            if (result[i] >= 10)
            {
                result[i - 1] += result[i] / 10;
                result[i] = result[i] % 10;
            }
        }

        i = 0;
        while (i < size && result[i] == 0)
            i++;

        // if all zeroes, return "0".
        if (i == size)
            return "0";

        String temp = "";

        // Remove starting zeroes.
        while (i < size)
        {
            temp += (result[i]).ToString();
            i++;
        }
        return temp;
    }

    // Removes Extra zeroes from front of a string.
    static String removeLeadingZeores(String s) 
    {
        int n = s.Length;
        int i = 0;
        while (i < n && s[i] == '0')
            i++;
        if (i == n)
            return "0";
        String temp = "";
        while (i < n) 
        {
            temp += s[i];
            i++;
        }

        return temp;
    }

    static bool isPower(String s1, String s2) 
    {

        // Make sure there are no leading zeroes
        // in the string.
        s1 = removeLeadingZeores(s1);
        s2 = removeLeadingZeores(s2);
        if (s1 == "0" || s2 == "0")
            return false;
        if (s1 == "1" && s2 == "1")
            return true;
        if (s1 == "1" || s2 == "1")
            return true;

        // Making sure that s1 is smaller.
        // If it is greater, we recur we
        // reversed parameters.
        if (s1.Length > s2.Length)
            return isPower(s2, s1);

        String temp = s1;
        while (!isGreaterThanEqual(s1, s2))
            s1 = multiply(s1, temp);

        if (s1.CompareTo(s2) == 0)
            return true;
        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s1 = "374747", s2 = "52627712618930723";
        if (isPower(s1, s2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        s1 = "4099";
        s2 = "2";

        if (isPower(s1, s2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Rajput-Ji
```

**输出**

```
YES
NO

```