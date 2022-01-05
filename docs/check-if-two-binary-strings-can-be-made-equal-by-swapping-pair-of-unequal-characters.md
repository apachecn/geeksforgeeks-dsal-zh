# 通过交换不相等的字符对

检查两个二进制字符串是否可以相等

> 原文:[https://www . geesforgeks . org/check-if-two-binary-strings-可以通过交换一对不相等的字符来使其相等/](https://www.geeksforgeeks.org/check-if-two-binary-strings-can-be-made-equal-by-swapping-pair-of-unequal-characters/)

给定两个长度为**N**(*1≤N≤10<sup>5</sup>*)的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)**【S1】**和 **S2** ，任务是通过执行以下任意次数的操作来检查是否有可能将字符串 **S1** 转换为
**S2** :

1.  选择任意两个指数 **i** 和 **j** ( *1 ≤ i < j ≤ N* )使得**S1【I】**为**“0”****S1【j】**为**“1”**。
2.  将**S1【I】**换成**S1【j】**。

**示例:**

> **输入:**S1 =“100111”，S2 =“111010”
> **输出**:是
> **说明:**分别用 S[4]和 S[6]交换 S[2]和 S[3]。
> 
> **输入:**S1 =“110100”，S2 =“010101”
> T3】输出:否

**方法:**按照以下步骤解决问题:

1.  检查两个字符串中字符**“0”**和**“1”**的出现次数是否相等。如果没有发现是真的，那么就不可能把弦 **S1** 变换成 **S2** 。
2.  如果字符数相等，那么我们进入下一步。在给定的条件下，通过与字符串 **S1** 中的字母“1”交换，可以仅在**向前方向**移动“0”。
3.  因此，迭代两个字符串的字符，并计算两个字符串中**‘0’**的出现次数。如果在任何时候字符串 **S2** 中的字符数“0”严格大于字符串 **S1** 中的字符数，则终止循环并打印**“否”**。
4.  如果两个字符串迭代成功，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// s1 can be converted into s2
void check(string s1, string s2)
{
    // Count of '0' in strings in s1 and s2
    int s1_0 = 0, s2_0 = 0;

    // Iterate both the strings and
    // count the number of occurrences of
    for (int i = 0; i < s1.size(); i++) {

        if (s1[i] == '0') {
            s1_0++;
        }

        if (s2[i] == '0') {
            s2_0++;
        }
    }

    // Count is not equal
    if (s1_0 != s2_0) {
        cout << "NO" << endl;
        return;
    }

    else {

        int Count1 = 0, Count2 = 0;

        // Iterating over both the
        // arrays and count the
        // number of occurrences of '0'
        for (int i = 0; i < s1.size(); i++) {

            if (s1[i] == '0') {
                Count1++;
            }

            if (s2[i] == '0') {
                Count2++;
            }

            // If the count of occurrences
            // of '0' in S2 exceeds that in S1
            if (Count1 < Count2) {
                cout << "NO" << endl;
                return;
            }
        }

        cout << "YES" << endl;
    }
}

// Driver program
int main()
{

    string s1 = "100111";
    string s2 = "111010";
    check(s1, s2);

    s1 = "110100";
    s2 = "010101";
    check(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to check if a string
// s1 can be converted into s2
static void check(String s1, String s2)
{

    // Count of '0' in strings in s1 and s2
    int s1_0 = 0, s2_0 = 0;

    // Iterate both the strings and
    // count the number of occurrences of
    for(int i = 0; i < s1.length(); i++)
    {
        if (s1.charAt(i) == '0')
        {
            s1_0++;
        }

        if (s2.charAt(i) == '0')
        {
            s2_0++;
        }
    }

    // Count is not equal
    if (s1_0 != s2_0)
    {
        System.out.println("NO");
        return;
    }

    else
    {
        int Count1 = 0, Count2 = 0;

        // Iterating over both the
        // arrays and count the
        // number of occurrences of '0'
        for(int i = 0; i < s1.length(); i++)
        {
            if (s1.charAt(i) == '0')
            {
                Count1++;
            }

            if (s2.charAt(i) == '0')
            {
                Count2++;
            }

            // If the count of occurrences
            // of '0' in S2 exceeds that in S1
            if (Count1 < Count2)
            {
                System.out.println("NO");
                return;
            }
        }
        System.out.println("YES");
    }
}

// Driver Code
public static void main(String[] args)
{
    String s1 = "100111";
    String s2 = "111010";    
    check(s1, s2);
    s1 = "110100";
    s2 = "010101";
    check(s1, s2);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program to implement
# of above approach

# Function to check if a string
# s1 can be converted into s2
def check(s1, s2):

    # Count of '0' in strings in s1 and s2
    s1_0 = 0
    s2_0 = 0

    # Iterate both the strings and
    # count the number of occurrences of
    for i in range(len(s1)):
        if (s1[i] == '0'):
            s1_0 += 1

        if (s2[i] == '0'):
            s2_0 += 1

    # Count is not equal
    if (s1_0 != s2_0):
        print("NO")
        return

    else:
        Count1 = 0
        Count2 = 0;

        # Iterating over both the
        # arrays and count the
        # number of occurrences of '0'
        for i in range(len(s1)):
            if (s1[i] == '0'):
                Count1 += 1

            if (s2[i] == '0'):
                Count2 += 1

            # If the count of occurrences
            # of '0' in S2 exceeds that in S1
            if (Count1 < Count2):
                print("NO")
                return

        print("YES")

# Driver code
if __name__ == "__main__":

    s1 = "100111"
    s2 = "111010"
    check(s1, s2)

    s1 = "110100"
    s2 = "010101"
    check(s1, s2)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// of above approach
using System;

class GFG{

// Function to check if a string
// s1 can be converted into s2
static void check(string s1, string s2)
{

    // Count of '0' in strings in s1 and s2
    int s1_0 = 0, s2_0 = 0;

    // Iterate both the strings and
    // count the number of occurrences of
    for(int i = 0; i < s1.Length; i++)
    {
        if (s1[i] == '0')
        {
            s1_0++;
        }

        if (s2[i] == '0')
        {
            s2_0++;
        }
    }

    // Count is not equal
    if (s1_0 != s2_0)
    {
        Console.WriteLine("NO");
        return;
    }

    else
    {
        int Count1 = 0, Count2 = 0;

        // Iterating over both the
        // arrays and count the
        // number of occurrences of '0'
        for(int i = 0; i < s1.Length; i++)
        {
            if (s1[i] == '0')
            {
                Count1++;
            }

            if (s2[i] == '0')
            {
                Count2++;
            }

            // If the count of occurrences
            // of '0' in S2 exceeds that in S1
            if (Count1 < Count2)
            {
                Console.WriteLine("NO");
                return;
            }
        }
        Console.WriteLine("YES");
    }
}

// Driver code
static void Main()
{
    string s1 = "100111";
    string s2 = "111010";

    check(s1, s2);

    s1 = "110100";
    s2 = "010101";

    check(s1, s2);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to implement of above approach

    // Function to check if a string
    // s1 can be converted into s2
    function check(s1, s2)
    {

        // Count of '0' in strings in s1 and s2
        let s1_0 = 0, s2_0 = 0;

        // Iterate both the strings and
        // count the number of occurrences of
        for(let i = 0; i < s1.length; i++)
        {
            if (s1[i] == '0')
            {
                s1_0++;
            }

            if (s2[i] == '0')
            {
                s2_0++;
            }
        }

        // Count is not equal
        if (s1_0 != s2_0)
        {
            document.write("NO");
            return;
        }

        else
        {
            let Count1 = 0, Count2 = 0;

            // Iterating over both the
            // arrays and count the
            // number of occurrences of '0'
            for(let i = 0; i < s1.length; i++)
            {
                if (s1[i] == '0')
                {
                    Count1++;
                }

                if (s2[i] == '0')
                {
                    Count2++;
                }

                // If the count of occurrences
                // of '0' in S2 exceeds that in S1
                if (Count1 < Count2)
                {
                    document.write("NO" + "</br>");
                    return;
                }
            }
            document.write("YES" + "</br>");
        }
    }

    let s1 = "100111";
    let s2 = "111010";

    check(s1, s2);

    s1 = "110100";
    s2 = "010101";

    check(s1, s2);

  // This code is contributed by decode 2207.
</script>
```

**Output:** 

```
YES
NO
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(1)