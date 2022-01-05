# 使用每个数字具有相同频率的 N 位旋转形成一个数

> 原文:[https://www . geesforgeks . org/form-a-number-use-bit-rotations-of-n-具有相同频率的每个数字/](https://www.geeksforgeeks.org/form-a-number-using-bit-rotations-of-n-having-same-frequency-of-each-digit/)

给定一个数字 **N** ，任务是通过顺时针或逆时针旋转其位，将其转换为所有不同数字具有相同频率的数字。如果无法将数字转换为 print -1，则打印该数字

**示例:**

> **输入:** N = 331
> **输出:** 421
> **解释:**
> 逆时针旋转后 331: 101001011
> 的二进制表示–421:110100101
> 421 是一个稳定的数字
> 
> **输入:**N = 58993
> T3】输出: 51097

**方法:**思路是旋转数字的位后，检查所有可能的场景。请按照以下步骤解决此问题:

1.  用地图记录数字的频率。
2.  使用一个设置来检查所有频率是否相同。
3.  如果所有数字的频率相同，则将其打印为答案
4.  否则，旋转数字的二进制表示并再次检查。
5.  如果在所有旋转之后，没有发现任何数字具有所有数字的相同频率，则打印-1。

下面是上述方法的表示。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rotate
// the number by one place
int rotate(int N, int bits)
{

    // Getting the least significant bit
    int ls = N & 1;

    // Rotating the number
    return (N >> 1) | (int(pow(2, (bits - 1))) * ls);
}

// Function to check
// if a number is steady or not
bool checkStead(int N)
{

    // Map for the frequency of the digits
    map<char, int> mp;
    for (auto i : to_string(N))
        mp[i]++;

    // Checking if all the
    // frequencies are same or not
    set<int> se;
    for (auto it = mp.begin(); it != mp.end(); ++it)
        se.insert(it->second);
    if (se.size() == 1)
        return true;
    return false;
}

void solve(int N)
{

    // Getting the number of bits needed
    int bits = int(log2(N)) + 1;
    bool flag = true;

    // Checking all the possible numbers
    for (int i = 1; i < bits; ++i) {
        if (checkStead(N)) {
            cout << N << "\n";
            flag = false;
            break;
        }
        N = rotate(N, bits);
    }
    if (flag)
        cout << -1;
}

// Driver Code
int main()
{

    int N = 331;
    solve(N);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.HashMap;
import java.util.HashSet;

class GFG
{

    // Function to rotate
    // the number by one place
    public static int rotate(int N, int bits) {

        // Getting the least significant bit
        int ls = N & 1;

        // Rotating the number
        return (N >> 1) | (int) (Math.pow(2, (bits - 1))) * ls;
    }

    // Function to check
    // if a number is steady or not
public static boolean checkStead(int N)
{

    // Map for the frequency of the digits
    HashMap<String, Integer> mp = new HashMap<String, Integer>();
    for (String i : Integer.toString(N).split("")){
        if(mp.containsKey(i)){
            mp.put(i, mp.get(i) + 1);
        }else{
            mp.put(i, 1);
        }
    }

    // Checking if all the
    // frequencies are same or not
    HashSet<Integer> se = new HashSet<Integer>();
    for (String it : mp.keySet())
        se.add(mp.get(it));
    if (se.size() == 1)
        return true;
    return false;
}

public static void solve(int N)
{

    // Getting the number of bits needed
    int bits = (int)(Math.log(N) / Math.log(2)) + 1;
    boolean flag = true;

    // Checking all the possible numbers
    for (int i = 1; i < bits; ++i) {
        if (checkStead(N)) {
            System.out.println(N);
            flag = false;
            break;
        }
        N = rotate(N, bits);
    }
    if (flag)
        System.out.println(-1);
}

    // Driver Code
    public static void main(String args[]) {

        int N = 331;
        solve(N);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# Python code for the above approach
import math

def solve(N):

    # Getting the number of bits needed
    bits = int(math.log(N, 2))+1
    flag = True

    # Checking all the possible numbers
    for i in range(1, bits):
        if checkStead(N):
            print(N)
            flag = False
            break
        N = rotate(N, bits)

    if flag:
        print(-1)

# Function to rotate
# the number by one place
def rotate(N, bits):

    # Getting the least significant bit
    ls = N & 1

    # Rotating the number
    return (N >> 1) | (2**(bits-1)*ls)

# Function to check
# if a number is steady or not
def checkStead(N):

    # Map for the frequency of the digits
    mp = {}
    for i in str(N):
        if i in mp:
            mp[i] += 1
        else:
            mp[i] = 1

    # Checking if all the
    # frequencies are same or not
    if len(set(mp.values())) == 1:
        return True
    return False

# Driver Code
N = 331
solve(N)
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG {

  // Function to rotate
  // the number by one place
  public static int rotate(int N, int bits)
  {

    // Getting the least significant bit
    int ls = N & 1;

    // Rotating the number
    return (N >> 1)
      | (int)(Math.Pow(2, (bits - 1))) * ls;
  }

  // Function to check
  // if a number is steady or not
  public static bool checkStead(int N)
  {

    // Map for the frequency of the digits
    Dictionary<char, int> mp
      = new Dictionary<char, int>();
    foreach(char i in N.ToString())
    {
      if (mp.ContainsKey(i)) {
        mp[i]++;
      }
      else {
        mp[i] = 1;
      }
    }

    // Checking if all the
    // frequencies are same or not
    HashSet<int> se = new HashSet<int>();
    foreach(KeyValuePair<char, int> it in mp)
      se.Add(it.Value);
    if (se.Count == 1)
      return true;
    return false;
  }

  public static void solve(int N)
  {

    // Getting the number of bits needed
    int bits = (int)(Math.Log(N) / Math.Log(2)) + 1;
    bool flag = true;

    // Checking all the possible numbers
    for (int i = 1; i < bits; ++i) {
      if (checkStead(N)) {
        Console.WriteLine(N);
        flag = false;
        break;
      }
      N = rotate(N, bits);
    }
    if (flag)
      Console.WriteLine(-1);
  }

  // Driver Code
  public static void Main()
  {

    int N = 331;
    solve(N);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript code for the above approach

// Function to check if a number
// is steady or not
function checkStead(N)
{

    // Map for the frequency of the digits
    let mp = new Map();
    let s = [];

    while (N != 0)
    {
        s.push(N % 10);
        N = Math.floor(N / 10)
    }

    for(let i = 0; i < s.length; i++)
    {
        if (mp.has(s[i]))
        {
            mp.set(s[i], mp.get(s[i]) + 1)
        }
        else
        {
            mp.set(s[i], 1);
        }
    }

    // Checking if all the
    // frequencies are same or not
    let st = new Set([...mp.values()]);

    if (st.size == 1)
        return true;
    else
        return false
}

// Function to rotate
// the number by one place
function rotate(N, bits)
{

    // Getting the least significant bit
    let ls = N & 1;

    // Rotating the number
    return ((N >> 1) | (Math.pow(2, bits - 1) * ls))
}

function solve(N)
{

    // Getting the number of bits needed
    let bits = Math.floor(Math.log2(N)) + 1
    let flag = true

    // Checking all the possible numbers
    for(let i = 1; i < bits; i++)
    {
        if (checkStead(N) == 1)
        {
            document.write(N)
            flag = false
            break
        }
        N = rotate(N, bits)
    }

    if (flag)
        document.write(-1)
}

// Driver Code
N = 331

solve(N)

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
421
```

**时间复杂度:**O(log<sub>2</sub>N)
T5】辅助空间: O(log <sub>10</sub> N)