# 对具有奇数和偶数索引字符的字符串数组进行排序，这些字符分别按降序和升序排序

> 原文:[https://www . geeksforgeeks . org/sort-字符串数组-具有奇数和偶数索引的字符-分别按递减和递增顺序排序/](https://www.geeksforgeeks.org/sort-an-array-of-strings-having-characters-at-odd-and-even-indices-sorted-in-decreasing-and-increasing-order-respectively/)

给定一个由**N**T6】字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是首先对数组中的每个字符串分别按降序和升序对字符串的奇数和偶数索引处的字符进行排序，然后对修改后的数组进行排序。

**示例:**

> **输入:** arr[] = {“球”、“蝙蝠”、“男孩”}
> **输出:** albl atb byo
> **解释:**
> S[0]=“球”转换为“albl”
> S[1]=“蝙蝠”转换为“ATB”
> S[2]=“男孩”转换为“byo”
> 修改后数组的排序顺序为:albl atb byo。
> 
> **输入:**arr[]= {“geeks”、“gfg”、“hello”、“world”}
> **输出:**dwell eohll esekg fgg

**方法:**给定的问题可以通过[遍历字符串](https://www.geeksforgeeks.org/arrays-and-strings-in-c/)的给定数组**arr【】**来解决，对于每个字符串，首先[对字符串](https://www.geeksforgeeks.org/sort-string-characters/)进行排序，然后重新排列每个字符串，使得**偶数索引**处的字符按升序排列，而**奇数索引**处的字符按降序排列。最后，以升序对新的字符串数组进行排序。按照以下步骤解决问题:

*   [遍历给定的字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr[]**，并对每个字符串执行以下步骤:
    *   **按字母顺序排列**字符串**arr【I】**。
    *   初始化一个变量，比如说 **temp** 为**“**，存储结果字符串。
    *   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**arr【I】**为字符串的半长**arr【I】**并存储从字符串的开始和结束到字符串 **temp** 的 **i <sup>th</sup> 索引**。
    *   如果字符串的大小为奇数，则在变量 **temp** 的末尾添加字符串**arr【I】**的**中间**字符。
    *   完成上述步骤后，将数组**arr【I】**的 **i <sup>第</sup>索引**处的字符串更新为字符串 **temp** 。
*   完成上述步骤后，[按升序对新的字符串数组进行排序](https://www.geeksforgeeks.org/sort-the-array-of-strings-according-to-alphabetical-order-defined-by-another-string/)并打印字符串数组 **arr[]** 。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort even indices in
// ascending order and odd indices in
// descending order and sort the array
// of strings in ascending order
void sortString(string S[], int N)
{
    // Traverse array of strings
    for (int i = 0; i < N; i++) {

        // Sort string in ascending order
        sort(S[i].begin(), S[i].end());

        // Length of string
        int n = S[i].size();

        string temp = "";

        // Traverse the string
        for (int j = 0; j < n / 2; j++) {
            temp += S[i][j];
            temp += S[i][n - j - 1];
        }

        // If length of string is odd
        if (n & 1)
            temp += S[i][n / 2];

        S[i] = temp;
    }

    // Sort array of strings
    sort(S, S + N);

    // Print array of strings
    for (int i = 0; i < N; i++) {
        cout << S[i] << " ";
    }
}

// Driver Code
int main()
{
    string arr[] = { "ball", "bat", "boy" };
    int N = sizeof(arr) / sizeof(arr[0]);
    sortString(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static String sortString(String inputString)
{

    // Convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // Sort tempArray
    Arrays.sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Function to sort even indices in
// ascending order and odd indices in
// descending order and sort the array
// of Strings in ascending order
static void sortString(String S[], int N)
{

    // Traverse array of Strings
    for(int i = 0; i < N; i++)
    {

        // Sort String in ascending order
        S[i] = sortString(S[i]);

        // Length of String
        int n = S[i].length();

        String temp = "";

        // Traverse the String
        for(int j = 0; j < n / 2; j++)
        {
            temp += S[i].charAt(j);
            temp += S[i].charAt(n - j - 1);
        }

        // If length of String is odd
        if (n %2== 1)
            temp += S[i].charAt(n / 2);

        S[i] = temp;
    }

    // Sort array of Strings
    Arrays.sort(S);

    // Print array of Strings
    for(int i = 0; i < N; i++)
    {
        System.out.print(S[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "ball", "bat", "boy" };
    int N = arr.length;

    sortString(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to sort even indices in
# ascending order and odd indices in
# descending order and sort the array
# of strings in ascending order
def sortString(S, N):

    # Traverse array of strings
    for i in range(N):

        # Sort string in ascending order
        S[i] = ''.join(sorted(S[i]))

        # Length of string
        n = len(S[i])

        temp = ""

        # Traverse the string
        for j in range(n // 2):
            temp += S[i][j]
            temp += S[i][n - j - 1]

        # If length of string is odd
        if (n & 1):
            temp += S[i][n // 2]

        S[i] = temp

    # Sort array of strings
    S.sort()

    # Print array of strings
    for i in range(N):
        print(S[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = ["ball", "bat", "boy"]
    N = len(arr)

    sortString(arr, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

static String sortString(String inputString)
{

    // Convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // Sort tempArray
    Array.Sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Function to sort even indices in
// ascending order and odd indices in
// descending order and sort the array
// of Strings in ascending order
static void sortString(String []S, int N)
{

    // Traverse array of Strings
    for(int i = 0; i < N; i++)
    {

        // Sort String in ascending order
        S[i] = sortString(S[i]);

        // Length of String
        int n = S[i].Length;

        String temp = "";

        // Traverse the String
        for(int j = 0; j < n / 2; j++)
        {
            temp += S[i][j];
            temp += S[i][n - j - 1];
        }

        // If length of String is odd
        if (n %2== 1)
            temp += S[i][n / 2];

        S[i] = temp;
    }

    // Sort array of Strings
    Array.Sort(S);

    // Print array of Strings
    for(int i = 0; i < N; i++)
    {
        Console.Write(S[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = { "ball", "bat", "boy" };
    int N = arr.Length;

    sortString(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
albl atb byo
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*