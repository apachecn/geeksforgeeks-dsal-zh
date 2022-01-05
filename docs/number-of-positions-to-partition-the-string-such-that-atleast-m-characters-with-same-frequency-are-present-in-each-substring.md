# 分割字符串的位置数，使得每个子字符串中至少有 m 个相同频率的字符

> 原文:[https://www . geesforgeks . org/对字符串进行分区的位置数，以便每个子字符串中至少有 m 个相同频率的字符/](https://www.geeksforgeeks.org/number-of-positions-to-partition-the-string-such-that-atleast-m-characters-with-same-frequency-are-present-in-each-substring/)

给定一个由小写英文字母组成的字符串和一个整数 T2 m。任务是计算字符串中有多少个位置，这样，如果将字符串划分为两个非空的子字符串，则两个子字符串中至少有 **m** 个频率相同的字符。
字符串**字符串**中需要出现字符。
**举例:**

> **输入:** str = "aabbccaa "，m = 2
> **输出:** 2
> 字符串长度为 8，因此有 7 个位置可以执行分割。
> 即 a|a|b|b|c|c|a|a
> 只有两个满足给定约束的分区是可能的。
> aab | bccaa–在分隔符的左半部分，“a”的频率为 2，“b”的频率为 1
> ，与右半部分相同。
> aabbc | CAA–在分隔符的左半部分，“a”为频率 2，“c”为频率 1
> ，与右半部分相同。
> **输入:** str = "aabbaa "，m = 2
> **输出:** 1

**方法:**对于每个分区位置，计算字符串的每个字符在两个分区中的频率。然后计算两个分区中具有相同频率的字符数。如果此类字符的数量至少为 m，则在所需的分区数量上加 1。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of ways
// to partition the given so that the
// given condition is satisfied
int countWays(string str, int m)
{
    // Hashset to store unique characters
    // in the given string
    set<char> s;
    for (int i = 0; i < str.length(); i++)
        s.insert(str[i]);

    // To store the number of ways
    // to partition the string
    int result = 0;

    for (int i = 1; i < str.length(); i++)
    {
        // Hashmaps to store frequency of characters
        // of both the partitions
        map<char, int> first_map, second_map;

        // Iterate in the first partition
        for (int j = 0; j < i; j++)

            // If character already exists in the hashmap
            // then increase it's frequency
            first_map[str[j]]++;

        // Iterate in the second partition
        for (int k = 0; k < str.length(); k++)

            // If character already exists in the hashmap
            // then increase it's frequency
            second_map[str[k]]++;

        // Iterator for HashSet
        set<char>::iterator itr = s.begin();

        // To store the count of characters that have
        // equal frequencies in both the partitions
        int total_count = 0;
        while (++itr != s.end())
        {
            // first_count and second_count keeps track
            // of the frequencies of each character
            int first_count = 0, second_count = 0;
            char ch = *(itr);

            // Frequency of the character
            // in the first partition
            if (first_map.find(ch) != first_map.end())
                first_count = first_map[ch];

            // Frequency of the character
            // in the second partition
            if (second_map.find(ch) != second_map.end())
                second_count = second_map[ch];

            // Check if frequency is same
            // in both the partitions
            if (first_count == second_count &&
                first_count != 0)
                total_count += 1;
        }

        // Check if the condition is satisfied
        // for the current partition
        if (total_count >= m)
            result += 1;
    }
    return result;
}

// Driver code
int main(int argc, char const *argv[])
{
    string str = "aabbccaa";
    int m = 2;
    cout << countWays(str, m) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the number of ways
    // to partition the given so that the
    // given condition is satisfied
    static int countWays(String str, int m)
    {

        // Hashset to store unique characters
        // in the given string
        HashSet<Character> set = new HashSet<Character>();
        for (int i = 0; i < str.length(); i++)
            set.add(str.charAt(i));

        // To store the number of ways
        // to partition the string
        int result = 0;

        for (int i = 1; i < str.length(); i++) {

            // Hashmaps to store frequency of characters
            // of both the partitions
            HashMap<Character, Integer> first_map
                = new HashMap<Character, Integer>();
            HashMap<Character, Integer> second_map
                = new HashMap<Character, Integer>();

            // Iterate in the first partition
            for (int j = 0; j < i; j++) {

                // If character already exists in the hashmap
                // then increase it's frequency
                if (first_map.containsKey(str.charAt(j)))
                    first_map.put(str.charAt(j),
                                  (first_map.get(str.charAt(j)) + 1));

                // Else create an entry for it in the Hashmap
                else
                    first_map.put(str.charAt(j), 1);
            }

            // Iterate in the second partition
            for (int k = i; k < str.length(); k++) {

                // If character already exists in the hashmap
                // then increase it's frequency
                if (second_map.containsKey(str.charAt(k)))
                    second_map.put(str.charAt(k),
                                   (second_map.get(str.charAt(k)) + 1));

                // Else create an entry for it in the Hashmap
                else
                    second_map.put(str.charAt(k), 1);
            }

            // Iterator for HashSet
            Iterator itr = set.iterator();

            // To store the count of characters that have
            // equal frequencies in both the partitions
            int total_count = 0;

            while (itr.hasNext()) {

                // first_count and second_count keeps track
                // of the frequencies of each character
                int first_count = 0, second_count = 0;
                char ch = (char)itr.next();

                // Frequency of the character
                // in the first partition
                if (first_map.containsKey(ch))
                    first_count = first_map.get(ch);

                // Frequency of the character
                // in the second partition
                if (second_map.containsKey(ch))
                    second_count = second_map.get(ch);

                // Check if frequency is same in both the partitions
                if (first_count == second_count && first_count != 0)
                    total_count += 1;
            }

            // Check if the condition is satisfied
            // for the current partition
            if (total_count >= m)
                result += 1;
        }

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "aabbccaa";
        int m = 2;
        System.out.println(countWays(str, m));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict

# Function to return the number of ways
# to partition the given so that the
# given condition is satisfied
def countWays(string, m):

    # Hashset to store unique
    # characters in the given string
    Set = set()
    for i in range(0, len(string)):
        Set.add(string[i])

    # To store the number of ways
    # to partition the string
    result = 0

    for i in range(1, len(string)):

        # Hashmaps to store frequency of
        # characters of both the partitions
        first_map = defaultdict(lambda:0)
        second_map = defaultdict(lambda:0)

        # Iterate in the first partition
        for j in range(0, i):

            first_map[string[j]] += 1

        # Iterate in the second partition
        for k in range(i, len(string)):

            second_map[string[k]] += 1

        # To store the count of characters that have
        # equal frequencies in both the partitions
        total_count = 0

        for ch in Set:

            # first_count and second_count keeps track
            # of the frequencies of each character
            first_count, second_count = 0, 0

            # Frequency of the character
            # in the first partition
            if ch in first_map:
                first_count = first_map[ch]

            # Frequency of the character
            # in the second partition
            if ch in second_map:
                second_count = second_map[ch]

            # Check if frequency is same in both the partitions
            if first_count == second_count and first_count != 0:
                total_count += 1

        # Check if the condition is satisfied
        # for the current partition
        if total_count >= m:
            result += 1

    return result

# Driver code
if __name__ == "__main__":

    string = "aabbccaa"
    m = 2
    print(countWays(string, m))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to return the number of ways
    // to partition the given so that the
    // given condition is satisfied
    static int countWays(String str, int m)
    {

        // Hashset to store unique characters
        // in the given string
        HashSet<char> set = new HashSet<char>();
        for (int i = 0; i < str.Length; i++)
            set.Add(str[i]);

        // To store the number of ways
        // to partition the string
        int result = 0;

        for (int i = 1; i < str.Length; i++) {

            // Hashmaps to store frequency of characters
            // of both the partitions
            Dictionary<char, int> first_map
                = new Dictionary<char, int>();
            Dictionary<char, int> second_map
                = new Dictionary<char, int>();

            // Iterate in the first partition
            for (int j = 0; j < i; j++) {

                // If character already exists in the hashmap
                // then increase it's frequency
                if (first_map.ContainsKey(str[j]))
                    first_map[str[j]] =
                                  (first_map[str[j]] + 1);

                // Else create an entry for it in the Hashmap
                else
                    first_map.Add(str[j], 1);
            }

            // Iterate in the second partition
            for (int k = i; k < str.Length; k++) {

                // If character already exists in the hashmap
                // then increase it's frequency
                if (second_map.ContainsKey(str[k]))
                    second_map[str[k]] =
                                   (second_map[str[k]] + 1);

                // Else create an entry for it in the Hashmap
                else
                    second_map.Add(str[k], 1);
            }

            // To store the count of characters that have
            // equal frequencies in both the partitions
            int total_count = 0;
             // Iterator for HashSet
            foreach (int itr in set) {

                // first_count and second_count keeps track
                // of the frequencies of each character
                int first_count = 0, second_count = 0;
                char ch = (char)itr;

                // Frequency of the character
                // in the first partition
                if (first_map.ContainsKey(ch))
                    first_count = first_map[ch];

                // Frequency of the character
                // in the second partition
                if (second_map.ContainsKey(ch))
                    second_count = second_map[ch];

                // Check if frequency is same in both the partitions
                if (first_count == second_count && first_count != 0)
                    total_count += 1;
            }

            // Check if the condition is satisfied
            // for the current partition
            if (total_count >= m)
                result += 1;
        }

        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "aabbccaa";
        int m = 2;
        Console.WriteLine(countWays(str, m));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of ways
// to partition the given so that the
// given condition is satisfied
function countWays(str, m)
{
    // Hashset to store unique characters
    // in the given string
    var s = new Set();
    for (var i = 0; i < str.length; i++)
        s.add(str[i]);

    // To store the number of ways
    // to partition the string
    var result = 0;

    for (var i = 1; i < str.length; i++)
    {
        // Hashmaps to store frequency of characters
        // of both the partitions
        var first_map = new Map(), second_map = new Map();

        // Iterate in the first partition
        for (var j = 0; j < i; j++)

            // If character already exists in the hashmap
            // then increase it's frequency
            if(first_map.has(str[j]))
                first_map.set(str[j], first_map.get(str[j])+1)
            else
                first_map.set(str[j], 1)

        // Iterate in the second partition
        for (var k = 0; k < str.length; k++)

            // If character already exists in the hashmap
            // then increase it's frequency
            if(second_map.has(str[k]))
                second_map.set(str[k], second_map.get(str[k])+1)
            else
                second_map.set(str[k], 1)

        // To store the count of characters that have
        // equal frequencies in both the partitions
        var total_count = 0;
        s.forEach(itr => {

            // first_count and second_count keeps track
            // of the frequencies of each character
            var first_count = 0, second_count = 0;
            var ch = itr;

            // Frequency of the character
            // in the first partition
            if (first_map.has(ch))
                first_count = first_map.get(ch);

            // Frequency of the character
            // in the second partition
            if (second_map.has(ch))
                second_count = second_map.get(ch);

            // Check if frequency is same
            // in both the partitions
            if (first_count == second_count &&
                first_count != 0)
                total_count += 1;
        });

        // Check if the condition is satisfied
        // for the current partition
        if (total_count >= m)
            result += 1;
    }
    return result;
}

// Driver code
var str = "aabbccaa";
var m = 2;
document.write( countWays(str, m));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
2
```