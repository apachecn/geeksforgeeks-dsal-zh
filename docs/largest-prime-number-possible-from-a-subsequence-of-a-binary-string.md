# 二进制串的子序列中可能的最大素数

> 原文:[https://www . geeksforgeeks . org/最大素数-二进制字符串的可能子序列/](https://www.geeksforgeeks.org/largest-prime-number-possible-from-a-subsequence-of-a-binary-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，任务是通过给定二进制字符串的子序列的十进制表示找到最大的[素数](https://www.geeksforgeeks.org/tag/prime-number/)。如果得不到质数，打印 **-1** 。

**示例:**

> **输入:** S = "1001"
> **输出:** 5
> **说明:**在字符串“1001”的所有子序列中，能得到的最大素数是“101”(= 5)。
> 
> **输入:**“1011”
> **输出:** 11
> **说明:**在字符串“1011”的所有子序列中，能得到的最大素数是“1011”(= 11)。

**方法:**解决问题的思路是[生成字符串](https://www.geeksforgeeks.org/print-subsequences-string/)的所有可能的子序列，并将每个子序列转换为其等价的十进制形式。打印由此子序列获得的最大素数。

按照以下步骤解决此问题:

*   分别在 **Pair.first** 和 **Pair.second** 中初始化一个成对的[向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)，比如说**向量，**用于存储成对的字符串及其等价的十进制值。
*   初始化一个变量，说 **ans，**存储需要的答案。
*   迭代一个循环，从 **i = 0** 到[字符串的长度](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/) **s:**
    *   迭代一个从 **j = 0** 到 **vec 长度的循环:**
        *   将第**j**对储存在**温度下。**
        *   如果字符串**的**中带有字符的**是**“1”**:**
            *   首先在**温度**中添加字符
            *   通过[向左移动](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)当前值并添加 **1** 来更新**温度秒**的值。
        *   否则:
            *   首先在**温度**中添加字符
            *   通过[向左移动](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)当前值并添加 **0** 来更新**温度秒**的值。
        *   将此**温度**对储存到 **vec** 中。
        *   如果**温度秒**是[质数](https://www.geeksforgeeks.org/tag/prime-number/):
            *   在 **ans** 中存储 **ans** 和**温度秒**的最大值。
    *   如果 **ans** 等于 **0** :
        *   从字符串 **s** 中得不到质数。
    *   否则:
        *   打印〔t0〕年〔t1〕年。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <iostream>
#include <vector>
using namespace std;

// Function to check if a
// number is prime or not
bool isPrime(int x)
{
    if (x <= 1)
        return false;

    for (int i = 2; i * i <= x; i++) {
        if (x % i == 0)

            // Return not prime
            return false;
    }

    // If prime return true
    return true;
}

// Function to find the largest prime
// number possible from a subsequence
void largestPrime(string s)
{

    // Stores pairs of subsequences and
    // their respective decimal value
    vector<pair<string, int> > vec{ { "", 0 } };

    // Stores the answer
    int ans = 0;

    // Traverse the string
    for (int i = 0; i < s.length(); i++) {
        // Stores the size of the vector
        int n = vec.size();

        // Traverse the vector
        for (int j = 0; j < n; j++) {

            // Extract the current pair
            pair<string, int> temp = vec[j];

            // Get the binary string from the pair
            string str = temp.first;

            // Stores equivalent decimal values
            int val = temp.second;

            // If the current character is '1'
            if (s[i] == '1') {
                // Add the character
                // to the subsequence
                temp.first = str + '1';

                // Update the value by left
                // shifting the current
                // value and adding 1 to it
                temp.second = ((val << 1) + 1);
            }

            // If s[i]=='0'
            else {

                // Add the character
                // to the subsequence
                temp.first = str + '0';

                // Update the value by left
                // shifting the current
                // value and adding 0 to it
                temp.second = ((val << 1) + 0);
            }

            // Store the subsequence in the vector
            vec.push_back(temp);

            // Check if the decimal
            // representation of current
            // subsequence is prime or not
            int check = temp.second;

            // If prime
            if (isPrime(check)) {
                // Update the answer
                // with the largest one
                ans = max(ans, check);
            }
        }
    }

    // If no prime number
    // could be obtained
    if (ans == 0)
        cout << -1 << endl;
    else
        cout << ans << endl;
}

// Driver Code
int main()
{
    // Input String
    string s = "110";

    largestPrime(s);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a
# number is prime or not
def isPrime(x):

    if (x <= 1):
        return False

    for i in range(2, x + 1):
        if i * i > x:
            break

        if (x % i == 0):

            # Return not prime
            return False

    # If prime return true
    return True

# Function to find the largest prime
# number possible from a subsequence
def largestPrime(s):

    # Stores pairs of subsequences and
    # their respective decimal value
    vec = [["", 0]]

    # Stores the answer
    ans = 0

    # Traverse the string
    for i in range(len(s)):

        # Stores the size of the vector
        n = len(vec)

        # Traverse the vector
        for j in range(n):

            # Extract the current pair
            temp = vec[j]

            # Get the binary string from the pair
            str = temp[0]

            # Stores equivalent decimal values
            val = temp[1]

            # If the current character is '1'
            if (s[i] == '1'):

                # Add the character
                # to the subsequence
                temp[0] = str + '1'

                # Update the value by left
                # shifting the current
                # value and adding 1 to it
                temp[1] = ((val << 1) + 1)

            # If s[i]=='0'
            else:

                # Add the character
                # to the subsequence
                temp[0] = str + '0'

                # Update the value by left
                # shifting the current
                # value and adding 0 to it
                temp[1] = ((val << 1) + 0)

            # Store the subsequence in the vector
            vec.append(temp)

            # Check if the decimal
            # representation of current
            # subsequence is prime or not
            check = temp[1]

            # If prime
            if (isPrime(check)):

                # Update the answer
                # with the largest one
                ans = max(ans, check)
                break

    # If no prime number
    # could be obtained
    if (ans == 0):
        print(-1)
    else:
        print(ans)

# Driver Code
if __name__ == '__main__':

    # Input String
    s = "110"

    largestPrime(s)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to check if a
// number is prime or not
function isPrime(x) {
    if (x <= 1)
        return false;

    for (let i = 2; i * i <= x; i++) {
        if(i * i > x){
            break
        }
        if (x % i == 0)

            // Return not prime
            return false;
    }

    // If prime return true
    return true;
}

// Function to find the largest prime
// number possible from a subsequence
function largestPrime(s) {

    // Stores pairs of subsequences and
    // their respective decimal value
    let vec = [["", 0]];

    // Stores the answer
    let ans = 0;

    // Traverse the string
    for (let i = 0; i < s.length; i++) {
        // Stores the size of the vector
        let n = vec.length;

        // Traverse the vector
        for (let j = 0; j < n; j++) {

            // Extract the current pair
            let temp = vec[j];

            // Get the binary string from the pair
            let str = temp[0];

            // Stores equivalent decimal values
            let val = temp[1];

            // If the current character is '1'
            if (s[i] == '1') {
                // Add the character
                // to the subsequence
                temp[0] = str + '1';

                // Update the value by left
                // shifting the current
                // value and adding 1 to it
                temp[1] = ((val << 1) + 1);
            }

            // If s[i]=='0'
            else {

                // Add the character
                // to the subsequence
                temp[0] = str + '0';

                // Update the value by left
                // shifting the current
                // value and adding 0 to it
                temp[1] = ((val << 1) + 0);
            }

            // Store the subsequence in the vector
            vec.push(temp);

            // Check if the decimal
            // representation of current
            // subsequence is prime or not
            let check = temp[1];

            // If prime
            if (isPrime(check)) {
                // Update the answer
                // with the largest one
                ans = Math.max(ans, check);
                break
            }
        }
    }

    // If no prime number
    // could be obtained
    if (ans == 0)
        document.write(-1 + "<br>");
    else
        document.write(ans + "<br>");
}

// Driver Code

// Input String
let s = "110";

largestPrime(s);

</script>
```

**Output:** 

```
3
```

***时间复杂度** : O(2 <sup>N</sup> * √N)，其中 **N** 为弦的长度。*
***辅助空间:** O(2 <sup>N</sup> * N)*