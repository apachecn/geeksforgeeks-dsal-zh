# 查找分数

中的重复序列

给定一个分数，找到一个数字的重复序列（如果存在），否则，打印“无重复序列”。

**示例：**

```
Input  : Numerator = 8, Denominator = 3
Output : Recurring sequence is 6 
Explanation : 8/3 = 2.66666666.......  

Input : Numerator = 50, Denominator = 22
Output : Recurring sequence is 27
Explanation : 50/22 = 2.272727272..... 

Input : Numerator = 11, Denominator = 2
Output : No recurring sequence
Explanation : 11/2 = 5.5 

```

## [我们强烈建议您单击此处并进行实践，然后再继续解决方案。](https://practice.geeksforgeeks.org/problem-page.php?pid=514)

**小数部分何时重复？**
让我们模拟一下将分数转换为小数的过程。 让我们看一下已经计算出整数部分的那部分，即楼板（分子/分母）。 现在我们剩下（余数=分子％分母）/分母。
如果您还记得转换为十进制的过程，则在每个步骤中，请执行以下操作：

1.  乘以 10。
2.  将余数/分母追加到结果中。
3.  余数=余数％分母。

任何时候，如果余数变为 0，我们就完成了。
但是，当存在重复序列时，余数永远不会变为 0。例如，如果您查看 1/3，则余数永远不会变为 0。
以下是一个重要的观察结果：
如果我们开始 使用余数“ rem”，并且如果余数在任何时间点重复，则两次出现的“ rem”之间的数字将继续重复。
因此，想法是将可见的剩余物存储在地图中。 每当余数重复时，我们将在下一次出现之前返回序列。

以下是上述想法的实现。

## C++

```cpp

// C++ program to find repeating sequence in a fraction
#include <bits/stdc++.h>
using namespace std;

// This function returns repeating sequence of
// a fraction.  If repeating sequence doesn't
// exits, then returns empty string
string fractionToDecimal(int numr, int denr)
{
    string res; // Initialize result

    // Create a map to store already seen remainders
    // remainder is used as key and its position in
    // result is stored as value. Note that we need
    // position for cases like 1/6.  In this case,
    // the recurring sequence doesn't start from first
    // remainder.
    map <int, int> mp;
    mp.clear();

    // Find first remainder
    int rem = numr%denr;

    // Keep finding remainder until either remainder
    // becomes 0 or repeats
    while ( (rem!=0) && (mp.find(rem) == mp.end()) )
    {
        // Store this remainder
        mp[rem] = res.length();

        // Multiply remainder with 10
        rem = rem*10;

        // Append rem / denr to result
        int res_part = rem / denr;
        res += to_string(res_part);

        // Update remainder
        rem = rem % denr;
    }

    return (rem == 0)? "" : res.substr(mp[rem]);
}

// Driver code
int main()
{
    int numr = 50, denr = 22;
    string res = fractionToDecimal(numr, denr);
    if (res == "")
        cout << "No recurring sequence";
    else
        cout << "Recurring sequence is " << res;
    return 0;
}

```

## Java

```java

// Java program to find 
// repeating sequence 
// in a fraction
import java.util.*;
class GFG{

// This function returns repeating 
// sequence of a fraction. If 
// repeating sequence doesn't
// exits, then returns empty String
static String fractionToDecimal(int numr, 
                                int denr)
{  
  // Initialize result
  String res=""; 

  // Create a map to store already 
  // seen remainders. Remainder is 
  // used as key and its position in
  // result is stored as value. 
  // Note that we need position for 
  // cases like 1/6.  In this case,
  // the recurring sequence doesn't 
  // start from first remainder.
  HashMap <Integer, 
           Integer> mp = new HashMap<>();
  mp.clear();

  // Find first remainder
  int rem = numr%denr;

  // Keep finding remainder until
  //  either remainder becomes 0 or repeats
  while ((rem!=0) && 
         (!mp.containsValue(rem)))
  {
    // Store this remainder
    mp.put(rem, res.length());

    // Multiply remainder with 10
    rem = rem * 10;

    // Append rem / denr to result
    int res_part = rem / denr;
    res += String.valueOf(res_part);

    // Update remainder
    rem = rem % denr;
  }

  if(rem == 0)
    return " ";
  else
    if(mp.containsKey(rem))
      return res.substring(mp.get(rem));

  return "";
}

// Driver code
public static void main(String[] args)
{
  int numr = 50, denr = 22;
  String res = fractionToDecimal(numr, denr);
  if (res == "")
    System.out.print("No recurring sequence");
  else
    System.out.print("Recurring sequence is " +  res);
}
}

// This code is contributed by gauravrajput1

```

## Python3

```py

# Python3 program to find repeating 
# sequence in a fraction

# This function returns repeating sequence 
# of a fraction.If repeating sequence doesn't
# exits, then returns empty string
def fractionToDecimal(numr, denr):

    # Initialize result
    res = "" 

    # Create a map to store already seen
    # remainders. Remainder is used as key
    # and its position in result is stored 
    # as value. Note that we need position
    # for cases like 1/6.  In this case,
    # the recurring sequence doesn't start
    # from first remainder.
    mp = {}

    # Find first remainder
    rem = numr % denr

    # Keep finding remainder until either
    # remainder becomes 0 or repeats
    while ((rem != 0) and (rem not in mp)):

        # Store this remainder
        mp[rem] = len(res)

        # Multiply remainder with 10
        rem = rem * 10

        # Append rem / denr to result
        res_part = rem // denr
        res += str(res_part)

        # Update remainder
        rem = rem % denr

    if (rem == 0):
        return ""
    else:
        return res[mp[rem]:]

# Driver code
numr, denr = 50, 22
res = fractionToDecimal(numr, denr)

if (res == ""):
    print("No recurring sequence")
else:
    print("Recurring sequence is", res)

# This code is contributed by divyeshrabadiya07

```

## C#

```cs

// C# program to find repeating sequence 
// in a fraction
using System;
using System.Collections.Generic;

class GFG{

// This function returns repeating 
// sequence of a fraction. If 
// repeating sequence doesn't
// exits, then returns empty String
static string fractionToDecimal(int numr, 
                                int denr)
{ 
  // Initialize result
  string res = ""; 

  // Create a map to store already 
  // seen remainders. Remainder is 
  // used as key and its position in
  // result is stored as value. 
  // Note that we need position for 
  // cases like 1/6.  In this case,
  // the recurring sequence doesn't 
  // start from first remainder.
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();

  // Find first remainder
  int rem = numr%denr;

  // Keep finding remainder until
  // either remainder becomes 0 
  // or repeats
  while ((rem != 0) && 
         (!mp.ContainsValue(rem)))
  {

    // Store this remainder
    mp[rem] = res.Length;

    // Multiply remainder with 10
    rem = rem * 10;

    // Append rem / denr to result
    int res_part = rem / denr;
    res += res_part.ToString();

    // Update remainder
    rem = rem % denr;
  }

  if (rem == 0)
    return " ";
  else
    if (mp.ContainsKey(rem))
      return res.Substring(mp[rem]);

  return "";
}

// Driver code
public static void Main(string[] args)
{
  int numr = 50, denr = 22;
  string res = fractionToDecimal(numr, denr);

  if (res == "")
    Console.Write("No recurring sequence");
  else
    Console.Write("Recurring sequence is " +  res);
}
}

// This code is contributed by rutvik_56

```

**输出：**

```
Recurring sequence is 27

```

本文由 **Dhruv Mahajan** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

