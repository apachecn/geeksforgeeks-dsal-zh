# 计算最小交换以生成字符串回文

> 原文:[https://www . geesforgeks . org/count-minimum-swap-make-string-回文/](https://www.geeksforgeeks.org/count-minimum-swap-to-make-string-palindrome/)

给定一个字符串 **s** ，任务是找出使字符串 **s** 回文所需的相邻交换的最小数量。如果不可能，则返回 **-1** 。

**示例:**

> **输入:**aabcb
> T3】输出: 3
> **解释:**
> 第一次交换后:abacb
> 第二次交换后:abcab
> 第三次交换后:abcba
> 
> **输入:** adbcdbad
> **输出:** -1

**走近**
下面是解决这个问题的详细步骤。

1.  取双指针，其中第一个指针从字符串的左侧跟踪，第二个指针从字符串的右侧跟踪。
2.  直到我们找到相同的字符，继续将右指针向左移动一步。
3.  如果没有找到相同的字符，则返回-1。
4.  如果找到相同的字符，则向右交换右指针的字符，直到它没有放在字符串中的正确位置。
5.  增加左指针并重复步骤 2。

下面是上述方法的实现:

## C++

```
// C++ program to Count
// minimum swap to make
// string palindrome
#include <bits/stdc++.h>
using namespace std;

// Function to Count minimum swap
int countSwap(string s)
{
    // calculate length of string as n
    int n = s.length();

    // counter to count minimum swap
    int count = 0;

    // A loop which run till mid of
    // string
    for (int i = 0; i < n / 2; i++) {
        // Left pointer
        int left = i;

        // Right pointer
        int right = n - left - 1;

        // A loop which run from right
        // pointer towards left pointer
        while (left < right) {
            // if both char same then
            // break the loop.
            // If not, then we have to
            // move right pointer to one
            // position left
            if (s[left] == s[right]) {
                break;
            }
            else {
                right--;
            }
        }

        // If both pointers are at same
        // position, it denotes that we
        // don't have sufficient characters
        // to make palindrome string
        if (left == right) {
            return -1;
        }

        // else swap and increase the count
        for (int j = right; j < n - left - 1; j++) {
            swap(s[j], s[j + 1]);
            count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    string s = "geeksfgeeks";

    // Function calling
    int ans1 = countSwap(s);

    reverse(s.begin(), s.end());
    int ans2 = countSwap(s);

    cout << max(ans1, ans2);

    return 0;
}
```

## 蟒蛇 3

```
''' Python3 program to Count 
    minimum swap to make
    string palindrome'''

# Function to Count minimum swap

def CountSwap(s, n):
    s = list(s)

    # Counter to count minimum swap
    count = 0
    ans = True

    # A loop which run in half string
    # from starting
    for i in range(n // 2):

        # Left pointer
        left = i

        # Right pointer
        right = n - left - 1

        # A loop which run from right pointer
        # to left pointer
        while left < right:

            # if both char same then
            # break the loop if not
            # same then we have to move
            # right pointer to one step left
            if s[left] == s[right]:
                break
            else:
                right -= 1

        # it denotes both pointer at
        # same position and we don't
        # have sufficient char to make
        # palindrome string
        if left == right:
            ans = False
            break
        else:
            for j in range(right, n - left - 1):
                (s[j], s[j + 1]) = (s[j + 1], s[j])
                count += 1
    if ans:
        return (count)
    else:
        return -1

# Driver Code
s = 'geeksfgeeks'

# Length of string
n = len(s)

# Function calling
ans1 = CountSwap(s, n)
ans2 = CountSwap(s[::-1], n)
print(max(ans1, ans2))
```

## C#

```
// C# program to Count
// minimum swap to make
// string palindrome
using System;

class GFG {

    // Function to Count minimum swap
    static int countSwap(String str)
    {

        // Length of string
        int n = str.Length;

        // it will convert string to
        // char array
        char[] s = str.ToCharArray();

        // Counter to count minimum
        // swap
        int count = 0;

        // A loop which run in half
        // string from starting
        for (int i = 0; i < n / 2; i++) {

            // Left pointer
            int left = i;

            // Right pointer
            int right = n - left - 1;

            // A loop which run from
            // right pointer to left
            // pointer
            while (left < right) {

                // if both char same
                // then break the loop
                // if not same then we
                // have to move right
                // pointer to one step
                // left
                if (s[left] == s[right]) {
                    break;
                }
                else {
                    right--;
                }
            }

            // it denotes both pointer at
            // same position and we don't
            // have sufficient char to make
            // palindrome string
            if (left == right) {
                return -1;
            }
            else {
                for (int j = right; j < n - left - 1; j++) {
                    char t = s[j];
                    s[j] = s[j + 1];
                    s[j + 1] = t;
                    count++;
                }
            }
        }

        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "geeksfgeeks";

        // Function calling
        int ans1 = countSwap(s);

        char[] charArray = s.ToCharArray();
        Array.Reverse(charArray);
        s = new string(charArray);

        int ans2 = countSwap(s);

        if (ans1 > ans2)
            Console.WriteLine(ans1);
        else
            Console.WriteLine(ans2);
    }
}

// This code is contributed by sapnasingh4991
```

**Output**

```
9
```

**复杂度分析**
**时间复杂度:**由于我们在字符串长度上运行两个嵌套循环，时间复杂度为 **O(n <sup>2</sup> )**
**辅助空间:**由于我们没有使用任何额外的空间，因此使用的辅助空间为 **O(1)**