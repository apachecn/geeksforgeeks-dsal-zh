# 第 n 个数字，数字在{0，1，2，3，4，5}

中

> 原文:[https://www . geeksforgeeks . org/n-th-0-1-2-3-4-5 位数/](https://www.geeksforgeeks.org/n-th-number-with-digits-in-0-1-2-3-4-5/)

给定一个数字 n，我们必须找到第 n 个数字，这样它的数字只由 0，1，2，3，4 或 5 组成。

**示例:**

```
Input: n = 6
Output: 5

Input:  n = 10
Output: 13
```

我们首先在数组中存储 0，1，2，3，4，5。我们可以看到，接下来的数字将是 10、11、12、13、14、15，之后的数字将是 20、21、23、24、25 等等。我们可以看到一次又一次重复的模式。我们保存计算结果，并将其用于进一步计算。
接下来的 6 个数字是-
1 * 10+0 = 10
1 * 10+1 = 11
1 * 10+2 = 12
1 * 10+3 = 13
1 * 10+4 = 14
1 * 10+5 = 15
之后的 6 个数字是-
2 * 10+0 = 20
2 * 10+1 = 21
2 * 10 下面是完整的算法。

```
1) push 0 to 5 in ans vector
2) for i=0 to n/6
     for j=0 to 6  
          // this will be the case when first 
          // digit will be zero 
          if (ans[i]*10! = 0) 
              ans.push_back(ans[i]*10 + ans[j])
3) print ans[n-1]
```

## C++

```
// C++ program to find n-th number with digits
// in {0, 1, 2, 3, 4, 5}
#include <bits/stdc++.h>
using namespace std;

// Returns the N-th number with given digits
int findNth(int n)
{
    // vector to store results
    vector<int> ans;

    // push first 6 numbers in the answer
    for (int i = 0; i < 6; i++)
        ans.push_back(i);

    // calculate further results
    for (int i = 0; i <= n / 6; i++)
        for (int j = 0; j < 6; j++)
            if ((ans[i] * 10) != 0)
                ans.push_back(ans[i]
                              * 10 + ans[j]);

    return ans[n - 1];
}

// Driver code
int main()
{
    int n = 10;
    cout << findNth(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number with digits
// in {0, 1, 2, 3, 4, 5}
import java.io.*;
import java.util.*;

class GFG
{

  // Returns the N-th number with given digits
  public static int findNth(int n)
  {
    // vector to store results
    ArrayList<Integer> ans = new ArrayList<Integer>();

    // push first 6 numbers in the answer
    for (int i = 0; i < 6; i++)
      ans.add(i);

    // calculate further results
    for (int i = 0; i <= n / 6; i++)
      for (int j = 0; j < 6; j++)
        if ((ans.get(i) * 10) != 0)
          ans.add(ans.get(i) * 10 + ans.get(j));
    return ans.get(n - 1);
  }

  // Driver code
  public static void main(String[] args)
  {
    int n = 10;
    int ans = findNth(n);
    System.out.println(ans);
  }
}

// This code is contributed by RohitOberoi.
```

## 蟒蛇 3

```
# Python3 program to find n-th number with digits
# in {0, 1, 2, 3, 4, 5}

# Returns the N-th number with given digits
def findNth(n):

    # vector to store results
    ans = []

    # push first 6 numbers in the answer
    for i in range(6):
        ans.append(i)

    # calculate further results
    for i in range(n // 6 + 1):
        for j in range(6):
            if ((ans[i] * 10) != 0):
                ans.append(ans[i]
                           * 10 + ans[j])

    return ans[n - 1]

# Driver code
if __name__ == "__main__":

    n = 10
    print(findNth(n))

    # This code is contributed by ukasp.
```

## C#

```
// C# program to find n-th number with digits
// in {0, 1, 2, 3, 4, 5}
using System;
using System.Collections.Generic;

class GFG{

// Returns the N-th number with given digits
public static int findNth(int n)
{

    // Vector to store results
    List<int> ans = new List<int>();

    // Push first 6 numbers in the answer
    for(int i = 0; i < 6; i++)
        ans.Add(i);

    // Calculate further results
    for(int i = 0; i <= n / 6; i++)
        for(int j = 0; j < 6; j++)
            if ((ans[i] * 10) != 0)
                ans.Add(ans[i] * 10 + ans[j]);

    return ans[n - 1];
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;
    int ans = findNth(n);

    Console.WriteLine(ans);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find n-th
// number with digits
// in {0, 1, 2, 3, 4, 5}   

// Returns the N-th number with given digits
    function findNth(n)
    {
        // vector to store results
        var ans = [];

        // push first 6 numbers in the answer
        for (i = 0; i < 6; i++)
            ans.push(i);

        // calculate further results
        for (i = 0; i <= n / 6; i++)
            for (j = 0; j < 6; j++)
                if ((ans[i] * 10) != 0)
                    ans.push(ans[i] * 10 + ans[j]);
        return ans[n - 1];
    }

    // Driver code

        var n = 10;
        var ans = findNth(n);
        document.write(ans);

// This code contributed by Rajput-Ji

</script>
```

**Output**

```
13
```