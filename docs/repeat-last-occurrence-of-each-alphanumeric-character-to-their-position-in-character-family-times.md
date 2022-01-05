# 将每个字母数字字符的最后一次出现重复到它们在字符族中的位置

> 原文:[https://www . geeksforgeeks . org/repeat-每个字母数字字符最后一次出现在字符系列中的位置-时间/](https://www.geeksforgeeks.org/repeat-last-occurrence-of-each-alphanumeric-character-to-their-position-in-character-family-times/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串[]** ，任务是对其进行编码，使得每个字符的最后一次出现与其在家族中的位置一样长。由于“a”是其家族的第一个字符(小写字母)，所以它将保持“a”，但“b”变成“bb”，“D”变成“DDDD”等等。如果是数字字符，字符出现的次数与其值一样多。由于“1”仍然是“1”，“2”变成了“22”，“0”变成了“等等”。但是除了一个角色的最后一次出现，其余的必须保持原样。(a-z)、(A-Z)和(0-9)以外的字符不受这种编码的影响。

**示例:**

> **输入:** str = "3bC"
> **输出:** 333bbCCC
> **说明:**在给定的字符串中，没有字符重复，因此所有字符都有一次出现，这显然是它们的最后一次出现。所以每个字符都会被编码。因为“3”是数值为 3 的数字字符，所以它将在结果字符串中出现三次。' b '是其家族的第二个字符，因此会出现两次。“C”是第三个大写字母，因此它会出现三次。
> 
> **输入:** str = "Ea2，0，E"
> **输出:** Ea22，，EEEEE
> **解释:**“E”在字符串中不是最后一次出现，因此它将保持在结果字符串中的原样。虽然“a”和“2”是它们在字符串中的唯一和最后一次出现，但它们将分别更改为“a”和“22”。字符'，'和' '将不受影响。“0”也将更改为。

**方法:** [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)跟踪每个字符的最新出现，然后为最后出现的字符进行编码。
按照以下步骤解决问题:

*   将变量[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **res** 初始化为空字符串来存储结果。
*   [用 **0** 初始化大小为 **26** 和 **num** 大小为 **10** 的小和**大写**数组，以存储](https://www.geeksforgeeks.org/arrays-in-c-cpp/)[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **str[]中任何字符的最后一次出现。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   如果 **str[i]** 大于等于**“0”**且小于等于**“9”**，则将**num【str[I]–“0”】**的值设置为 **i.**
    *   否则如果 **str[i]** 大于等于**‘a’**且小于等于**‘z’**，则将**小【str[I]–‘a’】**的值设置为 **i.**
    *   否则如果 **str[i]** 大于等于**‘A’**且小于等于**‘Z’**，则将**大写【str[I]–‘A’】**的值设置为 **i.**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   如果 **str[i]** 大于等于**“0”**且小于等于**“9”**且**num【str[I]—“0”】**等于 **i** ，则初始化变量**出现**为**str[I]—“0”**，并在结果字符串 **res 中追加 **str[i]** ，出现【T17**
    *   否则如果 **str[i]** 大于等于**‘a’**且小于等于**‘z’**且**小【str[I]—‘a’】**等于 **i** ，则将变量**初始化为**str[I]—‘a’，并在结果字符串 **res 中追加 **str[i]** ，出现【T11**
    *   否则如果 **str[i]** 大于等于**‘A’**且小于等于**‘Z’****大写【str[I]—‘0’】**等于 **i** ，那么初始化变量**出现**为**str[I]—‘A’**并在结果字符串 **res 中追加 **str[i]** ，出现【T11**
    *   否则，在结果[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **res.** 中追加**字符串【I】**
*   执行上述步骤后，打印[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **res** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to encode the given string
void encodeString(string str)
{

    // Variable string to store the result
    string res = "";

    // Arrays to store the last occuring index
    // of every character in the string
    int small[26] = { 0 }, capital[26] = { 0 },
        num[10] = { 0 };

    // Length of the string
    int n = str.size();

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // If str[i] is between 0 and 9
        if (str[i] >= '0' && str[i] <= '9') {
            num[str[i] - 48] = i;
        }

        // If str[i] is between a and z
        else if (str[i] >= 'a' && str[i] <= 'z') {
            small[str[i] - 97] = i;
        }

        // If str[i] is between A and Z
        else if (str[i] >= 'A' && str[i] <= 'Z') {
            capital[str[i] - 65] = i;
        }
    }

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // If str[i] is between a and z and i
        // is the last occurence in str
        if ((str[i] >= 'a' && str[i] <= 'z')
            && small[str[i] - 97] == i) {

            int occ = str[i] - 96;
            while (occ--) {
                res += str[i];
            }
        }

        // If str[i] is between A and Z and i
        // is the last occurence in str
        else if ((str[i] >= 'A' && str[i] <= 'Z')
                 && capital[str[i] - 65] == i) {

            int occ = str[i] - 64;
            while (occ--) {
                res += str[i];
            }
        }

        // If str[i] is between 0 and 9 and i
        // is the last occurence in str
        else if ((str[i] >= '0' && str[i] <= '9')
                 && num[str[i] - 48] == i) {

            int occ = str[i] - 48;
            while (occ--) {
                res += str[i];
            }
        }
        else {
            res += str[i];
        }
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    string str = "Ea2, 0, E";

    encodeString(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to encode the given string
static void encodeString(String str)
{
    // Variable string to store the result
    String res = "";

    // Arrays to store the last occuring index
    // of every character in the string
    int small[] = new int[26];
    int capital[] = new int[26];
    int num[] = new int[10];
        for(int i = 0; i < 26; i++)
        {
            small[i] = 0;
            capital[i] = 0;
        }
        for(int i = 0; i < 10; i++)
        {
            num[i] = 0;
        }

    // Length of the string
    int n = str.length();

    // Iterate over the range
    for (int i = 0; i < n; i++)
    {

        // If str[i] is between 0 and 9
        if (str.charAt(i)>= '0' && str.charAt(i) <= '9')
        {
            num[str.charAt(i) - 48] = i;
        }

        // If str[i] is between a and z
        else if (str.charAt(i) >= 'a' && str.charAt(i)<= 'z') {
            small[str.charAt(i)- 97] = i;
        }

        // If str[i] is between A and Z
        else if (str.charAt(i)>= 'A' && str.charAt(i) <= 'Z') {
            capital[str.charAt(i)- 65] = i;
        }
    }

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // If str[i] is between a and z and i
        // is the last occurence in str
        if ((str.charAt(i)>= 'a' && str.charAt(i)<= 'z')
            && small[str.charAt(i)- 97] == i) {

            int occ = str.charAt(i) - 96;
            while (occ-- >0)
            {
                res += str.charAt(i);
            }
        }

        // If str[i] is between A and Z and i
        // is the last occurence in str
        else if ((str.charAt(i) >= 'A' && str.charAt(i) <= 'Z') && capital[str.charAt(i)- 65] == i)
        {

            int occ = str.charAt(i) - 64;
            while (occ-- >0) {
                res = res+str.charAt(i);
            }
        }

        // If str[i] is between 0 and 9 and i
        // is the last occurence in str
        else if ((str.charAt(i)>= '0' && str.charAt(i) <= '9')
                 && num[str.charAt(i) - 48] == i) {

            int occ = str.charAt(i) - 48;
            while (occ-- >0) {
                res = res+str.charAt(i);
            }
        }
        else {
            res = res+str.charAt(i);
        }
    }

    // Print the result
    System.out.print(res);
}

    // Driver Code
    public static void main(String[] args)
    {
            String str = "Ea2, 0, E";

              encodeString(str);
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to encode the given string
def encodeString(str):

    # Variable string to store the result
    res = ""

    # Arrays to store the last occuring index
    # of every character in the string
    small = [0 for i in range(26)]
    capital = [0 for i in range(26)]
    num = [0 for i in range(10)]

    # Length of the string
    n = len(str)

    # Iterate over the range
    for i in range(n):
        # If str[i] is between 0 and 9
        if (str[i] >= '0' and str[i] <= '9'):
            num[ord(str[i]) - 48] = i

        # If str[i] is between a and z
        elif(str[i] >= 'a' and str[i] <= 'z'):
            small[ord(str[i]) - 97] = i

        # If str[i] is between A and Z
        elif(str[i] >= 'A' and str[i] <= 'Z'):
            capital[ord(str[i]) - 65] = i

    # Iterate over the range
    for i in range(n):

        # If str[i] is between a and z and i
        # is the last occurence in str
        if ((str[i] >= 'a' and str[i] <= 'z') and small[ord(str[i]) - 97] == i):
            occ = ord(str[i]) - 96
            while(occ>0):
                res += str[i]
                occ -= 1

        # If str[i] is between A and Z and i
        # is the last occurence in str
        elif((str[i] >= 'A' and str[i] <= 'Z') and capital[ord(str[i]) - 65] == i):
            occ = ord(str[i]) - 64
            while (occ>0):
                res += str[i]
                occ -= 1

        # If str[i] is between 0 and 9 and i
        # is the last occurence in str
        elif((str[i] >= '0' and str[i] <= '9') and num[ord(str[i]) - 48] == i):
            occ = ord(str[i]) - 48
            while (occ>0):
                res += str[i]
                occ -= 1
        else:
            res += str[i]

    # Print the result
    print(res)

# Driver Code
if __name__ == '__main__':
    str = "Ea2, 0, E"
    encodeString(str)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to encode the given string
  static void encodeString(String str)
  {

    // Variable string to store the result
    String res = "";

    // Arrays to store the last occuring index
    // of every character in the string
    int []small = new int[26];
    int []capital = new int[26];
    int []num = new int[10];
    for(int i = 0; i < 26; i++)
    {
      small[i] = 0;
      capital[i] = 0;
    }
    for(int i = 0; i < 10; i++)
    {
      num[i] = 0;
    }

    // Length of the string
    int n = str.Length;

    // Iterate over the range
    for (int i = 0; i < n; i++)
    {

      // If str[i] is between 0 and 9
      if (str[i]>= '0' && str[i] <= '9')
      {
        num[str[i] - 48] = i;
      }

      // If str[i] is between a and z
      else if (str[i] >= 'a' && str[i]<= 'z') {
        small[str[i]- 97] = i;
      }

      // If str[i] is between A and Z
      else if (str[i]>= 'A' && str[i] <= 'Z') {
        capital[str[i]- 65] = i;
      }
    }

    // Iterate over the range
    for (int i = 0; i < n; i++) {

      // If str[i] is between a and z and i
      // is the last occurence in str
      if ((str[i]>= 'a' && str[i]<= 'z')
          && small[str[i]- 97] == i) {

        int occ = str[i] - 96;
        while (occ-- >0)
        {
          res += str[i];
        }
      }

      // If str[i] is between A and Z and i
      // is the last occurence in str
      else if ((str[i] >= 'A' && str[i] <= 'Z') && capital[str[i]- 65] == i)
      {

        int occ = str[i] - 64;
        while (occ-- >0) {
          res = res+str[i];
        }
      }

      // If str[i] is between 0 and 9 and i
      // is the last occurence in str
      else if ((str[i]>= '0' && str[i] <= '9')
               && num[str[i] - 48] == i) {

        int occ = str[i] - 48;
        while (occ-- >0) {
          res = res+str[i];
        }
      }
      else {
        res = res+str[i];
      }
    }

    // Print the result
    Console.Write(res);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String str = "Ea2, 0, E";

    encodeString(str);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to encode the given string
        function encodeString(str) {

            // Variable string to store the result
            let res = "";

            // Arrays to store the last occuring index
            // of every character in the string
            let small = new Array(26).fill(0), capital = new Array(26).fill(0),
                num = new Array(26).fill(0);

            // Length of the string
            let n = str.length;

            // Iterate over the range
            for (let i = 0; i < n; i++) {

                // If str[i] is between 0 and 9
                if (str[i].charCodeAt(0) >= '0'.charCodeAt(0) && str[i].charCodeAt(0) <= '9'.charCodeAt(0)) {
                    num[str[i].charCodeAt(0) - 48] = i;
                }

                // If str[i] is between a and z
                else if (str[i].charCodeAt(0) >= 'a'.charCodeAt(0) && str[i].charCodeAt(0) <= 'z'.charCodeAt(0)) {
                    small[str[i].charCodeAt(0) - 97] = i;
                }

                // If str[i] is between A and Z
                else if (str[i].charCodeAt(0) >= 'A'.charCodeAt(0) && str[i].charCodeAt(0) <= 'Z'.charCodeAt(0)) {
                    capital[str[i].charCodeAt(0) - 65] = i;
                }
            }

            // Iterate over the range
            for (let i = 0; i < n; i++) {

                // If str[i] is between a and z and i
                // is the last occurence in str
                if ((str[i].charCodeAt(0) >= 'a'.charCodeAt(0) && str[i].charCodeAt(0) <= 'z'.charCodeAt(0))
                    && small[str[i].charCodeAt(0) - 97] == i) {

                    let occ = str[i].charCodeAt(0) - 96;
                    while (occ--) {
                        res += str[i];
                    }
                }

                // If str[i] is between A and Z and i
                // is the last occurence in str
                else if ((str[i].charCodeAt(0) >= 'A'.charCodeAt(0) && str[i].charCodeAt(0) <= 'Z'.charCodeAt(0))
                    && capital[str[i].charCodeAt(0) - 65] == i) {

                    let occ = str[i].charCodeAt(0) - 64;
                    while (occ--) {
                        res += str[i];
                    }
                }

                // If str[i] is between 0 and 9 and i
                // is the last occurence in str
                else if ((str[i].charCodeAt(0) >= '0'.charCodeAt(0) && str[i].charCodeAt(0) <= '9'.charCodeAt(0))
                    && num[str[i].charCodeAt(0) - 48] == i) {

                    let occ = str[i].charCodeAt(0) - 48;
                    while (occ--) {
                        res += str[i];
                    }
                }
                else {
                    res += str[i];
                }
            }

            // Print the result
            document.write(res);
        }

        // Driver Code
        let str = "Ea2, 0, E";
        encodeString(str);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Ea22, , EEEEE
```

***时间复杂度:** O(N)*
***辅助空间:** O(M)(合成字符串的大小)*