# 两组弦中的成对完整弦

> 原文:[https://www . geeksforgeeks . org/成对完整的两组字符串/](https://www.geeksforgeeks.org/pairs-of-complete-strings-in-two-sets-of-strings/)

如果两个字符串串联在一起，它们包含所有 26 个英文字母，则称为完整字符串。例如，“abcdefghi”和“jklmnopqrstuvwxyz”是完整的，因为它们一起具有从“a”到“z”的所有字符。
我们分别得到两组大小为 n 和 m 的字符串，我们需要找到将集合 1 中的每一个字符串连接到集合 2 中的每一个字符串时完成的对的数量。

```
Input : set1[] = {"abcdefgh", "geeksforgeeks",
                 "lmnopqrst", "abc"}
        set2[] = {"ijklmnopqrstuvwxyz", 
                 "abcdefghijklmnopqrstuvwxyz", 
                 "defghijklmnopqrstuvwxyz"} 
Output : 7
The total complete pairs that are forming are:
"abcdefghijklmnopqrstuvwxyz"
"abcdefghabcdefghijklmnopqrstuvwxyz"
"abcdefghdefghijklmnopqrstuvwxyz"
"geeksforgeeksabcdefghijklmnopqrstuvwxyz"
"lmnopqrstabcdefghijklmnopqrstuvwxyz"
"abcabcdefghijklmnopqrstuvwxyz"
"abcdefghijklmnopqrstuvwxyz"
```

**方法 1 (Naive 方法)**
一个简单的解决方案是考虑所有字符串对，将它们连接起来，然后通过使用频率数组检查连接的字符串是否具有从“A”到“z”的所有字符。

## C++

```
// C++ implementation for find pairs of complete
// strings.
#include <iostream>
using namespace std;

// Returns count of complete pairs from set[0..n-1]
// and set2[0..m-1]
int countCompletePairs(string set1[], string set2[],
                       int n, int m)
{
    int result = 0;

    // Consider all pairs of both strings
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            // Create a concatenation of current pair
            string concat = set1[i] + set2[j];

            // Compute frequencies of all characters
            // in the concatenated string.
            int frequency[26] = { 0 };
            for (int k = 0; k < concat.length(); k++)
                frequency[concat[k] - 'a']++;

            // If frequency of any character is not
            // greater than 0, then this pair is not
            // complete.
            int i;
            for (i = 0; i < 26; i++)
                if (frequency[i] < 1)
                    break;
            if (i == 26)
                result++;
        }
    }

    return result;
}

// Driver code
int main()
{
    string set1[] = { "abcdefgh", "geeksforgeeks",
                      "lmnopqrst", "abc" };
    string set2[] = { "ijklmnopqrstuvwxyz",
                      "abcdefghijklmnopqrstuvwxyz",
                      "defghijklmnopqrstuvwxyz" };
    int n = sizeof(set1) / sizeof(set1[0]);
    int m = sizeof(set2) / sizeof(set2[0]);

    cout << countCompletePairs(set1, set2, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for find pairs of complete
// strings.

class GFG {

    // Returns count of complete pairs from set[0..n-1]
    // and set2[0..m-1]
    static int countCompletePairs(String set1[], String set2[],
                                  int n, int m)
    {
        int result = 0;

        // Consider all pairs of both strings
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // Create a concatenation of current pair
                String concat = set1[i] + set2[j];

                // Compute frequencies of all characters
                // in the concatenated String.
                int frequency[] = new int[26];
                for (int k = 0; k < concat.length(); k++) {
                    frequency[concat.charAt(k) - 'a']++;
                }

                // If frequency of any character is not
                // greater than 0, then this pair is not
                // complete.
                int k;
                for (k = 0; k < 26; k++) {
                    if (frequency[k] < 1) {
                        break;
                    }
                }
                if (k == 26) {
                    result++;
                }
            }
        }

        return result;
    }

    // Driver code
    static public void main(String[] args)
    {
        String set1[] = { "abcdefgh", "geeksforgeeks",
                          "lmnopqrst", "abc" };
        String set2[] = { "ijklmnopqrstuvwxyz",
                          "abcdefghijklmnopqrstuvwxyz",
                          "defghijklmnopqrstuvwxyz" };
        int n = set1.length;
        int m = set2.length;

        System.out.println(countCompletePairs(set1, set2, n, m));
    }
}

// This code is contributed by PrinciRaj19992
```

蟒蛇 3

```
 # Python3 implementation for find pairs 
# of complete strings.

# Returns count of complete pairs 
# from set[0..n-1] and set2[0..m-1]
def countCompletePairs(set1: list, set2: list, 
                              n: int, m: int) -> int:
    result = 0

    # Consider all pairs of both strings
    for i in range(n):
        for j in range(m):

            # Create a concatenation of current pair
            concat = set1[i] + set2[j]

            # Compute frequencies of all characters
            # in the concatenated string.
            frequency = [0] * 26
            for k in range(len(concat)):
                frequency[ord(concat[k]) - ord('a')] += 1

            # If frequency of any character is not
            # greater than 0, then this pair is not
            # complete.
            k = 0
            while k < 26:
                if frequency[k] < 1:
                    break
                k += 1
            if k == 26:
                result += 1

    return result

# Driver Code
if __name__ == "__main__":
    set1 = ["abcdefgh", "geeksforgeeks", 
            "lmnopqrst", "abc"]
    set2 = ["ijklmnopqrstuvwxyz", 
            "abcdefghijklmnopqrstuvwxyz",
            "defghijklmnopqrstuvwxyz"]

    n = len(set1)
    m = len(set2)

    print(countCompletePairs(set1, set2, n, m))

# This code is contributed by
# sanjeev2552 
```

## C#

```
// C# implementation for find pairs of complete
// strings.

using System;
class GFG {

    // Returns count of complete pairs from set[0..n-1]
    // and set2[0..m-1]
    static int countCompletePairs(string[] set1, string[] set2,
                                  int n, int m)
    {
        int result = 0;

        // Consider all pairs of both strings
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // Create a concatenation of current pair
                string concat = set1[i] + set2[j];

                // Compute frequencies of all characters
                // in the concatenated String.
                int[] frequency = new int[26];
                for (int k = 0; k < concat.Length; k++) {
                    frequency[concat[k] - 'a']++;
                }

                // If frequency of any character is not
                // greater than 0, then this pair is not
                // complete.
                int l;
                for (l = 0; l < 26; l++) {
                    if (frequency[l] < 1) {
                        break;
                    }
                }
                if (l == 26) {
                    result++;
                }
            }
        }

        return result;
    }

    // Driver code
    static public void Main()
    {
        string[] set1 = { "abcdefgh", "geeksforgeeks",
                          "lmnopqrst", "abc" };
        string[] set2 = { "ijklmnopqrstuvwxyz",
                          "abcdefghijklmnopqrstuvwxyz",
                          "defghijklmnopqrstuvwxyz" };
        int n = set1.Length;
        int m = set2.Length;

        Console.Write(countCompletePairs(set1, set2, n, m));
    }
}
// This article is contributed by Ita_c.
```

## java 描述语言

```
<script>

// Javascript implementation for find pairs of complete
// strings. 

    // Returns count of complete pairs from set[0..n-1]
    // and set2[0..m-1]
    function countCompletePairs(set1,set2,n,m)
    {
        let result = 0;

        // Consider all pairs of both strings
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                // Create a concatenation of current pair
                let concat = set1[i] + set2[j];

                // Compute frequencies of all characters
                // in the concatenated String.
                let frequency = new Array(26);
                for(let i= 0;i<26;i++)
                {
                    frequency[i]=0;
                }

                for (let k = 0; k < concat.length; k++) {
                    frequency[concat[k].charCodeAt(0) - 'a'.charCodeAt(0)]++;
                }

                // If frequency of any character is not
                // greater than 0, then this pair is not
                // complete.
                let k;
                for (k = 0; k < 26; k++) {
                    if (frequency[k] < 1) {
                        break;
                    }
                }
                if (k == 26) {
                    result++;
                }
            }
        }

        return result;
    }

    // Driver code     
    let set1=["abcdefgh", "geeksforgeeks",
                          "lmnopqrst", "abc"];
    let set2=["ijklmnopqrstuvwxyz",
                          "abcdefghijklmnopqrstuvwxyz",
                          "defghijklmnopqrstuvwxyz"]
    let n = set1.length;
    let m=set2.length;
    document.write(countCompletePairs(set1, set2, n, m));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
7
```

时间复杂度:0(n * m * k)

辅助空间:0(1)

**方法 2(使用位操作的优化方法)**
在该方法中，我们将频率数组压缩为整数。我们为该整数的每个位分配一个字符，当找到该字符时，我们将其设置为 1。我们对两组中的所有字符串执行此操作。最后，我们只需比较集合中的两个整数，如果组合所有的位，它们就形成了一个完整的字符串对。

## C++14

```
// C++ program to find count of complete pairs
#include <iostream>
using namespace std;

// Returns count of complete pairs from set[0..n-1]
// and set2[0..m-1]
int countCompletePairs(string set1[], string set2[],
                       int n, int m)
{
    int result = 0;

    // con_s1[i] is going to store an integer whose
    // set bits represent presence/absence of characters
    // in string set1[i].
    // Similarly con_s2[i] is going to store an integer
    // whose set bits represent presence/absence of
    // characters in string set2[i]
    int con_s1[n], con_s2[m];

    // Process all strings in set1[]
    for (int i = 0; i < n; i++) {
        // initializing all bits to 0
        con_s1[i] = 0;
        for (int j = 0; j < set1[i].length(); j++) {
            // Setting the ascii code of char s[i][j]
            // to 1 in the compressed integer.
            con_s1[i] = con_s1[i] | (1 << (set1[i][j] - 'a'));
        }
    }

    // Process all strings in set2[]
    for (int i = 0; i < m; i++) {
        // initializing all bits to 0
        con_s2[i] = 0;
        for (int j = 0; j < set2[i].length(); j++) {
            // setting the ascii code of char s[i][j]
            // to 1 in the compressed integer.
            con_s2[i] = con_s2[i] | (1 << (set2[i][j] - 'a'));
        }
    }

    // assigning a variable whose all 26 (0..25)
    // bits are set to 1
    long long complete = (1 << 26) - 1;

    // Now consider every pair of integer in con_s1[]
    // and con_s2[] and check if the pair is complete.
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            // if all bits are set, the strings are
            // complete!
            if ((con_s1[i] | con_s2[j]) == complete)
                result++;
        }
    }

    return result;
}

// Driver code
int main()
{
    string set1[] = { "abcdefgh", "geeksforgeeks",
                      "lmnopqrst", "abc" };
    string set2[] = { "ijklmnopqrstuvwxyz",
                      "abcdefghijklmnopqrstuvwxyz",
                      "defghijklmnopqrstuvwxyz" };
    int n = sizeof(set1) / sizeof(set1[0]);
    int m = sizeof(set2) / sizeof(set2[0]);

    cout << countCompletePairs(set1, set2, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of complete pairs
class GFG {

    // Returns count of complete pairs from set[0..n-1]
    // and set2[0..m-1]
    static int countCompletePairs(String set1[], String set2[],
                                  int n, int m)
    {
        int result = 0;

        // con_s1[i] is going to store an integer whose
        // set bits represent presence/absence of characters
        // in string set1[i].
        // Similarly con_s2[i] is going to store an integer
        // whose set bits represent presence/absence of
        // characters in string set2[i]
        int[] con_s1 = new int[n];
        int[] con_s2 = new int[m];

        // Process all strings in set1[]
        for (int i = 0; i < n; i++) {

            // initializing all bits to 0
            con_s1[i] = 0;
            for (int j = 0; j < set1[i].length(); j++) {

                // Setting the ascii code of char s[i][j]
                // to 1 in the compressed integer.
                con_s1[i] = con_s1[i] | (1 << (set1[i].charAt(j) - 'a'));
            }
        }

        // Process all strings in set2[]
        for (int i = 0; i < m; i++) {

            // initializing all bits to 0
            con_s2[i] = 0;
            for (int j = 0; j < set2[i].length(); j++) {

                // setting the ascii code of char s[i][j]
                // to 1 in the compressed integer.
                con_s2[i] = con_s2[i] | (1 << (set2[i].charAt(j) - 'a'));
            }
        }

        // assigning a variable whose all 26 (0..25)
        // bits are set to 1
        long complete = (1 << 26) - 1;

        // Now consider every pair of integer in con_s1[]
        // and con_s2[] and check if the pair is complete.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // if all bits are set, the strings are
                // complete!
                if ((con_s1[i] | con_s2[j]) == complete) {
                    result++;
                }
            }
        }

        return result;
    }

    // Driver code
    public static void main(String args[])
    {
        String set1[] = { "abcdefgh", "geeksforgeeks",
                          "lmnopqrst", "abc" };
        String set2[] = { "ijklmnopqrstuvwxyz",
                          "abcdefghijklmnopqrstuvwxyz",
                          "defghijklmnopqrstuvwxyz" };
        int n = set1.length;
        int m = set2.length;

        System.out.println(countCompletePairs(set1, set2, n, m));
    }
}

// This code contributed by Rajput-Ji
```

## C#

```
// C# program to find count of complete pairs
using System;

class GFG {

    // Returns count of complete pairs from set[0..n-1]
    // and set2[0..m-1]
    static int countCompletePairs(String[] set1, String[] set2,
                                  int n, int m)
    {
        int result = 0;

        // con_s1[i] is going to store an integer whose
        // set bits represent presence/absence of characters
        // in string set1[i].
        // Similarly con_s2[i] is going to store an integer
        // whose set bits represent presence/absence of
        // characters in string set2[i]
        int[] con_s1 = new int[n];
        int[] con_s2 = new int[m];

        // Process all strings in set1[]
        for (int i = 0; i < n; i++) {

            // initializing all bits to 0
            con_s1[i] = 0;
            for (int j = 0; j < set1[i].Length; j++) {

                // Setting the ascii code of char s[i][j]
                // to 1 in the compressed integer.
                con_s1[i] = con_s1[i] | (1 << (set1[i][j] - 'a'));
            }
        }

        // Process all strings in set2[]
        for (int i = 0; i < m; i++) {

            // initializing all bits to 0
            con_s2[i] = 0;
            for (int j = 0; j < set2[i].Length; j++) {

                // setting the ascii code of char s[i][j]
                // to 1 in the compressed integer.
                con_s2[i] = con_s2[i] | (1 << (set2[i][j] - 'a'));
            }
        }

        // assigning a variable whose all 26 (0..25)
        // bits are set to 1
        long complete = (1 << 26) - 1;

        // Now consider every pair of integer in con_s1[]
        // and con_s2[] and check if the pair is complete.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // if all bits are set, the strings are
                // complete!
                if ((con_s1[i] | con_s2[j]) == complete) {
                    result++;
                }
            }
        }

        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String[] set1 = { "abcdefgh", "geeksforgeeks",
                          "lmnopqrst", "abc" };
        String[] set2 = { "ijklmnopqrstuvwxyz",
                          "abcdefghijklmnopqrstuvwxyz",
                          "defghijklmnopqrstuvwxyz" };
        int n = set1.Length;
        int m = set2.Length;

        Console.WriteLine(countCompletePairs(set1, set2, n, m));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find count of complete pairs

# Returns count of complete pairs from set[0..n-1]
# and set2[0..m-1]
def countCompletePairs(set1, set2, n, m):
    result = 0

    # con_s1[i] is going to store an integer whose
    # set bits represent presence/absence of characters
    # in set1[i].
    # Similarly con_s2[i] is going to store an integer
    # whose set bits represent presence/absence of
    # characters in set2[i]
    con_s1, con_s2 = [0] * n, [0] * m

    # Process all strings in set1[]
    for i in range(n):

        # initializing all bits to 0
        con_s1[i] = 0
        for j in range(len(set1[i])):

            # Setting the ascii code of char s[i][j]
            # to 1 in the compressed integer.
            con_s1[i] = con_s1[i] | (1 << (ord(set1[i][j]) - ord('a')))

    # Process all strings in set2[]
    for i in range(m):

        # initializing all bits to 0
        con_s2[i] = 0
        for j in range(len(set2[i])):

            # setting the ascii code of char s[i][j]
            # to 1 in the compressed integer.
            con_s2[i] = con_s2[i] | (1 << (ord(set2[i][j]) - ord('a')))

    # assigning a variable whose all 26 (0..25)
    # bits are set to 1
    complete = (1 << 26) - 1

    # Now consider every pair of integer in con_s1[]
    # and con_s2[] and check if the pair is complete.
    for i in range(n):
        for j in range(m):

            # if all bits are set, the strings are
            # complete!
            if ((con_s1[i] | con_s2[j]) == complete):
                result += 1

    return result

# Driver code
if __name__ == '__main__':
    set1 = ["abcdefgh", "geeksforgeeks",
            "lmnopqrst", "abc"]
    set2 = ["ijklmnopqrstuvwxyz",
            "abcdefghijklmnopqrstuvwxyz",
            "defghijklmnopqrstuvwxyz"]
    n = len(set1)
    m = len(set2)

    print(countCompletePairs(set1, set2, n, m))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program to find count of complete pairs

    // Returns count of complete pairs from set[0..n-1]
    // and set2[0..m-1]
    function countCompletePairs(set1,set2,n,m)
    {
        let result = 0;

        // con_s1[i] is going to store an integer whose
        // set bits represent presence/absence of characters
        // in string set1[i].
        // Similarly con_s2[i] is going to store an integer
        // whose set bits represent presence/absence of
        // characters in string set2[i]
        let con_s1 = new Array(n);
        let con_s2 = new Array(m);

        // Process all strings in set1[]
        for (let i = 0; i < n; i++) {

            // initializing all bits to 0
            con_s1[i] = 0;
            for (let j = 0; j < set1[i].length; j++) {

                // Setting the ascii code of char s[i][j]
                // to 1 in the compressed integer.
                con_s1[i] = con_s1[i] |
                (1 << (set1[i][j].charCodeAt(0) - 'a'.charCodeAt(0)));
            }
        }

        // Process all strings in set2[]
        for (let i = 0; i < m; i++) {

            // initializing all bits to 0
            con_s2[i] = 0;
            for (let j = 0; j < set2[i].length; j++) {

                // setting the ascii code of char s[i][j]
                // to 1 in the compressed integer.
                con_s2[i] = con_s2[i] |
                (1 << (set2[i][j].charCodeAt(0) - 'a'.charCodeAt(0)));
            }
        }

        // assigning a variable whose all 26 (0..25)
        // bits are set to 1
        let complete = (1 << 26) - 1;

        // Now consider every pair of integer in con_s1[]
        // and con_s2[] and check if the pair is complete.
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {

                // if all bits are set, the strings are
                // complete!
                if ((con_s1[i] | con_s2[j]) == complete) {
                    result++;
                }
            }
        }

        return result;
    }

    // Driver code
    let set1=["abcdefgh", "geeksforgeeks",
                          "lmnopqrst", "abc"];
    let set2=["ijklmnopqrstuvwxyz",
                          "abcdefghijklmnopqrstuvwxyz",
                          "defghijklmnopqrstuvwxyz" ]
    let n = set1.length;
    let m = set2.length;
    document.write(countCompletePairs(set1, set2, n, m));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
7
```

时间复杂度:0(n)

辅助空间:O(n)

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。