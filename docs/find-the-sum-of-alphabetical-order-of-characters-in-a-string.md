# 求字符串中字符字母顺序的总和

> 原文:[https://www . geesforgeks . org/find-按字母顺序排列的字符串字符总和/](https://www.geeksforgeeks.org/find-the-sum-of-alphabetical-order-of-characters-in-a-string/)

给定大小为 **N** 的字符串 **S** ，任务是找出给定字符串中每个字符的字母值之和。

**示例:**

> **输入:** S =“极客”
> 
> **输出:** 28
> 
> **说明:**
> 字母的和序得到的值是 7 + 5 + 5 + 11 = 28。
> 
> **输入:** S = "GeeksforGeeks "
> 
> **输出:** 133

**进场:**

*   遍历给定字符串中的所有字符
*   对于每个小写字符，将值**(S[I]–‘A’+1)**添加到最终答案，或者如果是大写字符，将**(S[I]–‘A’+1)**添加到最终答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int findTheSum(string alpha)
{
    // Stores the sum of order of values
    int score = 0;

    for (int i = 0; i < alpha.length(); i++)
    {
        // Find the score
        if (alpha[i] >= 'A' && alpha[i] <= 'Z')
            score += alpha[i] - 'A' + 1;
        else
            score += alpha[i] - 'a' + 1;
    }
    // Return the resultant sum
    return score;
}

// Driver Code
int main()
{
    string S = "GeeksforGeeks";
    cout << findTheSum(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;
public class GFG
{

static int findTheSum(String alpha)
{

    // Stores the sum of order of values
    int score = 0;

    for (int i = 0; i < alpha.length(); i++)
    {

        // Find the score
        if (alpha.charAt(i) >= 'A' && alpha.charAt(i) <= 'Z')
            score += alpha.charAt(i) - 'A' + 1;
        else
            score += alpha.charAt(i) - 'a' + 1;
    }

    // Return the resultant sum
    return score;
}

// Driver code
public static void main(String args[])
{
    String S = "GeeksforGeeks";
    System.out.println(findTheSum(S));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program for the above approach
def findTheSum(alpha):

    # Stores the sum of order of values
    score = 0

    for i in range(0, len(alpha)):

        # Find the score
        if (ord(alpha[i]) >= ord('A') and ord(alpha[i]) <= ord('Z')):
            score += ord(alpha[i]) - ord('A') + 1
        else:
            score += ord(alpha[i]) - ord('a') + 1

    # Return the resultant sum
    return score

# Driver Code
if __name__ == "__main__":

    S = "GeeksforGeeks"
    print(findTheSum(S))

# This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach
        function findTheSum(alpha)
        {

            // Stores the sum of order of values
            let score = 0;

            for (let i = 0; i < alpha.length; i++)
            {

                // Find the score
                if (alpha[i].charCodeAt(0) >= 'A'.charCodeAt(0) && alpha[i].charCodeAt(0) <= 'Z'.charCodeAt(0))
                    score += alpha[i].charCodeAt(0) - 'A'.charCodeAt(0) + 1;
                else
                    score += alpha[i].charCodeAt(0) - 'a'.charCodeAt(0) + 1;
            }

            // Return the resultant sum
            return score;
        }

        // Driver Code
        let S = "GeeksforGeeks";
        document.write(findTheSum(S));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
133
```