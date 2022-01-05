# 计算所有可以用给定数字的数字构成的素数

> 原文:[https://www . geeksforgeeks . org/count-all-prime-numbers-可以使用给定数字的数字来构成/](https://www.geeksforgeeks.org/count-all-prime-numbers-that-can-be-formed-using-digits-of-a-given-number/)

给定一个由 **N** 个数字组成的[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是找到不同的[个质数](https://www.geeksforgeeks.org/tag/prime-number/)的个数，这些质数可以用串 **S** 的数字组成。

**示例:**

> **输入:** S = "123"
> **输出:** 5
> **说明:**
> 可以由字符串 S 的数字组成的素数是 2、3、13、23 和 31。因此，总数是 5。
> 
> **输入:**S = " 1 "
> T3】输出: 0

**方法:**给定的问题可以通过使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)到[找到所有可能的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)并检查它们是否可以形成[素数](https://www.geeksforgeeks.org/tag/prime-number/)来解决。按照以下步骤解决问题:

*   [初始化一个 HashSet](https://www.geeksforgeeks.org/initializing-hashset-java/) **H** 来存储唯一的[质数](https://www.geeksforgeeks.org/tag/prime-number/) [字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)可能。
*   定义[功能](https://www.geeksforgeeks.org/function-interface-in-java-with-examples/) **检查(字符串编号)**检查**编号**是否为[质数](https://www.geeksforgeeks.org/tag/prime-number/)，并执行以下步骤:
    *   如果字符串**数字[]** 的长度为 **0、**，则返回**假**。
    *   使用[功能修剪](https://www.geeksforgeeks.org/java-string-trim-method-example/#:~:text=trim()is%20a%20built, and%20returns%20the%20omitted%20string.) 来修剪数字。
    *   初始化一个长变量 **num** ，并使用 [parseLong](https://www.geeksforgeeks.org/java-lang-long-class-in-java/) 函数将解析后的数字存储在其中。
    *   如果 **num** 等于 **1，**则返回 **false** 。
    *   如果 **num%2** 等于 **0** 且 **num** 不等于 **2、**，则返回 **false** 。
    *   如果 **num%3** 等于 **0** ， **num** 不等于 **3，**则返回 **false** 。
    *   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【6】，num<sup>1/2</sup>**，并执行以下步骤:
        *   如果 **num%(i-1)** 或 **num%(i+1)** 等于 **0，**则返回**假**。
    *   最后，返回**真**。
*   定义一个[函数](https://www.geeksforgeeks.org/function-interface-in-java-with-examples/) **DFS(int arr[]，string ans)** 来查找所有可能的素数，并执行以下步骤:
    *   调用[功能](https://www.geeksforgeeks.org/function-interface-in-java-with-examples/) **检查(ans)** ，如果[功能](https://www.geeksforgeeks.org/function-interface-in-java-with-examples/)返回**真，**则向 HashSet **H** 添加此字符串 **ans** 。
    *   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，10】**，并执行以下步骤:
        *   如果 **arr[i]** 等于 **0、**，则[继续迭代](https://www.geeksforgeeks.org/continue-statement-in-java/)。
        *   将 **i** 的值加到字符串**答案**中，并将**arr【I】**的值减少 **1** 。
        *   调用[函数](https://www.geeksforgeeks.org/function-interface-in-java-with-examples/) **DFS(arr，ans)** 寻找其他可能的答案[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)。
        *   从字符串**答案**中删除 **i** 的值，并通过 **1** 添加**arr【I】**的值。
*   [初始化一个大小为 **10** 的数组](https://www.geeksforgeeks.org/arrays-in-java/) **计数[]** ，以存储字符串 **S** 中每个数字的频率。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N】**，并执行以下步骤:
    *   将频率由 **1** 加到字符串 **S** 中第<sup>个</sup>索引的字符数组**计数【】**中。
*   调用函数 **DFS(count，“”**找到所有可能的素数。
*   执行上述步骤后，打印 HashSet **H** 的尺寸作为答案。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;
unordered_set<string> H;

// Function to check whether the
// number is prime or not
bool check(string number)
{
    if (number.length() == 0) {
        return false;
    }
    long num = stol(number);

    // Condition for prime number
    if (num == 1) {
        return false;
    }
    if (num % 2 == 0 && num != 2) {
        return false;
    }
    if (num % 3 == 0 && num != 3) {
        return false;
    }

    // Iterate over the range [6, num]
    for (int i = 6; i * i <= num; i += 6) {
        if (num % (i - 1) == 0 || num % (i + 1) == 0) {
            return false;
        }
    }

    // Otherwisem return true
    return true;
}

// Function to count the total number
// of prime numbers
void DFS(int arr[], string ans)
{
    // Add it in the HashSet
    if (check(ans)) {
        H.insert(ans);
    }

    for (int i = 0; i <= 9; ++i) {
        if (arr[i] == 0) {
            continue;
        }

        // Use the number
        ans = (ans + to_string(i));

        // Decrease the number
        arr[i]--;

        // Perform the DFS Call
        DFS(arr, ans);
        ans = ans.substr(0, ans.length() - 1);

        // Backtracking the frequency
        arr[i]++;
    }
}

// Driver Code
int main()
{
    string number = "123";
    int count[10];
    for (int i = 0; i < 10; i++) {
        count[i] = 0;
    }
    for (int i = 0; i < number.length(); i++) {
        count[number[i] - '0']++;
    }
    H.clear();
    DFS(count, "");
    cout << H.size();
    return 0;
}

// This code is contributed by maddler.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG {
    static HashSet<String> H = new HashSet<>();

    // Function to check whether the
    // number is prime or not
    static boolean check(String number)
    {
        if (number.length() == 0) {
            return false;
        }
        number = number.trim();
        long num = Long.parseLong(number);

        // Condition for prime number
        if (num == 1) {
            return false;
        }
        if (num % 2 == 0 && num != 2) {
            return false;
        }
        if (num % 3 == 0 && num != 3) {
            return false;
        }

        // Iterate over the range [6, num]
        for (int i = 6; i * i <= num; i += 6) {
            if (num % (i - 1) == 0 || num % (i + 1) == 0) {
                return false;
            }
        }

        // Otherwisem return true
        return true;
    }

    // Function to count the total number
    // of prime numbers
    static void DFS(int arr[], String ans)
    {
        // Add it in the HashSet
        if (check(ans) == true) {
            H.add(ans);
        }

        for (int i = 0; i <= 9; ++i) {
            if (arr[i] == 0) {
                continue;
            }

            // Use the number
            ans += i;

            // Decrease the number
            arr[i]--;

            // Perform the DFS Call
            DFS(arr, ans);
            ans = ans.substring(
                0, ans.length() - 1);

            // Backtracking the frequency
            arr[i]++;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String number = "123";

        int count[] = new int[10];
        for (int i = 0; i < number.length(); ++i) {
            count[number.charAt(i) - 48]++;
        }

        // Perform the DFS Traversal
        DFS(count, "");

        // Print the result
        System.out.println(H.size());
    }
}
```

## 蟒蛇 3

```
H = set()

# Function to check whether the
# number is prime or not
def check(number):
    if (len(number) == 0):
        return False
    num = int(number)

    # Condition for prime number
    if (num == 1):
        return False
    if (num % 2 == 0 and num != 2):
        return False
    if (num % 3 == 0 and num != 3):
        return False

    # Iterate over the range [6, num]
    i = 6
    while(i * i <= num):
        if (num % (i - 1) == 0 or num % (i + 1) == 0):
            return False
        i = i + 6

    # Otherwisem return true
    return True

# Function to count the total number
# of prime numbers
def DFS(arr, ans):
    # Add it in the HashSet
    if (check(ans)):
        H.add(ans)

    for i in range(10):
        if (arr[i] == 0):
            continue

        # Use the number
        ans = (ans + str(i))

        # Decrease the number
        arr[i] -= 1

        # Perform the DFS Call
        DFS(arr, ans)
        ans = ans[0: len(ans) - 1]

        # Backtracking the frequency
        arr[i]+=1

number = "123"
count = [0]*(10)
for i in range(10):
    count[i] = 0
for i in range(len(number)):
    count[ord(number[i]) - ord('0')] += 1
H.clear()
DFS(count, "")
print(len(H))

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {
    static HashSet<String> H = new HashSet<String>();

    // Function to check whether the
    // number is prime or not
    static bool check(String number)
    {
        if (number.Length == 0) {
            return false;
        }
        number = number.Trim();
        long num = long.Parse(number);

        // Condition for prime number
        if (num == 1) {
            return false;
        }
        if (num % 2 == 0 && num != 2) {
            return false;
        }
        if (num % 3 == 0 && num != 3) {
            return false;
        }

        // Iterate over the range [6, num]
        for (int i = 6; i * i <= num; i += 6) {
            if (num % (i - 1) == 0 || num % (i + 1) == 0) {
                return false;
            }
        }

        // Otherwisem return true
        return true;
    }

    // Function to count the total number
    // of prime numbers
    static void DFS(int []arr, String ans)
    {
        // Add it in the HashSet
        if (check(ans) == true) {
            H.Add(ans);
        }

        for (int i = 0; i <= 9; ++i) {
            if (arr[i] == 0) {
                continue;
            }

            // Use the number
            ans += i;

            // Decrease the number
            arr[i]--;

            // Perform the DFS Call
            DFS(arr, ans);
            ans = ans.Substring(
                0, ans.Length - 1);

            // Backtracking the frequency
            arr[i]++;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String number = "123";

        int []count = new int[10];
        for (int i = 0; i < number.Length; ++i) {
            count[number[i] - 48]++;
        }

        // Perform the DFS Traversal
        DFS(count, "");

        // Print the result
        Console.WriteLine(H.Count);
    }
}

// This code contributed by shikhasingrajput.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let H = new Set();

    // Function to check whether the
    // number is prime or not
    function check(number)
    {
        if (number.length == 0) {
            return false;
        }
        let num = parseInt(number);

        // Condition for prime number
        if (num == 1) {
            return false;
        }
        if (num % 2 == 0 && num != 2) {
            return false;
        }
        if (num % 3 == 0 && num != 3) {
            return false;
        }

        // Iterate over the range [6, num]
        for (let i = 6; i * i <= num; i += 6) {
            if (num % (i - 1) == 0 || num % (i + 1) == 0) {
                return false;
            }
        }

        // Otherwisem return true
        return true;
    }

    // Function to count the total number
    // of prime numbers
    function DFS(arr, ans)
    {
        // Add it in the HashSet
        if (check(ans)) {
            H.add(ans);
        }

        for (let i = 0; i <= 9; ++i) {
            if (arr[i] == 0) {
                continue;
            }

            // Use the number
            ans = (ans + i.toString());

            // Decrease the number
            arr[i]--;

            // Perform the DFS Call
            DFS(arr, ans);
            ans = ans.substring(0, ans.length - 1);

            // Backtracking the frequency
            arr[i]++;
        }
    }

    let number = "123";
    let count = new Array(10);
    for (let i = 0; i < 10; i++) {
        count[i] = 0;
    }
    for (let i = 0; i < number.length; i++) {
        count[number[i] - '0']++;
    }
    H.clear();
    DFS(count, "");
    document.write(H.size);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(9<sup>N</sup>)*
***辅助空间:** O(1)*