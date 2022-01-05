# 打印每个字符的字数、元音和频率

> 原文:[https://www . geesforgeks . org/print-number-word-元音-frequency-character/](https://www.geeksforgeeks.org/print-number-words-vowels-frequency-character/)

给定一个带有大写、小写和特殊字符的字符串**。输入字符串以空格或点结束。问题是在单独的一行中计算字符串中每个字符的字数、元音和频率。
**例:**** 

```
**Input :** How Good GOD Is.

**Output :** 
Number of words = 4
Number of vowels = 5
Number of upper case characters = 6
Character =   Frequency = 3
Character = . Frequency = 1
Character = D Frequency = 1
Character = G Frequency = 2
Character = H Frequency = 1
Character = I Frequency = 1
Character = O Frequency = 1
Character = d Frequency = 1
Character = o Frequency = 3
Character = s Frequency = 1
Character = w Frequency = 1
```

****方法:**我们使用[树图](https://www.geeksforgeeks.org/hashmap-treemap-java/)来存储字符及其频率。TreeMap 用于按排序顺序获取输出。
下面是上述方法的 Java 实现:** 

## **C++**

```
// C++ program to print Number of Words,
// Vowels and Frequency of Each Character
#include <bits/stdc++.h>
using namespace std;

void words(string str)
{
    int wcount = 0, ucount = 0, vcount = 0;
    for (int i = 0; i < str.length(); i++)
    {
        char c = str[i];
        switch (c)
        {
            case ' ':
            case '.':
            wcount++; // more delimiters can be given
        }

        switch (c)
        {
            case 'A':
            case 'E':
            case 'I':
            case 'O':
            case 'U':
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                vcount++;
        }

        if (c >= 65 and c <= 90) ucount++;
    }

    cout << "Number of words = "
         << wcount << endl;
    cout << "Number of vowels = "
         << vcount << endl;
    cout << "Number of upper case characters = "
         << ucount << endl;
}

// Function to calculate the frequency
// of each character in the string
void frequency(string str)
{
    // Creates an empty TreeMap
    map<char, int> hmap;

    // Traverse through the given array
    for (int i = 0; i < str.length(); i++)
        hmap[str[i]]++;

    // Print result
    for (auto i : hmap)
    {
        cout << "Character = " << i.first;
        cout << " Frequency = "
             << i.second << endl;
    }
}

// Driver Code
int main(int argc, char const *argv[])
{
    string str = "Geeks for Geeks.";
    words(str);
    frequency(str);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to print Number of Words,
// Vowels and Frequency of Each Character
import java.util.*;
import java.lang.*;
import java.io.*;

public class Stringfun
{
    String str = "Geeks for Geeks.";

    void words()
    {
        int wCount = 0, uCount = 0, vCount = 0;

        for (int i = 0; i < str.length(); i++)
        {
            char c = str.charAt(i);

            switch (c)
            {
            case ' ':
            case '.':
                wCount++; // more delimiters can be given
            }

            switch (c)
            {
            // program for calculating number of vowels
            case 'A':
            case 'E':
            case 'I':
            case 'O':
            case 'U':
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                vCount++;
            }

            if (c >= 65 && c <= 90)
            {
                uCount++;
            }
        }

        System.out.println("Number of words = " + wCount);
        System.out.println("Number of vowels = " + vCount);
        System.out.println("Number of upper case characters = "
                                                        + uCount);
    }

    // Function to calculate the frequency
    // of each character in the string
    void frequency()
    {
        // Creates an empty TreeMap
        TreeMap<Character, Integer> hmap =
                     new TreeMap<Character, Integer>();

        // Traverse through the given array
        for (int i = 0; i < str.length(); i++)
        {
            Integer c = hmap.get(str.charAt(i));

            // If this is first occurrence of element
            if (hmap.get(str.charAt(i)) == null)
               hmap.put(str.charAt(i), 1);

            // If elements already exists in hash map
            else
              hmap.put(str.charAt(i), ++c);
        }

        // Print result
        for (Map.Entry m:hmap.entrySet())
          System.out.println("Character = " + m.getKey() +
                         " Frequency = " + m.getValue());
    }

    // Driver program to run and test above program
    public static void main(String args[]) throws IOException
    {
        Stringfun obj = new Stringfun();
        obj.words();
        obj.frequency();
    }
}
```

## **蟒蛇 3**

```
# Python3 program to print Number of Words,
# Vowels and Frequency of Each Character

# A method to count the number of
# uppercase character, vowels and number of words
def words(str):
    wcount = vcount = ucount = i = 0
    while i < len(str):
        ch = str[i]

        # condition checking for word count
        if (ch == " " or ch == "."):
            wcount += 1

        # condition checking for vowels
        # in lower case    
        if(ch == "a" or ch == "e" or
           ch == "i" or ch == 'o' or ch == "u"):
            vcount += 1

        # condition checking for vowels in uppercase
        if (ch == "A" or ch == "E" or
            ch == "I" or ch == 'O' or ch == "U"):
            vcount += 1

        # condition checking for upper case characters
        if (ord(ch) >= 65 and ord(ch) <= 90):
            ucount += 1
        i += 1

    print("number of words = ", wcount)
    print("number of vowels = ", vcount)
    print("number of upper case characters = ",
                                        ucount)

# a method to print the frequency
# of each character.
def frequency(str):
    i = 1

    # checking each and every
    # ascii code character
    while i < 127:
        ch1 = chr(i)
        c = 0
        j = 0
        while j < len(str):
            ch2 = str[j]
            if(ch1 == ch2):
                c += 1
            j += 1

        # condition to print the frequency
        if c > 0:
            print("Character:", ch1 +
                  " Frequency:", c)
        i += 1

# Driver Code

# sample string to check the code    
s = "Geeks for Geeks."

# function calling
words(s)
frequency(s)

# This code is contributed by Animesh_Gupta
```

****输出:**** 

```
Number of words = 3
Number of vowels = 5
Number of upper case characters = 2
Character =   Frequency = 2
Character = . Frequency = 1
Character = G Frequency = 2
Character = e Frequency = 4
Character = f Frequency = 1
Character = k Frequency = 2
Character = o Frequency = 1
Character = r Frequency = 1
Character = s Frequency = 2
```

**时间复杂度:O(n)，其中 n 是字符串中的字符数。
辅助空间:O(1)。**