# 检查字符串是否包含连续的字母，每个字母恰好出现一次

> 原文:[https://www . geesforgeks . org/check-如果字符串包含连续字母，并且每个字母恰好出现一次/](https://www.geeksforgeeks.org/check-if-the-string-contains-consecutive-letters-and-each-letter-occurs-exactly-once/)

给定弦**弦**。任务是检查字符串是否包含连续的字母，每个字母恰好出现一次。

**示例:**

> **输入:** str = "fced"
> **输出:**是
> 该字符串包含连续的字母‘c’、‘d’、‘e’和‘f’。
> 
> **输入:**str = " XYZ "
> T3】输出:是
> 
> **输入:**str = " Abd "
> T3】输出:否

**方法:**
可以按照以下步骤解决问题:

*   给定字符串按升序排序。
*   检查 ***s[i]-s[i-1]==1*** ，对于从 1 到 n-1 的每个指数 I。
*   如果每个索引的条件都成立，则打印“是”，否则打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// the condition holds
bool check(string s)
{

    // Get the length of the string
    int l = s.length();

    // sort the given string
    sort(s.begin(), s.end());

    // Iterate for every index and
    // check for the condition
    for (int i = 1; i < l; i++) {

        // If are not consecutive
        if (s[i] - s[i - 1] != 1)
            return false;
    }

    return true;
}

// Driver code
int main()
{

    // 1st example
    string str = "dcef";
    if (check(str))
        cout << "Yes\n";
    else
        cout << "No\n";

    // 2nd example
    str = "xyza";

    if (check(str))
        cout << "Yes\n";
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GfG {

    // Function to check if
    // the condition holds
    static boolean check(char s[])
    {

        // Get the length of the string
        int l = s.length;

        // sort the given string
        Arrays.sort(s);

        // Iterate for every index and
        // check for the condition
        for (int i = 1; i < l; i++) {

            // If are not consecutive
            if (s[i] - s[i - 1] != 1)
                return false;
        }

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {

        // 1st example
        String str = "dcef";
        if (check(str.toCharArray()) == true)
            System.out.println("Yes");
        else
            System.out.println("No");

        // 2nd example
        String str1 = "xyza";

        if (check(str1.toCharArray()) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if
# the condition holds
def check(s):

    # Get the length of the string
    l = len(s)

    # sort the given string
    s = ''.join(sorted(s))

    # Iterate for every index and
    # check for the condition
    for i in range(1, l):

        # If are not consecutive
        if ord(s[i]) - ord(s[i - 1]) != 1:
            return False

    return True

# Driver code
if __name__ == "__main__":

    # 1st example
    string = "dcef"

    if check(string):
        print("Yes")
    else:
        print("No")

    # 2nd example
    string = "xyza"

    if check(string):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;

class GfG {

    // Function to check if
    // the condition holds
    static bool check(char[] s)
    {

        // Get the length of the string
        int l = s.Length;

        // sort the given string
        Array.Sort(s);

        // Iterate for every index and
        // check for the condition
        for (int i = 1; i < l; i++) {

            // If are not consecutive
            if (s[i] - s[i - 1] != 1)
                return false;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {

        // 1st example
        string str = "dcef";
        if (check(str.ToCharArray()) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        // 2nd example
        String str1 = "xyza";

        if (check(str1.ToCharArray()) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
    // Javascript program to implement
    // the above approach

    // Function to check if
    // the condition holds
    function check(s)
    {

        // Get the length of the string
        let l = s.length;

        // sort the given string
        s.sort();

        // Iterate for every index and
        // check for the condition
        for (let i = 1; i < l; i++) {

            // If are not consecutive
            if ((s[i].charCodeAt() - s[i - 1].charCodeAt()) != 1)
                return false;
        }

        return true;
    }

    // 1st example
    let str = "dcef";
    if (check(str.split('')) == true)
      document.write("Yes" + "</br>");
    else
      document.write("No" + "</br>");

    // 2nd example
    let str1 = "xyza";

    if (check(str1.split('')) == true)
      document.write("Yes");
    else
      document.write("No");

      // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
Yes
No
```

**时间复杂度:** O(N logN)

**高效方法:**

*   查找字符串字符的最大和最小 ASCII 值
*   找出字符串中所有字符的 ASCII 值之和
*   因此，如果一个字符序列是 a(ASCII = 96)到 d(ASCII = 99)，那么结果预期总和应该是(0 到 99 的总和)减去(0 到 95 的总和)
*   数学方程式:

```
 MAX_VALUE*(MAX_VALUE+1)/2 - (MIN_VALUE-1)*((MIN_VALUE-1)+1)/2
```

*   检查计算的总和和预期的总和是否相等

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

bool check(string str)
{
    int min = INT_MAX;
    int max = -INT_MAX;
    int sum = 0;

    // For all the characters of the string
    for(int i = 0; i < str.size(); i++)
    {

        // Find the ascii value of the character
        int ascii = str[i];

        // Check if if its a valid character,
        // if not then return false
        if (ascii < 96 || ascii > 122)
            return false;

        // Calculate sum of all the
        // characters ascii values
        sum += ascii;

        // Find minimum ascii value
        // from the string
        if (min > ascii)
            min = ascii;

        // Find maximum ascii value
        // from the string
        if (max < ascii)
            max = ascii;
    }

    // To get the previous element
    // of the minimum ASCII value
    min -= 1;

    // Take the expected sum
    // from the above equation
    int eSum = ((max * (max + 1)) / 2) -
               ((min * (min + 1)) / 2);

    // Check if the expected sum is
    // equals to the calculated sum or not
    return sum == eSum;
}

// Driver code
int main()
{

    // 1st example
    string str = "dcef";
    if (check(str))
        cout << ("Yes");
    else
        cout << ("No");

    // 2nd example
    string str1 = "xyza";
    if (check(str1))
        cout << ("\nYes");
    else
        cout << ("\nNo");
}

// This code is contributed by amreshkumar3
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
public class GFG {

    public static boolean check(String str)
    {
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        int sum = 0;

        // for all the characters of the string
        for (int i = 0; i < str.length(); i++) {

            // find the ascii value of the character
            int ascii = (int)str.charAt(i);

            // check if if its a valid character,
            // if not then return false
            if (ascii < 96 || ascii > 122)
                return false;

            // calculate sum of all the
            // characters ascii values
            sum += ascii;

            // find minimum ascii value
            // from the string
            if (min > ascii)
                min = ascii;

            // find maximum ascii value
            // from the string
            if (max < ascii)
                max = ascii;
        }

        // To get the previous element
        // of the minimum ASCII value
        min -= 1;

        // take the expected sum
        // from the above equation
        int eSum
            = ((max * (max + 1)) / 2)
              - ((min * (min + 1)) / 2);

        // check if the expected sum is
        // equals to the calculated sum or not
        return sum == eSum;
    }

    // Driver code
    public static void main(String[] args)
    {

        // 1st example
        String str = "dcef";
        if (check(str))
            System.out.println("Yes");
        else
            System.out.println("No");

        // 2nd example
        String str1 = "xyza";

        if (check(str1))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
// This code is contributed by Arijit Basu(ArijitXfx)
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

def check(str):

    min = sys.maxsize
    max = -sys.maxsize - 1
    sum = 0

    # For all the characters of the string
    for i in range(len(str)):

        # Find the ascii value of the character
        ascii = str[i]

        # Check if if its a valid character,
        # if not then return false
        if (ord(ascii) < 96 or ord(ascii) > 122):
            return False

        # Calculate sum of all the
        # characters ascii values
        sum += ord(ascii)

        # Find minimum ascii value
        # from the string
        if (min > ord(ascii)):
            min = ord(ascii)

        # Find maximum ascii value
        # from the string
        if (max < ord(ascii)):
            max = ord(ascii)

    # To get the previous element
    # of the minimum ASCII value
    min -= 1

    # Take the expected sum
    # from the above equation
    eSum = (((max * (max + 1)) // 2) -
            ((min * (min + 1)) // 2))

    # Check if the expected sum is
    # equals to the calculated sum or not
    return sum == eSum

# Driver code
if __name__ == '__main__':

    # 1st example
    str = "dcef"

    if (check(str)):
        print("Yes")
    else:
        print("No")

    # 2nd example
    str1 = "xyza"

    if (check(str1)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    static bool check(string str)
    {
        int min = Int32.MaxValue;
        int max = Int32.MinValue;
        int sum = 0;

        // for all the characters of the string
        for (int i = 0; i < str.Length; i++)
        {

            // find the ascii value of the character
            int ascii = (int)str[i];

            // check if if its a valid character,
            // if not then return false
            if (ascii < 96 || ascii > 122)
                return false;

            // calculate sum of all the
            // characters ascii values
            sum += ascii;

            // find minimum ascii value
            // from the string
            if (min > ascii)
                min = ascii;

            // find maximum ascii value
            // from the string
            if (max < ascii)
                max = ascii;
        }

        // To get the previous element
        // of the minimum ASCII value
        min -= 1;

        // take the expected sum
        // from the above equation
        int eSum
            = ((max * (max + 1)) / 2)
              - ((min * (min + 1)) / 2);

        // check if the expected sum is
        // equals to the calculated sum or not
        return sum == eSum;
    }

  // Driver code
  static void Main()
  {

    // 1st example
    string str = "dcef";
    if (check(str))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    // 2nd example
    string str1 = "xyza";

    if (check(str1))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    function check( str) {
        var min = Number.MAX_VALUE;
        var max = Number.MIN_VALUE;
        var sum = 0;

        // for all the characters of the string
        for (i = 0; i < str.length; i++) {

            // find the ascii value of the character
            var ascii = parseInt( str.charCodeAt(i));

            // check if if its a valid character,
            // if not then return false
            if (ascii < 96 || ascii > 122)
                return false;

            // calculate sum of all the
            // characters ascii values
            sum += ascii;

            // find minimum ascii value
            // from the string
            if (min > ascii)
                min = ascii;

            // find maximum ascii value
            // from the string
            if (max < ascii)
                max = ascii;
        }

        // To get the previous element
        // of the minimum ASCII value
        min -= 1;

        // take the expected sum
        // from the above equation
        var eSum = parseInt((max * (max + 1)) / 2) - ((min * (min + 1)) / 2);

        // check if the expected sum is
        // equals to the calculated sum or not
        return sum == eSum;
    }

    // Driver code

        // 1st example
        var str = "dcef";
        if (check(str))
            document.write("Yes<br/>");
        else
            document.write("No<br/>");

        // 2nd example
        var str1 = "xyza";

        if (check(str1))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
Yes
No
```

***时间复杂度:**O(N)*T4】