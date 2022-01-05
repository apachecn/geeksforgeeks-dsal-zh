# 检查一个数字是否是庞加莱

> 原文:[https://www . geesforgeks . org/check-if-a-number-a-pangram-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-a-pangram-or-not/)

给定一个整数 **N** ，任务是检查给定的数字是否为[庞加莱](https://www.geeksforgeeks.org/pangram-checking/)。
***注:**一个庞加兰号至少包含每一个数字**【0-9】**一次。*

**示例:**

> **输入:** N = 10239876540022
> **输出:**是
> **说明:** N 包含 0 到 9 的所有数字。因此，它是一只公羊。
> 
> **输入:** N = 234567890
> **输出:**否
> **说明:** N 不含数字 1。因此，它不是一只公羊。

[**设置**](https://www.geeksforgeeks.org/set-in-cpp-stl/) **基于方法:**想法是使用[设置](https://www.geeksforgeeks.org/python-sets/)来存储 **N** 中存在的不同数字的计数。按照以下步骤解决问题:

*   将[数字 N 转换为等效字符串。](https://www.geeksforgeeks.org/convert-integer-to-string-in-python/)
*   [将字符串转换为集合。](https://www.geeksforgeeks.org/convert-string-to-set-in-python/)
*   如果集合的[大小为 **10** ，则它包含所有可能的不同数字**【0–9】**。因此，打印**“是”**。](https://www.geeksforgeeks.org/find-the-length-of-a-set-in-python/)
*   否则，打印**“否”**

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N
// is a Pangram or not
string numberPangram(string N)
{

    // Add all characters pf arrNum to set
    set<char> setNum;

    for (int i = 0; i < N.length(); i++) {
        setNum.insert(N[i]);
    }

    // If the length of set is 10
    // The number is a Pangram
    if (setNum.size() == 10)
        return "True";
    else
        return "False";
}

// Driver code
int main()
{
    string N = "10239876540022";
    cout << (numberPangram(N));
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.math.BigInteger;
import java.util.HashSet;

class GFG{

// Function to check if N
// is a Pangram or not
static String numberPangram(BigInteger N)
{

    // Stores equivalent string
    // representation of N
    String num = N.toString();

    // Convert the string to Character array
    char[] arrNum = num.toCharArray();

    // Add all characters pf arrNum to set
    HashSet<Character> setNum = new HashSet<Character>();

    for(char ch : arrNum)
    {
        setNum.add(ch);
    }

    // If the length of set is 10
    // The number is a Pangram
    if (setNum.size() == 10)
        return "True";
    else
        return "False";
}

// Driver code
public static void main(String[] args)
{
    BigInteger N = new BigInteger("10239876540022");
    System.out.print(numberPangram(N));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to check if N
# is a Pangram or not
def numberPangram(N):

    # Stores equivalent string
    # representation of N
    num = str(N)

    # Convert the string to set
    setnum = set(num)

    # If the length of set is 10
    if(len(setnum) == 10):

          # The number is a Pangram
        return True
    else:
        return False

# Driver Code

N = 10239876540022
print(numberPangram(N))
```

## C#

```
// C# implementation of above approach
using System;
using System.Globalization;
using System.Numerics;
using System.Collections.Generic;
class GFG
{

// Function to check if N
// is a Pangram or not
static String numberPangram(ulong  N)
{

    // Stores equivalent string
    // representation of N
    string num = N.ToString();

    // Convert the string to Character array
    char[] arrNum = num.ToCharArray();

    // Add all characters pf arrNum to set
   HashSet<char> setNum = new HashSet<char>();

    foreach(char ch in arrNum)
    {
        setNum.Add(ch);
    }

    // If the length of set is 10
    // The number is a Pangram
    if (setNum.Count == 10)
        return "True";
    else
        return "False";
}

// Driver Code
    static void Main() {
      ulong  N = 10239876540022;
      Console.Write(numberPangram(N));
      }
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to check if N
// is a Pangram or not
function numberPangram(N)
{

    // Add all characters pf arrNum to set
    var setNum = new Set();

    for (var i = 0; i < N.length; i++) {
        setNum.add(N[i]);
    }

    // If the length of set is 10
    // The number is a Pangram
    if (setNum.size == 10)
        return "True";
    else
        return "False";
}

// Driver code
var N = "10239876540022";
document.write(numberPangram(N));

</script>
```

**Output:** 

```
True
```

***时间复杂度:**O(log<sub>10</sub>N * log(log<sub>10</sub>N))*
***辅助空间:** O(1)*

[](https://www.geeksforgeeks.org/hashing-data-structure/)****基于哈希的方法:**按照以下步骤解决问题:**

*   **[将 N 转换为其等价字符串。](https://www.geeksforgeeks.org/python-convert-string-to-n-chunks-tuple/)**
*   **计算该字符串中所有字符的[频率。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/) [Counter()](https://www.geeksforgeeks.org/python-counter-objects-elements/) 函数可以在 Python 中用于此目的。**
*   **如果存储频率的[字典](https://www.geeksforgeeks.org/python-dictionary/) / [散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)的长度为 **10** ，则该数字包含所有可能的不同数字。因此，打印**“是**”。**
*   **否则，打印**“否”**。**

**下面是上述方法的实现:**

## **蟒蛇 3**

```
# Python implementation of above approach

from collections import Counter

# Function to check if
# N is a Pangram or not
def numberPangram(N):

    # Stores equivalent string
    # representation of N
    num = str(N)

    # Count frequencies of
    # digits present in N
    frequency = Counter(num)

    # If the length of the
    # dictionary frequency is 10
    if(len(frequency) == 10):

          # The number is a Pangram
        return True
    else:
        return False

# Driver Code

N =10239876540022
print(numberPangram(N))
```

****Output:** 

```
True
```** 

*****时间复杂度:**O(log<sub>10</sub>N * log(log<sub>10</sub>N))*
***辅助空间:** O(1)***