# 检查通过交换相邻字符对是否可以使两个字符串相等

> 原文:[https://www . geesforgeks . org/check-if-two-strings-通过交换相邻字符对可以使其相等/](https://www.geeksforgeeks.org/check-if-two-strings-can-be-made-equal-by-swapping-pairs-of-adjacent-characters/)

给定长度分别为 **N** 和 **M** 的两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **A** 和 **B** 以及由 **K** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**【arr】**，任务是通过交换字符串 **A** 的任意一对相邻字符来检查字符串 **B** 是否可以从字符串 **A** 中获得如果可以将字符串 **A** 转换为字符串 **B，**打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** A = "abcabka "，B = "acbakba "，arr[] = {0，3，6}
> **输出:**是
> **说明:**
> 交换 A <sub>1</sub> 和 A <sub>2</sub> 。现在字符串变成了 A = "acbabka "。
> 互换 A <sub>4</sub> 和 A <sub>5</sub> 。现在字符串变成了 A =“acbakba”，和字符串 b 一样。
> 
> **输入:**A =“AAA”，B =“BBB”，arr[]= { 0 }
> T3】输出:否

**方法:**按照以下步骤解决问题:

*   如果两根弦的长度不相等，那么弦 **A** 就不能转化为弦 **B** 。因此，打印**“否”**。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，检查**A【arr[I]】**和**B【arr[I]】**处的字符是否相同。如果发现属实，则打印**“否”**。否则，请执行以下步骤:
    *   如果 **arr[i]** 的第一个元素不是 **0** :
        *   将从 **0** 到**的 **A** 和 **B** 的所有字符存储在两个字符串中，比如 **X** 和 **Y** 。**
        *   [查找字符串**X****Y**](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)的字符频率。
        *   如果所有字符的频率相同，则打印“**否**”。
    *   同样，如果 **arr[i]** 的最后一个元素不等于索引**(N–1)**处的元素，则:
        *   将从 **(arr[i] + 1)** 到 **N** 的 **A** 和 **B** 的所有字符存储在两个字符串中，比如说 **X** 和 **Y** 。
        *   [查找字符串**X****Y**](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)的字符频率。
        *   如果所有字符的频率相同，则打印“**否**”。
    *   迭代一个从 **1** 到 **N** 的循环，初始化两个指针，**L = arr[I–1]**和 **R = arr[i]** :
        *   将从 **(L + 1)** 到 **R** 的 **A** 和 **B** 的所有字符存储在两个字符串中，比如说 **X** 和 **Y** 。
        *   [查找字符串**X****Y**](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)的字符频率。
        *   如果所有字符的频率相同，则打印“**是”**。否则，打印“**否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count frequency of the
// characters of two given strings
bool isEqual(string& A, string& B)
{
    // Stores the frequencies of
    // characters of strings A and B
    map<char, int> mp, mp1;

    // Traverse the string A
    for (auto it : A) {

        // Update frequency of
        // each character
        mp[it]++;
    }

    // Traverse the string B
    for (auto it : B) {

        // Update frequency of
        // each character
        mp1[it]++;
    }

    // Traverse the Map
    for (auto it : mp) {

        // If the frequency a character
        // is not the same in both the strings
        if (it.second != mp1[it.first]) {
            return false;
        }
    }

    return true;
}

// Function to check if it is possible
// to convert string A to string B
void IsPossible(string& A, string& B,
                int arr[], int N)
{

    // Base Case
    if (A == B) {
        cout << "Yes" << endl;
        return;
    }

    // If length of both the
    // strings are not equal
    if (A.length() != B.length()) {
        cout << "No" << endl;
        return;
    }

    // Traverse the array and check
    // if the blocked indices
    // contains the same character
    for (int i = 0; i < N; i++) {
        int idx = arr[i];

        // If there is a different
        // character, return No
        if (A[idx] != B[idx]) {
            cout << "No" << endl;
            return;
        }
    }

    // If the first index is not present
    if (arr[0]) {
        string X = "";
        string Y = "";

        // Extract characters from
        // string A and B
        for (int i = 0; i < arr[0]; i++) {
            X += A[i];
            Y += B[i];
        }

        // If frequency is not same
        if (!isEqual(A, B)) {

            cout << "No" << endl;
            return;
        }
    }

    // If last index is not present
    if (arr[N - 1] != (A.length() - 1)) {
        string X = "";
        string Y = "";

        // Extract characters from
        // string A and B
        for (int i = arr[N - 1] + 1;
             i < A.length(); i++) {
            X += A[i];
            Y += B[i];
        }

        // If frequency is not same
        if (!isEqual(A, B)) {
            cout << "No" << endl;
            return;
        }
    }

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        int L = arr[i - 1];
        int R = arr[i];

        string X = "";
        string Y = "";

        // Extract characters from strings A and B
        for (int j = L + 1; j < R; j++) {
            X += A[j];
            Y += B[j];
        }

        // If frequency is not same
        if (!isEqual(A, B)) {
            cout << "No" << endl;
            return;
        }
    }

    // If all conditions are satisfied
    cout << "Yes" << endl;
}

// Driver Code
int main()
{
    string A = "abcabka";
    string B = "acbakba";
    int arr[] = { 0, 3, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    IsPossible(A, B, arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

// importing input-output and utility classes
import java.io.*;
import java.util.*;

class GFG {
    // method to count frequency of the
    // characters of two given strings
    static boolean isEqual(String A, String B)
    {
        // storing the frequencies of characters
        HashMap<Character, Integer> map = new HashMap<>();
        HashMap<Character, Integer> map2 = new HashMap<>();

        // Traversing the String A
        for (int i = 0; i < A.length(); i++) {
            if (map.containsKey(A.charAt(i)))
                map.put(A.charAt(i),
                        map.get(A.charAt(i)) + 1);
            else
                map.put(A.charAt(i), 1);
        }
        // Traversing the String B
        for (int i = 0; i < B.length(); i++) {
            if (map.containsKey(B.charAt(i)))
                map.put(B.charAt(i),
                        map.get(B.charAt(i)) + 1);
            else
                map.put(B.charAt(i), 1);
        }
        // checking if both map have same character
        // frequency
        if (!map.equals(map2))
            return false;
        return true;
    }

    // method to check possibility to convert A into B
    static void isPossible(String A, String B, int arr[],
                           int N)
    {
        // Base Case
        if (A.equals(B)) {
            System.out.println("Yes");
            return;
        }
        // If length is not equal
        if (A.length() != B.length()) {
            System.out.println("No");
            return;
        }
        for (int i = 0; i < N; i++) {
            int idx = arr[i];

            if (A.charAt(idx) != B.charAt(idx)) {
                System.out.println("No");
                return;
            }
        }
        // If first index is not present
        if (arr[0] == 0) {
            String X = "";
            String Y = "";
            // Extracting Characters from A and B
            for (int i = 0; i < arr[0]; i++) {
                X += A.charAt(i);
                Y += B.charAt(i);
            }
            // If frequency is not same
            if (!isEqual(A, B)) {
                System.out.println("No");
                return;
            }
        }
        // If last index is not present
        if (arr[N - 1] != (A.length() - 1)) {
            String X = "";
            String Y = "";

            for (int i = arr[N - 1] + 1; i < A.length();
                 i++) {
                X += A.charAt(i);
                Y += B.charAt(i);
            }

            if (!isEqual(A, B)) {
                System.out.println("No");
                return;
            }
        }
        // Traversing the Array
        for (int i = 1; i < N; i++) {
            int L = arr[i - 1];
            int R = arr[i - 1];
            String X = "";
            String Y = "";
            // Extract Characters from Strings A and B
            for (int j = L + 1; j < R; j++) {
                X += A.charAt(j);
                Y += B.charAt(j);
            }
            // if frequency is not same
            if (!isEqual(A, B)) {
                System.out.println("No");
                return;
            }
        }
        // if all condition satisfied
        System.out.println("Yes");
    }
    // main method
    public static void main(String[] args)
    {
        String A = "abcabka";
        String B = "abcabka";
        int arr[] = { 0, 3, 6 };
        int N = arr.length;
        // calling method
        isPossible(A, B, arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to count frequency of the
# characters of two given strings
def isEqual(A, B):

    # Stores the frequencies of
    # characters of strings A and B
    mp = defaultdict(int)
    mp1 = defaultdict(int)

    # Traverse the string A
    for it in A:

        # Update frequency of
        # each character
        mp[it] += 1

    # Traverse the string B
    for it in B:

        # Update frequency of
        # each character
        mp1[it] += 1

    # Traverse the Map
    for it in mp:

        # If the frequency a character
        # is not the same in both the strings
        if (mp[it] != mp1[it]):
            return False

    return True

# Function to check if it is possible
# to convert string A to string B
def IsPossible(A, B, arr, N):

    # Base Case
    if (A == B):
        print("Yes")
        return

    # If length of both the
    # strings are not equal
    if (len(A) != len(B)):
        print("No")
        return

    # Traverse the array and check
    # if the blocked indices
    # contains the same character
    for i in range(N):
        idx = arr[i]

        # If there is a different
        # character, return No
        if (A[idx] != B[idx]):
            print("No")
            return

    # If the first index is not present
    if (arr[0]):
        X = ""
        Y = ""

        # Extract characters from
        # string A and B
        for i in range(arr[0]):
            X += A[i]
            Y += B[i]

        # If frequency is not same
        if (not isEqual(A, B)):
            print("No")
            return

    # If last index is not present
    if (arr[N - 1] != (len(A) - 1)):
        X = ""
        Y = ""

        # Extract characters from
        # string A and B
        for i in range(arr[N - 1] + 1,
                       len(A)):
            X += A[i]
            Y += B[i]

        # If frequency is not same
        if (not isEqual(A, B)):
            print("No")
            return

    # Traverse the array arr[]
    for i in range(1, N):
        L = arr[i - 1]
        R = arr[i]

        X = ""
        Y = ""

        # Extract characters from strings A and B
        for j in range(L + 1, R):
            X += A[j]
            Y += B[j]

        # If frequency is not same
        if (not isEqual(A, B)):
            print("No")
            return

    # If all conditions are satisfied
    print("Yes")

# Driver Code
if __name__ == "__main__":

    A = "abcabka"
    B = "acbakba"
    arr = [ 0, 3, 6 ]
    N = len(arr)

    IsPossible(A, B, arr, N)

# This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count frequency of the
// characters of two given strings
function isEqual(A, B)
{

    // Stores the frequencies of
    // characters of strings A and B
    let mp = new Map();
    let mp1 = new Map();

    // Traverse the string A
    for(let it of A)
    {

        // Update frequency of
        // each character
        if (mp.has(it))
        {
            mp.set(it, mp.get(it) + 1)
        }
        else
        {
            mp.set(it, 1)
        }
    }

    // Traverse the string B
    for(let it of B)
    {

        // Update frequency of
        // each character
        if (mp1.has(it))
        {
            mp1.set(it, mp1.get(it) + 1)
        }
        else
        {
            mp1.set(it, 1)
        }
    }

    // Traverse the Map
    for(let it of mp)
    {

        // If the frequency a character
        // is not the same in both the strings
        if (it[1] != mp1.get(it[0]))
        {
            return false;
        }
    }
    return true;
}

// Function to check if it is possible
// to convert string A to string B
function IsPossible(A, B, arr, N)
{

    // Base Case
    if (A == B)
    {
        document.write("Yes" + "<br>");
        return;
    }

    // If length of both the
    // strings are not equal
    if (A.length != B.length)
    {
        document.write("No" + "<br>");
        return;
    }

    // Traverse the array and check
    // if the blocked indices
    // contains the same character
    for(let i = 0; i < N; i++)
    {
        let idx = arr[i];

        // If there is a different
        // character, return No
        if (A[idx] != B[idx])
        {
            document.write("No" + "<br>");
            return;
        }
    }

    // If the first index is not present
    if (arr[0])
    {
        let X = "";
        let Y = "";

        // Extract characters from
        // string A and B
        for(let i = 0; i < arr[0]; i++)
        {
            X += A[i];
            Y += B[i];
        }

        // If frequency is not same
        if (!isEqual(A, B))
        {
            document.write("No" + "<br>");
            return;
        }
    }

    // If last index is not present
    if (arr[N - 1] != (A.length - 1))
    {
        let X = "";
        let Y = "";

        // Extract characters from
        // string A and B
        for(let i = arr[N - 1] + 1;
                i < A.length; i++)
        {
            X += A[i];
            Y += B[i];
        }

        // If frequency is not same
        if (!isEqual(A, B))
        {
            document.write("No" + "<br>");
            return;
        }
    }

    // Traverse the array arr[]
    for(let i = 1; i < N; i++)
    {
        let L = arr[i - 1];
        let R = arr[i];
        let X = "";
        let Y = "";

        // Extract characters from strings A and B
        for(let j = L + 1; j < R; j++)
        {
            X += A[j];
            Y += B[j];
        }

        // If frequency is not same
        if (!isEqual(A, B))
        {
            document.write("No" + "<br>");
            return;
        }
    }

    // If all conditions are satisfied
    document.write("Yes" + "<br>");
}

// Driver Code
let A = "abcabka";
let B = "acbakba";
let arr = [ 0, 3, 6 ];
let N = arr.length

IsPossible(A, B, arr, N);

// This code is contributed by gfgking

</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)