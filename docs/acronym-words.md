# 首字母缩略词

> 原文:[https://www.geeksforgeeks.org/acronym-words/](https://www.geeksforgeeks.org/acronym-words/)

给定由英文字母表的小写字母组成的字符串。任务是找出这些 **N** 弦中有多少弦是其他**N–1**弦的首字母缩写。
对于字符串的子集，我们可以选择以任何方式对它们进行排序，然后将每个字符串的第一个字母串联起来。例如， **csa** 是子集**{计算机、学院、科学}** ans 的首字母缩略词， **acs** 也是。打印可以是其他字符串首字母缩略词的字符串数。
**举例:**

> **输入:**arr[]= {“abc”、“bcad”、“cabd”、“cba”、“dzzz”}
> **输出:** 2
> cabd 是{cba、ABC、bcad、dzzz}
> 的缩写 cba 是{cabd、bcad、abc}
> **的缩写输入:**arr[]= {“GNU”、“not”、“UNIX”}
> **输出:** 0
> 注意

**方法:**假设我们有一个频率数组 **freq** ，其中**freq【I】**是字符 **i** 在给定字符串中第一个出现的次数。为了检查一个字符串 **S** 是否可以是首字母缩略词，首先要降低 **S** 首字母的出现频率，然后检查 **S** 中每个字母的出现频率是否小于等于其在**freq【】**数组中的值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the number of strings
// that can be an acronym for other strings
int count_acronym(int n, string arr[])
{
    // Frequency array to store the
    // frequency of the first character
    // of every string in the array
    int freq[26] = {0};

    for (int i = 0; i < n; i++)
        freq[arr[i][0] - 'a']++;

    // To store the count of
    // required strings
    int cnt = 0;

    for (int i = 0; i < n; i++)
    {

        // Current word
        string st = arr[i];

        // Frequency array to store the
        // frequency of each of the character
        // of the current string
        int num[26] = {0};
        for (int j = 0; j < st.length(); j++)
            num[st[j] - 'a']++;

        bool flag = true;

        // Check if the frequency of every character in
        // the current string is <= its value in freq[]
        for (int j = 1; j < 26; j++)
        {
            if (num[j] > freq[j])
            {
                flag = false;
                break;
            }
        }

        // First character of the current string
        int x = st[0] - 'a';
        if (freq[x] - 1 < num[x])
            flag = false;

        if (flag)
            cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    string arr[] = {"abc", "bcad", "cabd",
                    "cba", "dzzz"};
    int n = 5;
    cout << count_acronym(n, arr);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the number of strings
    // that can be an acronym for other strings
    static int count_acronym(int n, String[] arr)
    {
        // Frequency array to store the frequency
        // of the first character of
        // every string in the array
        int[] freq = new int[26];

        for (int i = 0; i < n; i++)
            freq[arr[i].charAt(0) - 'a']++;

        // To store the count of required strings
        int cnt = 0;

        for (int i = 0; i < n; i++) {

            // Current word
            String st = arr[i];

            // Frequency array to store the frequency
            // of each of the character
            // of the current string
            int[] num = new int[26];
            for (int j = 0; j < st.length(); j++)
                num[st.charAt(j) - 'a']++;

            boolean flag = true;

            // Check if the frequency of every character in
            // the current string is <= its value in freq[]
            for (int j = 1; j < 26; j++) {
                if (num[j] > freq[j]) {
                    flag = false;
                    break;
                }
            }

            // First character of the current string
            int x = st.charAt(0) - 'a';
            if (freq[x] - 1 < num[x])
                flag = false;

            if (flag)
                cnt++;
        }

        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        String[] arr = { "abc",
                         "bcad",
                         "cabd",
                         "cba",
                         "dzzz" };
        int n = arr.length;
        System.out.println(count_acronym(n, arr));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of strings
# that can be an acronym for other strings
def count_acronym(n, arr):

    # Frequency array to store the
    # frequency of the first character
    # of every string in the array
    freq = [0] * 26

    for i in range(n):
        freq[ord(arr[i][0]) - ord('a')] += 1

    # To store the count of required strings
    cnt = 0

    for i in range(n):

        # Current word
        st = arr[i]

        # Frequency array to store the
        # frequency of each of the character
        # of the current string
        num = [0] * 26
        for j in range(len(st)):
            num[ord(st[j]) - ord('a')] += 1

        flag = True

        # Check if the frequency of every character in
        # the current string is <= its value in freq[]
        for j in range(1, 26):
            if num[j] > freq[j]:
                flag = False
                break

        # First character of the current string
        x = ord(st[0]) - ord('a')
        if freq[x] - 1 < num[x]:
            flag = False

        if flag:
            cnt += 1

    return cnt

# Driver Code
if __name__ == "__main__":
    arr = ["abc", "bcad", "cabd", "cba", "dzzz"]
    n = 5
    print(count_acronym(n, arr))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number of strings
    // that can be an acronym for other strings
    static int count_acronym(int n, string[] arr)
    {
        // Frequency array to store the frequency
        // of the first character of
        // every string in the array
        int[] freq = new int[26];

        for (int i = 0; i < n; i++)
            freq[arr[i][0] - 'a']++;

        // To store the count of required strings
        int cnt = 0;

        for (int i = 0; i < n; i++)
        {

            // Current word
            string st = arr[i];

            // Frequency array to store the frequency
            // of each of the character
            // of the current string
            int[] num = new int[26];
            for (int j = 0; j < st.Length; j++)
                num[st[j] - 'a']++;

            bool flag = true;

            // Check if the frequency of every character in
            // the current string is <= its value in freq[]
            for (int j = 1; j < 26; j++)
            {
                if (num[j] > freq[j])
                {
                    flag = false;
                    break;
                }
            }

            // First character of the current string
            int x = st[0] - 'a';
            if (freq[x] - 1 < num[x])
                flag = false;

            if (flag)
                cnt++;
        }
        return cnt;
    }

    // Driver code
    public static void Main()
    {
        string[] arr = { "abc",
                        "bcad",
                        "cabd",
                        "cba",
                        "dzzz" };
        int n = arr.Length;
        Console.WriteLine(count_acronym(n, arr));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the number of strings
    // that can be an acronym for other strings
    function count_acronym(n, arr)
    {
        // Frequency array to store the frequency
        // of the first character of
        // every string in the array
        let freq = new Array(26);
        freq.fill(0);

        for (let i = 0; i < n; i++)
            freq[arr[i][0].charCodeAt() - 'a'.charCodeAt()]++;

        // To store the count of required strings
        let cnt = 0;

        for (let i = 0; i < n; i++)
        {

            // Current word
            let st = arr[i];

            // Frequency array to store the frequency
            // of each of the character
            // of the current string
            let num = new Array(26);
            num.fill(0);
            for (let j = 0; j < st.length; j++)
                num[st[j].charCodeAt() - 'a'.charCodeAt()]++;

            let flag = true;

            // Check if the frequency of every character in
            // the current string is <= its value in freq[]
            for (let j = 1; j < 26; j++)
            {
                if (num[j] > freq[j])
                {
                    flag = false;
                    break;
                }
            }

            // First character of the current string
            let x = st[0].charCodeAt() - 'a'.charCodeAt();
            if (freq[x] - 1 < num[x])
                flag = false;

            if (flag)
                cnt++;
        }
        return cnt;
    }

    let arr = [ "abc",
               "bcad",
               "cabd",
               "cba",
               "dzzz" ];
    let n = arr.length;
    document.write(count_acronym(n, arr));

</script>
```

**Output:** 

```
2
```