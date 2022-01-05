# 检查重新排列数组元素是否能形成回文

> 原文:[https://www . geesforgeks . org/check-if-重排-array-elements-can-form-a-回文-or-not/](https://www.geeksforgeeks.org/check-if-rearranging-array-elements-can-form-a-palindrome-or-not/)

给定一个大小为 **N** 的正整数数组 **arr** ，任务是检查数组元素的任何排列所形成的数字是否形成回文。

**示例:**

> **输入:** arr = [1，2，3，1，2]
> **输出:** Yes
> **说明:**给定数组的元素可以重新排列为 1，2，3，2，1。
> 由于 12321 是回文，所以输出会是“是”
> 
> **输入:** arr = [1，2，3，4，1]
> **输出:** No
> **解释:**给定数组的元素不能在所有可能的排列中重新排列形成回文。所以输出将是“否”

**方式:**给定的问题可以使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储[阵元频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)来解决

*   存储所有数组元素的频率
*   检查每个元素的频率是否均匀
*   对于频率为奇数的元素，如果只有一个这样的元素，则打印“是”。否则打印号。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAX 256

// Function to check whether elements of
// an array can form a palindrome
bool can_form_palindrome(int arr[], int n)
{
    // create an empty string
    // to append elements of an array
    string str = "";

    // append each element to the string str to form
    // a string so that we can solve it in easy way
    for (int i = 0; i < n; i++) {
        str += arr[i];
    }

    // Create a freq array and initialize all
    // values as 0
    int freq[MAX] = { 0 };

    // For each character in formed string,
    // increment freq in the corresponding
    // freq array
    for (int i = 0; str[i]; i++) {
        freq[str[i]]++;
    }
    int count = 0;

    // Count odd occurring characters
    for (int i = 0; i < MAX; i++) {
        if (freq[i] & 1) {
            count++;
        }
        if (count > 1) {
            return false;
        }
    }

    // Return true if odd count is 0 or 1,
    return true;
}
// Drive code
int main()
{
    int arr[] = { 1, 2, 3, 1, 2 };
    int n = sizeof(arr) / sizeof(int);
    can_form_palindrome(arr, n)
        ? cout << "YES"
        : cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

  static int MAX = 256;

  // Function to check whether elements of
  // an array can form a palindrome
  static boolean can_form_palindrome(int []arr, int n)
  {

    // create an empty string
    // to append elements of an array
    String str = "";

    // append each element to the string str to form
    // a string so that we can solve it in easy way
    for (int i = 0; i < n; i++) {
      str += arr[i];
    }

    // Create a freq array and initialize all
    // values as 0
    int freq[] = new int[MAX];
    Arrays.fill(freq,0);

    // For each character in formed string,
    // increment freq in the corresponding
    // freq array
    for (int i = 0; i<str.length(); i++) {
      freq[str.charAt(i)]++;
    }
    int count = 0;

    // Count odd occurring characters
    for (int i = 0; i < MAX; i++) {
      if ((freq[i] & 1)!=0) {
        count++;
      }
      if (count > 1) {
        return false;
      }
    }

    // Return true if odd count is 0 or 1,
    return true;
  }

  // Drive code
  public static void main (String[] args)
  {
    int []arr = { 1, 2, 3, 1, 2 };
    int n = arr.length;
    if(can_form_palindrome(arr, n))
      System.out.println("YES");
    else
      System.out.println("NO");
  }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python implementation of the above approach

# Function to check whether elements of
# an array can form a palindrome
def can_form_palindrome(arr, n):
    MAX = 256
    # create an empty string
    # to append elements of an array
    s = ""

    # append each element to the string str to form
    # a string so that we can solve it in easy way
    for i in range(n) :
        s = s + str(arr[i])

    # Create a freq array and initialize all
    # values as 0
    freq = [0]*MAX

    # For each character in formed string,
    # increment freq in the corresponding
    # freq array
    for i in range(N) :
        freq[arr[i]]=freq[arr[i]]+1

    count = 0

    # Count odd occurring characters
    for i in range(MAX) :
        if (freq[i] & 1) :
            count=count+1
        if (count > 1) :
            return False

    # Return true if odd count is 0 or 1,
    return True

# Driver Code
if __name__ ==  "__main__":
    arr = [ 1, 2, 3, 1, 2 ]
    N = len(arr)

    # Function Call
    if(can_form_palindrome(arr, N)):
        print("YES")
    else:
        print("NO")

 # This code is contributed by anudeep23042002
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG{

static int MAX = 256;

// Function to check whether elements of
// an array can form a palindrome
static bool can_form_palindrome(int []arr, int n)
{
    // create an empty string
    // to append elements of an array
    string str = "";

    // append each element to the string str to form
    // a string so that we can solve it in easy way
    for (int i = 0; i < n; i++) {
        str += arr[i];
    }

    // Create a freq array and initialize all
    // values as 0
    int []freq = new int[MAX];
    Array.Clear(freq,0,MAX);

    // For each character in formed string,
    // increment freq in the corresponding
    // freq array
    for (int i = 0; i<str.Length; i++) {
         freq[str[i]]++;
    }
    int count = 0;

    // Count odd occurring characters
    for (int i = 0; i < MAX; i++) {
        if ((freq[i] & 1)!=0) {
            count++;
        }
        if (count > 1) {
            return false;
        }
    }

    // Return true if odd count is 0 or 1,
    return true;
}

// Drive code
public static void Main()
{
    int []arr = { 1, 2, 3, 1, 2 };
    int n = arr.Length;
    if(can_form_palindrome(arr, n))
       Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        let MAX = 256

        // Function to check whether elements of
        // an array can form a palindrome
        function can_form_palindrome(arr, n)
        {

            // create an empty string
            // to append elements of an array
            let str = "";

            // append each element to the string str to form
            // a string so that we can solve it in easy way
            for (let i = 0; i < n; i++) {
                str += toString(arr[i]);
            }

            // Create a freq array and initialize all
            // values as 0
            let freq = new Array(n).fill(0);

            // For each character in formed string,
            // increment freq in the corresponding
            // freq array
            for (let i = 0; i < str.length; i++) {
                freq[str.charCodeAt(i)]++;
            }
            let count = 0;

            // Count odd occurring characters
            for (let i = 0; i < MAX; i++) {
                if (freq[i] & 1) {
                    count++;
                }
                if (count > 1) {
                    return false;
                }
            }

            // Return true if odd count is 0 or 1,
            return true;
        }

        // Drive code
        let arr = [1, 2, 3, 1, 2];
        let n = arr.length;
        can_form_palindrome(arr, n)
            ? document.write("YES")
            : document.write("NO");

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
YES
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)