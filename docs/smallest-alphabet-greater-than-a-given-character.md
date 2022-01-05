# 大于给定字符的最小字母表

> 原文:[https://www . geesforgeks . org/minist-alphabet-大于给定字符/](https://www.geeksforgeeks.org/smallest-alphabet-greater-than-a-given-character/)

给定一个由大写字母和小写字母组成的排序字符列表和一个特定的目标值，比如 **K** ，任务是找到列表中大于 K 的最小元素。字母也是环绕的。例如，如果 K = 'z '和字母= ['A '，' r '，' z']，那么答案将是' A '。

**示例**:

```
Input : Letters = ["D", "J", "K"]
        K = "B"
Output: 'D'
Explanation:
The Next greater character of "B" is 'D'
since it is the smallest element from the 
set of given letters, greater than "B".

Input:  Letters = ["h", "n", "s"]
        K = "t"
Output: 'h'
```

**先决条件** : [二分搜索法](https://www.geeksforgeeks.org/binary-search/)

**逼近** : [二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以用来寻找给定字母集中最小字符的索引，使得该索引处的字符大于 K，如果当前 mid 处的元素小于或等于 K，二分搜索法应用于**右半部分**，否则应用于左半部分。

## C++

```
/* C++ Program to find the smallest character
from the given set of letter, which is greater
than the target element */
#include <bits/stdc++.h>
using namespace std;

/* Returns the smallest character from the given
set of letters that is greater than K */

// In this code we consider only uppercase characters or only lowercase characters
// Incase if we have mixed characters then we
//convert all either into lowercase or uppercase
char nextGreatestAlphabet(vector<char>& alphabets, char K)
{
    int n= alphabets.size();
    if(K>=alphabets[n-1]) return alphabets[0];

    int l = 0, r = alphabets.size() - 1;

    // Take the first element as l and
    // the rightmost element as r
    int ans = -1;
    while (l <= r) {

        // if this while condition does not satisfy
        // simply return the first element.
        int mid = (l + r) / 2;
        if (alphabets[mid] > K)
        {
            r = mid - 1;
            ans = mid;
        }
        else
            l = mid + 1;
    }

    // Return the smallest element
    return alphabets[ans];
}

// Driver Code
int main()
{
    vector<char> letters{ 'A', 'K', 'S' };
    char K = 'L';

    // Function call
    char result = nextGreatestAlphabet(letters, K);
    cout << result << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to find the smallest character
from the given set of letter, which is greater
than the target element */

class GFG
{

    /* Returns the smallest character from the given
    set of letters that is greater than K */
    static char nextGreatestAlphabet(char alphabets[],
                                     char K)
    {
      int n = alphabets.length;
      if(K>=alphabets[n-1])
        return alphabets[0];

        int l = 0, r = alphabets.length - 1;

        int ans = -1;
        // Take the first element as l and
        // the rightmost element as r
        while (l <= r)
        {
            // if this while condition does not
            // satisfy simply return the first
            // element.
            int mid = (l + r) / 2;
            if (alphabets[mid] > K)
            {
                r = mid - 1;
                ans = mid;
            }
            else
                l = mid + 1;
        }

        // Return the smallest element
        return alphabets[ans];
    }

    // Driver Code
    public static void main(String[] args)
    {
        char letters[] = { 'A', 'r', 'z' };
        char K = 'z';
        char result = nextGreatestAlphabet(letters, K);

        // Function call
        System.out.println(result);
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python 3 Program to find the smallest
# character from the given set of letter,
# which is greater than the target
# element */

# Returns the smallest character from
# the given set of letters that is
# greater than K

def nextGreatestAlphabet(alphabets, K):

    n = len(alphabets)
    if(K >= alphabets[n-1]):
       return alphabets[0]
    l = 0
    r = len(alphabets) - 1
    ans = -1
    # Take the first element as l and
    # the rightmost element as r
    while (l <= r):

        # if this while condition does
        # not satisfy simply return the
        # first element.
        mid = int((l + r) / 2)

        if (alphabets[mid] > K):
            r = mid - 1
            ans = mid
        else:
            l = mid + 1

    # Return the smallest element
    if (alphabets[ans] < K):
        return alphabets[0]
    else:
        return alphabets[ans]

# Driver Code
letters = ['A', 'r', 'z']
K = 'z'

# Function call
result = nextGreatestAlphabet(letters, K)
print(result)

# This code is contributed by Smitha
```

## C#

```
/* C# Program to find the smallest character
from the given set of letter, which is greater
than the target element */
using System;

class GFG {

    /* Returns the smallest character from the given
    set of letters that is greater than K */
    static char nextGreatestAlphabet(char[] alphabets,
                                     char K)
    {

        int n= alphabets.Length;
        if(K >= alphabets[n-1])
          return alphabets[0];
        int l = 0, r = alphabets.Length - 1;
        int ans = -1;
        // Take the first element as l and
        // the rightmost element as r
        while (l <= r)
        {

            // if this while condition does not
            // satisfy simply return the first
            // element.
            int mid = (l + r) / 2;

            if (alphabets[mid] > K)
            {
                ans = mid;
                r = mid - 1;
            }
            else
                l = mid + 1;
        }

        // Return the smallest element
        return alphabets[ans];
    }

    // Driver Code
    public static void Main()
    {
        char[] letters = { 'A', 'r', 'z' };
        char K = 'z';

        // Function call
        char result = nextGreatestAlphabet(letters, K);

        Console.Write(result);
    }
}

// This code is contributed by Smitha
```

## java 描述语言

```
<script>

/* JavaScript Program to find the smallest character
from the given set of letter, which is greater
than the target element */

      /* Returns the smallest character from the given
    set of letters that is greater than K */
      function nextGreatestAlphabet(alphabets, K)
      {
        var l = 0,
          r = alphabets.length - 1;
        var ans = -1;

        // Take the first element as l and
        // the rightmost element as r
        while (l <= r)
        {
          // if this while condition does not
          // satisfy simply return the first
          // element.
          var mid = (l + r) / 2;

          if (alphabets[mid] > K) {
            ans = mid;
            r = mid - 1;
          } else l = mid + 1;
        }

        // Return the smallest element
        return alphabets[ans];
      }

      // Driver Code
      var letters = ["A", "K", "S"];
      var K = "L";

      // Function call
      document.write(nextGreatestAlphabet(letters, K));

</script>
```

**Output**

```
S
```

上述方法的时间复杂度为， **O(log N)** ，其中 N 是给定字母集中的字符数。