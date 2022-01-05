# 以非常大的数字打印所有 3 位重复数字

> 原文:[https://www . geesforgeks . org/print-全 3 位重复数字中的数字-非常大的数字/](https://www.geeksforgeeks.org/print-all-3-digit-repeating-numbers-in-a-very-large-number/)

给定一个非常大的数字，打印所有 3 位数重复数字及其频率。如果一个 3 位数出现不止一次，打印该数字及其频率。
**例:**

```
Input: 123412345123456
Output: 123 - 3 times
         234 - 3 times
         345 - 2 times 

Input: 43243243
Output: 432 - 2 times
        324 - 2 times
        243 - 2 times
```

**方法:**由于数量很大，所以存储在一个字符串中。最初，第一个三位数将是左边的前三个字符。从字符串左边的第三个索引开始迭代字符串，并执行%100 删除第一个字符，并在末尾追加第 i <sup>个</sup>索引号，以获得新的数字。增加数字在哈希映射中的出现频率。最后，当所有的 3 位数生成后，打印所有频率大于 1 的数字。
以下是上述想法的实现:

## C++

```
// CPP program to print 3 digit repeating numbers
#include <bits/stdc++.h>
using namespace std;

// function to print 3
// digit repeating numbers
void printNum(string s)
{
    int i = 0, j = 0, val = 0;

    // Hashmap to store the
    // frequency of a 3 digit number
    map <int, int> mp;

    // first three digit number
    val = (s[0] - '0') * 100
            + (s[1] - '0') * 10
            + (s[2] - '0');

    mp[val] = 1;
    for (i = 3; i < s.length(); i++) {
        val = (val % 100) * 10 + s[i] - '0';

        // if key already exists
        // increase value by 1
        if (mp.find(val) != mp.end()) {
            mp[val] = mp[val] + 1;
        }
        else {
            mp[val] = 1;
        }
    }

    // Output the three digit numbers with frequency>1
    for (auto m : mp) {
        int key = m.first;
        int value = m.second;
        if (value > 1)
            cout << key  << " - " << value << " times" << endl;
    }
}

// Driver Code
int main()
{
    // Input string
    string input = "123412345123456";

    // Calling Function
    printNum(input);
}
// This code is contributed by Nishant Tanwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print 3 digit repeating numbers
import java.util.*;
import java.lang.*;

public class GFG {

    // function to print 3
    // digit repeating numbers
    static void printNum(String s)
    {
        int i = 0, j = 0, val = 0;

        // Hashmap to store the
        // frequency of a 3 digit number
        LinkedHashMap<Integer, Integer> hm
            = new LinkedHashMap<>();

        // first three digit number
        val = (s.charAt(0) - '0') * 100
              + (s.charAt(1) - '0') * 10
              + (s.charAt(2) - '0');

        hm.put(val, 1);
        for (i = 3; i < s.length(); i++) {
            val = (val % 100) * 10 + s.charAt(i) - '0';

            // if key already exists
            // increase value by 1
            if (hm.containsKey(val)) {
                hm.put(val, hm.get(val) + 1);
            }
            else {
                hm.put(val, 1);
            }
        }

        // Output the three digit numbers with frequency>1
        for (Map.Entry<Integer, Integer> en : hm.entrySet()) {
            int key = en.getKey();
            int value = en.getValue();
            if (value > 1)
                System.out.println(key + " - " + value + " times");
        }
    }

    // Driver Code
    public static void main(String args[])
    {

        // Input string
        String input = "123412345123456";

        // Calling Function
        printNum(input);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print
# 3 digit repeating numbers

# Function to print 3
# digit repeating numbers
def printNum(s):

    i, j, val = 0, 0, 0

    # Hashmap to store the
    # frequency of a 3 digit number
    mp = {}

    # first three digit number
    val = ((ord(s[0]) - ord('0')) * 100 +
           (ord(s[1]) - ord('0')) * 10 +
           (ord(s[2]) - ord('0')))

    mp[val] = 1
    for i in range (3, len(s)):
        val = (val % 100) * 10 + ord(s[i]) - ord('0')

        # if key already exists
        # increase value by 1
        if (val in mp):
            mp[val] = mp[val] + 1
        else:
            mp[val] = 1

    # Output the three digit
    # numbers with frequency>1
    for m in mp:
        key = m
        value = mp[m]
        if (value > 1):
            print (key, " - ", value, " times")

# Driver Code
if __name__ == "__main__":

    # Input string
    input = "123412345123456"

    # Calling Function
    printNum(input)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to print 3 digit repeating numbers
using System;
using System.Collections.Generic;            

class GFG
{

    // function to print 3
    // digit repeating numbers
    static void printNum(String s)
    {
        int i = 0, val = 0;

        // Hashmap to store the
        // frequency of a 3 digit number
        Dictionary<int,
                   int> hm = new Dictionary<int,
                                            int>();

        // first three digit number
        val = (s[0] - '0') * 100 +
              (s[1] - '0') * 10 +
              (s[2] - '0');

        hm.Add(val, 1);
        for (i = 3; i < s.Length; i++)
        {
            val = (val % 100) * 10 + s[i] - '0';

            // if key already exists
            // increase value by 1
            if (hm.ContainsKey(val))
            {
                hm[val] = hm[val] + 1;
            }
            else
            {
                hm.Add(val, 1);
            }
        }

        // Output the three digit numbers with frequency>1
        foreach(KeyValuePair<int, int> en in hm)
        {
            int key = en.Key;
            int value = en.Value;
            if (value > 1)
                Console.WriteLine(key + " - " +
                                  value + " times");
        }
    }

    // Driver Code
    public static void Main(String []args)
    {

        // Input string
        String input = "123412345123456";

        // Calling Function
        printNum(input);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to print 3 digit repeating numbers

    // function to print 3
    // digit repeating numbers
    function printNum(s)
    {
        let i = 0, j = 0, val = 0;

        // Hashmap to store the
        // frequency of a 3 digit number
        let hm = new Map();

        // first three digit number
        val = (s[0].charCodeAt(0) - '0'.charCodeAt(0)) * 100
              + (s[1].charCodeAt(0) - '0'.charCodeAt(0)) * 10
              + (s[2].charCodeAt(0) - '0'.charCodeAt(0));

        hm.set(val, 1);
        for (i = 3; i < s.length; i++) {
            val = (val % 100) * 10 + s[i].charCodeAt(0) - '0'.charCodeAt(0);

            // if key already exists
            // increase value by 1
            if (hm.has(val)) {
                hm.set(val, hm.get(val) + 1);
            }
            else {
                hm.set(val, 1);
            }
        }

        // Output the three digit numbers with frequency>1
        for (let [Key, Value] of hm.entries()) {
            let key = Key;
            let value = Value;
            if (value > 1)
                document.write(key + " - " + value + " times<br>");
        }
    }

    // Driver Code

    // Input string
    let input = "123412345123456";
    // Calling Function
    printNum(input);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
123 - 3 times
234 - 3 times
345 - 2 times
```