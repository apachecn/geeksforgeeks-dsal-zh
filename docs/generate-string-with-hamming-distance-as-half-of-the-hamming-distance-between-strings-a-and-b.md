# 生成汉明距离为字符串 A 和 B 汉明距离一半的字符串

> 原文:[https://www . geeksforgeeks . org/generate-string-with-hamming-distance-as-a-和-b-之间的汉明距离的一半/](https://www.geeksforgeeks.org/generate-string-with-hamming-distance-as-half-of-the-hamming-distance-between-strings-a-and-b/)

给定两个长度为 **N** 的二进制字符串 **A** 和 **B** ，任务是找到其[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)到字符串 **A** 和 **B** 是 **A** 和 **B** 的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)的一半的二进制字符串。

**示例:**

> **输入:** A = "1001010 "，B = "0101010"
> **输出:** 0001010
> **解释:**
> 字符串 **A** 和 **B** 的汉明距离为 2。
> 输出字符串到 **A** 的汉明距离为 1。
> 输出字符串到 **B** 的汉明距离为 1。
> 
> **输入:** A = "1001010 "，B = "1101010"
> **输出:**不可能
> **说明:**
> 不存在满足我们条件的字符串。

**天真方法:**天真方法是生成长度为 **N** 的所有可能的二进制字符串，并用 **A** 和 **B** 计算每个字符串的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)。如果生成的字符串与给定的字符串 **A** 和 **B** 之间的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)是 **A** 和 **B** 之间的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)的一半，那么生成的字符串就是结果字符串。否则不存在这样的字符串。

**时间复杂度:** O(2 <sup>N</sup>

**有效方法:**

1.  找出两个给定字符串 **A** 和 **B** 之间的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/) ( **说出一个**)。如果 A 是奇数，那么我们不能用字符串 **A** 和 **B** 生成另一个带有[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/) ( **a/2** )的字符串。
2.  如果 A 为偶数，则从字符串 **A** 中选择第一个( **a/2** 个)不等于字符串 **B** 的字符，然后从字符串 **B** 中选择第二个( **a/2** 个不等于字符串 **A** 的字符，组成结果字符串。
3.  将字符串 **A** 和 **B** 中的相等字符追加到结果字符串中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above
// approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required
// string
void findString(string A, string B)
{
    int dist = 0;

    // Find the hamming distance
    // between A and B
    for (int i = 0; A[i]; i++) {
        if (A[i] != B[i]) {
            dist++;
        }
    }

    // If distance is odd, then
    // resultant string is not
    // possible
    if (dist & 1) {
        cout << "Not Possible"
             << endl;
    }

    // Make the resultant string
    else {

        // To store the final
        // string
        string res = "";

        int K = dist / 2;
        // Pick k characters from
        // each string

        for (int i = 0; A[i]; i++) {

            // Pick K characters
            // from string B
            if (A[i] != B[i] && K > 0) {
                res.push_back(B[i]);
                K--;
            }

            // Pick K characters
            // from string A
            else if (A[i] != B[i]) {
                res.push_back(A[i]);
            }

            // Append the res characters
            // from string to the
            // resultant string
            else {
                res.push_back(A[i]);
            }
        }

        // Print the resultant
        // string
        cout << res << endl;
    }
}

// Driver's Code
int main()
{
    string A = "1001010";
    string B = "0101010";

    // Function to find the resultant
    // string
    findString(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above 
// approach 
class GFG
{

    // Function to find the required 
    // string 
    static void findString(String A, String B) 
    { 
        int dist = 0; 

        // Find the hamming distance 
        // between A and B 
        for (int i = 0; i < A.length(); i++) 
        { 
            if(A.charAt(i) != B.charAt(i)) 
                dist++; 
        } 

        // If distance is odd, then 
        // resultant string is not 
        // possible 
        if((dist & 1) == 1) 
        { 
            System.out.println("Not Possible");
        } 

        // Make the resultant string 
        else 
        { 

            // To store the final 
            // string 
            String res = ""; 

            int K = (int)dist / 2; 

            // Pick k characters from 
            // each string 
            for (int i = 0; i < A.length(); i++) { 

                // Pick K characters 
                // from string B 
                if (A.charAt(i) != B.charAt(i) && K > 0) { 
                    res += B.charAt(i); 
                    K--; 
                } 

                // Pick K characters 
                // from string A 
                else if (A.charAt(i) != B.charAt(i)) { 
                    res += A.charAt(i); 
                } 

                // Append the res characters 
                // from string to the 
                // resultant string 
                else { 
                    res += A.charAt(i); 
                } 
            } 

            // Print the resultant 
            // string 
            System.out.println(res) ; 
        }
    }

    // Driver's Code 
    public static void main (String[] args)
    { 
        String A = "1001010"; 
        String B = "0101010"; 

        // Function to find the resultant 
        // string 
        findString(A, B); 
    } 
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation of the above 
# approach 

# Function to find the required 
# string 
def findString(A, B) : 

    dist = 0; 

    # Find the hamming distance 
    # between A and B 
    for i in range(len(A)) :
        if (A[i] != B[i]) :
            dist += 1; 

    # If distance is odd, then 
    # resultant string is not 
    # possible 
    if (dist & 1) :
        print("Not Possible");

    # Make the resultant string 
    else :

        # To store the final 
        # string 
        res = ""; 

        K = dist // 2;

        # Pick k characters from 
        # each string 

        for i in range(len(A)) :

            # Pick K characters 
            # from string B 
            if (A[i] != B[i] and K > 0) : 
                res += B[i]; 
                K -= 1; 

            # Pick K characters 
            # from string A 
            elif (A[i] != B[i]) : 
                res += A[i]; 

            # Append the res characters 
            # from string to the 
            # resultant string 
            else :
                res += A[i]; 

        # Print the resultant 
        # string 
        print(res); 

# Driver's Code 
if __name__ == "__main__" : 

    A = "1001010"; 
    B = "0101010"; 

    # Function to find the resultant 
    # string 
    findString(A, B); 

# This code is contributed by Yash_R
```

## C#

```
// C# implementation of the above approach 
using System;

class GFG
{

    // Function to find the required 
    // string 
    static void findString(string A, string B) 
    { 
        int dist = 0; 

        // Find the hamming distance 
        // between A and B 
        for (int i = 0; i < A.Length; i++) 
        { 
            if(A[i] != B[i]) 
                dist++; 
        } 

        // If distance is odd, then 
        // resultant string is not 
        // possible 
        if((dist & 1) == 1) 
        { 
            Console.WriteLine("Not Possible");
        } 

        // Make the resultant string 
        else 
        { 

            // To store the final 
            // string 
            string res = ""; 

            int K = (int)dist / 2; 

            // Pick k characters from 
            // each string 
            for (int i = 0; i < A.Length; i++) { 

                // Pick K characters 
                // from string B 
                if (A[i] != B[i] && K > 0) { 
                    res += B[i]; 
                    K--; 
                } 

                // Pick K characters 
                // from string A 
                else if (A[i] != B[i]) { 
                    res += A[i]; 
                } 

                // Append the res characters 
                // from string to the 
                // resultant string 
                else { 
                    res += A[i]; 
                } 
            } 

            // Print the resultant 
            // string 
            Console.WriteLine(res) ; 
        }
    }

    // Driver's Code 
    public static void Main (string[] args)
    { 
        string A = "1001010"; 
        string B = "0101010"; 

        // Function to find the resultant 
        // string 
        findString(A, B); 
    } 
}

// This code is contributed by Yash_R
```

**Output:**

```
0001010

```

**时间复杂度:** O(N)，其中 N 为字符串的长度。