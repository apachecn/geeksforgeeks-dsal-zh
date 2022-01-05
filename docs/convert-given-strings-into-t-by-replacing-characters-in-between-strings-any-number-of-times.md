# 通过多次替换字符串之间的字符，将给定的字符串转换为 T

> 原文:[https://www . geesforgeks . org/通过任意次数替换字符串中的字符将给定字符串转换为 t/](https://www.geeksforgeeks.org/convert-given-strings-into-t-by-replacing-characters-in-between-strings-any-number-of-times/)

给定一个由 **N** [个字符串](https://www.geeksforgeeks.org/python-strings/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** 和一个大小为 **M** 的字符串 **T** ，任务是通过从一个字符串中删除任意字符，比如说 **arr[i]** 并将其插入到另一个字符串的任意位置，来检查是否有可能使数组 **arr[]** 中的所有字符串与字符串 **T** 相同

**示例:**

> **输入:**arr[]= {“ABC”、“abb”、“ACC”}，T =“ABC”
> **输出:**是
> **解释:**
> 下面是一种可能的方法，使数组中的所有字符串都变成字符串 T 的方法是:
> 
> *   删除字符串 arr[1]的索引 2 处的字符(= "abb ")，然后将其插入字符串 arr[2]的索引 1 处(= "acc ")。此后，数组修改为{“ABC”、“ab”、“abcc”}。
> *   删除字符串 arr[2]的索引 3 处的字符(= "abcc ")，然后将其插入字符串 arr[1]的索引 2 处(= "ab ")。此后，数组修改为{“abc”、“ABC”、“ABC”}。
> 
> 经过以上步骤，数组 arr[]的所有字符串都等于字符串 T(= abc)。因此，打印“是”。
> 
> **输入:**arr[]= {“ABC”、“bbb”、“CCC”}，T =“ABC”
> **输出:**否

**方法:**当且仅当满足以下条件时，基于以下观察，可以解决给定的问题，即输出将是“**是**:

*   无字符串包含任何在 **T** 中不存在的字符。
*   在所有给定的**S【】**组合字符串中， **T** 的所有字符必须出现 **N** 次。

按照以下步骤解决问题:

*   初始化两个数组，用值 **0** 表示**频率【256】**和**频率【256】**，分别存储数组所有字符串中出现字符的[频率、 **arr[]** 和字符串 **T** 。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   [遍历给定的字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr[]**，并存储数组 **freqS[]** 中每个字符串的字符频率。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/) **T** 的字符，并将字符串 **T** 的字符频率存储在数组 **freqT[]** 中。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，255】**中迭代，并执行以下步骤:
    *   如果**频率[i]** 和**频率[i]** 的值为 **0** 或者**频率[i]** 的值等于**N *频率[T]** ，则[继续迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   否则，初始化一个布尔变量，说 **A** 为**真**和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果 **A** 的值为真，则打印**“否”**。否则，打印“**是**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if it possible
// to make all the strings equal to
// the string T
string checkIfPossible(int N, string arr[], string T)
{

    // Stores the frequency of all
    // the strings in the array arr[]
    int freqS[256] = {0};

    // Stores the frequency of the
    // string T
    int freqT[256] = {0};

    // Iterate over the characters
    // of the string T
    for (char ch : T) {
        freqT[ch - 'a']++;
    }

    // Iterate in the range [0, N-1]
    for (int i = 0; i < N; i++) {

        // Iterate over the characters
        // of the string arr[i]
        for (char ch : arr[i]) {
            freqS[ch - 'a']++;
        }
    }

    for (int i = 0; i < 256; i++) {

        // If freqT[i] is 0 and
        // freqS[i] is not 0
        if (freqT[i] == 0
            && freqS[i] != 0) {
            return "No";
        }

        // If freqS[i] is 0 and
        // freqT[i] is not 0
        else if (freqS[i] == 0
                 && freqT[i] != 0) {
            return "No";
        }

        // If freqS[i] is not freqT[i]*N
        else if (freqT[i] != 0
                 && freqS[i]
                        != (freqT[i] * N)) {
            return "No";
        }
    }

    // Otherwise, return "Yes"
    return "Yes";
}

// Driver Code
int main() {

    string arr[] = { "abc", "abb", "acc" };
    string T = "abc";
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << checkIfPossible(N, arr, T);
    return 0;
}

// This code is contributed by Dharanendra L V.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

    // Function to check if it possible
    // to make all the strings equal to
    // the string T
    static String checkIfPossible(
        int N, String[] arr, String T)
    {
        // Stores the frequency of all
        // the strings in the array arr[]
        int[] freqS = new int[256];

        // Stores the frequency of the
        // string T
        int[] freqT = new int[256];

        // Iterate over the characters
        // of the string T
        for (char ch : T.toCharArray()) {
            freqT[ch - 'a']++;
        }

        // Iterate in the range [0, N-1]
        for (int i = 0; i < N; i++) {

            // Iterate over the characters
            // of the string arr[i]
            for (char ch : arr[i].toCharArray()) {
                freqS[ch - 'a']++;
            }
        }

        for (int i = 0; i < 256; i++) {

            // If freqT[i] is 0 and
            // freqS[i] is not 0
            if (freqT[i] == 0
                && freqS[i] != 0) {
                return "No";
            }

            // If freqS[i] is 0 and
            // freqT[i] is not 0
            else if (freqS[i] == 0
                     && freqT[i] != 0) {
                return "No";
            }

            // If freqS[i] is not freqT[i]*N
            else if (freqT[i] != 0
                     && freqS[i]
                            != (freqT[i] * N)) {
                return "No";
            }
        }

        // Otherwise, return "Yes"
        return "Yes";
    }

    // Driver Code
    public static void main(String[] args)
    {
        String[] arr = { "abc", "abb", "acc" };
        String T = "abc";
        int N = arr.length;
        System.out.println(
            checkIfPossible(N, arr, T));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it possible
# to make all the strings equal to
# the T
def checkIfPossible(N, arr, T):

    # Stores the frequency of all
    # the strings in the array arr[]
    freqS = [0] * 256

    # Stores the frequency of the
    # T
    freqT = [0] * 256

    # Iterate over the characters
    # of the T
    for ch in T:
        freqT[ord(ch) - ord('a')] += 1

    # Iterate in the range [0, N-1]
    for i in range(N):

        # Iterate over the characters
        # of the arr[i]
        for ch in arr[i]:
            freqS[ord(ch) - ord('a')] += 1

    for i in range(256):

        # If freqT[i] is 0 and
        # freqS[i] is not 0
        if (freqT[i] == 0 and freqS[i] != 0):
            return "No"

        # If freqS[i] is 0 and
        # freqT[i] is not 0
        elif (freqS[i] == 0 and freqT[i] != 0):
            return "No"

        # If freqS[i] is not freqT[i]*N
        elif (freqT[i] != 0 and freqS[i]!= (freqT[i] * N)):
            return "No"

    # Otherwise, return "Yes"
    return "Yes"

# Driver Code
if __name__ == '__main__':

    arr = [ "abc", "abb", "acc" ]
    T = "abc"
    N = len(arr)

    print(checkIfPossible(N, arr, T))

# This code is contributed by mohit kumar 29
```

## C#

```
// c# program for the above approach
using System;
public class GFG {

    // Function to check if it possible
    // to make all the strings equal to
    // the string T
    static string checkIfPossible(int N, string[] arr,
                                  string T)
    {
        // Stores the frequency of all
        // the strings in the array arr[]
        int[] freqS = new int[256];

        // Stores the frequency of the
        // string T
        int[] freqT = new int[256];

        // Iterate over the characters
        // of the string T
        foreach(char ch in T.ToCharArray())
        {
            freqT[ch - 'a']++;
        }

        // Iterate in the range [0, N-1]
        for (int i = 0; i < N; i++) {

            // Iterate over the characters
            // of the string arr[i]
            foreach(char ch in arr[i].ToCharArray())
            {
                freqS[ch - 'a']++;
            }
        }

        for (int i = 0; i < 256; i++) {

            // If freqT[i] is 0 and
            // freqS[i] is not 0
            if (freqT[i] == 0 && freqS[i] != 0) {
                return "No";
            }

            // If freqS[i] is 0 and
            // freqT[i] is not 0
            else if (freqS[i] == 0 && freqT[i] != 0) {
                return "No";
            }

            // If freqS[i] is not freqT[i]*N
            else if (freqT[i] != 0
                     && freqS[i] != (freqT[i] * N)) {
                return "No";
            }
        }

        // Otherwise, return "Yes"
        return "Yes";
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string[] arr = { "abc", "abb", "acc" };
        string T = "abc";
        int N = arr.Length;
        Console.WriteLine(checkIfPossible(N, arr, T));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if it possible
// to make all the strings equal to
// the string T
function checkIfPossible(N, arr, T)
{

    // Stores the frequency of all
    // the strings in the array arr[]
    let freqS = new Array(256).fill(0);

    // Stores the frequency of the
    // string T
    let freqT = new Array(256).fill(0);

    // Iterate over the characters
    // of the string T
    for (let ch of T) {
        freqT[ch.charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    // Iterate in the range [0, N-1]
    for (let i = 0; i < N; i++) {

        // Iterate over the characters
        // of the string arr[i]
        for (let ch of arr[i]) {
            freqS[ch.charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }
    }

    for (let i = 0; i < 256; i++) {

        // If freqT[i] is 0 and
        // freqS[i] is not 0
        if (freqT[i] == 0 && freqS[i] != 0) {
            return "No";
        }

        // If freqS[i] is 0 and
        // freqT[i] is not 0
        else if (freqS[i] == 0 && freqT[i] != 0) {
            return "No";
        }

        // If freqS[i] is not freqT[i]*N
        else if (freqT[i] != 0
                 && freqS[i]
                        != (freqT[i] * N)) {
            return "No";
        }
    }

    // Otherwise, return "Yes"
    return "Yes";
}

// Driver Code

    let arr = [ "abc", "abb", "acc" ];
    let T = "abc";
    let N = arr.length;
    document.write(checkIfPossible(N, arr, T));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N*L + M)，其中 **L** 是数组 arr[]中最长字符串的长度。*
***辅助空间:** O(26)*