# 泛数字串联的对数

> 原文:[https://www . geesforgeks . org/number-pairs-pan digital-concation/](https://www.geeksforgeeks.org/number-pairs-pandigital-concatenation/)

如果一对字符串的连接是由(0–9)中的所有数字以任何顺序至少组成一次，则称它们为“泛数字连接”。任务是，给定 N 个字符串，计算导致“泛数字连接”的对的数量。

**示例:**

```
Input  : num[] = {"123567", "098234", "14765", "19804"}
Output : 3
The pairs, 1st and 2nd giving 
(123567098234),1st and 4rd giving(12356719804) and 
2nd and 3rd giving (09823414765),
on concatenation result in Pandigital Concatenations. 

Input : num[] =  {"56789", "098345", "1234"}
Output : 0
None of the pairs on concatenation result in Pandigital 
Concatenations.
```

**方法 1(蛮力):**一种可能的蛮力解决方案是通过在 O(n)<sup>2</sup>中形成所有对来形成所有可能的连接，并使用数字(0–9)的频率数组，我们检查每个数字在为每个对形成的每个连接中是否至少存在一次。

## C++

```
// C++ program to find all
// Pandigital concatenations
// of two strings.
#include <bits/stdc++.h>
using namespace std;

// Checks if a given
// string is Pandigital
bool isPanDigital(string s)
{
    bool digits[10] = {false};
    for (int i = 0; i < s.length(); i++)
        digits[s[i] - '0'] = true;

    // digit i is not present
    // thus not pandigital
    for (int i = 0; i <= 9; i++)
        if (digits[i] == false)
            return false;

    return true;
}

// Returns number of pairs
// of strings resulting in
// Pandigital Concatenations
int countPandigitalPairs(vector<string> &v)
{
    // iterate over all
    // pair of strings
    int pairs = 0;
    for (int i = 0; i < v.size(); i++)
        for (int j = i + 1; j < v.size(); j++)
            if (isPanDigital(v[i] + v[j]))
                pairs++;
    return pairs;
}

// Driver code
int main()
{
    vector<string> v = {"123567", "098234",
                        "14765", "19804"};
    cout << countPandigitalPairs(v) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all
// Pandigital concatenations
// of two strings.
import java.io.*;
import java.util.*;

class GFG
{
    static ArrayList<String> v =
                  new ArrayList<String>();

    // Checks if a given
    // string is Pandigital
    static int isPanDigital(String s)
    {
        int digits[] = new int[10];

        for (int i = 0; i < s.length(); i++)
            digits[s.charAt(i) -
                        (int)'0'] = 1;

        // digit i is not present
        // thus not pandigital
        for (int i = 0; i <= 9; i++)
            if (digits[i] == 0)
                return 0;

        return 1;
    }

    // Returns number of pairs
    // of strings resulting in
    // Pandigital Concatenations
    static int countPandigitalPairs()
    {
        // iterate over all
        // pair of strings
        int pairs = 0;
        for (int i = 0; i < v.size(); i++)
            for (int j = i + 1;
                     j < v.size(); j++)
                if (isPanDigital(v.get(i) +
                                 v.get(j)) == 1)
                    pairs++;
        return pairs;
    }

    // Driver code
    public static void main(String args[])
    {
        v.add("123567");
        v.add("098234");
        v.add("14765");
        v.add("19804");
        System.out.print(countPandigitalPairs());
    }
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find all
# Pandigital concatenations
# of two strings.

# Checks if a given
# is Pandigital
def isPanDigital(s) :

    digits = [False] * 10;

    for i in range(0, len(s)) :
        digits[int(s[i]) -
               int('0')] = True

    # digit i is not present
    # thus not pandigital
    for i in range(0, 10) :
        if (digits[i] == False) :
            return False

    return True

# Returns number of pairs
# of strings resulting in
# Pandigital Concatenations
def countPandigitalPairs(v) :

    # iterate over all
    # pair of strings
    pairs = 0
    for i in range(0, len(v)) :

        for j in range (i + 1,
                        len(v)) :

            if (isPanDigital(v[i] +
                             v[j])) :
                pairs = pairs + 1
    return pairs

# Driver code
v = ["123567", "098234",
        "14765", "19804"]

print (countPandigitalPairs(v))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find all Pandigital
// concatenations of two strings.
using System;
using System.Collections.Generic;

class GFG
{
    // Checks if a given
    // string is Pandigital
    static int isPanDigital(string s)
    {
        int []digits = new int[10];
        Array.Clear(digits, 0, 10);
        for (int i = 0; i < s.Length; i++)
            digits[s[i] - (int)'0'] = 1;

        // digit i is not present
        // thus not pandigital
        for (int i = 0; i <= 9; i++)
            if (digits[i] == 0)
                return 0;

        return 1;
    }

    // Returns number of pairs
    // of strings resulting in
    // Pandigital Concatenations
    static int countPandigitalPairs(ref List<string> v)
    {
        // iterate over all
        // pair of strings
        int pairs = 0;
        for (int i = 0; i < v.Count; i++)
            for (int j = i + 1; j < v.Count; j++)
                if (isPanDigital(v[i] + v[j]) == 1)
                    pairs++;
        return pairs;
    }

    // Driver code
    static void Main()
    {
        List<string> v = new List<string>{"123567", "098234",
                                          "14765", "19804"};
        Console.WriteLine(countPandigitalPairs(ref v));
    }
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find all
// Pandigital concatenations
// of two strings.

// Checks if a given
// $is Pandigital
function isPanDigital($s)
{
    $digits = array();
    $digits = array_fill(0, 10, false);

    for ($i = 0; $i < strlen($s); $i++)
        $digits[ord($s[$i]) -
                ord('0')] = true;

    // digit i is not present
    // thus not pandigital
    for ($i = 0; $i <= 9; $i++)
        if ($digits[$i] == false)
            return false;

    return true;
}

// Returns number of pairs
// of strings resulting in
// Pandigital Concatenations
function countPandigitalPairs(&$v)
{
    // iterate over all
    // pair of strings
    $pairs = 0;
    for ($i = 0;
         $i < count($v); $i++)
    {
        for ($j = $i + 1;
             $j < count($v); $j++)
        {
            if (isPanDigital($v[$i].$v[$j]))
            {
                $pairs++;
            }
        }
    }
    return $pairs;
}

// Driver code
$v = array("123567", "098234",
           "14765", "19804");

echo (countPandigitalPairs($v));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find all
// Pandigital concatenations
// of two strings.

// Checks if a given
// is Pandigital
function isPanDigital(s)
{
    let digits = new Array(10).fill(false);

    for(let i = 0; i < s.length; i++)
        digits[s[i].charCodeAt(0) -
                '0'.charCodeAt(0)] = true;

    // digit i is not present
    // thus not pandigital
    for(let i = 0; i <= 9; i++)
        if (digits[i] == false)
            return false;

    return true;
}

// Returns number of pairs
// of strings resulting in
// Pandigital Concatenations
function countPandigitalPairs(v)
{

    // Iterate over all
    // pair of strings
    let pairs = 0;
    for(let i = 0; i < v.length; i++)
    {
        for(let j = i + 1;
                j < v.length; j++)
        {
            if (isPanDigital(v[i] + v[j]))
            {
                pairs++;
            }
        }
    }
    return pairs;
}

// Driver code
let v = [ "123567", "098234",
          "14765", "19804" ];

document.write(countPandigitalPairs(v));

// This code is contributed by gfgking

</script>
```

**输出:**

```
3
```

**方法 2(高效):**
现在我们寻找比上面讨论的蛮力更好的东西。仔细分析表明，每出现一个数字 0-9，我们就有一个掩码 1111111111(即所有数字 0-9 都存在于数字数组中

```
Digits -  0  1  2  3  4  5  6  7  8  9
          |  |  |  |  |  |  |  |  |  |
Mask   -  1  1  1  1  1  1  1  1  1  1 

Here 1 denotes that the corresponding digits
exists at-least once thus for all such Pandigital 
Concatenations, this relationship should hold.
So we can represent 11...11 as a valid mask for
pandigital concatenations.
```

因此，现在的方法是将每个字符串表示为 10 位的掩码，其中如果字符串中存在第 I<sup>位，则设置第 I<sup>位。</sup></sup>

```
E.g., "11405" can be represented as
Digits -           0  1  2  3  4  5  6  7  8  9
                   |  |  |  |  |  |  |  |  |  |
Mask for 11405 -   1  1  0  0  1  1  0  0  0  0
```

虽然这种方法看起来很完整，但仍然没有效率，因为我们仍然必须迭代所有的字符串对，并检查这两个字符串的或是否导致有效的泛数字连接掩码。

如果我们分析所有可能字符串的可能掩码，我们可以理解每一个字符串将只由数字 0–9 组成，因此每个数字最多可以包含所有数字 0 到 9 至少一次，因此这样一个数字的掩码将是 11111111111(十进制为 1023)。因此，在十进制系统中，所有掩码都以(0–1023)结束。

现在我们只需要维护一个频率数组来存储字符串数组中掩码存在的次数。

> 假设两个掩码分别为频率为 freq <sub>i</sub> 和 freq <sub>j</sub> 、
> If (i OR j) =掩码<sub>泛数字串联</sub>T7】，则
> 对数= freq <sub>i</sub> * freq <sub>j</sub>

## C++

```
// C++ program to count PanDigital pairs
#include <bits/stdc++.h>
using namespace std;

const int pandigitalMask = ((1 << 10) - 1);

void computeMaskFrequencies(vector<string> v, map<int,
                                        int>& freq)
{
    for (int i = 0; i < v.size(); i++) {
        int mask = 0;

        // Stores digits present in string v[i]
        // atleast once. We use a set as we only
        // need digits which exist only once
        // (irrespective of reputation)
        unordered_set<int> digits;
        for (int j = 0; j < v[i].size(); j++)
            digits.insert(v[i][j] - '0');

        // Calculate the mask by considering all digits
        // existing atleast once
        for (auto it = digits.begin(); it != digits.end(); it++) {
            int digit = (*it);
            mask += (1 << digit);
        }

        // Increment the frequency of this mask
        freq[mask]++;
    }
}

// Returns number of pairs of strings resulting
// in Pandigital Concatenations
int pandigitalConcatenations(map<int, int> freq)
{
    int ans = 0;

    // All possible strings lie between 1 and 1023
    // so we iterate over every possible mask
    for (int i = 1; i <= 1023; i++) {
        for (int j = 1; j <= 1023; j++) {

            // if the concatenation results in mask of
            // Pandigital Concatenation, calculate all
            // pairs formed with Masks i and j
            if ((i | j) == pandigitalMask) {
                if (i == j)
                    ans += (freq[i] * (freq[i] - 1));            
                else
                    ans += (freq[i] * freq[j]);            
            }
        }
    }

    // since every pair is considers twice,
    // we get rid of half of these
    return ans/2;
}

int countPandigitalPairs(vector<string> v)
{
    // Find frequencies of all masks in
    // given vector of strings
    map<int, int> freq;
    computeMaskFrequencies(v, freq);

    // Return all possiblg concatenations.
    return pandigitalConcatenations(freq);
}

// Driver code
int main()
{
    vector<string> v = {"123567", "098234", "14765", "19804"};
    cout << countPandigitalPairs(v) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count PanDigital pairs
import java.util.*;

class GFG{

static int pandigitalMask = ((1 << 10) - 1);

static void computeMaskFrequencies(Vector<String> v,
                         HashMap<Integer, Integer> freq)
{
    for(int i = 0; i < v.size(); i++)
    {
        int mask = 0;

        // Stores digits present in String v[i]
        // atleast once. We use a set as we only
        // need digits which exist only once
        // (irrespective of reputation)
        HashSet<Integer> digits = new HashSet<>();
        for(int j = 0; j < v.get(i).length(); j++)
            digits.add(v.get(i).charAt(j) - '0');

        // Calculate the mask by considering
        // all digits existing atleast once
        for(int it :digits)
        {
            int digit = (it);
            mask += (1 << digit);
        }

        // Increment the frequency of
        // this mask
        if (freq.containsKey(mask))
        {
            freq.put(mask, freq.get(mask) + 1);
        }
        else
        {
            freq.put(mask, 1);
        }
    }
}

// Returns number of pairs of Strings
// resulting in Pandigital Concatenations
static int pandigitalConcatenations(
    HashMap<Integer, Integer> freq)
{
    int ans = 0;

    // All possible Strings lie between
    // 1 and 1023 so we iterate over every
    // possible mask
    for(int i = 1; i <= 1023; i++)
    {
        for(int j = 1; j <= 1023; j++)
        {

            // If the concatenation results in mask of
            // Pandigital Concatenation, calculate all
            // pairs formed with Masks i and j
            if ((i | j) == pandigitalMask &&
                      freq.containsKey(j) &&
                      freq.containsKey(i))
            {
                if (i == j)
                    ans += (freq.get(i) *
                           (freq.get(i) - 1));            
                else
                    ans += (freq.get(i) *
                            freq.get(j));            
            }
        }
    }

    // Since every pair is considers twice,
    // we get rid of half of these
    return ans / 2;
}

static int countPandigitalPairs(Vector<String> v)
{

    // Find frequencies of all masks in
    // given vector of Strings
    HashMap<Integer,Integer> freq = new HashMap<>();
    computeMaskFrequencies(v, freq);

    // Return all possiblg concatenations.
    return pandigitalConcatenations(freq);
}

// Driver code
public static void main(String[] args)
{
    Vector<String> v  = new Vector<>();
    v.add("123567");
    v.add("098234");
    v.add("14765");
    v.add("19804");

    System.out.print(countPandigitalPairs(v) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## C#

```
// C# program to count
// PanDigital pairs
using System;
using System.Collections.Generic;
class GFG{

static int pandigitalMask =
           ((1 << 10) - 1);

static void computeMaskFrequencies(List<String> v,
                                   Dictionary<int,
                                   int> freq)
{
  for(int i = 0; i < v.Count; i++)
  {
    int mask = 0;

    // Stores digits present in String v[i]
    // atleast once. We use a set as we only
    // need digits which exist only once
    // (irrespective of reputation)
    HashSet<int> digits = new HashSet<int>();

    for(int j = 0; j < v[i].Length; j++)
      digits.Add(v[i][j] - '0');

    // Calculate the mask by considering
    // all digits existing atleast once
    foreach(int it in digits)
    {
      int digit = (it);
      mask += (1 << digit);
    }

    // Increment the frequency of
    // this mask
    if (freq.ContainsKey(mask))
    {
      freq[mask]++;
    }
    else
    {
      freq.Add(mask, 1);
    }
  }
}

// Returns number of pairs of
// Strings resulting in Pandigital
// Concatenations
static int pandigitalConcatenations(Dictionary<int,
                                    int> freq)
{
  int ans = 0;

  // All possible Strings lie between
  // 1 and 1023 so we iterate over every
  // possible mask
  for(int i = 1; i <= 1023; i++)
  {
    for(int j = 1; j <= 1023; j++)
    {
      // If the concatenation results in
      // mask of Pandigital Concatenation,
      // calculate all pairs formed with
      // Masks i and j
      if ((i | j) == pandigitalMask &&
          freq.ContainsKey(j) &&
          freq.ContainsKey(i))
      {
        if (i == j)
          ans += (freq[i] *
                  (freq[i] - 1));            
        else
          ans += (freq[i] *
                  freq[j]);            
      }
    }
  }

  // Since every pair is considers
  // twice, we get rid of half of
  // these
  return ans / 2;
}

static int countPandigitalPairs(List<String> v)
{   
  // Find frequencies of all masks in
  // given vector of Strings
  Dictionary<int,
             int> freq = new Dictionary<int,
                                        int>();
  computeMaskFrequencies(v, freq);

  // Return all possiblg concatenations.
  return pandigitalConcatenations(freq);
}

// Driver code
public static void Main(String[] args)
{
  List<String> v  = new List<String>();
  v.Add("123567");
  v.Add("098234");
  v.Add("14765");
  v.Add("19804");
  Console.Write(countPandigitalPairs(v) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count PanDigital pairs
const pandigitalMask = ((1 << 10) - 1);

function computeMaskFrequencies(v, freq)
{
    for(let i = 0; i < v.length; i++)
    {
        let mask = 0;

        // Stores digits present in string v[i]
        // atleast once. We use a set as we only
        // need digits which exist only once
        // (irrespective of reputation)
        let digits = new Set();
        for(let j = 0; j < v[i].length; j++)
            digits.add((v[i][j]).charCodeAt(0) -
                             '0'.charCodeAt(0));

        // Calculate the mask by considering
        // all digits existing atleast once
        for(let it of digits)
        {
            let digit = it;
            mask += (1 << digit);
        }

        // Increment the frequency of this mask
        if (freq.has(mask))
        {
            freq.set(mask, freq.get(mask) + 1)
        }
        else
        {
            freq.set(mask, 1)
        }
    }
}

// Returns number of pairs of strings resulting
// in Pandigital Concatenations
function pandigitalConcatenations(freq)
{
    let ans = 0;

    // All possible strings lie between 1 and 1023
    // so we iterate over every possible mask
    for(let i = 1; i <= 1023; i++)
    {
        for(let j = 1; j <= 1023; j++)
        {

            // if the concatenation results in mask of
            // Pandigital Concatenation, calculate all
            // pairs formed with Masks i and j
            if ((i | j) == pandigitalMask &&
                freq.has(i) && freq.has(j))
            {
                if (i == j)
                    ans += (freq.get(i) *
                           (freq.get(i) - 1));
                else
                    ans += (freq.get(i) *
                            freq.get(j));
            }
        }
    }

    // Since every pair is considers twice,
    // we get rid of half of these
    return Math.floor(ans / 2);
}

function countPandigitalPairs(v)
{

    // Find frequencies of all masks in
    // given vector of strings
    let freq = new Map();
    computeMaskFrequencies(v, freq);

    // Return all possiblg concatenations.
    return pandigitalConcatenations(freq);
}

// Driver code
let v = [ "123567", "098234", "14765", "19804" ];
document.write(countPandigitalPairs(v) + "<br>");

// This code is contributed by gfgking

</script>
```

**输出:**

```
3
```

**复杂度:** O(N * |s| + 1023 * 1023)其中|s|给出数组中字符串的长度