# 找出给定字符串中具有 k 个唯一字符的最长子串

> 原文:[https://www . geesforgeks . org/find-给定字符串中具有 k 个唯一字符的最长子字符串/](https://www.geeksforgeeks.org/find-the-longest-substring-with-k-unique-characters-in-a-given-string/)

给定一个字符串，您需要打印可能最长的子字符串，该子字符串正好有 M 个唯一字符。如果有多个可能长度最长的子字符串，则打印其中任何一个。

示例:

```
"aabbcc", k = 1
Max substring can be any one from {"aa" , "bb" , "cc"}.

"aabbcc", k = 2
Max substring can be any one from {"aabb" , "bbcc"}.

"aabbcc", k = 3
There are substrings with exactly 3 unique characters
{"aabbcc" , "abbcc" , "aabbc" , "abbc" }
Max is "aabbcc" with length 6.

"aaabbb", k = 3
There are only two unique characters, thus show error message. 
```

来源:谷歌面试问题。

**方法 1(蛮力)**
如果字符串长度为 n，那么可以有 n*(n+1)/2 个可能的子字符串。一个简单的方法是生成所有的子串，并检查每个子串是否有 k 个唯一的字符。如果我们应用这种蛮力，将需要 O(n <sup>2</sup> )来生成所有子字符串，并需要 O(n)来检查每个子字符串。因此，总的来说，它将为 0(n<sup>3</sup>)。
我们可以通过创建哈希表来进一步改进这个解决方案，在生成子字符串的同时，使用该哈希表检查唯一字符的数量。因此，它将提高到 0(n<sup>2</sup>)。

**方法 2(线性时间)**
问题可以在 O(n)中解决。想法是维护一个窗口，并添加元素到窗口，直到它包含少于或等于 k，更新我们的结果，如果需要，同时这样做。如果窗口中的唯一元素超过要求，则从左侧开始移除元素。
下面是上面的实现。实现假设输入字符串字母表只包含 26 个字符(从“a”到“z”)。代码可以轻松扩展到 256 个字符。

## C++

```
// C++ program to find the longest substring with k unique
// characters in a given string
#include <iostream>
#include <cstring>
#define MAX_CHARS 26
using namespace std;

// This function calculates number of unique characters
// using a associative array count[]. Returns true if
// no. of characters are less than required else returns
// false.
bool isValid(int count[], int k)
{
    int val = 0;
    for (int i=0; i<MAX_CHARS; i++)
        if (count[i] > 0)
            val++;

    // Return true if k is greater than or equal to val
    return (k >= val);
}

// Finds the maximum substring with exactly k unique chars
void kUniques(string s, int k)
{
    int u = 0; // number of unique characters
    int n = s.length();

    // Associative array to store the count of characters
    int count[MAX_CHARS];
    memset(count, 0, sizeof(count));

    // Traverse the string, Fills the associative array
    // count[] and count number of unique characters
    for (int i=0; i<n; i++)
    {
        if (count[s[i]-'a']==0)
            u++;
        count[s[i]-'a']++;
    }

    // If there are not enough unique characters, show
    // an error message.
    if (u < k)
    {
        cout << "Not enough unique characters";
        return;
    }

    // Otherwise take a window with first element in it.
    // start and end variables.
    int curr_start = 0, curr_end = 0;

    // Also initialize values for result longest window
    int max_window_size = 1, max_window_start = 0;

    // Initialize associative array count[] with zero
    memset(count, 0, sizeof(count));

    count[s[0]-'a']++;  // put the first character

    // Start from the second character and add
    // characters in window according to above
    // explanation
    for (int i=1; i<n; i++)
    {
        // Add the character 's[i]' to current window
        count[s[i]-'a']++;
        curr_end++;

        // If there are more than k unique characters in
        // current window, remove from left side
        while (!isValid(count, k))
        {
            count[s[curr_start]-'a']--;
            curr_start++;
        }

        // Update the max window size if required
        if (curr_end-curr_start+1 > max_window_size)
        {
            max_window_size = curr_end-curr_start+1;
            max_window_start = curr_start;
        }
    }

    cout << "Max substring is : "
         << s.substr(max_window_start, max_window_size)
         << " with length " << max_window_size << endl;
}

// Driver function
int main()
{
    string s = "aabacbebebe";
    int k = 3;
    kUniques(s, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to find the longest substring with k unique
// characters in a given string
class GFG {

    final static int MAX_CHARS = 26;

   // This function calculates number
   // of unique characters
   // using a associative array
   // count[]. Returns true if
   // no. of characters are less
   // than required else returns
   // false.
    static boolean isValid(int count[],
                                   int k)
    {
        int val = 0;
        for (int i = 0; i < MAX_CHARS; i++)
        {
            if (count[i] > 0)
            {
                val++;
            }
        }

        // Return true if k is greater
        // than or equal to val
        return (k >= val);
    }

    // Finds the maximum substring
    // with exactly k unique chars
    static void kUniques(String s, int k)
    {
        int u = 0;
        int n = s.length();

        // Associative array to store
        // the count of characters
        int count[] = new int[MAX_CHARS];
        Arrays.fill(count, 0);
        // Traverse the string, Fills
        // the associative array
        // count[] and count number
        // of unique characters
        for (int i = 0; i < n; i++)
        {
            if (count[s.charAt(i) - 'a'] == 0)
            {
                u++;
            }
            count[s.charAt(i) - 'a']++;
        }

        // If there are not enough
        // unique characters, show
        // an error message.
        if (u < k) {
            System.out.print("Not enough unique characters");
            return;
        }

        // Otherwise take a window with
        // first element in it.
        // start and end variables.
        int curr_start = 0, curr_end = 0;

        // Also initialize values for
        // result longest window
        int max_window_size = 1;
        int max_window_start = 0;

        // Initialize associative
        // array count[] with zero
        Arrays.fill(count, 0);

        // put the first character
        count[s.charAt(0) - 'a']++;

        // Start from the second character and add
        // characters in window according to above
        // explanation
        for (int i = 1; i < n; i++) {
            // Add the character 's[i]'
            // to current window
            count[s.charAt(i) - 'a']++;
            curr_end++;

            // If there are more than k
            // unique characters in
            // current window, remove from left side
            while (!isValid(count, k)) {
                count[s.charAt(curr_start) - 'a']--;
                curr_start++;
            }

            // Update the max window size if required
            if (curr_end - curr_start + 1 > max_window_size)
            {
                max_window_size = curr_end - curr_start + 1;
                max_window_start = curr_start;
            }
        }

        System.out.println("Max substring is : "
                + s.substring(max_window_start,
                    max_window_start + max_window_size)
                + " with length " + max_window_size);
    }

    // Driver Code
    static public void main(String[] args) {
        String s = "aabacbebebe";
        int k = 3;
        kUniques(s, k);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find the longest substring with k unique
# characters in a given string
MAX_CHARS = 26

# This function calculates number of unique characters
# using a associative array count[]. Returns true if
# no. of characters are less than required else returns
# false.
def isValid(count, k):
    val = 0
    for i in range(MAX_CHARS):
        if count[i] > 0:
            val += 1

    # Return true if k is greater than or equal to val
    return (k >= val)

# Finds the maximum substring with exactly k unique characters
def kUniques(s, k):
    u = 0 # number of unique characters
    n = len(s)

    # Associative array to store the count
    count = [0] * MAX_CHARS

    # Traverse the string, fills the associative array
    # count[] and count number of unique characters
    for i in range(n):
        if count[ord(s[i])-ord('a')] == 0:
            u += 1
        count[ord(s[i])-ord('a')] += 1

    # If there are not enough unique characters, show
    # an error message.
    if u < k:
        print ("Not enough unique characters")
        return

    # Otherwise take a window with first element in it.
    # start and end variables.
    curr_start = 0
    curr_end = 0

    # Also initialize values for result longest window
    max_window_size = 1
    max_window_start = 0

    # Initialize associative array count[] with zero
    count = [0] * len(count)

    count[ord(s[0])-ord('a')] += 1 # put the first character

    # Start from the second character and add
    # characters in window according to above
    # explanation
    for i in range(1,n):

        # Add the character 's[i]' to current window
        count[ord(s[i])-ord('a')] += 1
        curr_end+=1

        # If there are more than k unique characters in
        # current window, remove from left side
        while not isValid(count, k):
            count[ord(s[curr_start])-ord('a')] -= 1
            curr_start += 1

        # Update the max window size if required
        if curr_end-curr_start+1 > max_window_size:
            max_window_size = curr_end-curr_start+1
            max_window_start = curr_start

    print ("Max substring is : " + s[max_window_start:max_window_start  + max_window_size]
    + " with length " + str(max_window_size))

# Driver function
s = "aabacbebebe"
k = 3
kUniques(s, k)

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to find the longest substring with k unique 
// characters in a given string 
using System;
public class GFG
{

  static int MAX_CHARS = 26;

  // This function calculates number 
  // of unique characters 
  // using a associative array 
  // count[]. Returns true if 
  // no. of characters are less 
  // than required else returns 
  // false. 
  static bool isValid(int[] count, 
                      int k) 
  { 
    int val = 0; 
    for (int i = 0; i < MAX_CHARS; i++) 
    { 
      if (count[i] > 0) 
      { 
        val++; 
      } 
    } 

    // Return true if k is greater
    // than or equal to val 
    return (k >= val); 
  } 

  // Finds the maximum substring 
  // with exactly k unique chars 
  static void kUniques(string s, int k) 
  { 
    int u = 0; 
    int n = s.Length; 

    // Associative array to store 
    // the count of characters 
    int[] count = new int[MAX_CHARS]; 
    Array.Fill(count, 0);

    // Traverse the string, Fills 
    // the associative array 
    // count[] and count number 
    // of unique characters 
    for (int i = 0; i < n; i++) 
    { 
      if (count[s[i] - 'a'] == 0) 
      { 
        u++; 
      } 
      count[s[i] - 'a']++; 
    } 

    // If there are not enough 
    // unique characters, show 
    // an error message. 
    if (u < k) { 
      Console.Write("Not enough unique characters"); 
      return; 
    } 

    // Otherwise take a window with
    // first element in it. 
    // start and end variables. 
    int curr_start = 0, curr_end = 0; 

    // Also initialize values for
    // result longest window 
    int max_window_size = 1;
    int max_window_start = 0; 

    // Initialize associative 
    // array count[] with zero 
    Array.Fill(count, 0); 

    // put the first character 
    count[s[0] - 'a']++; 

    // Start from the second character and add 
    // characters in window according to above 
    // explanation 
    for (int i = 1; i < n; i++)
    {

      // Add the character 's[i]' 
      // to current window 
      count[s[i] - 'a']++; 
      curr_end++; 

      // If there are more than k 
      // unique characters in 
      // current window, remove from left side 
      while (!isValid(count, k)) { 
        count[s[curr_start] - 'a']--; 
        curr_start++; 
      } 

      // Update the max window size if required 
      if (curr_end - curr_start + 1 > max_window_size) 
      { 
        max_window_size = curr_end - curr_start + 1; 
        max_window_start = curr_start; 
      } 
    } 

    Console.WriteLine("Max substring is : "+
                      s.Substring(max_window_start, max_window_size) +
                      " with length " + max_window_size); 
  } 

  // Driver code
  static public void Main (){
    string s = "aabacbebebe"; 
    int k = 3; 
    kUniques(s, k); 
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program to find the longest
// substring with k unique characters in
// a given string
let MAX_CHARS = 26;

// This function calculates number of
// unique characters using a associative
// array count[]. Returns true if no. of
// characters are less than required else
// returns false.
function isValid(count, k)
{
    let val = 0;
    for(let i = 0; i < MAX_CHARS; i++)
    {
        if (count[i] > 0)
        {
            val++;
        }
    }

    // Return true if k is greater
    // than or equal to val
    return (k >= val);
}

// Finds the maximum substring
// with exactly k unique chars
function kUniques(s,k)
{

    // Number of unique characters
    let u = 0;
    let n = s.length;
    let count = new Array(MAX_CHARS);

    for(let i = 0; i < MAX_CHARS; i++)
    {
        count[i] = 0;
    }

    // Traverse the string, Fills
    // the associative array
    // count[] and count number
    // of unique characters
    for(let i = 0; i < n; i++)
    {
        if (count[s[i].charCodeAt(0) -
                   'a'.charCodeAt(0)] == 0)
        {
            u++;
        }
        count[s[i].charCodeAt(0) -
              'a'.charCodeAt(0)]++;
    }

    // If there are not enough
    // unique characters, show
    // an error message.
    if (u < k)
    {
        document.write("Not enough unique characters");
        return;
    }

    // Otherwise take a window with
    // first element in it.
    // start and end variables.
    let curr_start = 0, curr_end = 0;

    // Also initialize values for
    // result longest window
    let max_window_size = 1;
    let max_window_start = 0;

    // Initialize associative
    // array count[] with zero
    for(let i = 0; i < MAX_CHARS; i++)
    {
        count[i] = 0;
    }

    // put the first character
    count[s[0].charCodeAt(0) -
           'a'.charCodeAt(0)]++;

    // Start from the second character and add
    // characters in window according to above
    // explanation
    for(let i = 1; i < n; i++)
    {

        // Add the character 's[i]'
        // to current window
        count[s[i].charCodeAt(0) -
               'a'.charCodeAt(0)]++;
        curr_end++;

        // If there are more than k
        // unique characters in
        // current window, remove from left side
        while (!isValid(count, k))
        {
            count[s[curr_start].charCodeAt(0) -
                            'a'.charCodeAt(0)]--;
            curr_start++;
        }

        // Update the max window size if required
        if (curr_end - curr_start + 1 > max_window_size)
        {
            max_window_size = curr_end - curr_start + 1;
            max_window_start = curr_start;
        }
    }

    document.write("Max substring is : " +
                   s.substring(max_window_start,
                   max_window_start +
                   max_window_size + 1) +
                   " with length " + max_window_size);
}

// Driver Code
let s = "aabacbebebe";
let k = 3;

kUniques(s, k);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Max substring is : cbebebe with length 7
```

**时间复杂度:**考虑函数“isValid()”取常数时间，上述解的时间复杂度为 O(n)。
本文由[高拉夫·夏尔马](https://www.linkedin.com/in/gaurav34065)供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息