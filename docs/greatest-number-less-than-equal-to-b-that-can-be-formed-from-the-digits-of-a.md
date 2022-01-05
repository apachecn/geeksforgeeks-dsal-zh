# 由 A 的数字组成的小于或等于 B 的最大数字

> 原文:[https://www . geeksforgeeks . org/最大数-小于等于 b-可以由 a 的位数构成/](https://www.geeksforgeeks.org/greatest-number-less-than-equal-to-b-that-can-be-formed-from-the-digits-of-a/)

给定两个整数 **A** 和 **B** ，任务是找出用 **A** 的所有数字可以构成的最大数字 **≤ B** 。

**示例:**

> **输入:** A = 123，B = 222
> **输出:** 213
> 123，132 和 213 是唯一≤ 222 的有效数字。
> 其中以 213 为最大。
> 
> **输入:** A = 3921，B = 10000
> T3】输出: 9321

**方法:**让我们从最左边开始一个数字一个数字地构造答案。我们需要建立一个字典上最大的答案，所以我们应该在每一步中选择最大的数字。

迭代所有可能的数字，从最大的开始。对于每个数字，检查是否可以把它放在这个位置。为此，构造最小后缀(贪婪地放入最低的数字)并将结果数字与 B 进行比较。如果它小于或等于 B，则继续下一个数字。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the greatest number
// not gtreater than B that can be formed
// with the digits of A
string Permute_Digits(string a, long long b)
{
    // To store size of A
    int n = a.size();

    // To store the required answer
    string ans = "";

    // Traverse from leftmost digit and 
    // place a smaller digit for every
    // position.
    for (int i = 0; i < n; i++) {

        // Keep all digits in A
        set<char> temp(a.begin(), a.end());

        // To avoid leading zeros
        if (i == 0)
            temp.erase(0);

        // For all possible values at ith position from
        // largest value to smallest
        for (auto j = temp.rbegin(); j != temp.rend(); ++j) {

            // Take largest possible digit
            string s1 = ans + *j;

            // Keep duplicate of string a
            string s2 = a;

            // Remove the taken digit from s2
            s2.erase(s2.find(*j), 1);

            // Sort all the remaining digits of s2
            sort(s2.begin(), s2.end());

            // Add s2 to current s1
            s1 += s2;

            // If s1 is less than B then it can be
            // included in the answer. Note that 
            // stoll() converts a string to lomg
            // long int.
            if (stoll(s1) <= b) {
                ans += *j;

                // change A to s2
                a = s2;
                break;
            }
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    string a = "123";
    int b = 222;
    cout << Permute_Digits(a, b);

    return 0;
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the greatest number
# not gtreater than B that can be formed
# with the digits of A
def permuteDigits(a: str, b: int) -> str:

    # To store size of A
    n = len(a)

    # To store the required answer
    ans = ""

    # Traverse from leftmost digit and
    # place a smaller digit for every
    # position.
    for i in range(n):

        # Keep all digits in A
        temp = set(list(a))

        # To avoid leading zeros
        if i == 0:
            temp.discard(0)

        # For all possible values at ith position from
        # largest value to smallest
        for j in reversed(list(temp)):

            # Take largest possible digit
            s1 = ans + j

            # Keep duplicate of string a
            s2 = list(a).copy()

            # Remove the taken digit from s2
            s2.remove(j)

            # Sort all the remaining digits of s2
            s2 = ''.join(sorted(list(s2)))

            # Add s2 to current s1
            s1 += s2

            # If s1 is less than B then it can be
            # included in the answer. Note that
            # int() converts a string to integer
            if int(s1) <= b:
                ans += j

                # change A to s2
                a = ''.join(list(s2))
                break

    # Return the required answer
    return ans

# Driver Code
if __name__ == "__main__":

    a = "123"
    b = 222
    print(permuteDigits(a, b))

# This code is contributed by
# sanjeev2552
```

**Output:**

```
213

```

**优化**:我们可以使用[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)来保持集合中一个数字的所有出现。我们也可以用 C++中的[下界()来做二分搜索法，快速找到要放置的数字。](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)