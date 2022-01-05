# 检查表达式中的平衡括号| O(1)空间| O(N^2)时间复杂度

> 原文:[https://www . geesforgeks . org/check-for-balanced-in-in-a-expression-O1-space-on2-time-complexity/](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression-o1-space-on2-time-complexity/)

给定一个包含字符**(“**、**)”**、**“{“**、**“}”**、**“[”**、**”**的字符串**，任务是确定括号是否平衡。
如果出现以下情况，支架是平衡的:**

1.  开放式支架必须由相同类型的支架封闭。
2.  开放式括号必须以正确的顺序关闭。

**示例:**

> **输入:**str =(()[]”
> T3】输出:是
> 
> **输入:**str =)(({ } { "
> T3】输出:否

**进场:**

*   保留两个变量 **i** 和 **j** 来跟踪要比较的两个括号。
*   维护一个计数，该计数的值在遇到左括号时递增，在遇到右括号时递减。
*   遇到左括号时，设置 **j = i** 、 **i = i + 1** 和**计数器++** 。
*   当遇到右括号时，递减计数并在 **i** 和 **j** 比较括号，
    *   如果 **i** 和 **j** 处的括号匹配，则在**I<sup>th</sup>T9】和**j<sup>th</sup>T13】位置替换字符串中的 **'#'** 。递增 **i** ，递减 **j** ，直到遇到非 **'#'** 值或 **j ≥ 0** 。****
    *   如果 **i** 和 **j** 处的括号不匹配，则返回 false。
*   如果**计数！= 0** 则返回假。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// This helper function is called whenever 
// closing bracket is encountered. 
// Hence count is decremented 
// j and i points to opening and closing 
// brackets to be matched respectively 
// If brackets at i and j is a match 
// replace them with "#" character and decrement j 
// to point next opening bracket to * be matched 
// Similarly, increment i to point to next closing 
// bracket to be matched 
// If j is out of bound or brackets did not match return 0 
bool helperFunc(int& count, string& s, int& i, int& j, char tocom) 
{ 
    count--; 
    if (j > -1 && s[j] == tocom) { 
        s[i] = '#'; 
        s[j] = '#'; 
        while (j >= 0 && s[j] == '#') 
            j--; 
        i++; 
        return 1; 
    } 
    else
        return 0; 
} 

// Function that returns true if s is a 
// valid balanced bracket string 
bool isValid(string s) 
{ 

    // Empty string is considered balanced 
    if (s.length() == 0) 
        return true; 

    else { 
        int i = 0; 

        // Increments for opening bracket and 
        // decrements for closing bracket 
        int count = 0; 
        int j = -1; 
        bool result; 
        while (i < s.length()) { 
            switch (s[i]) { 
            case '}': 
                result = helperFunc(count, s, i, j, '{'); 
                if (result == 0) { 
                    return false; 
                } 
                break; 

            case ')': 
                result = helperFunc(count, s, i, j, '('); 
                if (result == 0) { 
                    return false; 
                } 
                break; 

            case ']': 
                result = helperFunc(count, s, i, j, '['); 
                if (result == 0) { 
                    return false; 
                } 
                break; 

            default: 
                j = i; 
                i++; 
                count++; 
            } 
        } 

        // count != 0 indicates unbalanced parentheses 
        // this check is required to handle cases where 
        // count of opening brackets > closing brackets 
        if (count != 0) 
            return false; 

        return true; 
    } 
} 

// Driver code 
int main() 
{ 
    string str = "[[]][]()"; 

    if (isValid(str)) 
        cout << "Yes"; 
    else
        cout << "No"; 

    return 0; 
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach 
import java.util.*; 

class GFG 
{ 

    static String s = "[[]][]()"; 
    static int count = 0; 
    static int i = 0; 
    static int j = -1; 

// This helper function is called whenever 
// closing bracket is encountered. 
// Hence count is decremented 
// j and i points to opening and closing 
// brackets to be matched respectively 
// If brackets at i and j is a match 
// replace them with "#" character and decrement j 
// to point next opening bracket to * be matched 
// Similarly, increment i to point to next closing 
// bracket to be matched 
// If j is out of bound or brackets did not match return 0 
static int helperFunc(char tocom) 
{ 
    count--; 
    char temp = s.charAt(j); 
    if (j > -1 && temp == tocom) 
    { 
        s = s.replace(s.charAt(i),'#'); 
        s = s.replace(s.charAt(j),'#'); 
        temp = s.charAt(j); 
        while (j >= 0 && temp == '#') 
            j--; 
        i++; 
        return 1; 
    } 
    else
        return 0; 
} 

// Function that returns true if s is a 
// valid balanced bracket string 
static boolean isValid() 
{ 

    // Empty string is considered balanced 
    if (s.length() == 0) 
        return true; 

    else { 
        int result; 
        while (i < s.length()) 
        { 
            char temp = s.charAt(i); 
            if(temp=='}') 
            { 
                result = helperFunc('{'); 
                if (result == 0) 
                { 
                    return false; 
                } 
            } 
            else if(temp == ')') 
            { 
                result = helperFunc('('); 
                if (result == 0) 
                { 
                    return false; 
                } 
            } 

            else if(temp == ']') 
            { 
                result = helperFunc('['); 
                if (result == 0) 
                { 
                    return false; 
                } 
            } 

            else
            { 
                j = i; 
                i++; 
                count++; 
            } 
        } 

        // count != 0 indicates unbalanced parentheses 
        // this check is required to handle cases where 
        // count of opening brackets > closing brackets 
        if (count != 0) 
            return false; 

        return true; 
    } 
} 

// Driver code 
public static void main(String args[]) 
{ 
    if (isValid()) 
    System.out.println("No"); 
    else
    System.out.println("Yes"); 
} 

} 

// This code is contributed by Surendra_Gangwar 
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# These are defined as global because they 
# are passed by reference 
count = 0
i = 0
j = -1

# This helper function is called whenever 
# closing bracket is encountered. 
# Hence count is decremented 
# j and i points to opening and closing 
# brackets to be matched respectively 
# If brackets at i and j is a match 
# replace them with "#" character and decrement j 
# to point next opening bracket to * be matched 
# Similarly, increment i to point to next closing 
# bracket to be matched 
# If j is out of bound or brackets 
# did not match return 0 
def helperFunc(s, tocom): 
    global i, j, count 
    count -= 1
    if j > -1 and s[j] == tocom: 
        s[i] = '#'
        s[j] = '#'
        while j >= 0 and s[j] == '#': 
            j -= 1
        i += 1
        return 1
    else: 
        return 0

# Function that returns true if s is a 
# valid balanced bracket string 
def isValid(s): 
    global i, j, count 

    # Empty string is considered balanced 
    if len(s) == 0: 
        return True
    else: 

        # Increments for opening bracket and 
        # decrements for closing bracket 
        result = False
        while i < len(s): 
            if s[i] == '}': 
                result = helperFunc(s, '{') 
                if result == 0: 
                    return False
            elif s[i] == ')': 
                result = helperFunc(s, '(') 
                if result == 0: 
                    return False
            elif s[i] == ']': 
                result = helperFunc(s, '[') 
                if result == 0: 
                    return False
            else: 
                j = i 
                i += 1
                count += 1

        # count != 0 indicates unbalanced parentheses 
        # this check is required to handle cases where 
        # count of opening brackets > closing brackets 
        if count != 0: 
            return False
        return True

# Driver Code 
if __name__ == "__main__": 
    string = "[[]][]()"
    string = list(string) 

    print("Yes") if isValid(string) else print("No") 

# This code is contributed by 
# sanjeev2552 
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

static string s = "[[]][]()";
static int count = 0;
static int i = 0;
static int j = -1;

// This helper function is called whenever
// closing bracket is encountered. Hence 
// count is decremented j and i points to
// opening and closing brackets to be matched 
// respectively. If brackets at i and j is a match
// replace them with "#" character and decrement j
// to point next opening bracket to * be matched
// Similarly, increment i to point to next closing
// bracket to be matched. If j is out of bound or
// brackets did not match return 0
static int helperFunc(char tocom)
{
    count--;
    char temp = s[j];

    if (j > -1 && temp == tocom) 
    {
        s = s.Replace(s[i],'#');
        s = s.Replace(s[j],'#');

        temp = s[j];
        while (j >= 0 && temp == '#')
            j--;

        i++;
        return 1;
    }
    else
        return 0;
}

// Function that returns true if s is a
// valid balanced bracket string
static bool isValid()
{

    // Empty string is considered balanced
    if (s.Length == 0)
        return true;

    else 
    {
        int result;
         while (i < s.Length) 
        { 
            char temp = s[i]; 
            if(temp == '}') 
            { 
                result = helperFunc('{'); 
                if (result == 0) 
                { 
                    return false; 
                } 
            } 

            else if(temp == ')') 
            { 
                result = helperFunc('('); 
                if (result == 0) 
                { 
                    return false; 
                } 
            } 

            else if(temp == ']') 
            { 
                result = helperFunc('['); 
                if (result == 0)  
                { 
                    return false; 
                } 
            } 

            else
            { 
                j = i; 
                i++; 
                count++; 
            } 
        } 

        // count != 0 indicates unbalanced 
        // parentheses this check is required 
        // to handle cases where count of opening
        // brackets > closing brackets 
        if (count != 0)
            return false;

        return true;
    }
}

// Driver code
public static void Main(string []args)
{
    if (isValid())
    {
        Console.Write("No");
    }
    else
    {
        Console.Write("Yes");
    }
}
}

// This code is contributed by rutvik_56
```

**Output:**

```
Yes

```