# 检查是否存在只有 2 个不同字符的 K 长度子串，每个字符的频率大于 K/3

> 原文:[https://www . geesforgeks . org/check-if-a-k-length-substring-exists-仅具有-2 个不同字符-每个字符的频率大于-k-3/](https://www.geeksforgeeks.org/check-if-a-k-length-substring-exists-having-only-2-distinct-characters-each-with-frequency-greater-than-k-3/)

给定一个由小写字母组成的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** 和一个整数 **K** ，任务是找出是否存在长度为 **K** 的[子字符串](https://www.geeksforgeeks.org/substring-in-java/)，只有 2 个唯一字符，并且两个字符的计数必须大于***K*****/3**。如果存在这样的字符串，则打印“**是**”否则“**否**”。

***例:***

> **输入**:“abbad”，K = 4
> **输出** : YES
> **解释**:子串“abba”有 2 个 A 和 2 个 b，总长度为 4，由于 2 大于 4/3，所以是有效的子串。
> 
> **输入**:“abaaaa”，K = 6
> **输出**:否
> **解释**:不存在有效的子串。

**方法:**通过跟踪**当前**子串中**唯一**字符的数量，使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)检查所有 **K** 长度子串，可以解决该任务。按照以下步骤解决问题:

*   取一张[无序图](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)存储当前[子串](https://www.geeksforgeeks.org/substring-in-java/)中的字符数及其出现频率，如果
    *   当前子串中只有 2 个**不同的**字符，并且
    *   没有一个字符的计数小于或等于 **K/3**
*   当前子字符串是有效的字符串。
*   因此打印**是**，
*   如果没有遇到有效的子串，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// a valid substring exists or not
void checkGoldenString(string S, int k)
{
    // Store the count of distinct chars
    // with their frequencies
    unordered_map<char, int> occ;

    int n = S.length();

    // First substring of length k
    for (int i = 0; i < k; i++)
        occ[S[i]]++;

    // Check if it is valid
    if (occ.size() == 2) {
        int x = -1, y = -1;
        for (auto item : occ) {
            if (x == -1)
                x = item.second;
            else
                y = item.second;
        }

        // Count of one of the chars is
        // greater than k/3
        if (x >= k / 3 && y >= k / 3) {
            cout << "YES\n";
            return;
        }
    }

    // Sliding over the entire string
    for (int i = k; i < n; i++) {

        // Discarding first character of
        // previous window
        occ[S[i - k]]--;

        // Erase it from the map, if its
        // frequency becomes 0
        if (occ[S[i - k]] == 0)
            occ.erase(S[i - k]);

        // Increment count of current char
        occ[S[i]]++;

        // Checking valid or not
        if (occ.size() == 2) {
            int x = -1, y = -1;
            for (auto item : occ) {
                if (x == -1)
                    x = item.second;
                else
                    y = item.second;
            }

            if (x >= k / 3 && y >= k / 3) {
                cout << "YES\n";
                return;
            }
        }
    }

    // No valid substring is found
    cout << "NO\n";
}

// Driver Code
int main()
{
    int K = 6;
    string S = "abaaaa";
    checkGoldenString(S, K);

    K = 4;
    S = "abbaaaa";
    checkGoldenString(S, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
class GFG {

    // Function to check whether
    // a valid substring exists or not
    public static void checkGoldenString(String S, int k)
    {

        // Store the count of distinct chars
        // with their frequencies
        HashMap<Character, Integer> occ = new HashMap<Character, Integer>();

        int n = S.length();

        // First substring of length k
        for (int i = 0; i < k; i++) {
            if (occ.containsKey(S.charAt(i))) {
                occ.put(S.charAt(i), occ.get(S.charAt(i)) + 1);
            } else {
                occ.put(S.charAt(i), 1);
            }
        }

        // Check if it is valid
        if (occ.size() == 2) {
            int x = -1, y = -1;
            for (char item : occ.keySet()) {
                if (x == -1)
                    x = occ.get(item);
                else
                    y = occ.get(item);
            }

            // Count of one of the chars is
            // greater than k/3
            if (x >= k / 3 && y >= k / 3) {
                System.out.println("YES");
                return;
            }
        }

        // Sliding over the entire string
        for (int i = k; i < n; i++) {

            // Discarding first character of
            // previous window
            occ.put(S.charAt(i - k), occ.get(S.charAt(i - k)) - 1);

            // Erase it from the map, if its
            // frequency becomes 0
            if (occ.get(S.charAt(i - k)) == 0)
                occ.remove(S.charAt(i - k));

            // Increment count of current char
            if (occ.containsKey(S.charAt(i))) {
                occ.put(S.charAt(i), occ.get(S.charAt(i)) + 1);
            } else {
                occ.put(S.charAt(i), 1);
            }

            // Checking valid or not
            if (occ.size() == 2) {
                int x = -1, y = -1;
                for (char item : occ.keySet()) {
                    if (x == -1)
                        x = occ.get(item);
                    else
                        y = occ.get(item);
                }

                if (x >= k / 3 && y >= k / 3) {
                    System.out.println("YES");
                    return;
                }
            }
        }

        // No valid substring is found
        System.out.println("NO");
    }

    // Driver Code
    public static void main(String args[]) {
        int K = 6;
        String S = "abaaaa";
        checkGoldenString(S, K);

        K = 4;
        S = "abbaaaa";
        checkGoldenString(S, K);
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to check whether
# a valid substring exists or not
def checkGoldenString(S, k):

    # Store the count of distinct chars
    # with their frequencies
    occ = dict()

    n = len(S)

    # First substring of length k
    for i in range(k):
        if (S[i] not in occ):
            occ[S[i]] = 1
        else:
            occ[S[i]] += 1

    # Check if it is valid
    if (len(occ) == 2):
        x = -1
        y = -1
        for z in occ.values():
            if (x == -1):
                x = z
            else:
                y = z

        # Count of one of the chars is
        # greater than k/3
        if (x >= k // 3 and y >= k // 3):
            print("YES")
            return

    # Sliding over the entire string
    for i in range(k, n):

        # Discarding first character of
        # previous window
        if (S[i - k] in occ):
            occ[[S[i - k]]] -= k

        # Erase it from the map, if its
        # frequency becomes 0
        if (occ[S[i - k]] == 0):
            del occ[S[i - k]]

        # Increment count of current char
        if (S[i] not in occ):
            occ[S[i]] = 1
        else:
            occ[S[i]] += 1

        # Checking valid or not
        if (len(occ) == 2):
            x = -1
            y = -1
            for z in occ.values:
                if (x == -1):
                    x = z
                else:
                    y = z

            if (x >= k // 3 and y >= k // 3):
                print("YES" + '<br>')
                return

    # No valid substring is found
    print("NO")

# Driver Code
K = 6
S = "abaaaa"
checkGoldenString(S, K)

K = 4
S = "abbaaaa"
checkGoldenString(S, K)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to check whether
    // a valid substring exists or not
    public static void checkGoldenString(String S, int k)
    {

        // Store the count of distinct chars
        // with their frequencies
        Dictionary<char, int> occ = new Dictionary<char, int>();

        int n = S.Length;

        // First substring of length k
        for (int i = 0; i < k; i++) {
            if (occ.ContainsKey(S[i])) {
                occ[S[i]] = occ[S[i]] + 1;
            } else {
                occ.Add(S[i], 1);
            }
        }

        // Check if it is valid
        if (occ.Count == 2) {
            int x = -1, y = -1;
            foreach (char item in occ.Keys) {
                if (x == -1)
                    x = occ[item];
                else
                    y = occ[item];
            }

            // Count of one of the chars is
            // greater than k/3
            if (x >= k / 3 && y >= k / 3) {
                Console.WriteLine("YES");
                return;
            }
        }

        // Sliding over the entire string
        for (int i = k; i < n; i++) {

            // Discarding first character of
            // previous window
            occ[S[i - k] ]= occ[S[i - k]] - 1;

            // Erase it from the map, if its
            // frequency becomes 0
            if (occ[S[i - k]] == 0)
                occ.Remove(S[i - k]);

            // Increment count of current char
            if (occ.ContainsKey(S[i])) {
                occ[S[i]] = occ[S[i]] + 1;
            } else {
                occ.Add(S[i], 1);
            }

            // Checking valid or not
            if (occ.Count == 2) {
                int x = -1, y = -1;
                foreach (char item in occ.Keys) {
                    if (x == -1)
                        x = occ[item];
                    else
                        y = occ[item];
                }

                if (x >= k / 3 && y >= k / 3) {
                    Console.WriteLine("YES");
                    return;
                }
            }
        }

        // No valid substring is found
        Console.WriteLine("NO");
    }

    // Driver Code
    public static void Main(String []args) {
        int K = 6;
        String S = "abaaaa";
        checkGoldenString(S, K);

        K = 4;
        S = "abbaaaa";
        checkGoldenString(S, K);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to check whether
       // a valid substring exists or not
       function checkGoldenString(S, k)
       {

           // Store the count of distinct chars
           // with their frequencies
           let occ = new Map();

           let n = S.length;

           // First substring of length k
           for (let i = 0; i < k; i++) {
               if (!occ.has(S[i])) {
                   occ.set(S[i], 1);
               }
               else {
                   occ.set(S[i], occ.get(S[i]) + 1);
               }
           }

           // Check if it is valid
           if (occ.size == 2) {
               let x = -1, y = -1;
               for (let [key, value] of occ) {
                   if (x == -1)
                       x = value;
                   else
                       y = value;
               }

               // Count of one of the chars is
               // greater than k/3
               if (x >= Math.floor(k / 3) && y >= Math.floor(k / 3)) {
                   document.write("YES" + '<br>');
                   return;
               }
           }

           // Sliding over the entire string
           for (let i = k; i < n; i++) {

               // Discarding first character of
               // previous window
               if (occ.has(S[i - k]))
                   occ.set([S[i - k]], occ.get(S[i - k]) - 1);

               // Erase it from the map, if its
               // frequency becomes 0
               if (occ.get(S[i - k]) == 0)
                   occ.delete(S[i - k]);

               // Increment count of current char
               if (!occ.has(S[i]))
                   occ.set(S[i], 1);
               else
                   occ.set(S[i], occ.get(S[i]) + 1)

               // Checking valid or not
               if (occ.size == 2) {
                   let x = -1, y = -1;
                   for (let [key, value] of occ) {
                       if (x == -1)
                           x = value;
                       else
                           y = value;
                   }

                   if (x >= Math.floor(k / 3) && y >= Math.floor(k / 3)) {
                       document.write("YES" + '<br>');
                       return;
                   }
               }
           }

           // No valid substring is found
           document.write("NO" + '<br>');
       }

       // Driver Code
       let K = 6;
       let S = "abaaaa";
       checkGoldenString(S, K);

       K = 4;
       S = "abbaaaa";
       checkGoldenString(S, K);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
NO
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)