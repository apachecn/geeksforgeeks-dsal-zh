# 设计一个可以提供最大频率元素的堆栈

给定 **N** 个元素，任务是实现一个堆栈，该堆栈将在每次弹出操作中删除并返回最大频率元素。 如果频率相等，则将返回最高频率元素。

**示例**：

> **输入**：
>
> ```
> push(4) 8
> push(6) 6
> push(7) 7
> push(6) 6
> push(8); 4
> ```
> 
> **输出**：
> 
> `pop()`返回 6，因为 6 是最常见的（频率`6 = 2`）。
> 
> `pop()`返回 8（6 的频率也最高，但不是最高）

**方法**：维护两个[`HashMap`](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)，一个是频率`HashMap`，它将元素映射到它们的频率，另一个是`setMap`，将所有具有相同频率的元素映射到一组（堆栈）。

`FrequencyStack`具有 2 个功能：

1.  **push（int x）**：使用频率 HashMap 映射元素（x）并更新 maxfreq 变量（即，直到现在都保持最大频率）。 **setMap** 维护一个堆栈，其中包含所有具有相同频率的元素。
2.  **pop（）**：首先从 setMap 中获取 maxfreq 元素，然后降低弹出元素的频率。 弹出后，如果堆栈变空，则减小 maxfreq。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 

#include<bits/stdc++.h> 

using namespace std; 

// freqMap is to map element to its frequency 

map<int, int> freqMap; 

// setMap is to map frequency to the 

// element list with this frequency 

map<int, stack<int> > setMap; 

// Variable which stores maximum frequency 

// of the stack element 

int maxfreq = 0; 

// Function to insert x in the stack 

void push(int x) 

{ 

    // Frequency of x 

    int freq = freqMap[x] + 1; 

    // Mapping of x with its frequency 

    freqMap[x]= freq; 

    // Update maxfreq variable 

    if (freq > maxfreq) 

        maxfreq = freq; 

    // Map element to its frequency list 

    // If given frequency list doesn't exist 

    // make a new list of the required frequency 

    setMap[freq].push(x); 

} 

// Function to remove maximum frequency element 

int pop() 

{ 

    // Remove element from setMap 

    // from maximum frequency list 

    int top = setMap[maxfreq].top(); 

    setMap[maxfreq].pop(); 

    // Decrement the frequency of the popped element 

    freqMap[top]--; 

    // If whole list is poppped 

    // then decrement the maxfreq 

    if (setMap[maxfreq].size() == 0) 

        maxfreq--; 

    return top; 

} 

// Driver code 

int main() 

{ 

    // Push elements to the stack 

    push(4); 

    push(6); 

    push(7); 

    push(6); 

    push(8); 

    // Pop elements 

    cout << (pop()) << "\n" ; 

    cout << (pop()); 

    return 0; 

} 

// This code is contributed by Arnab Kundu 

```

## Java

```java

// Java implementation of the approach 

import java.util.*; 

public class freqStack { 

    // freqMap is to map element to its frequency 

    static Map<Integer, Integer> freqMap = new HashMap<>(); 

    // setMap is to map frequency to the 

    // element list with this frequency 

    static Map<Integer, Stack<Integer> > setMap = new HashMap<>(); 

    // Variable which stores maximum frequency 

    // of the stack element 

    static int maxfreq = 0; 

    // Function to insert x in the stack 

    public static void push(int x) 

    { 

        // Frequency of x 

        int freq = freqMap.getOrDefault(x, 0) + 1; 

        // Mapping of x with its frequency 

        freqMap.put(x, freq); 

        // Update maxfreq variable 

        if (freq > maxfreq) 

            maxfreq = freq; 

        // Map element to its frequency list 

        // If given frequency list doesn't exist 

        // make a new list of the required frequency 

        setMap.computeIfAbsent(freq, z -> new Stack()).push(x); 

    } 

    // Function to remove maximum frequency element 

    public static int pop() 

    { 

        // Remove element from setMap 

        // from maximum frequency list 

        int top = setMap.get(maxfreq).pop(); 

        // Decrement the frequency of the popped element 

        freqMap.put(top, freqMap.get(top) - 1); 

        // If whole list is poppped 

        // then decrement the maxfreq 

        if (setMap.get(maxfreq).size() == 0) 

            maxfreq--; 

        return top; 

    } 

    // Driver code 

    public static void main(String[] args) 

    { 

        // Push elements to the stack 

        push(4); 

        push(6); 

        push(7); 

        push(6); 

        push(8); 

        // Pop elements 

        System.out.println(pop()); 

        System.out.println(pop()); 

    } 

} 

```

## Python3

```py

# Python3 implementation of the approach  

# freqMap is to map element to its frequency  

freqMap = {};  

# setMap is to map frequency to the  

# element list with this frequency  

setMap = {};  

# Variable which stores maximum frequency  

# of the stack element  

maxfreq = 0;  

# Function to insert x in the stack  

def push(x) : 

    global maxfreq; 

    if x not in freqMap : 

        freqMap[x] = 0

    # Frequency of x 

    freq = freqMap[x] + 1; 

    # Mapping of x with its Frequency 

    freqMap[x]= freq 

    # Update maxfreq Variable 

    if (freq > maxfreq) : 

        maxfreq = freq 

    # Map element to its frequency list 

    # If given frequency list doesn't exist 

    # make a new list of the required frequency 

    if freq not in setMap : 

        setMap[freq] = [] 

    setMap[freq].append(x);  

# Function to remove maximum frequency element  

def pop() : 

    global maxfreq 

    # Remove element from setMap 

    # from maximum frequency list 

    top = setMap[maxfreq][-1]; 

    setMap[maxfreq].pop(); 

    # Decrement the frequency 

    # of the popped element 

    freqMap[top] -= 1; 

    # If whole list is poppped 

    # then decrement the maxfreq 

    if (len(setMap[maxfreq]) == 0) : 

        maxfreq -= 1; 

    return top;  

# Driver code  

if __name__ == "__main__" :  

    # Push elements to the stack  

    push(4);  

    push(6);  

    push(7);  

    push(6);  

    push(8);  

    # Pop elements  

    print(pop()) ;  

    print(pop());  

# This code is contributed by AnkitRai01  

```

**Output:**

```

6

8

```



* * *

* * *



