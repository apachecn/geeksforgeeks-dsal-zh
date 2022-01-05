# 检查给定的字符串是否可以通过仅删除单一类型的字符

而成为回文

> 原文:[https://www . geesforgeks . org/check-if-给定字符串-只能通过移除单个字符类型来生成回文/](https://www.geeksforgeeks.org/check-if-given-string-can-be-made-palindrome-by-removing-only-single-type-of-character/)

给定一个字符串 **S** ，任务是在移除**相同**字符、**任意**次数的出现后，一个字符串是否可以被做成[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)

**示例:**

> **输入**:S =“abczdzacb”
> **输出**:是
> **解释**:去掉字符‘a’的第一次和第二次出现，字符串 S 变成“bczdzcb”，是回文。
> 
> **输入** : S = "madem"
> **输出**:否

**方法:**通过迭代给定字符串中的每个**唯一**字符，并在存在**不匹配**的地方移除其出现，可以解决该任务，如果找到有效的回文，在移除相同字符的出现任意次数后，返回“**是**”否则返回“**否**”。
按照以下步骤解决问题:

*   开始迭代字符串的每个**唯一**字符，这些字符的出现将被删除
*   使用[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)技术，检查不匹配，将 **l** 放置在琴弦的**起点**处，将 **r** 放置在琴弦的**终点**处
*   如果 **S[l] == S[r]** ，递增 **l** ，递减 **r** 。
*   如果 **S[l]！= S[r]，**检查 S[l[ == char，do l++，否则如果 S[r] == char，do r–
*   如果这些条件都不成立，意味着给定的不能转换成回文

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a palindrome is
// possible or not
string isPossible(string S)
{
    // Stores the length of string
    int n = (int)S.length();

    // Stores the unique characters in
    // the string
    set<char> st;

    for (int i = 0; i < n; i++) {
        st.insert(S[i]);
    }

    // Check if valid palindrome is
    // possible or not
    bool check = false;

    // Iterating over unique characters
    // of the string
    for (auto ele : st) {

        // Pointers to check the condition
        int low = 0, high = n - 1;
        bool flag = true;

        // Iterating over the string
        for (int i = 0; i < n; i++) {
            if (S[low] == S[high]) {

                // Updating low and high
                low++;
                high--;
            }

            else {
                if (S[low] == ele) {

                    // Updating low
                    low++;
                }
                else if (S[high] == ele) {

                    // Updating high
                    high--;
                }
                else {

                    // It is impossible
                    // to make palindrome
                    // by removing
                    // occurrences of char
                    flag = false;
                    break;
                }
            }
        }

        // If palindrome is formed
        // break the loop
        if (flag == true) {
            check = true;
            break;
        }
    }

    if (check)
        return "Yes";
    else
        return "No";
}

// Driver Code
int main()
{

    string S = "abczdzacb";
    cout << isPossible(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG
{

  // Function to check if a palindrome is
// possible or not
static String isPossible(String S)
{

    // Stores the length of string
    int n = S.length();

    // Stores the unique characters in
    // the string
    Set<Character> st = new HashSet<Character>();

    for (int i = 0; i < n; i++) {
        st.add(S.charAt(i));
    }

    // Check if valid palindrome is
    // possible or not
    boolean check = false;

    // Iterating over unique characters
    // of the string
    for (Character ele : st) {

        // Pointers to check the condition
        int low = 0, high = n - 1;
        boolean flag = true;

        // Iterating over the string
        for (int i = 0; i < n; i++) {
            if (S.charAt(low) == S.charAt(high)) {

                // Updating low and high
                low++;
                high--;
            }

            else {
                if (S.charAt(low) == ele) {

                    // Updating low
                    low++;
                }
                else if (S.charAt(high)== ele) {

                    // Updating high
                    high--;
                }
                else {

                    // It is impossible
                    // to make palindrome
                    // by removing
                    // occurrences of char
                    flag = false;
                    break;
                }
            }
        }

        // If palindrome is formed
        // break the loop
        if (flag == true) {
            check = true;
            break;
        }
    }

    if (check)
        return "Yes";
    else
        return "No";
}

// Driver Code
    public static void main (String[] args) {
      String S = "abczdzacb";

        System.out.println(isPossible(S));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to check if a palindrome is
# possible or not
def isPossible(S):

    # Stores the length of string
    n = len(S)

    # Stores the unique characters in
    # the string
    st = set()

    for i in range(0, n):
        st.add(S[i])

    # Check if valid palindrome is
    # possible or not
    check = False

    # Iterating over unique characters
    # of the string
    for ele in st:

        # Pointers to check the condition
        low = 0
        high = n - 1
        flag = True

        # Iterating over the string
        for i in range(0, n):
            if (S[low] == S[high]):

                # Updating low and high
                low += 1
                high -= 1

            else:
                if (S[low] == ele):

                    # Updating low
                    low += 1

                elif (S[high] == ele):

                    # Updating high
                    high -= 1

                else:

                    # It is impossible
                    # to make palindrome
                    # by removing
                    # occurrences of char
                    flag = False
                    break

                # If palindrome is formed
                # break the loop
        if (flag == True):
            check = True
            break

    if (check):
        return "Yes"

    else:
        return "No"

# Driver Code
if __name__ == "__main__":

    S = "abczdzacb"
    print(isPossible(S))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to check if a palindrome is
// possible or not
static String isPossible(String S)
{

    // Stores the length of string
    int n = S.Length;

    // Stores the unique characters in
    // the string
    HashSet<char> st = new HashSet<char>();

    for (int i = 0; i < n; i++) {
        st.Add(S[i]);
    }

    // Check if valid palindrome is
    // possible or not
    bool check = false;

    // Iterating over unique characters
    // of the string
    foreach (char ele in st) {

        // Pointers to check the condition
        int low = 0, high = n - 1;
        bool flag = true;

        // Iterating over the string
        for (int i = 0; i < n; i++) {
            if (S[low] == S[high]) {

                // Updating low and high
                low++;
                high--;
            }

            else {
                if (S[low] == ele) {  

                    // Updating low
                    low++;
                }
                else if (S[high]== ele) {

                    // Updating high
                    high--;
                }
                else {

                    // It is impossible
                    // to make palindrome
                    // by removing
                    // occurrences of char
                    flag = false;
                    break;
                }
            }
        }

        // If palindrome is formed
        // break the loop
        if (flag == true) {
            check = true;
            break;
        }
    }

    if (check)
        return "Yes";
    else
        return "No";
}

// Driver Code
    public static void Main(String[] args) {
      String S = "abczdzacb";

        Console.WriteLine(isPossible(S));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if a palindrome is
// possible or not
function isPossible(S)
{

  // Stores the length of string
  let n = S.length;

  // Stores the unique characters in
  // the string
  let st = new Set();

  for (let i = 0; i < n; i++) {
    st.add(S[i]);
  }

  // Check if valid palindrome is
  // possible or not
  let check = false;

  // Iterating over unique characters
  // of the string
  for (ele of st) {

    // Pointers to check the condition
    let low = 0, high = n - 1;
    let flag = true;

    // Iterating over the string
    for (let i = 0; i < n; i++) {
      if (S[low] == S[high]) {

        // Updating low and high
        low++;
        high--;
      }

      else {
        if (S[low] == ele) {

          // Updating low
          low++;
        }
        else if (S[high] == ele) {

          // Updating high
          high--;
        }
        else {

          // It is impossible
          // to make palindrome
          // by removing
          // occurrences of char
          flag = false;
          break;
        }
      }
    }

    // If palindrome is formed
    // break the loop
    if (flag == true) {
      check = true;
      break;
    }
  }

  if (check)
    return "Yes";
  else
    return "No";
}

// Driver Code
let S = "abczdzacb";
document.write(isPossible(S));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度***:**O(n * 26)
***辅助空间*** : O(n)**