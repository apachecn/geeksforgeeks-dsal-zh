# 检查所有字符是否具有偶数频率的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-all-characters-with-even-frequency/](https://www.geeksforgeeks.org/program-to-check-if-all-characters-have-even-frequency/)

给定一个仅由小写字母组成的字符串，检查该字符串是否所有字符出现偶数次。
**例:**

> 输入:abaccaba
> 输出:Yes
> 解释:“a”出现四次，“b”出现两次，“c”出现两次，其他字母出现零次。
> 输入:第
> 输出:否

**方法:**
我们将遍历字符串，统计所有字符的出现次数，然后检查出现次数是否为偶数，是否有奇数频率的字符，然后立即打印 No

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

bool check(string s)
{

    // creating a frequency array
    int freq[26] = {0};

    // Finding length of s
    int n = s.length();
    for (int i = 0; i < s.length(); i++)

    // counting frequency of all characters
        freq[s[i] - 97]++;

    // checking if any odd frequency
    // is there or not
    for (int i = 0; i < 26; i++)
        if (freq[i] % 2 == 1)
        return false;
    return true;
}

// Driver Code
int main()
{
    string s = "abaccaba";
    check(s) ? cout << "Yes" << endl :
               cout << "No" << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    static boolean check(String s)
    {

        // creating a frequency array
        int[] freq = new int[26];

        // Finding length of s
        int n = s.length();

        // counting frequency of all characters
        for (int i = 0; i < s.length(); i++)
        {
            freq[(s.charAt(i)) - 97] += 1;
        }

        // checking if any odd frequency
        // is there or not
        for (int i = 0; i < freq.length; i++)
        {
            if (freq[i] % 2 == 1)
            {
                return false;
            }
        }
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "abaccaba";
        if (check(s))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the above approach
def check(s):

    # creating a frequency array
    freq =[0]*26

    # Finding length of s
    n = len(s)

    for i in range(n):

        # counting frequency of all characters
        freq[ord(s[i])-97]+= 1

    for i in range(26):

        # checking if any odd frequency
        # is there or not
        if (freq[i]% 2 == 1):
            return False
    return True

# Driver code
s ="abaccaba"
if(check(s)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static Boolean check(String s)
    {

        // creating a frequency array
        int[] freq = new int[26];

        // Finding length of s
        int n = s.Length;

        // counting frequency of all characters
        for (int i = 0; i < s.Length; i++)
        {
            freq[(s[i]) - 97] += 1;
        }

        // checking if any odd frequency
        // is there or not
        for (int i = 0; i < freq.Length; i++)
        {
            if (freq[i] % 2 == 1)
            {
                return false;
            }
        }
        return true;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "abaccaba";
        if (check(s))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

function check(s)
{

    // creating a frequency array
    var freq = Array(26).fill(0);

    // Finding length of s
    var n = s.length;
    for (var i = 0; i < s.length; i++)

    // counting frequency of all characters
        freq[s[i] - 97]++;

    // checking if any odd frequency
    // is there or not
    for (var i = 0; i < 26; i++)
        if (freq[i] % 2 == 1)
        return false;
    return true;
}

// Driver Code
var s = "abaccaba";
check(s) ? document.write("Yes") :
           document.write("No");

</script>
```

**输出:**

```
Yes
```

### 方法 2:使用内置的 python 函数。

**接近**:

我们将扫描字符串，并使用内置的[**【Counter()**](https://www.geeksforgeeks.org/python-counter-objects-elements/)功能计算所有字符的出现次数，然后遍历计数器列表，检查出现次数是否为偶数，如果有任何奇数频率的字符，则立即打印“否”

**注意:**该方法适用于所有类型的字符

## 蟒蛇 3

```
# Python implementation for
# the above approach

# importing Counter function
from collections import Counter

# Function to check if all
# elements occur even times
def checkString(s):

    # Counting the frequency of all
    # character using Counter function
    frequency = Counter(s)

    # Traversing frequency
    for i in frequency:

        # Checking if any element
        # has odd count
        if (frequency[i] % 2 == 1):
            return False
    return True

# Driver code
s = "geeksforgeeksfor"
if(checkString(s)):
    print("Yes")
else:
    print("No")

# This code is contributed by vikkycirus
```

**输出**:

```
Yes
```