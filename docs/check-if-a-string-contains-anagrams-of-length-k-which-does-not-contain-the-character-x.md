# 检查字符串是否包含长度为 K 的不包含字符 X 的字谜

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-长度-k-其中不包含字符-x/](https://www.geeksforgeeks.org/check-if-a-string-contains-anagrams-of-length-k-which-does-not-contain-the-character-x/)

给定一个字符串 **S** ，任务是检查 S 是否包含一对长度为 **K** 的子字符串，它们是彼此的[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)，并且其中不包含字符 **X** 。如果不存在这样的子串，打印 **-1** 。

**示例:**

> **输入:** S = "geeksforgeeks "，X = 'f '，K = 5
> **输出:**geeks geeks
> T6】解释:
> Substrings“geeks”和“geeks”互为字谜，不含' f '。
> 
> **输入:** S =“旋转体”，X =‘a’，K = 3
> **输出:** rot tor
> **解释:**
> 子串“rot”和“tor”互为字谜，不含‘a’。

**方法:**
思路是在字符的基础上生成 [**前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 。按照以下步骤解决问题:

*   使用**前缀和数组**迭代字符串并生成子字符串的频率。
*   如果在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中已经存在具有相同字符频率的子串。
*   否则，如果子串中字符 **X** 的频率为 **0** ，则将当前子串所在子串的字符频率存储在 **HashMap** 中。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

// Class to represent a Substring
// in terms of frequency of
// characters present in it
class Substring {
    int MOD = 1000000007;

    // Store count of characters
    int count[];
    Substring() { count = new int[26]; }

    public int hashCode()
    {
        int hash = 0;
        for (int i = 0; i < 26; i++) {
            hash += (i + 1) * count[i];
            hash %= MOD;
        }
        return hash;
    }

    public boolean equals(Object o)
    {
        if (o == this)
            return true;
        if (!(o instanceof Substring))
            return false;
        Substring ob = (Substring)o;
        for (int i = 0; i < 26; i++) {
            if (ob.count[i] != count[i])
                return false;
        }
        return true;
    }
}
class GFG {

    // Function to check anagrams
    static void checkForAnagrams(String s, int n,
                                 char X, int k)
    {
        boolean found = false;

        // Prefix array to store frequencies
        // of characters
        int prefix[][] = new int[n + 1][26];
        for (int i = 0; i < n; i++) {
            prefix[i][s.charAt(i) - 97]++;
        }

        // Generate prefix sum
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < 26; j++)
                prefix[i][j] += prefix[i - 1][j];
        }

        // Map to store frequencies
        HashMap<Substring, Integer> map
            = new HashMap<>();

        // Check for anagrams
        for (int i = 0; i < n; i++) {
            if (i + k > n)
                break;

            // Generate frequencies of characters
            // of substring starting from i
            Substring sub = new Substring();
            for (int j = 0; j < 26; j++) {
                sub.count[j]
                    = prefix[i + k - 1][j]
                      - (i - 1 >= 0
                             ? prefix[i - 1][j]
                             : 0);
            }

            // Check if forbidden character is
            // present, then continue
            if (sub.count[X - 97] != 0)
                continue;

            // If already present in HashMap
            if (map.containsKey(sub)) {

                found = true;

                // Print the substrings
                System.out.println(
                    s.substring(map.get(sub),
                                map.get(sub) + k)
                    + " " + s.substring(i, i + k));
                break;
            }
            else {
                map.put(sub, i);
            }
        }

        // If no such substring is found
        if (!found)
            System.out.println("-1");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "rotator";
        int n = s.length();
        char X = 'a';
        int k = 3;
        checkForAnagrams(s, n, X, k);
    }
}
```

**Output:** 

```
rot tor
```

***时间复杂度:** O(N*26)*
***辅助空间:** O(N*26)*