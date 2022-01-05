# 去除相邻重复后，查找 N 位数字排序形成的数字

> 原文:[https://www . geesforgeks . org/find-number-by-sorting-digits-of-n-after-near-duplicates/](https://www.geeksforgeeks.org/find-number-formed-by-sorting-digits-of-n-after-removing-adjacent-duplicates/)

给定一个数字 **N** ，任务是删除一个数字 **N** 的相邻副本，然后按降序对数字 **N** 的数字进行排序。

**示例:**

> **输入:**N = 11123134
> T3】输出: 433211
> 
> **输入:**N = 22133455
> T3】输出: 54321

**方法:**按照以下步骤解决以下问题:

1.  创建一个地图来存储所有字符的频率，比如 **mp** 。
2.  创建一个函数**获取数字**，它将接受一个整数作为参数，并以字符串的形式返回它。
3.  对该字符串进行迭代，只增加在前一个索引中没有重复的数字的频率。
4.  在地图 **mp** 上迭代，创建一个整数字符串，该字符串将自动按排序顺序排列。
5.  将该字符串转换为整数，并相应地打印答案。

下面是上述方法的实现。

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to change integer N to string
string getDigits(int N) { return to_string(N); }

// Function to remove the adjacent duplicates
// of a number N and then sort the digits
// of the number N in decreasing order
int getSolution(int N)
{
    string s = getDigits(N);
    if (s.size() == 1) {
        return stoi(s);
    }

    map<int, int> mp;
    for (int i = 1; i < s.size(); ++i) {
        if (s[i] != s[i - 1]) {
            mp[s[i - 1] - '0']++;
        }
    }

    mp[s[s.size() - 1] - '0']++;

    // Creating the number
    int mul = 1;
    int ans = 0;
    for (auto x : mp) {
        for (int i = 0; i < x.second; i++) {
            ans += x.first * mul;
            mul *= 10;
        }
    }

    // Returning the created number
    return ans;
}

// Driver Code
int main()
{
    int N = 11123134;
    cout << getSolution(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to change integer N to String
static String getDigits(int N) { return String.valueOf(N); }

// Function to remove the adjacent duplicates
// of a number N and then sort the digits
// of the number N in decreasing order
static int getSolution(int N)
{
    char []s = getDigits(N).toCharArray();
    if (s.length == 1) {
        return Integer.valueOf(String.valueOf(s));
    }

    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();
    for (int i = 1; i < s.length; ++i) {
        if (s[i] != s[i - 1]) {
            if(mp.containsKey(s[i - 1] - '0')){
                mp.put(s[i - 1] - '0', mp.get(s[i - 1] - '0')+1);
            }
            else
                mp.put(s[i - 1] - '0', 1);
        }
    }

    if(mp.containsKey(s[s.length - 1] - '0')){
        mp.put(s[s.length - 1] - '0', mp.get(s[s.length - 1] - '0')+1);
    }
    else
        mp.put(s[s.length - 1] - '0', 1);

    // Creating the number
    int mul = 1;
    int ans = 0;
    for (Map.Entry<Integer,Integer> x : mp.entrySet()) {
        for (int i = 0; i < x.getValue(); i++) {
            ans += x.getKey() * mul;
            mul *= 10;
        }
    }

    // Returning the created number
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 11123134;
    System.out.print(getSolution(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to change integer N to string
def getDigits(N) :
    return str(N);

# Function to remove the adjacent duplicates
# of a number N and then sort the digits
# of the number N in decreasing order
def getSolution(N):
    s = getDigits(N);

    if (len(s) == 1):
        return int(s);

    mp = {}
    for i in range(1, len(s)):
        if (s[i] != s[i - 1]):
            if ((ord(s[i - 1]) -  ord('0')) in mp):
                mp[ord(s[i - 1]) -  ord('0')] += 1;
            else:
                mp[ord(s[i - 1]) - ord('0')] =  1;

    if (s[-1] in mp):
        mp[ord(s[-1]) -  ord('0')]  += 1
    else:
        mp[ord(s[-1]) -  ord('0')]  = 1

    # Creating the number
    mul = 1;
    ans = 0;

    for x in mp:
        for i in range(mp[x]):
            ans = ans + x * mul;
            mul = mul * 10;

    # Returning the created number
    return ans;

# Driver Code
N = 11123134;

print(getSolution(N));

# This code is contributed by gfgking
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to change integer N to String
static string getDigits(int N)
{
    return (N).ToString();
}

// Function to remove the adjacent duplicates
// of a number N and then sort the digits
// of the number N in decreasing order
static int getSolution(int N)
{
    char[] s = getDigits(N).ToCharArray();

    if (s.Length == 1)
    {
        return Int32.Parse((s).ToString());
    }

    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    for(int i = 1; i < s.Length; ++i)
    {
        if (s[i] != s[i - 1])
        {
            if (mp.ContainsKey(s[i - 1] - '0'))
            {
                mp[s[i - 1] - '0']++;
            }
            else
                mp[s[i - 1] - '0'] = 1;
        }
    }

    if (mp.ContainsKey(s[s.Length - 1] - '0'))
    {
        mp[s[s.Length - 1] - '0'] += 1;
    }
    else
        mp[s[s.Length - 1] - '0'] = 1;

    // Creating the number
    int mul = 1;
    int ans = 0;
    foreach(KeyValuePair<int, int> x in mp)
    {
        for(int i = 0; i < x.Value; i++)
        {
            ans += x.Key * mul;
            mul *= 10;
        }
    }

    // Returning the created number
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 11123134;

    Console.WriteLine(getSolution(N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript code for the above approach

// Function to change integer N to string
function getDigits(N)
{
    return N.toString();
}

// Function to remove the adjacent duplicates
// of a number N and then sort the digits
// of the number N in decreasing order
function getSolution(N)
{
    let s = getDigits(N);

    if (s.length == 1)
    {
        return parseInt(s);
    }

    let mp = new Map();
    for(let i = 1; i < s.length; ++i)
    {
        if (s[i] != s[i - 1])
        {
            if (mp.has(s[i - 1].charCodeAt(0) -
                            '0'.charCodeAt(0)))
            {
                mp.set(s[i - 1].charCodeAt(0) -
                            '0'.charCodeAt(0),
                mp.get(s[i - 1].charCodeAt(0) -
                            '0'.charCodeAt(0)) + 1);
            }
            else
            {
                mp.set(s[i - 1].charAt(0) -
                            '0'.charAt(0), 1);
            }
        }
    }
    if (mp.has(s[s.length - 1]))
        mp.set(s[s.length - 1].charCodeAt(0) -
                           '0'.charCodeAt(0),
        mp.get(s[s.length - 1].charCodeAt(0) -
                           '0'.charCodeAt(0)) + 1);
    else
        mp.set(s[s.length - 1].charCodeAt(0) -
                           '0'.charCodeAt(0), 1)

    // Creating the number
    let mul = 1;
    let ans = 0;

    for(let [key, value] of mp)
    {
        for(let i = 0; i < value; i++)
        {
            ans = ans + key * mul;
            mul = mul * 10;
        }
    }

    // Returning the created number
    return ans;
}

// Driver Code
let N = 11123134;

document.write(getSolution(N));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
433211
```

**时间复杂度:**O(logN)
T3】辅助空间: O(1)