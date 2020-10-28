# 最小化要更改的字符以使字符串的左右旋转相同

给定小写英文字母的字符串 **S** ，任务是找到要更改的最小字符数，以使字符串的[左右旋转相同。](https://www.geeksforgeeks.org/left-rotation-right-rotation-string-2/)

**示例**：

> **输入**：S =“ abcd”
> **输出**：2
> **说明**：
> 左移后的字符串：“ bcda”
> 右移后的字符串：“ dabc”
> 将位置 3 的字符更改为“ a”，将位置 4 的字符更改为“ b”，将字符串修改为“ abab”。
> 因此，左右旋转都变为“ baba”。
> 
> **输入**：S =“ gfg”
> **输出**：1
> **说明**：
> 将位置 1 的字符更新为“ g”后 ，字符串变成“ ggg”。
> 因此，左右旋转相等。

**方法**：解决此问题的关键观察结果是，当字符串的[长度为偶数时，则偶数索引处的所有字符和奇数索引处的字符必须相同 左右旋转相同。 对于奇数长度的字符串，所有字符必须相等。 请按照以下步骤解决问题：](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)

*   检查字符串的长度是否为偶数，则要更改的最少字符数是字符串的长度，不包括偶数索引和奇数索引处最常出现的元素的频率。

*   否则，如果字符串的长度为奇数，则要更改的最小字符数是字符串的长度，不包括字符串中出现频率最高的字符的频率。

*   打印获得的最终计数。

下面是上述方法的实现：

## C++

```cpp

// C++ Program of the
// above approch

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// characters to be removed from
// the string
int getMinimumRemoval(string str)
{
    int n = str.length();

    // Initialize answer by N
    int ans = n;

    // If length is even
    if (n % 2 == 0) {

        // Frequency array for odd
        // and even indices
        vector<int> freqEven(128);
        vector<int> freqOdd(128);

        // Store the frequency of the
        // characters at even and odd
        // indices
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                freqEven[str[i]]++;
            }
            else {
                freqOdd[str[i]]++;
            }
        }

        // Stores the most occuring frequency
        // for even and odd indices
        int evenMax = 0, oddMax = 0;

        for (char chr = 'a'; chr <= 'z'; chr++) {

            evenMax = max(evenMax, freqEven[chr]);
            oddMax = max(oddMax, freqOdd[chr]);
        }

        // Update the answer
        ans = ans - evenMax - oddMax;
    }

    // If length is odd
    else {
        // Stores the frequency of the
        // characters of the string
        vector<int> freq(128);
        for (int i = 0; i < n; i++) {
            freq[str[i]]++;
        }

        // Stores the most occuring character
        // in the string
        int strMax = 0;
        for (char chr = 'a'; chr <= 'z'; chr++) {
            strMax = max(strMax, freq[chr]);
        }

        // Update the answer
        ans = ans - strMax;
    }

    return ans;
}

// Driver Code
int main()
{
    string str = "geeksgeeks";

    cout << getMinimumRemoval(str);
}

```

## Java

```java

// Java program of the 
// above approch 
class GFG{

// Function to find the minimum 
// characters to be removed from 
// the string 
public static int getMinimumRemoval(String str) 
{ 
    int n = str.length(); 

    // Initialize answer by N 
    int ans = n; 

    // If length is even 
    if (n % 2 == 0)
    { 

        // Frequency array for odd 
        // and even indices 
        int[] freqEven = new int[128];
        int[] freqOdd = new int[128];

        // Store the frequency of the 
        // characters at even and odd 
        // indices 
        for(int i = 0; i < n; i++) 
        { 
            if (i % 2 == 0)
            { 
                freqEven[str.charAt(i)]++; 
            } 
            else
            { 
                freqOdd[str.charAt(i)]++; 
            } 
        } 

        // Stores the most occuring frequency 
        // for even and odd indices 
        int evenMax = 0, oddMax = 0; 

        for(char chr = 'a'; chr <= 'z'; chr++)
        { 
            evenMax = Math.max(evenMax, 
                               freqEven[chr]); 
            oddMax = Math.max(oddMax,
                              freqOdd[chr]); 
        } 

        // Update the answer 
        ans = ans - evenMax - oddMax; 
    } 

    // If length is odd 
    else
    {

        // Stores the frequency of the 
        // characters of the string 
        int[] freq = new int[128];
        for(int i = 0; i < n; i++)
        { 
            freq[str.charAt(i)]++; 
        } 

        // Stores the most occuring character 
        // in the string 
        int strMax = 0; 
        for(char chr = 'a'; chr <= 'z'; chr++) 
        { 
            strMax = Math.max(strMax, freq[chr]); 
        } 

        // Update the answer 
        ans = ans - strMax; 
    } 
    return ans; 
} 

// Driver code
public static void main(String[] args) 
{
    String str = "geeksgeeks"; 

    System.out.print(getMinimumRemoval(str));
}
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```py

# Python3 Program of the
# above approch

# Function to find the minimum
# characters to be removed from
# the string
def getMinimumRemoval(str):

    n = len(str)

    # Initialize answer by N
    ans = n

    # If length is even
    if(n % 2 == 0):

        # Frequency array for odd
        # and even indices
        freqEven = {}
        freqOdd = {}
        for ch in range(ord('a'), 
                        ord('z') + 1):
            freqEven[chr(ch)] = 0
            freqOdd[chr(ch)] = 0

        # Store the frequency of the
        # characters at even and odd
        # indices
        for i in range(n):
            if(i % 2 == 0):
                if str[i] in freqEven:
                    freqEven[str[i]] += 1
            else:
                if str[i] in freqOdd:
                    freqOdd[str[i]] += 1

        # Stores the most occuring 
        # frequency for even and 
        # odd indices
        evenMax = 0
        oddMax = 0

        for ch in range(ord('a'), 
                        ord('z') + 1):
            evenMax = max(evenMax, 
                      freqEven[chr(ch)])
            oddMax = max(oddMax, 
                     freqOdd[chr(ch)])

        # Update the answer
        ans = ans - evenMax - oddMax

    # If length is odd
    else:

        # Stores the frequency of the
        # characters of the string
        freq = {}

        for ch in range('a','z'):
            freq[chr(ch)] = 0
        for i in range(n):
            if str[i] in freq:
                freq[str[i]] += 1

        # Stores the most occuring 
        # characterin the string
        strMax = 0

        for ch in range('a','z'):
            strMax = max(strMax, 
                     freq[chr(ch)])

        # Update the answer
        ans = ans - strMax

    return ans

# Driver Code
str = "geeksgeeks"
print(getMinimumRemoval(str))

# This code is contributed by avanitrachhadiya2155

```

## C#

```cs

// C# program of the 
// above approch 
using System;
class GFG{

// Function to find the minimum 
// characters to be removed from 
// the string 
public static int getMinimumRemoval(String str) 
{ 
  int n = str.Length; 

  // Initialize answer by N 
  int ans = n; 

  // If length is even 
  if (n % 2 == 0)
  { 
    // Frequency array for odd 
    // and even indices 
    int[] freqEven = new int[128];
    int[] freqOdd = new int[128];

    // Store the frequency of the 
    // characters at even and odd 
    // indices 
    for(int i = 0; i < n; i++) 
    { 
      if (i % 2 == 0)
      { 
        freqEven[str[i]]++; 
      } 
      else
      { 
        freqOdd[str[i]]++; 
      } 
    } 

    // Stores the most occuring frequency 
    // for even and odd indices 
    int evenMax = 0, oddMax = 0; 

    for(char chr = 'a'; chr <= 'z'; chr++)
    { 
      evenMax = Math.Max(evenMax, 
                         freqEven[chr]); 
      oddMax = Math.Max(oddMax,
                        freqOdd[chr]); 
    } 

    // Update the answer 
    ans = ans - evenMax - oddMax; 
  } 

  // If length is odd 
  else
  {
    // Stores the frequency of the 
    // characters of the string 
    int[] freq = new int[128];
    for(int i = 0; i < n; i++)
    { 
      freq[str[i]]++; 
    } 

    // Stores the most occuring character 
    // in the string 
    int strMax = 0; 
    for(char chr = 'a'; chr <= 'z'; chr++) 
    { 
      strMax = Math.Max(strMax, freq[chr]); 
    } 

    // Update the answer 
    ans = ans - strMax; 
  } 
  return ans; 
} 

// Driver code
public static void Main(String[] args) 
{
  String str = "geeksgeeks"; 
  Console.Write(getMinimumRemoval(str));
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
6

```

***时间复杂度**：O（N）*

***辅助空间**：O（1）*

