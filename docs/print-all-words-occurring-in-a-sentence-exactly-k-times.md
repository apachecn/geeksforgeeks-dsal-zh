# 将一个句子中出现的所有单词精确打印 K 次

> 原文:[https://www . geesforgeks . org/print-all-words-in-a-in-in-a-their-k-times/](https://www.geeksforgeeks.org/print-all-words-occurring-in-a-sentence-exactly-k-times/)

给定一个由小写字母和整数组成的[字符串](https://www.geeksforgeeks.org/python-strings/) **S** ，任务是打印字符串 **S** 中出现 **K** 次的所有单词。

**示例:**

> **输入:** S =“香蕉是黄色的，太阳花也是黄色的”，K = 2
> **输出:**“是”“黄色的”“在”
> **解释:**单词“是”“黄色的”“在”在字符串中出现两次。
> 
> **输入:** S =“极客为极客”，K = 2
> **输出:**“极客”

**方法:**按照以下步骤解决问题:

*   初始化一个[列表](https://www.geeksforgeeks.org/python-list/) **l** 来存储字符串中出现的单词。
*   [拆分](https://www.geeksforgeeks.org/python-string-split/)单词并存储在列表中。
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)，对于每个单词:
    *   如果发现单词的频率为 **K** :
        *   把那个字打印出来。
        *   从列表中删除该单词当前出现的位置。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print all the words
// occurring k times in a string
void kFreqWords(string S, int K)
{

  // Stores the words
  string temp = "";
  vector<string> l;
  for (auto x: S)
  {
    if(x == ' ')
    {
      l.push_back(temp);
      temp = "";
    }
    else
      temp += x;
  }

  // Traverse the list
  for (auto x: l)
  {

    // Check for count
    if (count(l.begin(), l.end(), x) == K)
    {

      // Print the word
      cout << x << endl;

      // Remove from list
      remove(l.begin(),l.end(), x);
    }
  }
}

// Driver Code
int main()
{

  // Given string
  string S = "banana is in yellow and sun flower is also in yellow ";

  // Given value of K
  int K = 2;

  // Function call to find
  // all words occurring K times
  kFreqWords(S, K);

}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all the words
# occurring k times in a string

def kFreqWords(S, K):

    # Stores the words
    l = list(S.split(" "))

    # Traverse the list
    for i in l:

        # Check for count
        if l.count(i) == K:

            # Print the word
            print(i)

            # Remove from list
            l.remove(i)

# Driver Code
if __name__ == "__main__":

    # Given string
    S = "banana is in yellow and sun flower is also in yellow"

    # Given value of K
    K = 2

    # Function call to find
    # all words occurring K times
    kFreqWords(S, K)
```

**Output**

```
is
yellow
in
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

#### 方法 2:使用内置的 python 函数:

*   因为一个句子中的所有单词都用空格隔开。
*   我们必须用 split()将句子用空格分开。
*   我们将所有的单词用空格分开，并存储在一个列表中。
*   使用计数器功能统计单词的出现频率
*   遍历频率字典，打印频率为 k 的单词

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach
from collections import Counter

# Python program to print words
# which occurs k times
def printWords(sentence, k):

    # splitting the string
    lis = list(sentence.split(" "))

    # Calculating frequency of every word
    frequency = Counter(lis)

    # Traversing the frequency
    for i in frequency:

        # checking if frequency is k

        if(frequency[i] == k):

            # print the word
            print(i, end=" ")

# Driver code
# Given string
sentence = "sky is blue and my favourite color is blue"

# Given value of K
K = 2

printWords(sentence, K)
# this code is contributed by vikkycirus
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

/*
Function to print words
which occur k times
*/
function printWords(sentence, k)
{

    // splitting the string
    let lis = sentence.split(" ");

    // Calculating frequency of each word
    frequency = {};
    for(const word of lis)
    {

        // if word exists, increase the value by 1, otherwise mark it as 1
        frequency[word] = frequency[word] ? frequency[word] + 1 : 1;
    }

    // Iterating through frequency
    for(const key of Object.keys(frequency)){

        // if frequency is k
        if(frequency[key] == k){

            // print the word
            document.write(key + " ");
        }
    }
}

// Driver code
// Given string
let sentence = "sky is blue and my favourite color is blue"

// Given value of K
let K = 2
printWords(sentence, K)

// This code is contributed by mostaptname
</script>
```

**输出:**

```
is blue 
```

**时间复杂度:** O(N)

**空间复杂度:** O(N)