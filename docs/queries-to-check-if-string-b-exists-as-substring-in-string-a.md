# 查询字符串 B 是否作为子字符串存在于字符串 A 中

> 原文:[https://www . geesforgeks . org/query-to-check-if-string-b-exists-as-substring-in-string-a/](https://www.geeksforgeeks.org/queries-to-check-if-string-b-exists-as-substring-in-string-a/)

给定两个字符串 **A** 、 **B** 和一些由整数 **i** 组成的查询，任务是检查从索引 **i** 开始到索引 **i +长度(B)–1**的子字符串是否等于 B。如果相等，则打印**是**否则打印**否**。**注意****I+长度(B)** 永远小于**长度(A)** 。

**示例:**

> **输入:** A = "abababa "，B = "aba "，q[] = {0，1，2，3}
> **输出:**T5】是
> 否
> 是
> 否
> a[0-2] = "aba" = b(两者相等)
> a[1-3] = "bab "！= b
> a[2-4]= " ABA " = b
> a[3-5]= " Bab "！=b
> 
> **输入:** A = "GeeksForGeeks "，B = "Geeks "，q[] = {0，5，8 }
> T3】输出:T5】是
> 否
> 是

一种简单的方法是对每个查询逐个字符地比较字符串，回答每个查询需要 O(长度(B))个时间。

**高效方法:**我们将使用[滚动哈希](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)算法优化查询处理。
首先，我们将找到字符串 b 的哈希值。然后，使用滚动哈希技术，我们将对字符串 a 进行预处理。
假设我们创建了一个数组 hash_A。然后，该数组的第一个元素将存储。

> ((a[0]–97)+(a[1]–97)* d+(a[2]–97)* d<sup>2</sup>+…..+(a[I]–97)* d<sup>I</sup>)% mod
> 其中 d 是滚动哈希中的乘数。

我们将使用它来查找 a 的子字符串的散列。

从 I 开始的子串 A 的散列可以被发现为(hash _ A[I+len _ b–1]–hash _ A[I–1])/d<sup>I</sup>或者更具体地

> ((hash _ a[I+len _ b–1]-hash _ a[I–1]+2 * mod)* mi(d<sup>I</sup>))% mod

因此，使用这个我们可以回答 O(1)中的每个查询。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define mod 3803
#define d 26
using namespace std;

int hash_b;
int* hash_a;
int* mul;

// Function to return the modular inverse
// using Fermat's little theorem
int mi(int x)
{
    int p = mod - 2;
    int s = 1;
    while (p != 1) {
        if (p % 2 == 1)
            s = (s * x) % mod;
        x = (x * x) % mod;
        p /= 2;
    }

    return (s * x) % mod;
}

// Function to generate hash
void genHash(string& a, string& b)
{
    // To store prefix-sum
    // of rolling hash
    hash_a = new int[a.size()];

    // Multiplier for different values of i
    mul = new int[a.size()];

    // Generating hash value for string b
    for (int i = b.size() - 1; i >= 0; i--)
        hash_b = (hash_b * d + (b[i] - 97)) % mod;

    // Generating prefix-sum of hash of a
    mul[0] = 1;
    hash_a[0] = (a[0] - 97) % mod;
    for (int i = 1; i < a.size(); i++) {
        mul[i] = (mul[i - 1] * d) % mod;
        hash_a[i]
            = (hash_a[i - 1] + mul[i] * (a[i] - 97)) % mod;
    }
}

// Function that returns true if the
// required sub-string in a is equal to b
bool checkEqual(int i, int len_a, int len_b)
{
    // To store hash of required
    // sub-string of A
    int x;

    // If i = 0 then
    // requires hash value
    if (i == 0)
        x = hash_a[len_b - 1];

    // Required hash if i != 0
    else {
        x = (hash_a[i + len_b - 1] - hash_a[i - 1]
             + 2 * mod)
            % mod;
        x = (x * mi(mul[i])) % mod;
    }

    // Comparing hash with hash of B
    if (x == hash_b)
        return true;

    return false;
}

// Driver code
int main()
{
    string a = "abababababa";
    string b = "aba";

    // Generating hash
    genHash(a, b);

    // Queries
    int queries[] = { 0, 1, 2, 3 };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Perform queries
    for (int i = 0; i < q; i++) {
        if (checkEqual(queries[i], a.size(), b.size()))
            cout << "Yes\n";
        else
            cout << "No\n";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    static int mod = 3803;
    static int d = 26;

    static int hash_b;
    static int[] hash_a;
    static int[] mul;

    // Function to return the modular inverse
    // using Fermat's little theorem
    static int mi(int x)
    {
        int p = mod - 2;
        int s = 1;
        while (p != 1) {
            if (p % 2 == 1) {
                s = (s * x) % mod;
            }
            x = (x * x) % mod;
            p /= 2;
        }

        return (s * x) % mod;
    }

    // Function to generate hash
    static void genHash(char[] a, char[] b)
    {
        // To store prefix-sum
        // of rolling hash
        hash_a = new int[a.length];

        // Multiplier for different values of i
        mul = new int[a.length];

        // Generating hash value for string b
        for (int i = b.length - 1; i >= 0; i--) {
            hash_b = (hash_b * d + (b[i] - 97)) % mod;
        }

        // Generating prefix-sum of hash of a
        mul[0] = 1;
        hash_a[0] = (a[0] - 97) % mod;
        for (int i = 1; i < a.length; i++) {
            mul[i] = (mul[i - 1] * d) % mod;
            hash_a[i]
                = (hash_a[i - 1] + mul[i] * (a[i] - 97))
                  % mod;
        }
    }

    // Function that returns true if the
    // required sub-string in a is equal to b
    static boolean checkEqual(int i, int len_a, int len_b)
    {
        // To store hash of required
        // sub-string of A
        int x;

        // If i = 0 then
        // requires hash value
        if (i == 0) {
            x = hash_a[len_b - 1];
        }
        // Required hash if i != 0
        else {
            x = (hash_a[i + len_b - 1] - hash_a[i - 1]
                 + 2 * mod)
                % mod;
            x = (x * mi(mul[i])) % mod;
        }

        // Comparing hash with hash of B
        if (x == hash_b) {
            return true;
        }

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "abababababa";
        String b = "aba";

        // Generating hash
        genHash(a.toCharArray(), b.toCharArray());

        // Queries
        int queries[] = { 0, 1, 2, 3 };
        int q = queries.length;

        // Perform queries
        for (int i = 0; i < q; i++) {
            if (checkEqual(queries[i], a.length(),
                           b.length())) {
                System.out.println("Yes");
            }
            else {
                System.out.println("No");
            }
        }
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 3803
d = 26

hash_b = 0
hash_a = []
mul = []

# Function to return the modular inverse
# using Fermat's little theorem

def mi(x):
    global mod
    p = mod - 2
    s = 1
    while p != 1:
        if p % 2 == 1:
            s = (s * x) % mod

        x = (x * x) % mod
        p //= 2

    return (s * x) % mod

# Function to generate hash

def genHash(a, b):
    global hash_b, hash_a, mul, d, mod

    # To store prefix-sum
    # of rolling hash
    hash_a = [0] * len(a)

    # Multiplier for different values of i
    mul = [0] * len(a)

    # Generating hash value for string b
    for i in range(len(b) - 1, -1, -1):
        hash_b = (hash_b * d +
                  (ord(b[i]) - 97)) % mod

    # Generating prefix-sum of hash of a
    mul[0] = 1
    hash_a[0] = (ord(a[0]) - 97) % mod
    for i in range(1, len(a)):
        mul[i] = (mul[i - 1] * d) % mod
        hash_a[i] = (hash_a[i - 1] + mul[i] *
                     (ord(a[i]) - 97)) % mod

# Function that returns true if the
# required sub-string in a is equal to b

def checkEqual(i, len_a, len_b):
    global hash_b, hash_a, mul, d, mod

    # To store hash of required
    # sub-string of A
    x = -1

    # If i = 0 then
    # requires hash value
    if i == 0:
        x = hash_a[len_b - 1]

    # Required hash if i != 0
    else:
        x = (hash_a[i + len_b - 1] -
             hash_a[i - 1] + 2 * mod) % mod
        x = (x * mi(mul[i])) % mod

    # Comparing hash with hash of B
    if x == hash_b:
        return True

    return False

# Driver Code
if __name__ == "__main__":
    a = "abababababa"
    b = "aba"

    # Generating hash
    genHash(a, b)

    # Queries
    queries = [0, 1, 2, 3]
    q = len(queries)

    # Perform queries
    for i in range(q):
        if checkEqual(queries[i], len(a), len(b)):
            print("Yes")
        else:
            print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    static int mod = 3803;
    static int d = 26;

    static int hash_b;
    static int[] hash_a;
    static int[] mul;

    // Function to return the modular inverse
    // using Fermat's little theorem
    static int mi(int x)
    {
        int p = mod - 2;
        int s = 1;
        while (p != 1) {
            if (p % 2 == 1) {
                s = (s * x) % mod;
            }
            x = (x * x) % mod;
            p /= 2;
        }

        return (s * x) % mod;
    }

    // Function to generate hash
    static void genHash(char[] a, char[] b)
    {
        // To store prefix-sum
        // of rolling hash
        hash_a = new int[a.Length];

        // Multiplier for different values of i
        mul = new int[a.Length];

        // Generating hash value for string b
        for (int i = b.Length - 1; i >= 0; i--) {
            hash_b = (hash_b * d + (b[i] - 97)) % mod;
        }

        // Generating prefix-sum of hash of a
        mul[0] = 1;
        hash_a[0] = (a[0] - 97) % mod;
        for (int i = 1; i < a.Length; i++) {
            mul[i] = (mul[i - 1] * d) % mod;
            hash_a[i]
                = (hash_a[i - 1] + mul[i] * (a[i] - 97))
                  % mod;
        }
    }

    // Function that returns true if the
    // required sub-string in a is equal to b
    static Boolean checkEqual(int i, int len_a, int len_b)
    {
        // To store hash of required
        // sub-string of A
        int x;

        // If i = 0 then
        // requires hash value
        if (i == 0) {
            x = hash_a[len_b - 1];
        }
        // Required hash if i != 0
        else {
            x = (hash_a[i + len_b - 1] - hash_a[i - 1]
                 + 2 * mod)
                % mod;
            x = (x * mi(mul[i])) % mod;
        }

        // Comparing hash with hash of B
        if (x == hash_b) {
            return true;
        }

        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String a = "abababababa";
        String b = "aba";

        // Generating hash
        genHash(a.ToCharArray(), b.ToCharArray());

        // Queries
        int[] queries = { 0, 1, 2, 3 };
        int q = queries.Length;

        // Perform queries
        for (int i = 0; i < q; i++) {
            if (checkEqual(queries[i], a.Length,
                           b.Length)) {
                Console.WriteLine("Yes");
            }
            else {
                Console.WriteLine("No");
            }
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var mod = 3803;
var d = 26;

var hash_b = 0;
var hash_a = [];
var mul = [];

// Function to return the modular inverse
// using Fermat's little theorem
function mi(x)
{
    var p = mod - 2;
    var s = 1;
    while (p != 1) {
        if (p % 2 == 1)
            s = (s * x) % mod;
        x = (x * x) % mod;
        p = parseInt(p/2);
    }

    return (s * x) % mod;
}

// Function to generate hash
function genHash(a, b)
{
    // To store prefix-sum
    // of rolling hash
    hash_a = Array(a.length).fill(0);

    // Multiplier for different values of i
    mul = Array(a.length).fill(0);

    // Generating hash value for string b
    for (var i = b.length - 1; i >= 0; i--)
        hash_b = (hash_b * d + (b[i].charCodeAt(0) - 97)) % mod;

    // Generating prefix-sum of hash of a
    mul[0] = 1;
    hash_a[0] = (a[0].charCodeAt(0) - 97) % mod;
    for (var i = 1; i < a.length; i++) {
        mul[i] = (mul[i - 1] * d) % mod;
        hash_a[i]
            = (hash_a[i - 1] + mul[i] * (a[i].charCodeAt(0) - 97)) % mod;
    }
}

// Function that returns true if the
// required sub-string in a is equal to b
function checkEqual(i, len_a, len_b)
{
    // To store hash of required
    // sub-string of A
    var x;

    // If i = 0 then
    // requires hash value
    if (i == 0)
        x = hash_a[len_b - 1];

    // Required hash if i != 0
    else {
        x = (hash_a[i + len_b - 1] - hash_a[i - 1]
             + 2 * mod)
            % mod;
        x = (x * mi(mul[i])) % mod;
    }

    // Comparing hash with hash of B
    if (x == hash_b)
        return true;

    return false;
}

// Driver code
var a = "abababababa";
var b = "aba";

// Generating hash
genHash(a.split(''), b.split(''));

// Queries
var queries = [0, 1, 2, 3];
var q = queries.length

// Perform queries
for (var i = 0; i < q; i++) {
    if (checkEqual(queries[i], a.length, b.length))
        document.write("Yes<br>");
    else
    document.write("No<br>");
}

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
Yes
No
Yes
No
```

**注意:**为了简单起见，我们只使用了一个哈希函数。使用双重/三重散列来消除任何冲突的机会和更准确的结果。

上面的问题也可以用 DP 来解决，下面是 java 代码。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
import java.lang.*;
import java.io.*;

public class GFG
{
    private static void
    substringCheck(String stra, String strb, int[] query)
    {

        // Dp Array
        int[][] matrix
            = new int[strb.length()][stra.length()];

        // String to character array
        char[] charCrr = stra.toCharArray();
        char[] charRrr = strb.toCharArray();

        // initialize matrix with 1
        for (int c = 0; c < stra.length(); c++)
        {
            if (charRrr[0] == charCrr)
            {
                matrix[0] = 1;
            }
        }

        // for r from 1 to string length
        for (int r = 1; r < charRrr.length; r++)
        {
            char ch = charRrr[r];

            // for c from 1 b string length
            for (int c = 1; c < charCrr.length; c++)
            {
                if (ch == charCrr
                    && matrix[r - 1] == 1)
                {
                    matrix[r] = 1;
                }
            }
        }

        // For every query
        for (int q : query)
        {
            int matLoc = (q + (strb.length() - 1));
            if (matLoc >= stra.length()) {
                System.out.println(false);
            }
            else
            {
                // print true
                if (matrix[strb.length() - 1][matLoc]
                    == 1)
                {
                    System.out.println(true);
                }
                else
                {
                    // print false
                    System.out.println(false);
                }
            }
        }

    }

    // Driver Code
    public static void main(String[] args)
    {
        String stra = "GeeksForGeeks";
        String strb = "Geeks";
        int[] query = { 0,5,8 };
        substringCheck(stra, strb, query);
    }

} // class
// Code contributed by Swapnil Gupta
```

## C#

```
using System;

public class GFG {
    private static void
    substringCheck(string stra, string strb, int[] query)
    {

        // Dp Array
        int[, ] matrix = new int[strb.Length, stra.Length];

        // String to character array
        char[] charCrr = stra.ToCharArray();
        char[] charRrr = strb.ToCharArray();

        // initialize matrix with 1
        for (int c = 0; c < stra.Length; c++) {
            if (charRrr[0] == charCrr) {
                matrix[0, c] = 1;
            }
        }

        // for r from 1 to string length
        for (int r = 1; r < charRrr.Length; r++) {
            char ch = charRrr[r];

            // for c from 1 b string length
            for (int c = 1; c < charCrr.Length; c++) {
                if (ch == charCrr
                    && matrix[r - 1, c - 1] == 1) {
                    matrix[r, c] = 1;
                }
            }
        }

        // For every query
        foreach(int q in query)
        {
            int matLoc = (q + (strb.Length - 1));
            if (matLoc >= stra.Length) {
                Console.WriteLine(false);
            }
            else {
                // print true
                if (matrix[strb.Length - 1, matLoc] == 1) {
                    Console.WriteLine(true);
                }
                else {
                    // print false
                    Console.WriteLine(false);
                }
            }
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string stra = "GeeksForGeeks";
        string strb = "Geeks";
        int[] query = { 0, 5, 8 };
        substringCheck(stra, strb, query);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

function substringCheck(stra, strb, query)
{
    // Dp Array
    var matrix = Array.from(Array(strb.length), ()=>Array(stra.length));

    // String to character array
    var charCrr = stra.split('');
    var charRrr = strb.split('');
    // initialize matrix with 1
    for (var c = 0; c < stra.length; c++)
    {
        if (charRrr[0] == charCrr)
        {
            matrix[0] = 1;
        }
    }
    // for r from 1 to string length
    for (var r = 1; r < charRrr.length; r++)
    {
        var ch = charRrr[r];
        // for c from 1 b string length
        for (var c = 1; c < charCrr.length; c++)
        {
            if (ch == charCrr
                && matrix[r - 1] == 1)
            {
                matrix[r] = 1;
            }
        }
    }
    // For every query
    for (var q of query)
    {
        var matLoc = (q + (strb.length - 1));
        if (matLoc >= stra.length) {
            document.write(false + "<br>");
        }
        else
        {
            // print true
            if (matrix[strb.length - 1][matLoc]
                == 1)
            {
                document.write(true+ "<br>");
            }
            else
            {
                // print false
                document.write(false+ "<br>");
            }
        }
    }
}

// Driver Code
var stra = "GeeksForGeeks";
var strb = "Geeks";
var query = [0,5,8];
substringCheck(stra, strb, query);

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
true
false
true
```

**时间复杂度:** O(M*N)