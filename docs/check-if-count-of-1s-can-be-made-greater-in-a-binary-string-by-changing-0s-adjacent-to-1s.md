# 通过将 0 更改为与 1 相邻的 0 来检查二进制字符串中的 1 的计数是否可以更大

> 原文:[https://www . geeksforgeeks . org/check-if-count-of-1s-可以通过将-0s-邻近-1s/](https://www.geeksforgeeks.org/check-if-count-of-1s-can-be-made-greater-in-a-binary-string-by-changing-0s-adjacent-to-1s/) 更改为二进制字符串中的更大值

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过将与 **1s** 相邻的 **0s** 更改为任何其他字符，来检查 **1s** 的[计数是否可以大于 **0s**](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/) 的[计数。如果可能，则打印**是**。否则，打印**否**。](https://www.geeksforgeeks.org/find-number-zeroes/)

**注意:**任何具有 **1** 的指标最多只能选择一次。

**示例:**

> **输入:** S = "01"
> **输出:**是
> **解释:**
> 在索引 1 处选择‘1’，并将其左边相邻的 0 更改为“_”，将字符串修改为“_1”。
> 现在，1 的计数是 1，大于 0 的计数，即 0。因此，打印“是”。
> 
> **输入:**S = " 001110000 "
> T3】输出:否

**方法:**给定的问题可以通过计算[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 中的 **1s** 和 **0s** 的数量来解决，然后在遍历字符串时，如果任何索引 **i** 的值为**“1”**，如果左侧或右侧(不是两者)为**“0”**，则将其更改为**“_”**。该值更改为 **'_'** 而不是 **'1'** ，因此不再使用。更改数值后，将 **0 的**计数减少 **1** 。按照以下步骤解决问题:

*   初始化两个变量，将 **cnt0** 和 **cnt1** 设为 **0** ，存储 **0s** 和 **1s** 的计数。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 并将 **1s** 和 **0s** 的计数分别存储在变量 **cnt0** 和 **cnt1** 中。
*   [从左侧遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，检查当前字符是否为 **1** 如果发现为真，则检查条件:
    *   **如果(I>0&&S[I–1]= = ' 0 ')**如果发现为真，则将左边相邻的 0 更改为 **S[i-1] = '_'** ，并将 **cnt0** 的值递减 **1** 。
    *   **否则如果(I<S . length()&&S[I+1]= ' 0 ')**如果发现为真，则将右边的 0 更改为 **S[i+1] = '_'** ，并将 **cnt0** 的值递减 **1** 。
*   完成上述步骤后，如果 **(cnt1 > cnt0)** 的值，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check whether in a given
// binary string can we make number of
// 1's greater than the  number of 0's
// by doing the given operation
void isOnesGreater(string S, int N)
{

    // Stores the count of 0's
    int cnt0 = 0;

    // Stores the count of 1's
    int cnt1 = 0;

    // Traverse through the string S
    for (int i = 0; i < N; i++) {

        // Check current character is 1
        if (S[i] == '1')

            // Update cnt1
            cnt1++;

        else
            // Update cnt0
            cnt0++;
    }

    // Traverse through the string S
    for (int i = 0; i < N; i++) {

        // Check curretn character is 1
        if (S[i] == '1') {

            // Check if left adjacent
            // character is 0
            if (i > 0 && S[i - 1] == '0') {

                // Change the left adjacent
                // character to _
                S[i - 1] = '_';

                // Update the cnt0
                cnt0--;
            }

            // Check if right adjacent
            // character is 0
            else if (i < N && S[i + 1] == '0') {

                // Change the right adjacent
                // character to _
                S[i + 1] = '_';

                // Update the cnt0
                cnt0--;
            }
        }
    }

    // Check count of 1's is greater
    // than the count of 0's
    if (cnt1 > cnt0) {

        cout << "Yes";
    }
    else {

        cout << "No";
    }
}

// Driver Code
int main()
{

    string S = "01";
    int N = S.length();

    isOnesGreater(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to check whether in a given
    // binary string can we make number of
    // 1's greater than the  number of 0's
    // by doing the given operation
    static void isOnesGreater(String S, int N)
    {
        char[] st = new char[S.length()];

        // Copy character by character into array
        for (int i = 0; i < S.length(); i++) {
            st[i] = S.charAt(i);
        }

        // Stores the count of 0's
        int cnt0 = 0;

        // Stores the count of 1's
        int cnt1 = 0;

        // Traverse through the string S
        for (int i = 0; i < N; i++) {

            // Check current character is 1
            if (st[i] == '1')

                // Update cnt1
                cnt1++;

            else
                // Update cnt0
                cnt0++;
        }

        // Traverse through the string S
        for (int i = 0; i < N; i++) {

            // Check curretn character is 1
            if (st[i] == '1') {

                // Check if left adjacent
                // character is 0
                if (i > 0 && st[i - 1] == '0') {

                    // Change the left adjacent
                    // character to _
                    st[i - 1] = '_';

                    // Update the cnt0
                    cnt0--;
                }

                // Check if right adjacent
                // character is 0
                else if (i < N && st[i + 1] == '0') {

                    // Change the right adjacent
                    // character to _
                    st[i + 1] = '_';

                    // Update the cnt0
                    cnt0--;
                }
            }
        }

        // Check count of 1's is greater
        // than the count of 0's
        if (cnt1 > cnt0) {

            System.out.println("Yes");
        }
        else {

            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(String args[])
    {

        String S = "01";
        int N = S.length();

        isOnesGreater(S, N);
    }
}

// This code is contributed by bgangwar59.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to check whether in a given
# binary string can we make number of
# 1's greater than the  number of 0's
# by doing the given operation
def isOnesGreater(S, N):
    S = list(S)

    # Stores the count of 0's
    cnt0 = 0

    # Stores the count of 1's
    cnt1 = 0

    # Traverse through the string S
    for i in range(N):

        # Check current character is 1
        if (S[i] == '1'):

            # Update cnt1
            cnt1 += 1

        else:
            # Update cnt0
            cnt0 += 1

    # Traverse through the string S
    for i in range(N):

        # Check curretn character is 1
        if (S[i] == '1'):

            # Check if left adjacent
            # character is 0
            if (i > 0 and S[i - 1] == '0'):

                # Change the left adjacent
                # character to _
                S[i - 1] = '_'

                # Update the cnt0
                cnt0 -= 1

            # Check if right adjacent
            # character is 0
            elif (i < N and S[i + 1] == '0'):

                # Change the right adjacent
                # character to _
                S[i + 1] = '_'

                # Update the cnt0
                cnt0 -= 1

    # Check count of 1's is greater
    # than the count of 0's
    if (cnt1 > cnt0):
        print("Yes")
    else:
        print("No")

# Driver Code
S = "01"
N = len(S)

isOnesGreater(S, N)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Text;
class GFG {

    // Function to check whether in a given
    // binary string can we make number of
    // 1's greater than the  number of 0's
    // by doing the given operation
    static void isOnesGreater(string S, int N)
    {
        StringBuilder st = new StringBuilder(S);
        // Stores the count of 0's
        int cnt0 = 0;

        // Stores the count of 1's
        int cnt1 = 0;

        // Traverse through the string S
        for (int i = 0; i < N; i++) {

            // Check current character is 1
            if (st[i] == '1')

                // Update cnt1
                cnt1++;

            else
                // Update cnt0
                cnt0++;
        }

        // Traverse through the string S
        for (int i = 0; i < N; i++) {

            // Check curretn character is 1
            if (st[i] == '1') {

                // Check if left adjacent
                // character is 0
                if (i > 0 && st[i - 1] == '0') {

                    // Change the left adjacent
                    // character to _
                    st[i - 1] = '_';

                    // Update the cnt0
                    cnt0--;
                }

                // Check if right adjacent
                // character is 0
                else if (i < N && st[i + 1] == '0') {

                    // Change the right adjacent
                    // character to _
                    st[i + 1] = '_';

                    // Update the cnt0
                    cnt0--;
                }
            }
        }

        // Check count of 1's is greater
        // than the count of 0's
        if (cnt1 > cnt0) {

            Console.WriteLine("Yes");
        }
        else {

            Console.WriteLine("No");
        }
    }

    // Driver Code
    public static void Main()
    {

        string S = "01";
        int N = S.Length;

        isOnesGreater(S, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check whether in a given
        // binary string can we make number of
        // 1's greater than the  number of 0's
        // by doing the given operation
        function isOnesGreater(S, N) {

            // Stores the count of 0's
            let cnt0 = 0;

            // Stores the count of 1's
            let cnt1 = 0;

            // Traverse through the string S
            for (let i = 0; i < N; i++) {

                // Check current character is 1
                if (S[i] == '1')

                    // Update cnt1
                    cnt1++;

                else
                    // Update cnt0
                    cnt0++;
            }

            // Traverse through the string S
            for (let i = 0; i < N; i++) {

                // Check curretn character is 1
                if (S[i] == '1') {

                    // Check if left adjacent
                    // character is 0
                    if (i > 0 && S[i - 1] == '0') {

                        // Change the left adjacent
                        // character to _
                        S[i - 1] = '_';

                        // Update the cnt0
                        cnt0--;
                    }

                    // Check if right adjacent
                    // character is 0
                    else if (i < N && S[i + 1] == '0') {

                        // Change the right adjacent
                        // character to _
                        S[i + 1] = '_';

                        // Update the cnt0
                        cnt0--;
                    }
                }
            }

            // Check count of 1's is greater
            // than the count of 0's
            if (cnt1 > cnt0) {

                document.write("Yes");
            }
            else {

                document.write("No");
            }
        }

        // Driver Code
        let S = "01";
        let N = S.length;

        isOnesGreater(S, N);

     // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)