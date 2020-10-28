# 检查在给定的二进制字符串

> 原文：[https://www.geeksforgeeks.org/check-if-binary-representations-of-0-to-n-are-present-as-substrings-in-given-binary-string/](https://www.geeksforgeeks.org/check-if-binary-representations-of-0-to-n-are-present-as-substrings-in-given-binary-string/)

中，子字符串是否存在 0 到 N 的二进制表示形式

给出二进制**字符串** str 和整数 **N，**，任务是检查字符串的子字符串是否包含小于或等于给定整数 N 的所有非负整数的二进制表示形式 。

**示例**：

> **输入**：str =“ 0110”，N = 3
> **输出**：True
> **说明**：
> 由于子串“ 0”，“ 1”，“ 10”和“ 11”可以由给定的字符串形成。 因此，所有 0 到 3 的二进制表示形式都以给定二进制字符串中的子字符串形式出现。
> 
> **输入**：str =“ 0110”，N = 4
> **输出**：错误
> **说明**：
> 由于子串“ 0”，“ 1”，“ 10”和“ 11”可以由给定的字符串组成，但不能由“ 100”组成。 因此答案是错误的

**方法**：

可以使用 [BitSet](https://www.geeksforgeeks.org/c-bitset-and-its-application/) 和 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 解决上述问题。 请按照以下步骤解决问题

*   初始化 **map []** 以标记字符串，并使用位设置变量**和**将数字从十进制转换为二进制。

*   再将一个变量计数设为零。

*   使用变量 **i** 从 **N** 到 **1** 循环运行，并检查对应的数字是否在映射中标记为的**。**

*   如果**映射[]** 中没有标记 **i** ，则使用**位设置**变量 ans 将当前数字转换为二进制。

*   然后检查转换后的二进制字符串是否为给定字符串的**子字符串**。

*   如果不是子字符串，则

*   循环运行，除非未标记 **i** 并且二进制数变为零

    *   在地图上标记 **i**

    *   增加计数

    *   右移转换后的数字。 这样做是因为，如果将任何字符串 **x** 转换为二进制（例如 **111001** ）并且该子字符串已在映射中标记，则 **11100** 将已经是**自动标记为**。

        这是基于以下事实：如果存在 i，则 **i > > 1** 也存在。

*   最后检查**是否计数？ N + 1** ，然后打印 True

    否则打印 False

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach  

#include <bits/stdc++.h>  
using namespace std;  

// Function to convert decimal to binary  
// representation  
string decimalToBinary(int N)  
{  

    string ans = "";  

    // Iterate over all bits of N  
    while (N > 0) {  

        // If bit is 1  
        if (N & 1) {  
            ans = '1' + ans;  
        }  
        else {  
            ans = '0' + ans;  
        }  

        N /= 2;  
    }  

    // Return binary representation  
    return ans;  
}  

// Function to check if binary conversion  
// of numbers from N to 1 exists in the  
// string as a substring or not  
string checkBinaryString(string& str, int N)  
{  

    // To store the count of number  
    // exists as a substring  
    int map[N + 10], cnt = 0;  

    memset(map, 0, sizeof(map));  

    // Traverse from N to 1  
    for (int i = N; i > 0; i--) {  

        // If current number is not  
        // present in map  
        if (!map[i]) {  

            // Store current number  
            int t = i;  

            // Find binary of t  
            string s = decimalToBinary(t);  

            // If the string s is a  
            // substring of str  
            if (str.find(s) != str.npos) {  

                while (t && !map[t]) {  

                    // Mark t as true  
                    map[t] = 1;  

                    // Increment the count  
                    cnt++;  

                    // Update for t/2  
                    t >>= 1;  
                }  
            }  
        }  
    }  

    // Special judgment '0'  
    for (int i = 0; i < str.length(); i++) {  
        if (str[i] == '0') {  
            cnt++;  
            break;  
        }  
    }  
    // If the count is N+1, return "yes"  
    if (cnt == N + 1)  
        return "True";  
    else
        return "False";  
}  

// Driver Code  
int main()  
{  
    // Given String  
    string str = "0110";  

    // Given Number  
    int N = 3;  

    // Function Call  
    cout << checkBinaryString(str, N);  
    return 0;  
}  

```

## Java

```java

// Java program for the above approach  
import java.util.*; 

class GFG{  

// Function to convert decimal to binary  
// representation  
static String decimalToBinary(int N)  
{  
    String ans = "";  

    // Iterate over all bits of N  
    while (N > 0)  
    {  

        // If bit is 1  
        if (N % 2 == 1) 
        {  
            ans = '1' + ans;  
        }  
        else
        {  
            ans = '0' + ans;  
        }  
        N /= 2;  
    }  

    // Return binary representation  
    return ans;  
}  

// Function to check if binary conversion  
// of numbers from N to 1 exists in the  
// String as a subString or not  
static String checkBinaryString(String str, int N)  
{  

    // To store the count of number  
    // exists as a subString  
    int []map = new int[N + 10]; 
    int cnt = 0;  

    // Traverse from N to 1  
    for(int i = N; i > 0; i--) 
    {  

        // If current number is not  
        // present in map  
        if (map[i] == 0) 
        {  

            // Store current number  
            int t = i;  

            // Find binary of t  
            String s = decimalToBinary(t);  

            // If the String s is a  
            // subString of str  
            if (str.contains(s)) 
            {  
                while (t > 0 && map[t] == 0) 
                {  

                    // Mark t as true  
                    map[t] = 1;  

                    // Increment the count  
                    cnt++;  

                    // Update for t/2  
                    t >>= 1;  
                }  
            }  
        }  
    }  

    // Special judgment '0'  
    for(int i = 0; i < str.length(); i++) 
    {  
        if (str.charAt(i) == '0') 
        {  
            cnt++;  
            break;  
        }  
    } 

    // If the count is N+1, return "yes"  
    if (cnt == N + 1)  
        return "True";  
    else
        return "False";  
}  

// Driver Code  
public static void main(String[] args)  
{  

    // Given String  
    String str = "0110";  

    // Given number  
    int N = 3;  

    // Function call  
    System.out.print(checkBinaryString(str, N));  
} 
}  

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation of 
# the above approach 

# Function to convert decimal to  
# binary representation 
def decimalToBinary(N): 

    ans = "" 

    # Iterate over all bits of N 
    while(N > 0): 

        # If bit is 1 
        if(N & 1): 
            ans = '1' + ans 
        else: 
            ans = '0' + ans 

        N //= 2

    # Return binary representation 
    return ans 

# Function to check if binary conversion 
# of numbers from N to 1 exists in the 
# string as a substring or not 
def checkBinaryString(str, N): 

    # To store the count of number 
    # exists as a substring 
    map = [0] * (N + 10) 
    cnt = 0

    # Traverse from N to 1 
    for i in range(N, -1, -1): 

        # If current number is not 
        # present in map 
        if(not map[i]): 

            # Store current number 
            t = i 

            # Find binary of t 
            s = decimalToBinary(t) 

            # If the string s is a 
            # substring of str 
            if(s in str): 
                while(t and not map[t]): 

                    # Mark t as true 
                    map[t] = 1

                    # Increment the count 
                    cnt += 1

                    # Update for t/2 
                    t >>= 1

    # Special judgment '0' 
    for i in range(len(str)): 
        if(str[i] == '0'): 
            cnt += 1
            break

    # If the count is N+1, return "yes"  
    if(cnt == N + 1): 
        return "True"
    else: 
        return "False"

# Driver Code 
if __name__ == '__main__': 

    # Given String 
    str = "0110"

    # Given Number 
    N = 3

    # Function Call 
    print(checkBinaryString(str, N)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program for the above approach  
using System; 

class GFG{  

// Function to convert decimal to binary  
// representation  
static String decimalToBinary(int N)  
{  
    String ans = "";  

    // Iterate over all bits of N  
    while (N > 0)  
    {  

        // If bit is 1  
        if (N % 2 == 1) 
        {  
            ans = '1' + ans;  
        }  
        else
        {  
            ans = '0' + ans;  
        }  
        N /= 2;  
    }  

    // Return binary representation  
    return ans;  
}  

// Function to check if binary conversion  
// of numbers from N to 1 exists in the  
// String as a subString or not  
static String checkBinaryString(String str, int N)  
{  

    // To store the count of number  
    // exists as a subString  
    int []map = new int[N + 10]; 
    int cnt = 0;  

    // Traverse from N to 1  
    for(int i = N; i > 0; i--) 
    {  

        // If current number is not  
        // present in map  
        if (map[i] == 0) 
        {  

            // Store current number  
            int t = i;  

            // Find binary of t  
            String s = decimalToBinary(t);  

            // If the String s is a  
            // subString of str  
            if (str.Contains(s)) 
            {  
                while (t > 0 && map[t] == 0) 
                {  

                    // Mark t as true  
                    map[t] = 1;  

                    // Increment the count  
                    cnt++;  

                    // Update for t/2  
                    t >>= 1;  
                }  
            }  
        }  
    }  

    // Special judgment '0'  
    for(int i = 0; i < str.Length; i++) 
    {  
        if (str[i] == '0') 
        {  
            cnt++;  
            break;  
        }  
    } 

    // If the count is N+1, return "yes"  
    if (cnt == N + 1)  
        return "True";  
    else
        return "False";  
}  

// Driver Code  
public static void Main(String[] args)  
{  

    // Given String  
    String str = "0110";  

    // Given number  
    int N = 3;  

    // Function call  
    Console.Write(checkBinaryString(str, N));  
} 
}  

// This code is contributed by PrinciRaj1992 

```

**Output:** 

```
True

```



* * *

* * *



