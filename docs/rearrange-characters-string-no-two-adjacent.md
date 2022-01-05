# 重新排列字符串中的字符，使相邻的字符不相同

> 原文:[https://www . geesforgeks . org/rearray-characters-string-no-two-neighbor/](https://www.geeksforgeeks.org/rearrange-characters-string-no-two-adjacent/)

给定一个包含重复字符的字符串，任务是重新排列字符串中的字符，使相邻的两个字符不相同。
注意:可以假设字符串只有小写英文字母。
示例:

```
Input: aaabc 
Output: abaca 

Input: aaabb
Output: ababa 

Input: aa 
Output: Not Possible

Input: aaaabc 
Output: Not Possible
```

问于:[亚马逊采访](https://www.geeksforgeeks.org/amazon-interview-experience-set-330/)

先决条件:[优先级 _ 队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。
想法是把最高频率的字符放在第一位(贪婪的方法)。我们使用一个优先级队列(或二进制最大堆)并把所有的字符和它们的频率排序(最高频率的字符在根)。我们一个接一个地从堆中取出频率最高的字符，并将其添加到结果中。在我们添加之后，我们降低了角色的出现频率，并暂时将这个角色移出优先队列，这样下次就不会被选中了。
我们要按照步骤来解决这个问题，他们是:
1。建立一个优先级队列或最大堆，存储字符及其频率。
…… Priority_queue 或 max_heap 是基于字符的出现频率而构建的。
2。创建一个临时键，用作先前访问过的元素(结果字符串中的前一个元素。初始化它{ char = '# '，freq = '-1' }
3。而 **pq** 不为空。
…..弹出一个元素并将其添加到结果中。
…..将弹出元素的频率减少“1”
…..如果是频率>‘0’
，将前一个元素推回到 priority _ queue..将当前元素作为下一次迭代的前一个元素。
4。如果结果字符串和原始字符串的长度不相等，则打印“不可能”。否则打印结果。
以下是上述思路的实施

## C++

```
// C++ program to rearrange characters in a string
// so that no two adjacent characters are same.
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

struct Key {
    int freq; // store frequency of character
    char ch;

    // function for priority_queue to store Key
    // according to freq
    bool operator<(const Key& k) const
    {
        return freq < k.freq;
    }
};

// Function to rearrange character of a string
// so that no char repeat twice
void rearrangeString(string str)
{
    int n = str.length();

    // Store frequencies of all characters in string
    int count[MAX_CHAR] = { 0 };
    for (int i = 0; i < n; i++)
        count[str[i] - 'a']++;

    // Insert all characters with their frequencies
    // into a priority_queue
    priority_queue<Key> pq;
    for (char c = 'a'; c <= 'z'; c++) {
          int val = c - 'a';
        if (count[val]) {
            pq.push(Key{ count[val], c });
        }
    }

    // 'str' that will store resultant value
    str = "";

    // work as the previous visited element
    // initial previous element be. ( '#' and
    // it's frequency '-1' )
    Key prev{ -1, '#' };

    // traverse queue
    while (!pq.empty()) {
        // pop top element from queue and add it
        // to string.
        Key k = pq.top();
        pq.pop();
        str = str + k.ch;

        // IF frequency of previous character is less
        // than zero that means it is useless, we
        // need not to push it
        if (prev.freq > 0)
            pq.push(prev);

        // make current character as the previous 'char'
        // decrease frequency by 'one'
        (k.freq)--;
        prev = k;
    }

    // If length of the resultant string and original
    // string is not same then string is not valid
    if (n != str.length())
        cout << " Not valid String " << endl;

    else // valid string
        cout << str << endl;
}

// Driver program to test above function
int main()
{
    string str = "bbbaa";
    rearrangeString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange characters in a string
// so that no two adjacent characters are same.
import java.io.*;
import java.util.*;

class KeyComparator implements Comparator<Key> {

    // Overriding compare()method of Comparator
    public int compare(Key k1, Key k2)
    {
        if (k1.freq < k2.freq)
            return 1;
        else if (k1.freq > k2.freq)
            return -1;
        return 0;
    }
}

class Key {
    int freq; // store frequency of character
    char ch;
    Key(int val, char c)
    {
        freq = val;
        ch = c;
    }
}

class GFG {
    static int MAX_CHAR = 26;

    // Function to rearrange character of a string
    // so that no char repeat twice
    static void rearrangeString(String str)
    {
        int n = str.length();

        // Store frequencies of all characters in string
        int[] count = new int[MAX_CHAR];

        for (int i = 0; i < n; i++)
            count[str.charAt(i) - 'a']++;

        // Insert all characters with their frequencies
        // into a priority_queue
        PriorityQueue<Key> pq
            = new PriorityQueue<>(new KeyComparator());
        for (char c = 'a'; c <= 'z'; c++) {
            int val = c - 'a';
            if (count[val] > 0)
                pq.add(new Key(count[val], c));
        }

        // 'str' that will store resultant value
        str = "";

        // work as the previous visited element
        // initial previous element be. ( '#' and
        // it's frequency '-1' )
        Key prev = new Key(-1, '#');

        // traverse queue
        while (pq.size() != 0) {

            // pop top element from queue and add it
            // to string.
            Key k = pq.peek();
            pq.poll();
            str = str + k.ch;

            // If frequency of previous character is less
            // than zero that means it is useless, we
            // need not to push it
            if (prev.freq > 0)
                pq.add(prev);

            // make current character as the previous 'char'
            // decrease frequency by 'one'
            (k.freq)--;
            prev = k;
        }

        // If length of the resultant string and original
        // string is not same then string is not valid
        if (n != str.length())
            System.out.println(" Not valid String ");
        else
            System.out.println(str);
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        String str = "bbbaa";
        rearrangeString(str);
    }
}

// This code is contributed by rachana soma
```

**输出:**

```
babab
```

**时间复杂度:** O(n)

### 另一种方法:

另一种方法是首先用频率最高的字符填充结果字符串的所有偶数位置。如果还剩下一些偶数位置，先补上。一旦完成偶数位置，然后填充奇数位置。这样，我们可以确保没有两个相邻的字符是相同的。

## C++14

```
#include <bits/stdc++.h>
using namespace std;

char getMaxCountChar(const vector<int>& count)
{
    int max = 0;
    char ch;
    for (int i = 0; i < 26; i++) {
        if (count[i] > max) {
            max = count[i];
            ch = 'a' + i;
        }
    }

    return ch;
}

string rearrangeString(string S)
{

    int n = S.size();
    if (!n)
        return "";

    vector<int> count(26, 0);
    for (auto ch : S)
        count[ch - 'a']++;

    char ch_max = getMaxCountChar(count);
    int maxCount = count[ch_max - 'a'];

    // check if the result is possible or not
    if (maxCount > (n + 1) / 2)
        return "";

    string res(n, ' ');

    int ind = 0;
    // filling the most frequently occurring char in the even
    // indices
    while (maxCount) {
        res[ind] = ch_max;
        ind = ind + 2;
        maxCount--;
    }
    count[ch_max - 'a'] = 0;

    // now filling the other Chars, first filling the even
    // positions and then the odd positions
    for (int i = 0; i < 26; i++) {
        while (count[i] > 0) {
            ind = (ind >= n) ? 1 : ind;
            res[ind] = 'a' + i;
            ind += 2;
            count[i]--;
        }
    }
    return res;
}

// Driver program to test above function
int main()
{
    string str = "bbbaa";
    string res = rearrangeString(str);
    if (res == "")
        cout << "Not valid string" << endl;
    else
        cout << res << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python program for rearrangeing characters in a string such
# that no two adjacent are same

# Function to find the char with maximum frequency in the given
# string
def getMaxCountChar(count):
  maxCount = 0
  for i in range(26):
    if count[i] > maxCount:
        maxCount = count[i]
        maxChar = chr(i + ord('a'))

  return maxCount, maxChar

# Main function for rearranging the characters
def rearrangeString(S):
  n = len(S)

  # if length of string is None return False
  if not n:
      return False

  # create a hashmap for the alphabets
  count = [0] * 26
  for char in S:
      count[ord(char) - ord('a')] += 1

  maxCount, maxChar = getMaxCountChar(count)

  # if the char with maximum frequency is more than the half of the
  # total length of the string than return False
  if maxCount > (n + 1) // 2:
      return False

  # create a list for storing the result
  res = [None] * n

  ind = 0

  # place all occurrences of the char with maximum frequency in
  # even positions
  while maxCount:
      res[ind] = maxChar
      ind += 2
      maxCount -= 1

  # replace the count of the char with maximum frequency to zero
  # as all the maxChar are already placed in the result
  count[ord(maxChar) - ord('a')] = 0

  # place all other char in the result starting from remaining even
  # positions and then place in the odd positions
  for i in range(26):
      while count[i] > 0:
          if ind >= n:
              ind = 1
          res[ind] = chr(i + ord('a') )
          ind += 2
          count[i] -= 1

  # convert the result list to string and return
  return ''.join(res)

# Driver Code
str = 'bbbaa'
res = rearrangeString(str)
if res:
  print(res)
else:
  print('Not valid string')

# This code is contributed by Manish Thapa
```

**输出**

**时间复杂度:** O(n)

**空间复杂度:** O(n+26)其中 26 是词汇量的大小。

本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。