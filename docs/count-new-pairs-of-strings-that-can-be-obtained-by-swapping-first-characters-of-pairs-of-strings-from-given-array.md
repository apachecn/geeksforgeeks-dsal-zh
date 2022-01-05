# 计算新的字符串对，这些字符串对可以通过交换给定数组中字符串对的第一个字符获得

> 原文:[https://www . geesforgeks . org/count-新字符串对-可以通过从给定数组中交换字符串对的第一个字符来获得/](https://www.geeksforgeeks.org/count-new-pairs-of-strings-that-can-be-obtained-by-swapping-first-characters-of-pairs-of-strings-from-given-array/)

给定由 **N** [字符串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过交换字符串 **arr[i]** 和 **arr[j]** 的第一个字符，找到由任意对 **(arr[i]，arr[j])组成的数组中不存在的一对[字符串。](https://www.geeksforgeeks.org/find-elements-present-first-array-not-second/)**

**示例:**

> **输入:** arr[] = {“好”、“坏”、“食物”}
> **输出:** 2
> **解释:**
> 通过交换任意一对的第一个字符可以形成的可能的对有:
> 
> 1.  **(“好”、“坏”):**交换字符‘g’和‘b’，将字符串修改为数组中不存在的“bood”和 gad。
> 2.  **(“坏的”、“食物”):**交换字符“g”和“b”，将字符串修改为数组中不存在的“bood”和 gad。
> 
> 因此，总计数为 2。
> 
> **输入:** arr[] = {“极客”、“窥视”}
> **输出:** 0

**天真方法:**解决给定问题的最简单方法是[生成所有字符串对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每一对[交换两个字符串的第一个字符](https://www.geeksforgeeks.org/swap-in-cpp/)，如果两个字符串都出现在数组中，则计算这一对。检查所有对后，打印获得的计数值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count new pairs of strings
// that can be obtained by swapping first
// characters of any pair of strings
void countStringPairs(string a[], int n)
{

    // Stores the count of pairs
    int ans = 0;

    // Generate all possible pairs of
    // strings from the array arr[]
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Stores the current
            // pair of strings
            string p = a[i], q = a[j];

            // Swap the first characters
            if (p[0] != q[0]) {

                swap(p[0], q[0]);
                int flag1 = 0;
                int flag2 = 0;

                // Check if they are already
                // present in the array or not
                for (int k = 0; k < n; k++) {

                    if (a[k] == p) {
                        flag1 = 1;
                    }
                    if (a[k] == q) {
                        flag2 = 1;
                    }
                }

                // If both the strings
                // are not present
                if (flag1 == 0 && flag2 == 0) {

                    // Increment the ans
                    // by 1
                    ans = ans + 1;
                }
            }
        }
    }

    // Print the resultant count
    cout << ans;
}

// Driver Code
int main()
{
    string arr[] = { "good", "bad", "food" };
    int N = sizeof(arr) / sizeof(arr[0]);
    countStringPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count new pairs of strings
// that can be obtained by swapping first
// characters of any pair of strings
static void countStringPairs(String a[], int n)
{

    // Stores the count of pairs
    int ans = 0;

    // Generate all possible pairs of
    // strings from the array arr[]
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Stores the current
            // pair of strings
            char p[] = a[i].toCharArray();
            char q[] = a[j].toCharArray();

            // Swap the first characters
            if (p[0] != q[0])
            {
                char temp = p[0];
                p[0] = q[0];
                q[0] = temp;
                int flag1 = 0;
                int flag2 = 0;

                // Check if they are already
                // present in the array or not
                for(int k = 0; k < n; k++)
                {
                    if (a[k].equals(new String(p)))
                    {
                        flag1 = 1;
                    }
                    if (a[k].equals(new String(q)))
                    {
                        flag2 = 1;
                    }
                }

                // If both the strings
                // are not present
                if (flag1 == 0 && flag2 == 0)
                {

                    // Increment the ans
                    // by 1
                    ans = ans + 1;
                }
            }
        }
    }

    // Print the resultant count
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "good", "bad", "food" };
    int N = arr.length;

    countStringPairs(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to count new pairs of strings
# that can be obtained by swapping first
# characters of any pair of strings
def countStringPairs(a, n):

    # Stores the count of pairs
    ans = 0

    # Generate all possible pairs of
    # strings from the array arr[]
    for i in range(n):
        for j in range(i + 1, n, 1):

            # Stores the current
            # pair of strings
            p = a[i]
            q = a[j]

            # Swap the first characters
            if (p[0] != q[0]):
                p = list(p)
                q = list(q)
                temp = p[0]
                p[0] = q[0]
                q[0] = temp

                p = ''.join(p)
                q = ''.join(q)
                flag1 = 0
                flag2 = 0

                # Check if they are already
                # present in the array or not
                for k in range(n):
                    if (a[k] == p):
                        flag1 = 1
                    if (a[k] == q):
                        flag2 = 1

                # If both the strings
                # are not present
                if (flag1 == 0 and flag2 == 0):

                    # Increment the ans
                    # by 1
                    ans = ans + 1

    # Print the resultant count
    print(ans)

# Driver Code
if __name__ == '__main__':
    arr = ["good", "bad", "food"]
    N = len(arr)
    countStringPairs(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C # program for the above approach
using System;
class GFG {

    // Function to count new pairs of strings
    // that can be obtained by swapping first
    // characters of any pair of strings
    static void countStringPairs(string[] a, int n)
    {

        // Stores the count of pairs
        int ans = 0;

        // Generate all possible pairs of
        // strings from the array arr[]
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                // Stores the current
                // pair of strings
                char[] p = a[i].ToCharArray();
                char[] q = a[j].ToCharArray();

                // Swap the first characters
                if (p[0] != q[0]) {
                    char temp = p[0];
                    p[0] = q[0];
                    q[0] = temp;
                    int flag1 = 0;
                    int flag2 = 0;

                    // Check if they are already
                    // present in the array or not
                    for (int k = 0; k < n; k++) {
                        if (a[k].Equals(new string(p))) {
                            flag1 = 1;
                        }
                        if (a[k].Equals(new string(q))) {
                            flag2 = 1;
                        }
                    }

                    // If both the strings
                    // are not present
                    if (flag1 == 0 && flag2 == 0) {

                        // Increment the ans
                        // by 1
                        ans = ans + 1;
                    }
                }
            }
        }

        // Print the resultant count
        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string[] arr = { "good", "bad", "food" };
        int N = arr.Length;

        countStringPairs(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count new pairs of strings
      // that can be obtained by swapping first
      // characters of any pair of strings
      function countStringPairs(a, n) {
        // Stores the count of pairs
        var ans = 0;

        // Generate all possible pairs of
        // strings from the array arr[]
        for (let i = 0; i < n; i++) {
          for (let j = i + 1; j < n; j++) {
            // Stores the current
            // pair of strings
            var p = a[i];
            var q = a[j];

            // Swap the first characters
            if (p[0] !== q[0]) {
              p = p.split("");
              q = q.split("");
              var temp = p[0];
              p[0] = q[0];
              q[0] = temp;

              p = p.join("");
              q = q.join("");
              var flag1 = 0;
              var flag2 = 0;

              // Check if they are already
              // present in the array or not
              for (let k = 0; k < n; k++) {
                if (a[k] === p) flag1 = 1;
                if (a[k] === q) flag2 = 1;
              }
              // If both the strings
              // are not present
              if (flag1 === 0 && flag2 === 0) {
                // Increment the ans
                // by 1
                ans = ans + 1;
              }
            }
          }
        }

        // Print the resultant count
        document.write(ans);
      }
      // Driver Code
      var arr = ["good", "bad", "food"];
      var N = arr.length;
      countStringPairs(arr, N);
    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(M)，其中 M 是数组中出现的字符串的最大大小，A[]*

**高效方法:**上述方法也可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)的概念进行优化。按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans** 为 **0** 来存储字符串对的可能计数。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) ，比如 **M** 来存储数组**arr【】**中存在的所有字符串。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，增加 **M** 中**arr【I】**的出现次数。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**中迭代，并执行以下步骤:
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N–1】**中迭代，并执行以下步骤:
        *   将当前一对字符串存储在两个临时字符串中，比如 **p** 和 **q** 。
        *   [交换](https://www.geeksforgeeks.org/swap-in-cpp/)字符串的第一个字符 **p** 和 **q** 。
        *   [如果字符串 **p** 和 **q** 都不在哈希表](https://www.geeksforgeeks.org/map-find-function-in-c-stl/)、 **M** 中，那么将 **ans** 的值增加 **1** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count newly created pairs
// by swapping the first characters of
// any pairs of strings
void countStringPairs(string a[], int n)
{

    // Stores the count all possible
    // pair of strings
    int ans = 0;

    // Push all the strings
    // into the Unordered Map
    unordered_map<string, int> s;
    for (int i = 0; i < n; i++) {
        s[a[i]]++;
    }

    // Generate all possible pairs of
    // strings from the array arr[]
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Store the current
            // pair of strings
            string p = a[i];
            string q = a[j];

            // Swap the first character
            if (p[0] != q[0]) {
                swap(p[0], q[0]);

                // Check if both string
                // are not present in map
                if (s.find(p) == s.end()
                    && s.find(q) == s.end()) {
                    ans++;
                }
            }
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    string arr[] = { "good", "bad", "food" };
    int N = sizeof(arr) / sizeof(arr[0]);
    countStringPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to count newly created pairs
// by swapping the first characters of
// any pairs of strings
static void countStringPairs(String a[], int n)
{

    // Stores the count all possible
    // pair of strings
    int ans = 0;

    // Push all the strings
    // into the Unordered Map
    Map<String, Integer> s = new HashMap<>();
    for(int i = 0; i < n; i++)
    {
        s.put(a[i], s.getOrDefault(a[i], 0));
    }

    // Generate all possible pairs of
    // strings from the array arr[]
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Store the current
            // pair of strings
            StringBuilder p = new StringBuilder(a[i]);
            StringBuilder q = new StringBuilder(a[j]);

            // Swap the first character
            if (p.charAt(0) != q.charAt(0))
            {
                char t = p.charAt(0);
                p.setCharAt(0, q.charAt(0));
                q.setCharAt(0, t);

                // Check if both string
                // are not present in map
                if (!s.containsKey(p.toString()) &&
                    !s.containsKey(q.toString()))
                {
                    ans++;
                }
            }
        }
    }

    // Print the result
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    String arr[] = {"good", "bad", "food"};
    int N = arr.length;

    countStringPairs(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count newly created pairs
# by swapping the first characters of
# any pairs of strings
def countStringPairs(a, n):

    # Stores the count all possible
    # pair of strings
    ans = 0

    # Push all the strings
    # into the Unordered Map
    s = {}
    for i in range(n):
        s[a[i]] = s.get(a[i], 0) + 1

    # Generate all possible pairs of
    # strings from the array arr[]
    for i in range(n):
        for j in range(i + 1, n):

            # Store the current
            # pair of strings
            p = [i for i in a[i]]
            q = [j for j in a[j]]

            # Swap the first character
            if (p[0] != q[0]):
                p[0], q[0] = q[0], p[0]

                # Check if both string
                # are not present in map
                if (("".join(p) not in s) and
                    ("".join(q) not in s)):
                    ans += 1

    # Print the result
    print (ans)

# Driver Code
if __name__ == '__main__':

    arr = [ "good", "bad", "food" ]
    N = len(arr)

    countStringPairs(arr, N)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count newly created pairs
// by swapping the first characters of
// any pairs of strings
function countStringPairs(a, n)
{

    // Stores the count all possible
    // pair of strings
    let ans = 0;

    // Push all the strings
    // into the Unordered Map
    let s = new Map();
    for(let i = 0; i < n; i++)
    {
        if(!s.has(a[i]))
            s.set(a[i],0);
        s.set(a[i], s.get(a[i]) + 1);
    }

    // Generate all possible pairs of
    // strings from the array arr[]
    for(let i = 0; i < n; i++)
    {
        for(let j = i + 1; j < n; j++)
        {

            // Store the current
            // pair of strings
            let p = (a[i]).split("");
            let q = (a[j]).split("");

            // Swap the first character
            if (p[0] != q[0])
            {
                let t = p[0];
                p[0] = q[0];
                q[0] = t;

                // Check if both string
                // are not present in map
                if (!s.has(p.join("")) &&
                    !s.has(q.join("")))
                {
                    ans++;
                }
            }
        }
    }

    // Print the result
    document.write(ans);
}

// Driver code
let arr=["good", "bad", "food"];
let N = arr.length;
countStringPairs(arr, N);

// This code is contributed by avanitrachhadiya2155
</script>
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Function to count newly created pairs
// by swapping the first characters of
// any pairs of strings
static void countStringPairs(string[] a, int n)
{

    // Stores the count all possible
    // pair of strings
    int ans = 0;

    // Push all the strings
    // into the Unordered Map
    Dictionary<string,int> s = new Dictionary<string,int>();
    for(int i = 0; i < n; i++)
    {
        if(!s.ContainsKey(a[i]))
            s.Add(a[i],0);
        s[a[i]]++;
    }

    // Generate all possible pairs of
    // strings from the array arr[]
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Store the current
            // pair of strings
            char[] p = (a[i]).ToCharArray();
            char[] q = (a[j]).ToCharArray();

            // Swap the first character
            if (p[0] != q[0])
            {
                char t = p[0];
                p[0]=q[0];
                q[0]=t;

                // Check if both string
                // are not present in map
                if (!s.ContainsKey(new string(p)) &&
                    !s.ContainsKey(new string(q)))
                {
                    ans++;
                }
            }
        }
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver code
    static public void Main ()
    {

        string[] arr = {"good", "bad", "food"};
    int N = arr.Length;

    countStringPairs(arr, N);

    }
}

// This code is contributed by rag2127.
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*