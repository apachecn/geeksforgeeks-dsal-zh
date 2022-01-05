# 找到发光时间最长的灯泡

> 原文:[https://www . geeksforgeeks . org/find-最大发光时间灯泡/](https://www.geeksforgeeks.org/find-the-light-bulb-with-maximum-glowing-time/)

给定一个字符串 **S** ，该字符串由 **N** 个唯一的小写字母和一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**组成，其中字符**S【I】**代表灯泡，**arr【I】**代表 **i <sup>th</sup>** 灯泡发光的时间，从**arr【I–1】**开始。任务是找到发光时间最长的灯泡。如果有一个以上的灯泡具有相同的最大发光时间，则打印字典中较大的一个。

**示例:**

> **输入:**S =“ABCD”，arr[] = {9，29，49，50}
> **输出:** c
> **说明:**
> 索引 0 处的‘c’持续时间= 9。索引 1 处的
> “b”的持续时间= arr[1]–arr[0]= 29–9 = 20
> “c”在索引 2 处的持续时间= arr[2]–arr[1]= 49–29 = 20
> “d”在索引 3 处的持续时间= arr[3]–arr[2]= 50–49 = 1
> 两个灯泡“b”和“c”的发光时间最长。在这两个当中，c 在字典上更大。
> 
> **输入:** S =“开钻”，arr[] = {12，23，36，46，62}
> **输出:** a
> **说明:**
> S 在索引 0 处的持续时间= 12。
> 索引 1 处的“p”的持续时间= arr[1]–arr[0]= 23-12 = 11。
> 索引 2 处的“u”的持续时间= arr[2]–arr[1]= 36-23 = 13。
> 索引 3 处的“d”的持续时间= arr[3]–arr[2]= 46-36 = 10。
> “a”在索引 4 处的持续时间= arr[4]–arr[3]= 62-46 = 16。
> 因此，‘a’的发光时间最长。

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，计算**arr[I]–arr[I–1]**。然后，打印字典上最大发光时间的较大灯泡。按照以下步骤解决问题:

*   初始化两个变量，比如 **maxDur** 和 **maxPos** ，分别存储发光时间和发光时间最长的灯泡的指数。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
    *   如果当前时间**(arr[I]–arr[I–1])**小于 **maxCurr** ，则将 **maxCurr** 更新为**maxCurr = arr[I]–arr[I–1]**。
    *   否则，如果等于 **maxCurr** ， **maxPos** 不包含任何有效索引，**S【maxPos】**在字典上小于**S【I】**，则更新 **maxPos** 为 **maxPos = i** 。
*   完成上述步骤后，打印**S【maxPos】**作为所需输出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the bulb
// having maximum glow
char longestLastingBulb(
    vector<int> onTime, string s)
{
    char ans;
    int n = onTime.size();

    // Initialize variables
    int maxDur = INT_MIN;
    int maxPos = INT_MIN;
    int currentDiff = 0;

    // Traverse the array consisting
    // of glowing time of the bulbs
    for (int i = 0; i < n; i++) {

        // For 1st bulb
        if (i == 0) {
            currentDiff = onTime[i];
            maxDur = currentDiff;
            maxPos = i;
        }
        else {

            // Calculate the glowing time
            currentDiff = onTime[i]
                          - onTime[i - 1];

            // Update the maximum glow
            if (maxDur < currentDiff) {
                maxDur = currentDiff;
                maxPos = i;
            }

            // Find lexicographically
            // largest bulb
            else {

                if (maxDur == currentDiff) {
                    char one = s[i];
                    char two = s[maxPos];

                    if (one > two) {
                        maxDur = currentDiff;
                        maxPos = i;
                    }
                }
            }
        }
    }

    // Bulb with maximum time
    ans = s[maxPos];

    // Return the resultant bulb
    return ans;
}

// Driver Code
int main()
{
    string S = "spuda";
    vector<int> arr = { 12, 23, 36, 46, 62 };

    // Function call
    cout << longestLastingBulb(arr, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the bulb
// having maximum glow
static char longestLastingBulb(
    int []onTime, char []s)
{
    char ans;
    int n = onTime.length;

    // Initialize variables
    int maxDur = Integer.MIN_VALUE;
    int maxPos = Integer.MIN_VALUE;
    int currentDiff = 0;

    // Traverse the array consisting
    // of glowing time of the bulbs
    for (int i = 0; i < n; i++) {

        // For 1st bulb
        if (i == 0) {
            currentDiff = onTime[i];
            maxDur = currentDiff;
            maxPos = i;
        }
        else {

            // Calculate the glowing time
            currentDiff = onTime[i]
                          - onTime[i - 1];

            // Update the maximum glow
            if (maxDur < currentDiff) {
                maxDur = currentDiff;
                maxPos = i;
            }

            // Find lexicographically
            // largest bulb
            else {

                if (maxDur == currentDiff) {
                    char one = s[i];
                    char two = s[maxPos];

                    if (one > two) {
                        maxDur = currentDiff;
                        maxPos = i;
                    }
                }
            }
        }
    }

    // Bulb with maximum time
    ans = s[maxPos];

    // Return the resultant bulb
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String S = "spuda";
    int []arr = { 12, 23, 36, 46, 62 };

    // Function call
    System.out.print(longestLastingBulb(arr, S.toCharArray()));

}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

INT_MIN = (sys.maxsize - 1)

# Function to find the bulb
# having maximum glow
def longestLastingBulb(onTime, s):

    n = len(onTime)

    # Initialize variables
    maxDur = INT_MIN
    maxPos = INT_MIN
    currentDiff = 0

    # Traverse the array consisting
    # of glowing time of the bulbs
    for i in range(n):

        # For 1st bulb
        if (i == 0):
            currentDiff = onTime[i]
            maxDur = currentDiff
            maxPos = i

        else:

            # Calculate the glowing time
            currentDiff = onTime[i] - onTime[i - 1]

            # Update the maximum glow
            if (maxDur < currentDiff):
                maxDur = currentDiff
                maxPos = i

            # Find lexicographically
            # largest bulb
            else:

                if (maxDur == currentDiff):
                    one = s[i]
                    two = s[maxPos]

                    if (one > two):
                        maxDur = currentDiff
                        maxPos = i

    # Bulb with maximum time
    ans = s[maxPos]

    # Return the resultant bulb
    return ans

# Driver Code
if __name__ == "__main__" :

    S = "spuda"
    arr = [ 12, 23, 36, 46, 62 ]

    # Function call
    print(longestLastingBulb(arr, S))

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the bulb
    // having maximum glow
    static char longestLastingBulb(
        List<int> onTime, string s)
    {
        char ans;
        int n = onTime.Count;

        // Initialize variables
        int maxDur = Int32.MinValue;
        int maxPos = Int32.MinValue;
        int currentDiff = 0;

        // Traverse the array consisting
        // of glowing time of the bulbs
        for (int i = 0; i < n; i++) {

            // For 1st bulb
            if (i == 0) {
                currentDiff = onTime[i];
                maxDur = currentDiff;
                maxPos = i;
            }
            else {

                // Calculate the glowing time
                currentDiff = onTime[i]
                              - onTime[i - 1];

                // Update the maximum glow
                if (maxDur < currentDiff) {
                    maxDur = currentDiff;
                    maxPos = i;
                }

                // Find lexicographically
                // largest bulb
                else {

                    if (maxDur == currentDiff) {
                        char one = s[i];
                        char two = s[maxPos];

                        if (one > two) {
                            maxDur = currentDiff;
                            maxPos = i;
                        }
                    }
                }
            }
        }

        // Bulb with maximum time
        ans = s[maxPos];

        // Return the resultant bulb
        return ans;
    }

  static void Main() {

    string S = "spuda";
    List<int> arr = new List<int>(new int[] {12, 23, 36, 46, 62});

    // Function call
    Console.Write(longestLastingBulb(arr, S));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the bulb
// having maximum glow
function longestLastingBulb(onTime, s)
{
    let ans;
    let n = onTime.length;

    // Initialize variables
    let maxDur = Number.MIN_VALUE;
    let maxPos = Number.MIN_VALUE;
    let currentDiff = 0;

    // Traverse the array consisting
    // of glowing time of the bulbs
    for(let i = 0; i < n; i++)
    {

        // For 1st bulb
        if (i == 0)
        {
            currentDiff = onTime[i];
            maxDur = currentDiff;
            maxPos = i;
        }
        else
        {

            // Calculate the glowing time
            currentDiff = onTime[i] -
                          onTime[i - 1];

            // Update the maximum glow
            if (maxDur < currentDiff)
            {
                maxDur = currentDiff;
                maxPos = i;
            }

            // Find lexicographically
            // largest bulb
            else
            {
                if (maxDur == currentDiff)
                {
                    let one = s[i];
                    let two = s[maxPos];

                    if (one > two)
                    {
                        maxDur = currentDiff;
                        maxPos = i;
                    }
                }
            }
        }
    }

    // Bulb with maximum time
    ans = s[maxPos];

    // Return the resultant bulb
    return ans;
}

// Driver code
let S = "spuda";
let arr = [ 12, 23, 36, 46, 62 ];

// Function call
document.write(longestLastingBulb(arr, S));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
a
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)