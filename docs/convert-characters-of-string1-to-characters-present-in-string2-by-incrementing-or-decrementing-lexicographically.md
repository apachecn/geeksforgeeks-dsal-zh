# 通过按字典顺序递增或递减将字符串 1 的字符转换为字符串 2 中的字符

> 原文:[https://www . geesforgeks . org/将字符串中的字符 1 转换为字符串中的字符 2，方法是按字典顺序递增或递减/](https://www.geeksforgeeks.org/convert-characters-of-string1-to-characters-present-in-string2-by-incrementing-or-decrementing-lexicographically/)

给定两个具有小写英文字母的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **A** 和 **B** ，任务是找到转换字符串 **A** 所需的操作数，使得它只包含也在字符串 **B** 中的字母，其中在每次操作时，当前字符可以被更改为下一个字符或前一个字符。此外，' **z** 后的下一个字符是' **a** '，而' **a** 后的上一个字符是' **z** '。

**示例**:

> **输入**:A =“ABCD”，B =“BC”
> **输出** : 2
> **说明:**给定的字符串 A =“ABCD”可以通过在第一次移动中增加字符串的第一个字符和在第二次移动中减少最后一个字符来转换为字符串“bbcc”。因此，A =“bbcc”包含了字符串 b 中的所有字符。因此，所需的移动次数是 2，这是最小的可能。
> 
> **输入**:A =“abcde”，B =“yg”
> 输出 : 14

**方法:****给定的问题可以使用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。其思想是将字符串 A 中不在字符串 B 中的所有字符转换为字符串 B 中存在的最接近的可能字符，这可以通过以下步骤来完成:**

*   **将字符串 **B** 的[字符频率存储在](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)[无序地图](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) m 中**
*   **遍历给定的字符串 **A** 并检查 **B** 中的每个字符，将当前字符转换为该字符所需的步骤数。**
*   **将字符 **x** 转换为 **y** 的方法可以有以下两种不同类型:

    *   1 <sup>st</sup> 一是增加字符 **x** 直到达到 **y** ，即顺时针旋转。
    *   第二个<sup>和第一个</sup>是递减字符 **x** 直到达到 **y** ，即逆时针旋转。** 
*   **因此，在变量**和**中，保持 A 中每个字符顺时针和逆时针旋转的所有最小移动的总和，这是所需的值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the above appraoch
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum number
// of operations required to convert A
// such that it only contains letters
// in the string B
int minOperations(string a, string b)
{
    // Stores the characters in string B
    unordered_map<char, int> m;
    for (int i = 0; i < b.size(); i++) {
        m[b[i]]++;
    }

    // Stores the min count of operations
    int ans = 0;

    // Loop to iterte the given array
    for (int i = 0; i < a.size(); i++) {

        // Stores the minimum number of
        // moves required for ith index
        int mn = INT_MAX;

        // Loop to calculate the number
        // of moves required to convert
        // the current index
        for (int j = 0; j < 26; j++) {
            int val = a[i] - 'a';

            // If the current character
            // is also in b
            if (m[a[i]] > 0) {
                mn = 0;
                break;
            }
            else if (m['a' + j] > 0) {

                // Minimum of abs(val - j),
                // clockwise rotation and
                // anti clockwise rotation
                mn = min(mn, min(abs(val - j),
                                 min((26 - val) + j,
                                     val + (26 - j))));
            }
        }

        // Update answer
        ans += mn;
    }

    // Return Answer
    return ans;
}

int main()
{
    string A = "abcde";
    string B = "yg";

    cout << minOperations(A, B);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above appraoch
import java.util.*;
class GFG
{

// Function to calculate minimum number
// of operations required to convert A
// such that it only contains letters
// in the String B
static int minOperations(String a, String b)
{

    // Stores the characters in String B
    HashMap<Character,Integer> m = new HashMap<Character,Integer>();
    for (int i = 0; i < b.length(); i++) {
         if(m.containsKey(b.charAt(i))){
                m.put(b.charAt(i), m.get(b.charAt(i))+1);
            }
            else{
                m.put(b.charAt(i), 1);
            }
    }

    // Stores the min count of operations
    int ans = 0;

    // Loop to iterte the given array
    for (int i = 0; i < a.length(); i++) {

        // Stores the minimum number of
        // moves required for ith index
        int mn = Integer.MAX_VALUE;

        // Loop to calculate the number
        // of moves required to convert
        // the current index
        for (int j = 0; j < 26; j++) {
            int val = a.charAt(i) - 'a';

            // If the current character
            // is also in b
            if (m.containsKey(a.charAt(i))&&m.get(a.charAt(i)) > 0) {
                mn = 0;
                break;
            }
            else if (m.containsKey((char)('a' + j))&&m.get((char)('a' + j)) > 0) {

                // Minimum of Math.abs(val - j),
                // clockwise rotation and
                // anti clockwise rotation
                mn = Math.min(mn, Math.min(Math.abs(val - j),
                                 Math.min((26 - val) + j,
                                     val + (26 - j))));
            }
        }

        // Update answer
        ans += mn;
    }

    // Return Answer
    return ans;
}

public static void main(String[] args)
{
    String A = "abcde";
    String B = "yg";

    System.out.print(minOperations(A, B));

}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 implementation of the above appraoch
INT_MAX = 2147483647

# Function to calculate minimum number
# of operations required to convert A
# such that it only contains letters
# in the string B
def minOperations(a, b):

    # Stores the characters in string B
    m = {}
    for i in range(0, len(b)):
        if b[i] in m:
            m[b[i]] += 1
        else:
            m[b[i]] = 1

    # Stores the min count of operations
    ans = 0

    # Loop to iterte the given array
    for i in range(0, len(a)):

        # Stores the minimum number of
        # moves required for ith index
        mn = INT_MAX

        # Loop to calculate the number
        # of moves required to convert
        # the current index
        for j in range(0, 26):
            val = ord(a[i]) - ord('a')

            # If the current character
            # is also in b
            if (a[i] in m and m[a[i]] > 0):
                mn = 0
                break

            elif (chr(ord('a') + j) in m and m[chr(ord('a') + j)] > 0):

                # Minimum of abs(val - j),
                # clockwise rotation and
                # anti clockwise rotation
                mn = min(mn, min(abs(val - j),
                                 min((26 - val) + j,
                               val + (26 - j))))

        # Update answer
        ans += mn

    # Return Answer
    return ans

# Driver code
if __name__ == "__main__":

    A = "abcde"
    B = "yg"

    print(minOperations(A, B))

# This code is contributed by rakeshsahni
```

## **C#**

```
// C# implementation of the above appraoch
using System;
using System.Collections.Generic;
class GFG
{

    // Function to calculate Minimum number
    // of operations required to convert A
    // such that it only contains letters
    // in the String B
    static int MinOperations(String a, String b)
    {

        // Stores the characters in String B
        Dictionary<char, int> m = new Dictionary<char, int>();
        for (int i = 0; i < b.Length; i++)
        {
            if (m.ContainsKey(b[i]))
            {
                m[b[i]] += 1;
            }
            else
            {
                m[b[i]] = 1;
            }
        }

        // Stores the Min count of operations
        int ans = 0;

        // Loop to iterte the given array
        for (int i = 0; i < a.Length; i++)
        {

            // Stores the Minimum number of
            // moves required for ith index
            int mn = int.MaxValue;

            // Loop to calculate the number
            // of moves required to convert
            // the current index
            for (int j = 0; j < 26; j++)
            {
                int val = a[i] - 'a';

                // If the current character
                // is also in b
                if (m.ContainsKey(a[i]) && m[a[i]] > 0)
                {
                    mn = 0;
                    break;
                }
                else if (m.ContainsKey((char)('a' + j)) && m[(char)('a' + j)] > 0)
                {

                    // Minimum of Math.abs(val - j),
                    // clockwise rotation and
                    // anti clockwise rotation
                    mn = Math.Min(mn, Math.Min(Math.Abs(val - j),
                                     Math.Min((26 - val) + j,
                                         val + (26 - j))));
                }
            }

            // Update answer
            ans += mn;
        }

        // Return Answer
        return ans;
    }

    public static void Main()
    {
        String A = "abcde";
        String B = "yg";

        Console.Write(MinOperations(A, B));

    }
}

// This code is contributed by gfgking
```

## **java 描述语言**

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to calculate minimum number
       // of operations required to convert A
       // such that it only contains letters
       // in the string B
       function minOperations(a, b)
       {

           // Stores the characters in string B
           let m = new Map();
           for (let i = 0; i < b.length; i++)
           {
               if (m.has(b[i])) {
                   m.set(b[i], m.get(b[i]) + 1);
               }
               else {
                   m.set(b[i], 1);
               }
           }

           // Stores the min count of operations
           let ans = 0;

           // Loop to iterte the given array
           for (let i = 0; i< a.length; i++)
           {

               // Stores the minimum number of
               // moves required for ith index
               let mn = 999999;

               // Loop to calculate the number
               // of moves required to convert
               // the current index
               for (let j = 0; j< 26; j++)
               {

                   let val = a[i].charCodeAt(0) - 'a'.charCodeAt(0);

                   // If the current character
                   // is also in b
                   if (m.get(a[i]) > 0) {
                       mn = 0;
                       break;
                   }
                   else if (m.has(String.fromCharCode('a'.charCodeAt(0) + j))
                       && m.get(String.fromCharCode('a'.charCodeAt(0) + j)) > 0)
                   {

                       // Minimum of abs(val - j),
                       // clockwise rotation and
                       // anti clockwise rotation
                       mn = Math.min(mn, Math.min(Math.abs(val - j),
                           Math.min((26 - val) + j,
                               val + (26 - j))));
                   }
               }

               // Update answer
               ans += mn;
           }

           // Return Answer
           return ans;
       }
       let A = "abcde";
       let B = "yg";
       document.write(minOperations(A, B));

   // This code is contributed by Potta Lokesh
   </script>
```

****Output**

```
14
```** 

*****时间** **复杂度:** O(N)*
***辅助空间:** O(1)***