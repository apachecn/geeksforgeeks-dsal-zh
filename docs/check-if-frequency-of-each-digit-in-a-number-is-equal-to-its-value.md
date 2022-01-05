# 检查数字中每个数字的频率是否等于其值

> 原文:[https://www . geesforgeks . org/检查数字中每个数字的频率是否等于其值/](https://www.geeksforgeeks.org/check-if-frequency-of-each-digit-in-a-number-is-equal-to-its-value/)

给定一个数字 **N** 任务是检查一个数字中每个数字的频率是否等于它的值
**示例:**

> **输入** : N = 3331
> **输出**:是
> **解释**:3 的频率为 3，1 的频率为 1
> **输入** : N = 121
> **输出**:否
> **解释**:1 的频率为 2，2 的频率为 1，不是有效数字

**逼近**:将一个数字的频率存储在 [hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中，然后迭代 hashmap 检查该数字的频率是否等于它的值，就可以解决这个任务。
以下是上述办法的实施情况:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number
// is valid or not
void check(int N)
{
    // Stores the frequencies
    // of digits
    unordered_map<char, int> occ;

    while (N > 0) {

        // Extracting the digits
        int r = N % 10;

        // Incrementing the frequency
        occ[r]++;

        N /= 10;
    }

    // Iterating the hashmap
    for (auto i : occ) {

        // Check if frequency of digit
        // is equal to its value or not
        if (i.first != i.second) {
            cout << "No\n";
            return;
        }
    }
    cout << "Yes\n";
}
int main()
{
    int N = 3331;
    check(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.HashMap;
import java.util.Map;

class GFG
{

    // Function to check if the number
    // is valid or not
    public static void check(Integer N)
    {

        // Stores the frequencies
        // of digits
        HashMap<Integer, Integer> occ = new HashMap<>();

        while (N > 0) {

            // Extracting the digits
            Integer r = N % 10;
            if (occ.containsKey(r)) {

                // If char is present in charCountMap,
                // incrementing it's count by 1
                occ.put(r, occ.get(r) + 1);
            }
            else {

                // If char is not present in charCountMap,
                // putting this char to charCountMap with 1
                // as it's value
                occ.put(r, 1);
            }
            N = N / 10;
        }
        for (Map.Entry<Integer, Integer> e :
             occ.entrySet()) {
            if (e.getKey() != e.getValue()) {
                System.out.print("NO");
                return;
            }
        }

        System.out.print("Yes");
    }

  // Driver code
    public static void main(String[] args)
    {

        Integer N = 3331;
        check(N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if the number
# is valid or not
def check(N):

  # Stores the frequencies
  # of digits
  occ = dict();

  while (N > 0):

    # Extracting the digits
    r = N % 10;

    # Incrementing the frequency
    if r in occ:
      occ[r] += 1
    else:
      occ[r] = 1

    N = N // 10

  # Iterating the hashmap
  for i in occ.keys():

    # Check if frequency of digit
    # is equal to its value or not
    if (i != occ[i]):
      print("No");
      return;

  print("Yes");

N = 3331;
check(N);

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to check if the number
    // is valid or not
    public static void check(int N)
    {

        // Stores the frequencies
        // of digits
        Dictionary<int, int> occ = new Dictionary<int, int>();

        while (N > 0) {

            // Extracting the digits
            int r = N % 10;
            if (occ.ContainsKey(r)) {

                // If char is present in charCountMap,
                // incrementing it's count by 1
                occ[r] = occ[r] + 1;
            }
            else {

                // If char is not present in charCountMap,
                // putting this char to charCountMap with 1
                // as it's value
                occ.Add(r, 1);
            }
            N = N / 10;
        }
        foreach(int key in occ.Keys) {
            if (key != occ[key]) {
                Console.Write("NO");
                return;
            }
        }

        Console.Write("Yes");
    }

  // Driver code
    public static void Main()
    {

        int N = 3331;
        check(N);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if the number
// is valid or not
function check(N) {
  // Stores the frequencies
  // of digits
  let occ = new Map();

  while (N > 0) {

    // Extracting the digits
    let r = N % 10;

    // Incrementing the frequency
    if(occ.has(r)){
      occ.set(r, occ.get(r) + 1)
    }else{
      occ.set(r, 1)
    }

    N = Math.floor(N / 10);
  }

  // Iterating the hashmap
  for (i of occ) {

    // Check if frequency of digit
    // is equal to its value or not
    if (i[0] != i[1]) {
      document.write("No<br>");
      return;
    }
  }
  document.write("Yes<br>");
}
let N = 3331;
check(N);
</script>
```

**Output**

```
Yes
```

***时间复杂度*** : O(D)，D = N 中的位数
***辅助空间*** : O(D)