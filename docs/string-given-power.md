# 找到给定功率的子串

> 原文:[https://www.geeksforgeeks.org/string-given-power/](https://www.geeksforgeeks.org/string-given-power/)

给定一串小写字母，任务是找到给定幂的子串的索引。假设 a 的幂是 1，b 是 2，c 是 3，以此类推。这里，子串的幂指的是该特定子串中所有字符的幂之和。
**例:**

> 输入:str = "geeksforgeeks "幂= 36
> 输出:从索引 3 到 5 的子串有幂 36
> 说明:k = 11，s = 19，f = 6 即 k + s + e = 36。
> 输入:str = "aditya "幂= 2
> 输出:不存在给定幂的子串。

**简单方法:**
1。使用嵌套 for 循环计算所有子字符串的幂。
2。如果任何子串的幂等于给定的幂，则打印该子串的索引。
3。如果不存在这样的子串，则打印“不存在具有给定功率的子串”。
**时间复杂度:** O(北^ 2)。
**高效进场:**使用地图储存异能。
1。对于每个元素，检查 curr _ power–power 是否存在于映射中。
2。如果它存在于映射中，这意味着我们有一个给定幂的子串，否则我们将 curr_power 插入到映射中，并继续下一个字符。
3。如果字符串的所有字符都被处理了，而我们没有找到任何给定幂的子串，那么子串就不存在。

## C++

```
// C++ program to find substring with given power
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to print indexes of substring with
// power as given power.
void findSubstring(string str, ll power)
{
    ll i;
    // Create an empty map
    unordered_map<ll, ll> map;

    // Maintains sum of powers of characters so far.
    int curr_power = 0;
    int len = str.length();

    for (i = 0; i < len; i++) {
        // Add current character power to curr_power.
        curr_power = curr_power + (str[i] - 'a' + 1);

        // If curr_power is equal to target power
        // we found a substring starting from index 0
        // and ending at index i.
        if (curr_power == power) {
            cout << "Substring from index " << 0 << " to "
                 << i << " has power " << power << endl;
            return;
        }

        // If curr_power - power already exists in map
        // then we have found a subarray with target power.
        if (map.find(curr_power - power) != map.end()) {
            cout << "Substring from index "
                 << map[curr_power - power] + 1
                 << " to " << i <<" has power " <<power << endl;
            return;
        }

        map[curr_power] = i;
    }

    // If we reach here, then no substring exists.
    cout << "No substring with given power exists.";
}

// Drivers code
int main()
{
    string str = "geeksforgeeks";
    ll power = 36;

    findSubstring(str, power);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find substring with given power
import java.util.*;

class GFG
{

    // Function to print indexes of substring with
    // power as given power.
    static void findSubstring(String str, int power)
    {

        // Create an empty map
        HashMap<Integer,
                Integer> map = new HashMap<>();

        // Maintains sum of powers of characters so far.
        int curr_power = 0;
        int len = str.length();

        for (int i = 0; i < len; i++)
        {

            // Add current character power to curr_power.
            curr_power = curr_power + (str.charAt(i) - 'a' + 1);

            // If curr_power is equal to target power
            // we found a substring starting from index 0
            // and ending at index i.
            if (curr_power == power)
            {
                System.out.println("Substring from index 0" +
                                   " to " + i + " has power " + power);
                return;
            }

            // If curr_power - power already exists in map
            // then we have found a subarray with target power.
            if (map.containsKey(curr_power - power))
            {
                System.out.println("Substring from index " +
                                  (map.get(curr_power - power) + 1) +
                                 " to " + i + " has power " + power);
                return;
            }

            map.put(curr_power, i);
        }

        // If we reach here, then no substring exists.
        System.out.println("No substring with given power exists.");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int power = 36;

        findSubstring(str, power);
    }
}

// This code is contributed by
// sanjeev2552
```

## C#

```
// C# program to find substring
// with given power
using System;
using System.Collections.Generic;

class GFG
{

    // Function to print indexes of substring
    // with power as given power.
    static void findSubstring(String str,
                              int power)
    {

        // Create an empty map
        Dictionary<int,
                   int> map = new Dictionary<int,
                                             int>();

        // Maintains sum of powers
        // of characters so far.
        int curr_power = 0;
        int len = str.Length;

        for (int i = 0; i < len; i++)
        {

            // Add current character power
            // to curr_power.
            curr_power = curr_power +
                        (str[i] - 'a' + 1);

            // If curr_power is equal to target power
            // we found a substring starting from index 0
            // and ending at index i.
            if (curr_power == power)
            {
                Console.WriteLine("Substring from index 0" +
                                  " to " + i +
                                  " has power " + power);
                return;
            }

            // If curr_power - power already exists in map
            // then we have found a subarray with target power.
            if (map.ContainsKey(curr_power - power))
            {
                Console.WriteLine("Substring from index " +
                            (map[curr_power - power] + 1) +
                       " to " + i + " has power " + power);
                return;
            }

            if (!map.ContainsKey(curr_power))
                    map.Add(curr_power, i);
            else
                map[curr_power] = i;
        }

        // If we reach here, then no substring exists.
        Console.WriteLine("No substring with " +
                          "given power exists");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        int power = 36;

        findSubstring(str, power);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find substring with given power

// Function to print indexes of substring with
    // power as given power.
function findSubstring(str,power)
{
    let  map = new Map();

        // Maintains sum of powers of characters so far.
        let curr_power = 0;
        let len = str.length;

        for (let i = 0; i < len; i++)
        {

            // Add current character power to curr_power.
            curr_power = curr_power + (str[i].charCodeAt(0) - 'a'.charCodeAt(0) + 1);

            // If curr_power is equal to target power
            // we found a substring starting from index 0
            // and ending at index i.
            if (curr_power == power)
            {
                document.write("Substring from index 0" +
                                   " to " + i + " has power " + power+"<br>");
                return;
            }

            // If curr_power - power already exists in map
            // then we have found a subarray with target power.
            if (map.has(curr_power - power))
            {
                document.write("Substring from index " +
                                  (map.get(curr_power - power) + 1) +
                                 " to " + i + " has power " + power+"<br>");
                return;
            }

            map.set(curr_power, i);
        }

        // If we reach here, then no substring exists.
        document.write("No substring with given power exists.<br>");
}

// Driver Code
let str = "geeksforgeeks";
let power = 36;

findSubstring(str, power);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Substring from index 3 to 5 has power 36
```

**时间复杂度:** O (n)