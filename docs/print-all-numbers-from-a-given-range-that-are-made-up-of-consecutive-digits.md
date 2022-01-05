# 打印给定范围内由连续数字组成的所有数字

> 原文:[https://www . geeksforgeeks . org/print-由连续数字组成的给定范围内的所有数字/](https://www.geeksforgeeks.org/print-all-numbers-from-a-given-range-that-are-made-up-of-consecutive-digits/)

给定一个范围**【L，R】**，任务是从范围**【L，R】**中找出所有数字连续的数字。按递增顺序打印所有这些数字。

**示例:**

> **输入:** L = 12，R = 34
> T3】输出: 12 23 34
> 
> **输入:** L = 12，R = 25
> T3】输出: 12 23

**方法:**给定的问题可以通过[生成所有可能的数字](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)并存储所有满足给定条件的数字来解决。生成所有数字后，按排序顺序打印所有存储的数字。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说 **num** 为**“**，它存储所有可能的数字的[串](https://www.geeksforgeeks.org/string-data-structure/)形式，这些数字具有连续的数字并且是递增的顺序。
*   [使用变量 **i** 迭代范围【1，9】](https://www.geeksforgeeks.org/range-based-loop-c/)，并执行以下步骤:
    *   将字符串 **num** 更新为 **i** 的字符串形式，如果该值在**【L，R】**的范围内，则将其存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **Ans[]** 中。
    *   使用变量 **j** 迭代范围【1，9】将 **j** 的字符形式添加到字符串 **num** 中，如果字符串 **num** 的整数形式位于范围**【L，R】**中，则将其存储在向量**Ans【】**中。
*   完成上述步骤后，[对向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) Ans[]进行排序，打印所有生成的数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the consecutive
// digit numbers in the given range
vector<int> solve(int start, int end)
{
    // Initialize num as empty string
    string num = "";

    // Stores the resultant number
    vector<int> ans;

    // Iterate over the range [1, 9]
    for (int i = 1; i <= 9; i++) {

        num = to_string(i);
        int value = stoi(num);

        // Check if the current number
        // is within range
        if (value >= start
            and value <= end) {
            ans.push_back(value);
        }

        // Iterate on the digits starting
        // from i
        for (int j = i + 1; j <= 9; j++) {

            num += to_string(j);
            value = stoi(num);

            // Checking the consecutive
            // digits numbers starting
            // from i and ending at j
            // is within range or not
            if (value >= start
                and value <= end) {
                ans.push_back(value);
            }
        }
    }

    // Sort the numbers in the
    // increasing order
    sort(ans.begin(), ans.end());

    return ans;
}

// Driver Code
int main()
{
    int L = 12, R = 87;

    vector<int> ans = solve(12, 87);

    // Print the required numbers
    for (auto& it : ans)
        cout << it << ' ';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the consecutive
// digit numbers in the given range
static Vector<Integer> solve(int start, int end)
{

    // Initialize num as empty String
    String num = "";

    // Stores the resultant number
    Vector<Integer> ans = new Vector<>();

    // Iterate over the range [1, 9]
    for(int i = 1; i <= 9; i++)
    {
        num = Integer.toString(i);
        int value = i;

        // Check if the current number
        // is within range
        if (value >= start &&
            value <= end)
        {
            ans.add(value);
        }

        // Iterate on the digits starting
        // from i
        for(int j = i + 1; j <= 9; j++)
        {
            num += Integer.toString(j);
            value = Integer.valueOf(num);

            // Checking the consecutive
            // digits numbers starting
            // from i and ending at j
            // is within range or not
            if (value >= start &&
                value <= end)
            {
                ans.add(value);
            }
        }
    }

    // Sort the numbers in the
    // increasing order
    Collections.sort(ans);;

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int L = 12, R = 87;

    Vector<Integer> ans = solve(L,R);

    // Print the required numbers
    for(int it : ans)
        System.out.print(it + " ");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the consecutive
# digit numbers in the given range
def solve(start, end):
    # Initialize num as empty string
    num = ""

    # Stores the resultant number
    ans = []

    # Iterate over the range [1, 9]
    for i in range(1,10,1):
        num = str(i)
        value = int(num)

        # Check if the current number
        # is within range
        if (value >= start and value <= end):
            ans.append(value)

        # Iterate on the digits starting
        # from i
        for j in range(i + 1,10,1):
            num += str(j)
            value = int(num)

            # Checking the consecutive
            # digits numbers starting
            # from i and ending at j
            # is within range or not
            if (value >= start and value <= end):
                ans.append(value)

    # Sort the numbers in the
    # increasing order
    ans.sort()

    return ans

# Driver Code
if __name__ == '__main__':
    L = 12
    R = 87

    ans = solve(12, 87)

    # Print the required numbers
    for it in ans:
        print(it,end = " ")

        # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class Program
{

// Function to find the consecutive
// digit numbers in the given range
static void solve(int start, int end)
{

    // Initialize num as empty String
    string num = "";

    // Stores the resultant number
    List<int> ans = new List<int>();

    // Iterate over the range [1, 9]
    for(int i = 1; i <= 9; i++)
    {
        num = i.ToString();
        int value = i;

        // Check if the current number
        // is within range
        if (value >= start && value <= end)
        {
            ans.Add(value);
        }

        // Iterate on the digits starting
        // from i
        for(int j = i + 1; j <= 9; j++)
        {
            num += j.ToString();
            value = Int32.Parse(num);

            // Checking the consecutive
            // digits numbers starting
            // from i and ending at j
            // is within range or not
            if (value >= start &&
                value <= end)
            {
                ans.Add(value);
            }
        }
    }

    // Sort the numbers in the
    // increasing order
    ans.Sort();

    // Print the required numbers
    foreach(int it in ans)
        Console.Write(it + " ");
}

  // Driver code
    static void Main() {
        int L = 12, R = 87;
        solve(L,R);
    }
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the consecutive
    // digit numbers in the given range
     function solve(start , end) {

        // Initialize num as empty String
        var num = "";

        // Stores the resultant number
        var ans = [];

        // Iterate over the range [1, 9]
        for (var i = 1; i <= 9; i++) {
            num = i.toString();
            var value = i;

            // Check if the current number
            // is within range
            if (value >= start && value <= end) {
                ans.push(value);
            }

            // Iterate on the digits starting
            // from i
            for (j = i + 1; j <= 9; j++) {
                num += j.toString();
                value = num;

                // Checking the consecutive
                // digits numbers starting
                // from i and ending at j
                // is within range or not
                if (value >= start && value <= end) {
                    ans.push(value);
                }
            }
        }

        // Sort the numbers in the
        // increasing order
        return ans;
    }

    // Driver Code
        var L = 12, R = 87;
        var ans = solve(L, R);

        // Prvar the required numbers
        for (it of ans)
            document.write(it + " ");

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
12 23 34 45 56 67 78
```

**时间复杂度:**O(1)
T3】空间复杂度: O(1)