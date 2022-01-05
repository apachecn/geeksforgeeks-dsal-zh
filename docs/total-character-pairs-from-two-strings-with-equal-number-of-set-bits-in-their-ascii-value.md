# 两个字符串中的全部字符对，其 ascii 值中的设置位数量相等

> 原文:[https://www . geeksforgeeks . org/总字符对-从两个字符串开始-在它们的 ascii 值中具有相等的集合位数/](https://www.geeksforgeeks.org/total-character-pairs-from-two-strings-with-equal-number-of-set-bits-in-their-ascii-value/)

给定两根弦 **s1** 和 **s2** 。任务是从第一个字符串中提取一个字符，从第二个字符串中提取一个字符，并检查这两个字符的 ASCII 值是否具有相同的设置位数。打印此类对的总数。

**示例:**

> **输入:**S1 =“xcd”，S2 =“swa”
> **输出:** 1
> 唯一有效的对是(d，a)，ASCII 值分别为 100 和 97。
> 两者均包含 3 个置位位。
> **输入:** s1 =“极客”，s2 =“伪造者”
> **输出:** 17

**进场:**

*   制作大小为 6 的两个数组 arr1 和 arr2，并将所有值初始化为 0，以存储设置位数的频率。因为小写字母的最大设置位数是 6。
*   遍历字符串 s1，找到每个字符的 ASCII 值。将每个 ASCII 值的设置位数的频率存储在数组 arr1 中。(例如，如果有 3 个字符有 4 个设置位，则在 arr[4]处存储 3)
*   对字符串 s2 执行类似的操作，并将其值存储在另一个数组 arr2 中。
*   用 0 初始化计数变量。
*   对于总对数，继续在计数变量中为 I 的所有有效值添加(arr1[i] * arr2[i])。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of valid pairs
int totalPairs(string s1, string s2)
{
    int count = 0;

    int arr1[7], arr2[7];

    // Initialise both arrays with 0
    for (int i = 1; i <= 6; i++) {
        arr1[i] = 0;
        arr2[i] = 0;
    }

    // Store frequency of number of set bits for s1
    for (int i = 0; i < s1.length(); i++) {
        int set_bits = __builtin_popcount((int)s1[i]);
        arr1[set_bits]++;
    }

    // Store frequency of number of set bits for s2
    for (int i = 0; i < s2.length(); i++) {
        int set_bits = __builtin_popcount((int)s2[i]);
        arr2[set_bits]++;
    }

    // Calculate total pairs
    for (int i = 1; i <= 6; i++)
        count += (arr1[i] * arr2[i]);

    // Return the count of valid pairs
    return count;
}

// Driver code
int main()
{
    string s1 = "geeks";
    string s2 = "forgeeks";
    cout << totalPairs(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count of valid pairs
    static int totalPairs(String s1, String s2)
    {
        int count = 0;

        int[] arr1 = new int[7];
        int[] arr2 = new int[7];

        // Default Initialise both arrays 0
        // Store frequency of number of set bits for s1
        for (int i = 0; i < s1.length(); i++)
        {
            int set_bits = Integer.bitCount(s1.charAt(i));
            arr1[set_bits]++;
        }

        // Store frequency of number of set bits for s2
        for (int i = 0; i < s2.length(); i++)
        {
            int set_bits = Integer.bitCount(s2.charAt(i));
            arr2[set_bits]++;
        }

        // Calculate total pairs
        for (int i = 1; i <= 6; i++)
        {
            count += (arr1[i] * arr2[i]);
        }

        // Return the count of valid pairs
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {

        String s1 = "geeks";
        String s2 = "forgeeks";
        System.out.println(totalPairs(s1, s2));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to get no of set bits in binary
# representation of positive integer n
def countSetBits(n):
    count = 0
    while (n):
        count += n & 1
        n >>= 1
    return count

# Function to return the count
# of valid pairs
def totalPairs(s1, s2) :

    count = 0;

    arr1 = [0] * 7; arr2 = [0] * 7;

    # Store frequency of number
    # of set bits for s1
    for i in range(len(s1)) :
        set_bits = countSetBits(ord(s1[i]))
        arr1[set_bits] += 1;

    # Store frequency of number of
    # set bits for s2
    for i in range(len(s2)) :
        set_bits = countSetBits(ord(s2[i]));
        arr2[set_bits] += 1;

    # Calculate total pairs
    for i in range(1, 7) :
        count += (arr1[i] * arr2[i]);

    # Return the count of valid pairs
    return count;

# Driver code
if __name__ == "__main__" :

    s1 = "geeks";
    s2 = "forgeeks";
    print(totalPairs(s1, s2));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to return the count of valid pairs
static int totalPairs(string s1, string s2)
{
    int count = 0;

    int[] arr1 = new int[7];
    int[] arr2 = new int[7];

    // Default Initialise both arrays 0

    // Store frequency of number of set bits for s1
    for (int i = 0; i < s1.Length; i++)
    {
        int set_bits = Convert.ToString((int)s1[i], 2).Count(c => c == '1');
        arr1[set_bits]++;
    }

    // Store frequency of number of set bits for s2
    for (int i = 0; i < s2.Length; i++)
    {
        int set_bits = Convert.ToString((int)s2[i], 2).Count(c => c == '1');
        arr2[set_bits]++;
    }

    // Calculate total pairs
    for (int i = 1; i <= 6; i++)
        count += (arr1[i] * arr2[i]);

    // Return the count of valid pairs
    return count;
}

// Driver code
static void Main()
{
    string s1 = "geeks";
    string s2 = "forgeeks";
    Console.WriteLine(totalPairs(s1, s2));
}
}

// This code is contributed by chandan_jnu
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to get no of set bits in binary
      // representation of positive integer n
      function countSetBits(n) {
        var count = 0;
        while (n) {
          count += n & 1;
          n >>= 1;
        }
        return count;
      }

      // Function to return the count
      // of valid pairs
      function totalPairs(s1, s2) {
        var count = 0;

        var arr1 = new Array(7).fill(0);
        var arr2 = new Array(7).fill(0);

        // Store frequency of number
        // of set bits for s1
        for (let i = 0; i < s1.length; i++) {
          set_bits = countSetBits(s1[i].charCodeAt(0));
          arr1[set_bits] += 1;
        }
        // Store frequency of number of
        // set bits for s2
        for (let i = 0; i < s2.length; i++) {
          set_bits = countSetBits(s2[i].charCodeAt(0));
          arr2[set_bits] += 1;
        }
        // Calculate total pairs
        for (let i = 1; i < 7; i++) {
          count += arr1[i] * arr2[i];
        }

        // Return the count of valid pairs
        return count;
      }
      // Driver code
      var s1 = "geeks";
      var s2 = "forgeeks";
      document.write(totalPairs(s1, s2));
    </script>
```

**Output:** 

```
17
```