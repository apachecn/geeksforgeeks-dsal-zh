# 检查一个大数是否可以分成两个或两个以上等份

> 原文:[https://www . geeksforgeeks . org/check-如果一个大数可以被分成两个或更多的等份/](https://www.geeksforgeeks.org/check-if-a-large-number-can-be-divided-into-two-or-more-segments-of-equal-sum/)

给定一个非常大的数 n，任务是检查这个数是否可以分成两个或更多相等和的段。
**例** :

```
Input: N = 73452  
Output: Yes
Segments of {7}, {3, 4}, {5, 2} which has equal sum of 7

Input: N = 1248
Output: No
```

可以按照以下步骤解决问题:

1.  由于该数字可能很大，因此该数字在字符串中初始化。
2.  使用前缀 Sum 数组存储数组的前缀和。
3.  现在从第二个元素遍历到最后一个元素，因此第一个片段将是 0 到 i-1，其和是 Prefixsum[i-1]。
4.  使用另一个从 I 遍历到 n 的指针，并不断添加总和。
5.  如果任何阶段的总和等于 Prefixsum[i-1]，则该段的总和等于 first。
6.  将段和值重新初始化为 0，并继续移动指针。
7.  如果在任何阶段，段总和超过第一段的总和，则中断，因为以段总和作为前缀[i-1]的除法是不可能的。
8.  如果指针到达最后一个数字，检查最后一个段和是否等于第一个段和，即 prefixsum[i-1]，然后它可以被分成相等和的段。

下面是上述方法的实现。

## C++

```
// C++ program to Check if a large number can be divided
// into two or more segments of equal sum
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// can be divided into segments
bool check(string s)
{
    // length of string
    int n = s.length();

    // array to store prefix sum
    int Presum[n];

    // first index
    Presum[0] = s[0] - '0';

    // calculate the prefix
    for (int i = 1; i < n; i++) {
        Presum[i] = Presum[i - 1] + (s[i] - '0');
    }

    // iterate for all number from second number
    for (int i = 1; i <= n - 1; i++) {

        // sum from 0th index to i-1th index
        int sum = Presum[i - 1];
        int presum = 0;
        int it = i;

        // counter turns true when sum
        // is obtained from a segment
        int flag = 0;

        // iterate till the last number
        while (it < n) {
            // sum of segments
            presum += s[it] - '0';

            // if segment sum is equal
            // to first segment
            if (presum == sum) {
                presum = 0;
                flag = 1;
            }
            // when greater than not possible
            else if (presum > sum) {
                break;
            }
            it++;
        }

        // if at the end all values are traversed
        // and all segments have sum equal to first segment
        // then it is possible
        if (presum == 0 && it == n && flag == 1) {
            return true;
        }
    }
    return false;
}

// Driver Code
int main()
{
    string s = "73452";
    if (check(s))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if a large number can be divided
// into two or more segments of equal sum

public class GFG {

    // Function to check if a number
    // can be divided into segments
    static boolean check(String s)
    {
        // length of string
        int n = s.length();

        // array to store prefix sum
        int[] Presum = new int[n];

        // first index
        char[] s1 = s.toCharArray();
        Presum[0] = s1[0] - '0';

        // calculate the prefix
        for (int i = 1; i < n; i++) {
            Presum[i] = Presum[i - 1] + (s1[i] - '0');
        }

        // iterate for all number from second number
        for (int i = 1; i <= n - 1; i++) {

            // sum from 0th index to i-1th index
            int sum = Presum[i - 1];
            int presum = 0;
            int it = i;

            // counter turns true when sum
            // is obtained from a segment
            int flag = 0;

            // iterate till the last number
            while (it < n) {
                // sum of segments
                presum += s1[it] - '0';

                // if segment sum is equal
                // to first segment
                if (presum == sum) {
                    presum = 0;
                    flag = 1;
                }
                // when greater than not possible
                else if (presum > sum) {
                    break;
                }
                it++;
            }

            // if at the end all values are traversed
            // and all segments have sum equal to first segment
            // then it is possible
            if (presum == 0 && it == n && flag == 1) {
                return true;
            }
        }
        return false;
    }

    // Driver Code
    public static void main(String[] args) {

        String s = "73452";
        if (check(s))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-2">巨蟒 3</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-2" data-code-lang="Python3"></gfg-panel>

```
# Python program to Check if a large number can be divided
# into two or more segments of equal sum

# Function to check if a number
# can be divided into segments
def check(s):

    # length of string
    n = len(s)

    # array to store prefix sum
    Presum = [None]*n

    # first index
    Presum[0] = ord(s[0]) - ord('0')

    # calculate the prefix
    for i in range(1, n):
        Presum[i] = Presum[i - 1] + (ord(s[i]) - ord('0'))

    # iterate for all number from second number
    for i in range(1, n):

        # sum from 0th index to i-1th index
        sum = Presum[i - 1]
        presum = 0
        it = i

        # counter turns true when sum
        # is obtained from a segment
        flag = 0

        # iterate till the last number
        while (it < n):

            # sum of segments
            presum = presum + ord(s[it]) - ord('0')

            # if segment sum is equal
            # to first segment
            if (presum == sum):
                presum = 0
                flag = 1

            # when greater than not possible
            elif (presum > sum):
                break

            it = it + 1

        # if at the end all values are traversed
        # and all segments have sum equal to first segment
        # then it is possible
        if (presum == 0 and it == n and flag == 1):
            return True
    return False

# Driver Code
if __name__ == '__main__':
    s = "73452"
    if (check(s)):
        print("Yes")
    else:
        print("No")

# This code is contributed by rakeshsahni 
```

## C#

```
// C# program to Check if a large
// number can be divided into two
// or more segments of equal sum
using System;

class GFG
{

    // Function to check if a number
    // can be divided into segments
    static bool check(String s)
    {
        // length of string
        int n = s.Length;

        // array to store prefix sum
        int[] Presum = new int[n];

        // first index
        char[] s1 = s.ToCharArray();
        Presum[0] = s1[0] - '0';

        // calculate the prefix
        for (int i = 1; i < n; i++)
        {
            Presum[i] = Presum[i - 1] + (s1[i] - '0');
        }

        // iterate for all number from second number
        for (int i = 1; i <= n - 1; i++)
        {

            // sum from 0th index to i-1th index
            int sum = Presum[i - 1];
            int presum = 0;
            int it = i;

            // counter turns true when sum
            // is obtained from a segment
            int flag = 0;

            // iterate till the last number
            while (it < n)
            {
                // sum of segments
                presum += s1[it] - '0';

                // if segment sum is equal
                // to first segment
                if (presum == sum)
                {
                    presum = 0;
                    flag = 1;
                }

                // when greater than not possible
                else if (presum > sum)
                {
                    break;
                }
                it++;
            }

            // if at the end all values are traversed
            // and all segments have sum equal to first segment
            // then it is possible
            if (presum == 0 && it == n && flag == 1)
            {
                return true;
            }
        }
        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        String s = "73452";
        if (check(s))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to Check if a large number can be divided
    // into two or more segments of equal sum

    // Function to check if a number
    // can be divided into segments
    function check(s)
    {

        // length of string
        let n = s.length;

        // array to store prefix sum
        var Presum = [];

        // first index
        Presum.push(parseInt(s[0]));

        // calculate the prefix
        let i;
        for (i = 1; i < n; i++) {
            Presum.push(Presum[i - 1] + parseInt(s[i]));
        }

        // iterate for all number from second number
        for (i = 1; i <= n - 1; i++) {

            // sum from 0th index to i-1th index
            let sum = Presum[i - 1];
            let presum = 0;
            let it = i;

            // counter turns true when sum
            // is obtained from a segment
            let flag = 0;

            // iterate till the last number
            while (it < n) {
                // sum of segments
                presum += parseInt(s[it]);

                // if segment sum is equal
                // to first segment
                if (presum == sum) {
                    presum = 0;
                    flag = 1;
                }
                // when greater than not possible
                else if (presum > sum) {
                    break;
                }
                it++;
            }

            // if at the end all values are traversed
            // and all segments have sum equal to first segment
            // then it is possible
            if (presum == 0 && it == n && flag == 1) {
                return true;
            }
        }
        return false;
    }

    // Driver Code
    var s = "73452";
    if (check(s))
        document.write("Yes");
    else
        document.write("No");

        // This code is contributed by ajaykrsharma132.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)