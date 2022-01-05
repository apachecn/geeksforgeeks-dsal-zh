# 检查一个给定字符串的任何排列在词典上是否大于另一个给定字符串

> 原文:[https://www . geeksforgeeks . org/检查给定字符串的任何排列在词典上是否大于其他给定字符串/](https://www.geeksforgeeks.org/check-if-any-permutation-of-a-given-string-is-lexicographically-larger-than-the-other-given-string/)

给定两个相同长度的字符串 **str1** 和**str 2****N**，任务是检查在任何给定的字符串中是否存在任何可能的排列，使得一个字符串的每个字符在相应的索引处大于或等于另一个字符串的每个字符。如果存在置换，则返回 true，否则返回 false。

**示例:**

> **输入:**str 1 =“ADB”，str2 =“CDA”
> **输出:**真
> **解释:**在置换 str 1 =“Abd”和 str 2 =“ACD”之后，所以 str 2 中的每个字符都大于或等于 s1 中的每个字符。
> 
> **输入:**str 1 =“gfg”，str 2 =“AGD”
> T3】输出:真

**方法:**上述问题可以通过对两个字符串进行排序，然后按字典顺序进行比较来解决。
按照以下步骤了解如何:

*   [将给定字符串转换为字符数组](https://www.geeksforgeeks.org/convert-a-string-to-character-array-in-java/)
*   [对两个字符数组进行排序](https://www.geeksforgeeks.org/bubble-sort/)
*   [现在，遍历这些数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，检查一个数组中的每个字符是否大于或等于另一个数组中的相应字符
*   如果发现词典较大，打印为真，否则为假。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <algorithm>
#include <iostream>
#include <string>
using namespace std;
bool checkGreaterOrNot(string str1,
                       string str2)
{
    // Sorting both strings
    sort(str1.begin(), str1.end());
    sort(str2.begin(), str2.end());

    // Checking if any string
      //is greater or not
    bool flag = true;

    for (int i = 0; i < str1.length(); i++) {
        if (str1[i] < str2[i]) {
            flag = false;
            break;
        }
    }

    // If str1 is greater returning true
    if (flag)
        return true;

    flag = true;
    for(int i = 0; i < str2.length(); i++){
        if (str1[i] > str2[i]) {
            return false;
        }
    }

    // If str2 is greater returning true
    return true;
}
int main()
{
    string str1 = "adb";
    string str2 = "cda";
    bool ans =
      checkGreaterOrNot(str1, str2);
    if (ans) {
        cout << "true";
    }
    else {
        cout << "false";
    }
    return 0;
}

// This code is contributed by Kdheeraj.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;
import java.util.*;

class GFG {
    public static boolean
    checkGreaterOrNot(String str1,
                      String str2)
    {
        // Sorting strings
        char[] arr1 = str1.toCharArray();
        Arrays.sort(arr1);
        char[] arr2 = str2.toCharArray();
        Arrays.sort(arr2);
        boolean flag = true;

        // str1 is greater
        // if it does not break the loop
        for (int i = 0; i < arr1.length; i++) {
            if (arr1[i] < arr2[i]) {
                flag = false;
                break;
            }
        }

        // If str1 is greater returning true
        if (flag)
            return true;
        flag = true;

        // If characters of str1 is greater
        // then none of the strings have all
        // corresponding characters greater
        // so return false
        for (int i = 0; i < arr2.length; i++) {
            if (arr1[i] > arr2[i]) {
                return false;
            }
        }

        // If str2 is greater returning true
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "adb";
        String str2 = "cda";
        boolean ans = checkGreaterOrNot(str1, str2);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach
def checkGreaterOrNot(str1, str2):

    # Sorting both strings
    str1  = sorted(str1)
    str1 = "".join(str1)
    str2  = sorted(str2)
    str2 = "".join(str2)

    # Checking if any string
      #is greater or not
    flag = True

    for i in range(len(str1)):
        if(str1[i] < str2[i]):
            flag = False
            break

    # If str1 is greater returning true
    if (flag):
        return True
    flag = True
    for i in range(len(str2)):
        if (str1[i] > str2[i]):
            return False

    # If str2 is greater returning true
    return True

  # Driver code
if __name__ == '__main__':
    str1 = "adb"
    str2 = "cda"
    ans = checkGreaterOrNot(str1, str2)
    if (ans):
        print("true")
    else:
        print("false")

        # This code is contributed by ipg2016107.
```

## C#

```
// C# implementation for the above approach
using System;

class GFG {
    public static bool checkGreaterOrNot(string str1,
                                         string str2)
    {
        // Sorting strings
        char[] arr1 = str1.ToCharArray();
        Array.Sort(arr1);
        char[] arr2 = str2.ToCharArray();
        Array.Sort(arr2);
        bool flag = true;

        // str1 is greater
        // if it does not break the loop
        for (int i = 0; i < arr1.Length; i++) {
            if (arr1[i] < arr2[i]) {
                flag = false;
                break;
            }
        }

        // If str1 is greater returning true
        if (flag)
            return true;
        flag = true;

        // If characters of str1 is greater
        // then none of the strings have all
        // corresponding characters greater
        // so return false
        for (int i = 0; i < arr2.Length; i++) {
            if (arr1[i] > arr2[i]) {
                return false;
            }
        }

        // If str2 is greater returning true
        return true;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string str1 = "adb";
        string str2 = "cda";
        bool ans = checkGreaterOrNot(str1, str2);
        Console.WriteLine(ans);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       function checkGreaterOrNot(str1,
           str2)
       {

           // Sorting both strings
           str1.sort(function (a, b) { return a.charCodeAt(0) - b.charCodeAt(0); });
           str2.sort(function (a, b) { return a.charCodeAt(0) - b.charCodeAt(0); });

           // Checking if any string
           //is greater or not
           let flag = true;

           for (let i = 0; i < str1.length; i++) {
               if (str1[i].charCodeAt(0) > str2[i].charCodeAt(0)) {
                   flag = false;
                   break;
               }
           }

           // If str1 is greater returning true
           if (flag)
               return true;

           flag = true;
           for (let i = 0; i < str2.length; i++) {
               if (str1[i].charCodeAt(0) > str2[i].charCodeAt(0)) {
                   return false;
               }
           }

           // If str2 is greater returning true
           return true;
       }

       let str1 = ['a', 'd', 'b'];
       let str2 = ['c', 'd', 'a']
       let ans =
           checkGreaterOrNot(str1, str2);
       if (ans) {
           document.write("true");
       }
       else {
           document.write("false");
       }

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
true
```

**时间复杂度:**O(n * log n)
T3】辅助空间: O(n)

**方法 2:** 上述方法可以使用给定字符串的频率图进行优化。

*   为两个给定的字符串制作频率图
*   创建变量**计数 1** 和**计数 2** 以指示各个字符串的累计频率
*   遍历频率图，检查任何字符串的值是否大于另一个。
*   如果是，则打印 true。否则打印为假。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <iostream>
#include <string>
using namespace std;
bool checkGreaterOrNot(string str1,
                       string str2)
{
    int arr1[26] = { 0 };
    int arr2[26] = { 0 };

    // Making frequency map for both strings
    for (int i = 0;
         i < str1.length(); i++) {
        arr1[str1[i] - 'a']++;
    }
    for (int i = 0;
         i < str2.length(); i++) {
        arr1[str2[i] - 'a']++;
    }

    // To check if any array
    // is greater to the other or not
    bool str1IsSmaller = false,
          str2IsSmaller = false;

    int count1 = 0, count2 = 0;
    for (int i = 0; i < 26; i++) {
        count1 += arr1[i];
        count2 += arr2[i];

        if (count1 > count2) {

         // None of the strings have
         // all corresponding characters
         // greater than other string
            if (str2IsSmaller)
                return false;

            str1IsSmaller = true;
        }

        if (count1 < count2) {

         // None of the strings have
         // all corresponding characters
         // greater than other string
            if (str1IsSmaller)
                return false;

            str2IsSmaller = true;
        }
    }
    return true;
}

// Driver code
int main()
{
    string str1 = "geeks";
    string str2 = "peeks";
    bool ans =
      checkGreaterOrNot(str1, str2);
    if (ans) {
        cout << "true";
    }
    else {
        cout << "false";
    }
}

// This code is contributed by Kdheeraj.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG {

    public static boolean checkGreaterOrNot(
        String str1, String str2)
    {
        int[] freq1 = new int[26];
        int[] freq2 = new int[26];

        // Making frequency map
        // for both strings
        for (int i = 0;
             i < str1.length(); i++) {

            freq1[str1.charAt(i) - 'a']++;
        }

        for (int i = 0;
             i < str2.length(); i++) {
            freq2[str2.charAt(i) - 'a']++;
        }

        boolean str1IsSmaller = false;
        boolean str2IsSmaller = false;
        int count1 = 0, count2 = 0;

        // Checking if any array
        // is strictly increasing or not
        for (int i = 0; i < 26; i++) {

            count1 += freq1[i];
            count2 += freq2[i];
            if (count1 > count2) {

                // None of the strings have
                // all corresponding characters
                // greater than other string
                if (str2IsSmaller)
                    return false;

                str1IsSmaller = true;
            }
            else if (count2 > count1) {

                // None of the strings have
                // all corresponding characters
                // greater than other string
                if (str1IsSmaller)
                    return false;

                str2IsSmaller = true;
            }
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "geeks";
        String str2 = "peeks";
        boolean ans = checkGreaterOrNot(str1, str2);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# python implementation for the above approach
def checkGreaterOrNot(str1, str2):
    arr1 = [0 for x in range(26)]
    arr2 = [0 for x in range(26)]

    # Making frequency map for both strings
    for val in str1:
        arr1[ord(val)-97] += 1
    for val in str2:
        arr1[ord(val)-97] += 1

    # To check if any array
    # is greater to the other or not
    str1IsSmaller = False
    str2IsSmaller = False

    count1 = 0
    count2 = 0
    for i in range(0, 26):
        count1 += arr1[i]
        count2 += arr2[i]
        if (count1 > count2):

            #  None of the strings have
            #  all corresponding characters
            #  greater than other string
            if str2IsSmaller == True:
                return False
            str1IsSmaller = True

        if (count1 < count2):

            #  None of the strings have
            # all corresponding characters
            # greater than other string
            if str1IsSmaller == True:
                return False
            str2IsSmaller = True
    return True

# Driver code
str1 = "geeks"
str2 = "peeks"
ans = checkGreaterOrNot(str1, str2)
if ans == True:
    print("true")
else:
    print("false")

    # This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    public static bool checkGreaterOrNot(
        string str1, string str2)
    {
        int[] freq1 = new int[26];
        int[] freq2 = new int[26];

        // Making frequency map
        // for both strings
        for (int i = 0;
             i < str1.Length; i++) {

            freq1[str1[(i)] - 'a']++;
        }

        for (int i = 0;
             i < str2.Length; i++) {
            freq2[str2[(i)] - 'a']++;
        }

        bool str1IsSmaller = false;
        bool str2IsSmaller = false;
        int count1 = 0, count2 = 0;

        // Checking if any array
        // is strictly increasing or not
        for (int i = 0; i < 26; i++) {

            count1 += freq1[i];
            count2 += freq2[i];
            if (count1 > count2) {

                // None of the strings have
                // all corresponding characters
                // greater than other string
                if (str2IsSmaller)
                    return false;

                str1IsSmaller = true;
            }
            else if (count2 > count1) {

                // None of the strings have
                // all corresponding characters
                // greater than other string
                if (str1IsSmaller)
                    return false;

                str2IsSmaller = true;
            }
        }
        return true;
    }

    // Driver Code
    public static void Main()
    {
        string str1 = "geeks";
        string str2 = "peeks";
        bool ans = checkGreaterOrNot(str1, str2);
        Console.WriteLine(ans);
    }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>

// Javascript implementation for the above approach

function checkGreaterOrNot(str1, str2)
{
    var arr1 = Array(26).fill(0);
    var arr2 = Array(26).fill(0);

    // Making frequency map for both strings
    for (var i = 0;
         i < str1.length; i++) {
        arr1[str1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }
    for (var i = 0;
         i < str2.length; i++) {
        arr1[str2[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    // To check if any array
    // is greater to the other or not
    var str1IsSmaller = false,
          str2IsSmaller = false;

    var count1 = 0, count2 = 0;
    for (var i = 0; i < 26; i++) {
        count1 += arr1[i];
        count2 += arr2[i];

        if (count1 > count2) {

         // None of the strings have
         // all corresponding characters
         // greater than other string
            if (str2IsSmaller)
                return false;

            str1IsSmaller = true;
        }

        if (count1 < count2) {

         // None of the strings have
         // all corresponding characters
         // greater than other string
            if (str1IsSmaller)
                return false;

            str2IsSmaller = true;
        }
    }
    return true;
}

// Driver code
var str1 = "geeks";
var str2 = "peeks";
var ans =
  checkGreaterOrNot(str1, str2);
if (ans) {
    document.write("true");
}
else {
    document.write("false");
}

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
true
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)