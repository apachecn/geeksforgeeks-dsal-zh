# 用 Y 替换 X，去掉 Z 后找到结果字符串

> 原文:[https://www . geesforgeks . org/find-the-result-string-after-replace-x-with-y-remove-z/](https://www.geeksforgeeks.org/find-the-resultant-string-after-replacing-x-with-y-and-removing-z/)

给定一个字符串 **str** ，任务是用给定的 **Y** 替换给定的 **X** 的所有出现，并移除给定的 **Z** 的任何出现，如果给定的**中没有多余的空间**
**示例:**

> **输入:**【str = " Batman】，x =‘a’，y =‘d’，z =【b】
> **输出:**
> **输入:**【str = " ABBA】，x =‘a’，y =‘d’，z =【b】

**[推荐:请先在{IDE}上尝试您的方法，然后再继续解决方案。](https://ide.geeksforgeeks.org/index.php)
**进场:**** 

*   **这个想法基于 **2 个指针**。**
*   **让双变量**开始**和**结束**指向字符串的开始和结束。**
*   **现在，如果开始的字符是 Z，用另一个指针指向一个位置时没有 Y 的字符替换它>开始记住，如果找到，用 Y 替换字符 X。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program to find the resultant String
// after replacing X with Y and removing Z

#include <bits/stdc++.h>
using namespace std;

// Function to replace and remove
void replaceRemove(string& s, char X, char Y, char Z)
{

    // Two pointer start and end points
    // to beginning and end position in the string
    int start = 0, end = s.size() - 1;

    while (start <= end) {

        // If start is having Z
        // find X pos in end and
        // replace Z with another character
        if (s[start] == Z) {

            // Find location for having
            // different character
            // instead of Z
            while (end >= 0 && s[end] == Z) {
                end--;
            }

            // If found swap character
            // at start and end
            if (end > start) {
                swap(s[start], s[end]);
                if (s[start] == X)
                    s[start] = Y;
                start++;
            }
        }
        // Else increment start
        // Also checkin for X
        // at start position
        else {
            if (s[start] == X)
                s[start] = Y;
            start++;
        }
    }
    while (s.size() > 0 && s[s.size() - 1] == Z) {
        s.pop_back();
    }
}

// Driver code
int main()
{

    string str = "batman";
    char X = 'a', Y = 'd', Z = 'b';

    replaceRemove(str, X, Y, Z);

    if (str.size() == 0) {
        cout << -1;
    }
    else {
        cout << str;
    }

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the resultant String
// after replacing X with Y and removing Z
class GFG
{

    // Function to replace and remove
    static String replaceRemove(char []s, char X,
                                   char Y, char Z)
    {

        // Two pointer start and end points
        // to beginning and end position in the string
        int start = 0, end = s.length - 1;

        while (start <= end)
        {

            // If start is having Z
            // find X pos in end and
            // replace Z with another character
            if (s[start] == Z)
            {

                // Find location for having
                // different character
                // instead of Z
                while (end >= 0 && s[end] == Z)
                {
                    end--;
                }

                char temp ;

                // If found swap character
                // at start and end
                if (end > start)
                {
                    temp = s[start];
                    s[start] = s[end];
                    s[end] = temp;

                    if (s[start] == X)
                        s[start] = Y;
                    start++;
                }
            }

            // Else increment start
            // Also checkin for X
            // at start position
            else
            {
                if (s[start] == X)
                    s[start] = Y;
                start++;
            }
        }

        String new_s = new String(s);
        while (new_s.length() > 0 &&
            new_s.charAt(new_s.length() - 1) == Z)
        {
            new_s = new_s.substring(0,new_s.length() - 1);
        }
        return new_s;
    }

    // Driver code
    public static void main (String[] args)
    {

        String str = "batman";
        char X = 'a', Y = 'd', Z = 'b';

        str = replaceRemove(str.toCharArray() , X, Y, Z);

        if (str.length() == 0)
        {
            System.out.println(-1);
        }
        else
        {
            System.out.println(str);
        }
    }
}

// This code is contributed by AnkitRai01
```

## **蟒蛇 3**

```
# Python3 program to find the resultant String
# after replacing X with Y and removing Z

# Function to replace and remove
def replaceRemove(s, X, Y, Z) :

    s = list(s);

    # Two pointer start and end points
    # to beginning and end position in the string
    start = 0;
    end = len(s) - 1;

    while (start <= end) :

        # If start is having Z
        # find X pos in end and
        # replace Z with another character
        if (s[start] == Z) :

            # Find location for having
            # different character
            # instead of Z
            while (end >= 0 and s[end] == Z) :
                end -= 1;

            # If found swap character
            # at start and end
            if (end > start) :
                s[start], s[end] = s[end], s[start]
                if (s[start] == X):
                    s[start] = Y;

                start += 1

        # Else increment start
        # Also checkin for X
        # at start position
        else :
            if (s[start] == X) :
                s[start] = Y;

            start += 1;

    while (len(s) > 0 and s[len(s) - 1] == Z):
        s.pop();

    return "".join(s)

# Driver code
if __name__ == "__main__" :

    string = "batman";
    X = 'a'; Y = 'd'; Z = 'b';

    string = replaceRemove(string, X, Y, Z);

    if (len(string) == 0) :
        print(-1);

    else :
        print(string);

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# program to find the resultant String
// after replacing X with Y and removing Z
using System;

class GFG
{

    // Function to replace and remove
    static String replaceRemove(char []s, char X,
                                char Y, char Z)
    {

        // Two pointer start and end points
        // to beginning and end position in the string
        int start = 0, end = s.Length - 1;

        while (start <= end)
        {

            // If start is having Z
            // find X pos in end and
            // replace Z with another character
            if (s[start] == Z)
            {

                // Find location for having
                // different character
                // instead of Z
                while (end >= 0 && s[end] == Z)
                {
                    end--;
                }

                char temp ;

                // If found swap character
                // at start and end
                if (end > start)
                {
                    temp = s[start];
                    s[start] = s[end];
                    s[end] = temp;

                    if (s[start] == X)
                        s[start] = Y;
                    start++;
                }
            }

            // Else increment start
            // Also checkin for X
            // at start position
            else
            {
                if (s[start] == X)
                    s[start] = Y;
                start++;
            }
        }

        String new_s = new String(s);
        while (new_s.Length > 0 &&
               new_s[new_s.Length - 1] == Z)
        {
            new_s = new_s.Substring(0,new_s.Length - 1);
        }
        return new_s;
    }

    // Driver code
    public static void Main(String[] args)
    {

        String str = "batman";
        char X = 'a', Y = 'd', Z = 'b';

        str = replaceRemove(str.ToCharArray() , X, Y, Z);

        if (str.Length == 0)
        {
            Console.WriteLine(-1);
        }
        else
        {
            Console.WriteLine(str);
        }
    }
}

// This code is contributed by PrinciRaj1992
```

****输出:**** 

```
ndtmd
```