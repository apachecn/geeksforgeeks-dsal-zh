# 从 N 个具有单位相邻差的连续整数的给定频率构建序列

> 原文:[https://www . geeksforgeeks . org/construct-a-sequence-from-给定频率的 n 个相邻单位差整数/](https://www.geeksforgeeks.org/construct-a-sequence-from-given-frequencies-of-n-consecutive-integers-with-unit-adjacent-difference/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **freq[]** ，该数组存储从 **0 到 N–1**的 **N** 整数的频率。任务是构造一个序列，其中数字 I 出现 freq[i]次(0≤I≤N–1)，使得两个相邻数字之间的绝对差为 1。如果无法生成任何序列，则打印 **-1** 。

**示例:**

> **输入:** freq[] = {2，2，2，3，1}
> **输出:**0 1 0 1 2 3 3 4 3
> **解释:**
> 上述序列中相邻数字的绝对差始终为 1。
> 
> **输入:** freq[] = {1，2，3}
> **输出:** -1
> **解释:**
> 不可能有绝对差永远为 1 的序列。

**方法:**序列可以从 **0 和 N–1**之间的任意数字开始。想法是考虑起始元素的所有可能性，即 **0 到 N–1**。选择元素后，我们尝试构建序列。以下是步骤:

1.  创建一个[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 来存储数字的频率。另外，在一个变量中找到频率的总和，比如说**总数**。
2.  迭代地图，并对地图中的每个元素执行以下操作:
    *   创建地图副本 **M** 。
    *   创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **序列**，存储可能的答案。如果当前元素的频率为非零，则降低其频率并将其推入**序列**，并尝试按以下方式形成序列的其余**总计–1**元素:
        1.  让我们将插入到**序列**中的最后一个元素称为**最后一个**。如果 last-1 的频率不为零，则降低其频率并将其推入**序列**。更新最后一个**元素。**
        2.  否则，如果**最后+ 1** 的频率为非零，则递减其频率并将其推入**序列**。更新最后一个**元素。**
        3.  否则，从内部循环中断开。
    *   如果**序列**的大小等于**总数**，则将其作为答案返回。
    *   如果没有找到这样的序列，那么就返回一个空序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function generates the sequence
vector<int> generateSequence(int* freq,
                             int n)
{
    // Map to store the frequency
    // of numbers
    map<int, int> m;

    // Sum of all frequencies
    int total = 0;

    for (int i = 0; i < n; i++) {
        m[i] = freq[i];

        total += freq[i];
    }

    // Try all possibilities
    // for the starting element
    for (int i = 0; i < n; i++) {

        // If the frequency of current
        // element is non-zero
        if (m[i]) {

            // vector to store the answer
            vector<int> sequence;

            // Copy of the map for every
            // possible starting element
            auto mcopy = m;

            // Decrement the frequency
            mcopy[i]--;

            // Push the starting element
            // to the vector
            sequence.push_back(i);

            // The last element inserted
            // is i
            int last = i;

            // Try to fill the rest of
            // the positions if possible
            for (int i = 0;
                 i < total - 1; i++) {

                // If the frequency of last - 1
                // is non-zero

                if (mcopy[last - 1]) {

                    // Decrement the frequency
                    // of last - 1
                    mcopy[last - 1]--;

                    // Insert  it into the
                    // sequence
                    sequence.push_back(last - 1);

                    // Update last number
                    // added to sequence
                    last--;
                }

                else if (mcopy[last + 1]) {
                    mcopy[last + 1]--;
                    sequence.push_back(last + 1);
                    last++;
                }

                // Break from the inner loop
                else
                    break;
            }

            // If the size of the sequence
            // vector is equal to sum of
            // total frequqncies
            if (sequence.size() == total) {

                // Return sequence
                return sequence;
            }
        }
    }

    vector<int> empty;

    // If no such sequence if found
    // return empty sequence
    return empty;
}

// Function Call to print the sequence
void PrintSequence(int freq[], int n)
{
    // The required sequence
    vector<int> sequence
        = generateSequence(freq, n);

    // If the size of sequence
    // if zero it means no such
    // sequence was found
    if (sequence.size() == 0) {
        cout << "-1";
    }

    // Otherwise print the sequence
    else {

        for (int i = 0;
             i < sequence.size(); i++) {
            cout << sequence[i] << " ";
        }
    }
}

// Driver Code
int main()
{
    // Frequency of all elements
    // from 0 to n-1
    int freq[] = { 2, 2, 2, 3, 1 };

    // Number of elements whose
    // frequencies are given
    int N = 5;

    // Function Call
    PrintSequence(freq, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function generates the sequence
static Vector<Integer> generateSequence(int []freq,
                                        int n)
{

    // Map to store the frequency
    // of numbers
    HashMap<Integer,
            Integer> m = new HashMap<Integer,
                                     Integer>();

    // Sum of all frequencies
    int total = 0;

    for(int i = 0; i < n; i++)
    {
        m.put(i, freq[i]);
        total += freq[i];
    }

    // Try all possibilities
    // for the starting element
    for(int i = 0; i < n; i++)
    {

        // If the frequency of current
        // element is non-zero
        if (m.containsKey(i))
        {

            // vector to store the answer
            Vector<Integer> sequence = new Vector<Integer>();

            // Copy of the map for every
            // possible starting element
            @SuppressWarnings("unchecked")
            HashMap<Integer,
                    Integer> mcopy = (HashMap<Integer,
                                              Integer>) m.clone();

            // Decrement the frequency
            if (mcopy.containsKey(i) && mcopy.get(i) > 0)
                mcopy.put(i, mcopy.get(i) - 1);

            // Push the starting element
            // to the vector
            sequence.add(i);

            // The last element inserted
            // is i
            int last = i;

            // Try to fill the rest of
            // the positions if possible
            for(int i1 = 0; i1 < total - 1; i1++)
            {

                // If the frequency of last - 1
                // is non-zero
                if (mcopy.containsKey(last - 1) &&
                            mcopy.get(last - 1) > 0)
                {

                    // Decrement the frequency
                    // of last - 1
                    mcopy.put(last - 1,
                    mcopy.get(last - 1) - 1);

                    // Insert  it into the
                    // sequence
                    sequence.add(last - 1);

                    // Update last number
                    // added to sequence
                    last--;
                }

                else if (mcopy.containsKey(last + 1))
                {
                    mcopy.put(last + 1,
                    mcopy.get(last + 1) - 1);
                    sequence.add(last + 1);
                    last++;
                }

                // Break from the inner loop
                else
                    break;
            }

            // If the size of the sequence
            // vector is equal to sum of
            // total frequqncies
            if (sequence.size() == total)
            {

                // Return sequence
                return sequence;
            }
        }
    }

    Vector<Integer> empty = new Vector<Integer>();

    // If no such sequence if found
    // return empty sequence
    return empty;
}

// Function call to print the sequence
static void PrintSequence(int freq[], int n)
{

    // The required sequence
    Vector<Integer> sequence = generateSequence(freq, n);

    // If the size of sequence
    // if zero it means no such
    // sequence was found
    if (sequence.size() == 0)
    {
        System.out.print("-1");
    }

    // Otherwise print the sequence
    else
    {
        for(int i = 0; i < sequence.size(); i++)
        {
            System.out.print(sequence.get(i) + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Frequency of all elements
    // from 0 to n-1
    int freq[] = { 2, 2, 2, 3, 1 };

    // Number of elements whose
    // frequencies are given
    int N = 5;

    // Function call
    PrintSequence(freq, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function generates the sequence
def generateSequence(freq, n):

    # Map to store the frequency
    # of numbers
    m = {}

    # Sum of all frequencies
    total = 0

    for i in range(n):
        m[i] = freq[i]
        total += freq[i]

    # Try all possibilities
    # for the starting element
    for i in range(n):

        # If the frequency of current
        # element is non-zero
        if (m[i]):

            # vector to store the answer
            sequence = []

            # Copy of the map for every
            # possible starting element
            mcopy = {}

            for j in m:
                mcopy[j] = m[j]

            # Decrement the frequency
            mcopy[i] -= 1

            # Push the starting element
            # to the vector
            sequence.append(i)

            # The last element inserted
            # is i
            last = i

            # Try to fill the rest of
            # the positions if possible
            for j in range(total - 1):

                # If the frequency of last - 1
                # is non-zero
                if ((last - 1) in mcopy and
                   mcopy[last - 1] > 0):

                    # Decrement the frequency
                    # of last - 1
                    mcopy[last - 1] -= 1

                    # Insert  it into the
                    # sequence
                    sequence.append(last - 1)

                    # Update last number
                    # added to sequence
                    last -= 1

                elif (mcopy[last + 1]):
                    mcopy[last + 1] -= 1
                    sequence.append(last + 1)
                    last += 1

                # Break from the inner loop
                else:
                    break

            # If the size of the sequence
            # vector is equal to sum of
            # total frequqncies
            if (len(sequence) == total):

                # Return sequence
                return sequence

    # If no such sequence if found
    # return empty sequence
    return []

# Function Call to print the sequence
def PrintSequence(freq, n):

    # The required sequence
    sequence = generateSequence(freq, n)

    # If the size of sequence
    # if zero it means no such
    # sequence was found
    if (len(sequence) == 0):
        print("-1")

    # Otherwise print the sequence
    else:
        for i in range(len(sequence)):
            print(sequence[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Frequency of all elements
    # from 0 to n-1
    freq = [ 2, 2, 2, 3, 1 ]

    # Number of elements whose
    # frequencies are given
    N = 5

    # Function Call
    PrintSequence(freq, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function generates the sequence
static List<int> generateSequence(int []freq,
                                  int n)
{
  // Map to store the frequency
  // of numbers
  Dictionary<int,
             int> m = new Dictionary<int,
                                     int>();

  // Sum of all frequencies
  int total = 0;

  for(int i = 0; i < n; i++)
  {
    m.Add(i, freq[i]);
    total += freq[i];
  }

  // Try all possibilities
  // for the starting element
  for(int i = 0; i < n; i++)
  {
    // If the frequency of current
    // element is non-zero
    if (m.ContainsKey(i))
    {
      // vector to store the answer
      List<int> sequence = new List<int>();

      // Copy of the map for every
      // possible starting element

      Dictionary<int,
                 int> mcopy = new Dictionary<int,
                                             int>(m);

      // Decrement the frequency
      if (mcopy.ContainsKey(i) && mcopy[i] > 0)
        mcopy[i] = mcopy[i] - 1;

      // Push the starting element
      // to the vector
      sequence.Add(i);

      // The last element inserted
      // is i
      int last = i;

      // Try to fill the rest of
      // the positions if possible
      for(int i1 = 0; i1 < total - 1; i1++)
      {
        // If the frequency of last - 1
        // is non-zero
        if (mcopy.ContainsKey(last - 1) &&
            mcopy[last - 1] > 0)
        {
          // Decrement the frequency
          // of last - 1
          mcopy[last - 1] = mcopy[last - 1] - 1;

          // Insert  it into the
          // sequence
          sequence.Add(last - 1);

          // Update last number
          // added to sequence
          last--;
        }

        else if (mcopy.ContainsKey(last + 1))
        {
          mcopy[last + 1] = mcopy[last + 1] - 1;
          sequence.Add(last + 1);
          last++;
        }

        // Break from the inner loop
        else
          break;
      }

      // If the size of the sequence
      // vector is equal to sum of
      // total frequqncies
      if (sequence.Count == total)
      {
        // Return sequence
        return sequence;
      }
    }
  }

  List<int> empty = new List<int>();

  // If no such sequence if found
  // return empty sequence
  return empty;
}

// Function call to print the sequence
static void PrintSequence(int []freq, int n)
{
  // The required sequence
  List<int> sequence = generateSequence(freq, n);

  // If the size of sequence
  // if zero it means no such
  // sequence was found
  if (sequence.Count == 0)
  {
    Console.Write("-1");
  }

  // Otherwise print the sequence
  else
  {
    for(int i = 0; i < sequence.Count; i++)
    {
      Console.Write(sequence[i] + " ");
    }
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Frequency of all elements
  // from 0 to n-1
  int []freq = {2, 2, 2, 3, 1};

  // Number of elements whose
  // frequencies are given
  int N = 5;

  // Function call
  PrintSequence(freq, N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function generates the sequence
function generateSequence(freq, n)
{

    // Map to store the frequency
    // of numbers
    let m = new Map();

    // Sum of all frequencies
    let total = 0;

    for(let i = 0; i < n; i++)
    {
        m.set(i, freq[i]);
        total += freq[i];
    }

    // Try all possibilities
    // for the starting element
    for(let i = 0; i < n; i++)
    {

        // If the frequency of current
        // element is non-zero
        if (m.has(i))
        {

            // vector to store the answer
            let sequence = [];

            // Copy of the map for every
            // possible starting element

            let mcopy = new Map();
            for(let [key, value] of m.entries())
            {
                mcopy.set(key,value);
            }

            // Decrement the frequency
            if (mcopy.has(i) && mcopy.get(i) > 0)
                mcopy.set(i, mcopy.get(i) - 1);

            // Push the starting element
            // to the vector
            sequence.push(i);

            // The last element inserted
            // is i
            let last = i;

            // Try to fill the rest of
            // the positions if possible
            for(let i1 = 0; i1 < total - 1; i1++)
            {

                // If the frequency of last - 1
                // is non-zero
                if (mcopy.has(last - 1) &&
                            mcopy.get(last - 1) > 0)
                {

                    // Decrement the frequency
                    // of last - 1
                    mcopy.set(last - 1,
                    mcopy.get(last - 1) - 1);

                    // Insert  it into the
                    // sequence
                    sequence.push(last - 1);

                    // Update last number
                    // added to sequence
                    last--;
                }

                else if (mcopy.has(last + 1))
                {
                    mcopy.set(last + 1,
                    mcopy.get(last + 1) - 1);
                    sequence.push(last + 1);
                    last++;
                }

                // Break from the inner loop
                else
                    break;
            }

            // If the size of the sequence
            // vector is equal to sum of
            // total frequqncies
            if (sequence.length == total)
            {

                // Return sequence
                return sequence;
            }
        }
    }

    let empty = [];

    // If no such sequence if found
    // return empty sequence
    return empty;
}

// Function call to print the sequence
function PrintSequence(freq, n)
{

    // The required sequence
    let sequence = generateSequence(freq, n);

    // If the size of sequence
    // if zero it means no such
    // sequence was found
    if (sequence.length == 0)
    {
        document.write("-1");
    }

    // Otherwise print the sequence
    else
    {
        for(let i = 0; i < sequence.length; i++)
        {
            document.write(sequence[i] + " ");
        }
    }
}

// Driver Code

// Frequency of all elements
// from 0 to n-1
let freq = [ 2, 2, 2, 3, 1 ];

// Number of elements whose
// frequencies are given
let N = 5;

// Function call
PrintSequence(freq, N);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
0 1 0 1 2 3 2 3 4 3
```

**时间复杂度:** *O(N * total)* ，其中 N 为数组的大小，total 为数组的累计和。
**辅助空间:** *O(合计)*，其中合计为数组的累计和。