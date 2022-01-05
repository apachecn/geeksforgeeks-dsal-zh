# Sudo 放置|特殊子序列

> 原文:[https://www . geesforgeks . org/sudo-placement-special-subseries/](https://www.geeksforgeeks.org/sudo-placement-special-subsequences/)

给定一个只包含小写字母的非空字符串 S，打印 S 的所有'**特殊子序列**。例如，“ab”有以下特殊子序列-:{“A”、“Ab”、“aB”、“B”、“A”、“ab”、“AB”、“B”、“B”、“B”、“AB”、“AB”、“B”}。

**注**:只考虑 s 的非空特殊子序列。

**示例**:

```
Input : S = "a"
Output : { "A", "a" }

Input : S = "ab"
Output : { "A", "AB", "Ab", "B", "a", "aB", "ab", "b" }
```

**先决条件** : [字符串的子序列](https://www.geeksforgeeks.org/print-subsequences-string/)

**逼近**:这是一个细微的变化，对于经典问题，打印一个字符串的子序列。假设我们有一个递归函数**生成一个序列(输入，i)** ，它打印输入字符串的所有特殊子序列直到 i <sup>第</sup>个位置。假设当前位置是输入字符串中的 I，那么有三种可能:

1.  按原样将输入[i]包含在输出字符串中，并调用 generateSubsequences(输入，i + 1)
2.  在输出字符串中排除输入[i]，并调用 generate subsquence(str，i + 1)，或者
3.  包括输入[i]的大写形式和调用 generate suissues(str，i + 1)。请务必首先从输出字符串中删除当前添加的字符。

下面是上述方法的实现。

## C++

```
// C++ Program to find all special subsequences
// of the given type
#include <bits/stdc++.h>
using namespace std;

// Function to generate the required subsequences
void generateSubsequences(string input, string output,
                          int idx, vector<string>& ans)
{
    // If the index pointer has reached the
    // end of input string
    if (input[idx] == '\0') {
        // Skip empty (" ") subsequence
        if (output.size())
            ans.push_back(output);
        return;
    }

    // Exclude current character in output string
    generateSubsequences(input, output, idx + 1, ans);

    // Include current character in output string
    output += input[idx];
    generateSubsequences(input, output, idx + 1, ans);

    // Remove the current included character and
    // and include it in its uppercase form
    output.pop_back();
    char upper = input[idx];
    upper = toupper(upper);

    output += upper;
    generateSubsequences(input, output, idx + 1, ans);
}

// Function to print the required subsequences
void printSubsequences(string S)
{
    // Output String to store every subsequence
    string output;

    // Set of strings that will store all special
    // subsequences in lexicographical sorted order
    vector<string> ans;
    generateSubsequences(S, output, 0, ans);

    // Sort the strings to print in sorted order
    sort(ans.begin(), ans.end());

    for (auto str : ans)
        cout << str << " ";
}

// Driver Code
int main()
{
    string S = "ab";
    printSubsequences(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find all special subsequences
// of the given type
import java.util.*;
import java.io.*;

public class SpecialSubsequences {

    // Function to generate the required subsequences
    public static void generateSubsequences(String input, String output,
                                        int index, ArrayList<String> ans)
    {

        // If the index pointer has reached the
        // end of input string
        if(index == input.length()){

            // Skip empty (" ") subsequence
            if(output.length() != 0){
                ans.add(output);
            }
            return;
        }

        //Exclude the character in the output string
        generateSubsequences(input, output, index+1, ans);

        //Include the current character as it is
        output += String.valueOf(input.charAt(index));
        generateSubsequences(input, output, index+1, ans);

        //Include the current character in its upper case form
        //To remove the last character, we generate a substring till the
        //second last character
        output = output.substring(0, output.length()-1);
        output += String.valueOf(
                    Character.toUpperCase(input.charAt(index)));
        generateSubsequences(input, output, index+1, ans);
    }

    // Function to print the required subsequences
    public static void printSubsequences(String s){

        // Output String to store every subsequence
        String output = "";

        // Set of strings that will store all special
        // subsequences in lexicographical sorted order
        ArrayList<String> ans = new ArrayList<>();
        generateSubsequences(s, output, 0, ans);

        //Sort the strings to print in the sorted order
        Collections.sort(ans);

        for(String str: ans){
            System.out.print(str+" ");
        }
        System.out.println();
    }

    //Driver code
    public static void main(String[] args){
            String s = "ab";
            printSubsequences(s);
    }

}
```

## 蟒蛇 3

```
# Python3 program to find all special subsequences
# of the given type
from typing import List

# Function to generate the required subsequences
def generateSubsequences(input: str, output: str,
                         idx: int, ans: List[str]) -> None:

    # If the index pointer has reached the
    # end of input string
    if idx == len(input):

        # Skip empty (" ") subsequence
        if (len(output)):
            ans.append(output)

        return

    # Exclude current character in output string
    generateSubsequences(input, output, idx + 1, ans)

    # Include current character in output string
    output += input[idx]
    generateSubsequences(input, output, idx + 1, ans)

    # Remove the current included character and
    # and include it in its uppercase form
    output = output[:-1]
    upper = input[idx]
    upper = upper.upper()
    output += upper

    generateSubsequences(input, output, idx + 1, ans)

# Function to print the required subsequences
def printSubsequences(S: str) -> None:

    # Output String to store every subsequence
    output = ""

    # Set of strings that will store all special
    # subsequences in lexicographical sorted order
    ans = []
    generateSubsequences(S, output, 0, ans)

    # Sort the strings to print in sorted order
    ans.sort()

    for string in ans:
        print(string, end = " ")

# Driver Code
if __name__ == "__main__":

    S = "ab"

    printSubsequences(S)

# This code is contributed by sanjeev2552
```

**输出**:

```
A AB Ab B a aB ab b
```

**时间复杂度** : O(3 <sup>N</sup> ，其中 N 为弦的大小。