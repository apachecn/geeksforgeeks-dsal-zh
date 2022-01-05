# 实现浏览器的后退和前进按钮

> 原文:[https://www . geesforgeks . org/implementing-backward-and-forward-buttons-of-browser/](https://www.geeksforgeeks.org/implementing-backward-and-forward-buttons-of-browser/)

使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)设计浏览器的前进和后退按钮。如果在任何情况下，按下两个按钮后[网址](https://en.wikipedia.org/wiki/URL)不存在，则打印**“不可用”**。否则，打印**当前网址**。

**方法:**想法是使用两个栈**向后**和**向前**来跟踪已访问的 **URL** s 和一个变量“**currentstateul**”来存储当前已访问的 URL。按照以下步骤解决问题:

*   初始化**当前状态网址**，它将存储浏览器的当前网址。
*   初始化两个堆栈**向前堆栈**和**向后堆栈**，它们将存储分别按下向前和向后按钮时访问的网址序列。
*   当访问任何新的网址时，[将其推入**反向堆栈**。](https://www.geeksforgeeks.org/stack-push-method-in-java/)
*   按前进按钮的同时，将**当前状态 URL** 推入**向后堆栈**和**T5[中，弹出**向前堆栈**中的**最后一个 URL** ，并将其设置为**当前状态 URL。**](https://www.geeksforgeeks.org/stack-pop-method-in-java/)**
*   按下后退按钮的同时，将**当前状态 URL** 推入**前进堆栈**，从**后退堆栈**弹出**最后一个 URL** ，并设置为**当前状态 URL** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the current visiting page
string current_state_url = "";

// Stores url when pressed forward
stack<string> forward_stack;

// Stores url when pressed backward
stack<string> backward_stack;

// Function for when visit a url
void visit_new_url(string url)
{
    // If current URL is empty
    if (current_state_url != "") {

        // Push into backward_stack
        backward_stack.push(
            current_state_url);
    }

    // Set curr_state_url to url
    current_state_url = url;
}

// Function to handle state when the
// forward button is pressed
void forward()
{
    // If current url is the last url
    if (forward_stack.empty()
        || current_state_url
               == forward_stack.top()) {
        cout << "Not Available\n";
        return;
    }

    // Otherwise
    else {

        // Push current state to the
        // backward stack
        backward_stack.push(
            current_state_url);

        // Set current state to top
        // of forward stack
        current_state_url
            = forward_stack.top();

        // Remove from forward stack
        forward_stack.pop();
    }
}

// Function to handle state when the
// backward button is pressed
void backward()
{
    // If current url is the last url
    if (backward_stack.empty()
        || current_state_url
               == backward_stack.top()) {

        cout << "Not Available\n";
        return;
    }

    // Otherwise
    else {

        // Push current url to the
        // forward stack
        forward_stack.push(
            current_state_url);

        // Set current url to top
        // of backward stack
        current_state_url
            = backward_stack.top();

        // Pop it from backward stack
        backward_stack.pop();
    }
}

// Function that performs the process
// of pressing forward and backward
// button in a Browser
void simulatorFunction()
{
    // Current URL
    string url = "ajay.com";

    // Visit the current URL
    visit_new_url(url);

    // Print the current URL
    cout << "Current URL is: "
         << current_state_url
         << " \n";

    // New current URL
    url = "abc.com";

    // Visit the current URL
    visit_new_url(url);

    // Print the current URL
    cout << "Current URL is: "
         << current_state_url
         << " \n";

    // Pressed backward button
    backward();

    // Print the current URL
    cout << "Current URL after pressing"
         << " Backward button is: "
         << current_state_url
         << " \n";

    // Pressed forward button
    forward();

    // Print the current URL
    cout << "Current URL after pressing"
         << " Forward button is: "
         << current_state_url
         << " \n";

    // New current URL
    url = "nikhil.com";

    // Visit the current URL
    visit_new_url(url);

    // Print the current URL
    cout << "Current URL is: "
         << current_state_url
         << " \n";

    // Pressed forward button
    forward();

    // Print the current URL
    cout << "Current URL after pressing"
         << " Forward button is: "
         << current_state_url
         << " \n";
    // Pressed backward button
    backward();

    // Print the current URL
    cout << "Current URL after pressing"
         << " Backward button is: "
         << current_state_url
         << " \n";
}

// Driver Code
int main()
{
    // Function to simulate process of
    // pressing forward & backward button
    simulatorFunction();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Stores the current
// visiting page
static String current_state_url = "";

// Stores url when pressed forward
static Stack<String>
       forward_stack = new Stack<>();

// Stores url when pressed backward
static Stack<String>
       backward_stack = new Stack<>();

// Function for when visit a url
static void visit_new_url(String url)
{
  // If current URL is empty
  if (current_state_url != "")
  {
    // Push into backward_stack
    backward_stack.add(
             current_state_url);
  }

  // Set curr_state_url to url
  current_state_url = url;
}

// Function to handle state
// when the forward button
// is pressed
static void forward()
{
  // If current url is the last url
  if (forward_stack.isEmpty() ||
      current_state_url ==
      forward_stack.peek())
  {
    System.out.print("Not Available\n");
    return;
  }

  // Otherwise
  else
  {
    // Push current state to the
    // backward stack
    backward_stack.add(
             current_state_url);

    // Set current state to top
    // of forward stack
    current_state_url =
            forward_stack.peek();

    // Remove from forward
    // stack
    forward_stack.pop();
  }
}

// Function to handle state
// when the backward button
// is pressed
static void backward()
{
  // If current url is the
  // last url
  if (backward_stack.isEmpty() ||
      current_state_url ==
      backward_stack.peek())
  {
    System.out.print("Not Available\n");
    return;
  }

  // Otherwise
  else
  {
    // Push current url to the
    // forward stack
    forward_stack.add(
            current_state_url);

    // Set current url to top
    // of backward stack
    current_state_url =
            backward_stack.peek();

    // Pop it from backward
    // stack
    backward_stack.pop();
  }
}

// Function that performs the
// process of pressing forward
// and backward button in a
// Browser
static void simulatorFunction()
{
  // Current URL
  String url = "ajay.com";

  // Visit the current URL
  visit_new_url(url);

  // Print the current URL
  System.out.print("Current URL is: " +
                   current_state_url +
                   " \n");

  // New current URL
  url = "abc.com";

  // Visit the current URL
  visit_new_url(url);

  // Print the current URL
  System.out.print("Current URL is: " +
                   current_state_url +
                   " \n");

  // Pressed backward button
  backward();

  // Print the current URL
  System.out.print("Current URL after pressing" +
                   " Backward button is: " +
                   current_state_url + " \n");

  // Pressed forward button
  forward();

  // Print the current URL
  System.out.print("Current URL after pressing" +
                   " Forward button is: " +
                   current_state_url + " \n");

    // New current URL
    url = "nikhil.com";

    // Visit the current URL
    visit_new_url(url);

    // Print the current URL
    System.out.print("Current URL is: " +
                     current_state_url +
                     " \n");

    // Pressed forward button
    forward();

    // Print the current URL
    System.out.print("Current URL after pressing" +
                     " Forward button is: " +
                     current_state_url + " \n");
    // Pressed backward button
    backward();

    // Print the current URL
    System.out.print("Current URL after pressing" +
                     " Backward button is: " +
                     current_state_url + " \n");
}

// Driver Code
public static void main(String[] args)
{
  // Function to simulate process of
  // pressing forward & backward button
  simulatorFunction();
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the current
# visiting page
current_state_url = ""

# Stores url when pressed forward
forward_stack = []

# Stores url when pressed backward
backward_stack = []   

# Function for when visit a url
def visit_new_url(url):
  global current_state_url

  # If current URL is empty
  if (current_state_url != ""):
    # Push into backward_stack
    backward_stack.append(current_state_url)

  # Set curr_state_url to url
  current_state_url = url

# Function to handle state
# when the forward button
# is pressed
def forward():
  # If current url is the last url
  if (len(forward_stack) == 0 or current_state_url == forward_stack[-1]):
    print("Not Available")
    return

  # Otherwise
  else:
    # Push current state to the
    # backward stack
    backward_stack.append(current_state_url)

    # Set current state to top
    # of forward stack
    current_state_url = forward_stack[-1]

    # Remove from forward
    # stack
    forward_stack.pop()

# Function to handle state
# when the backward button
# is pressed
def backward():
  # If current url is the
  # last url
  if (len(backward_stack) != 0 or current_state_url == backward_stack[-1]):
    print("Not Available")
    return

  # Otherwise
  else:
    # Push current url to the
    # forward stack
    forward_stack.append(current_state_url)

    # Set current url to top
    # of backward stack
    current_state_url = backward_stack[-1]

    # Pop it from backward
    # stack
    backward_stack[-1]

# Function that performs the
# process of pressing forward
# and backward button in a
# Browser
def simulatorFunction():
  # Current URL
  url = "ajay.com"

  # Visit the current URL
  visit_new_url(url)

  # Print the current URL
  print("Current URL is: " + current_state_url)

  # New current URL
  url = "abc.com"

  # Visit the current URL
  visit_new_url(url)

  # Print the current URL
  print("Current URL is: " + current_state_url)

  # Pressed backward button
  backward()

  # Print the current URL
  print("Current URL after pressing" + " Backward button is: " + current_state_url)

  # Pressed forward button
  forward()

  # Print the current URL
  print("Current URL after pressing" + " Forward button is: " + current_state_url)

  # New current URL
  url = "nikhil.com"

  # Visit the current URL
  visit_new_url(url)

  # Print the current URL
  print("Current URL is: " + current_state_url)

  # Pressed forward button
  forward()

  # Print the current URL
  print("Current URL after pressing" + " Forward button is: " + current_state_url)
  # Pressed backward button
  backward()

  # Print the current URL
  print("Current URL after pressing" + " Backward button is: " + current_state_url)

# Function to simulate process of
# pressing forward & backward button
simulatorFunction()

# This code is contributed by suresh07.
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Stores the current
// visiting page
static String current_state_url = "";

// Stores url when pressed forward
static Stack<String>
       forward_stack = new Stack<String>();

// Stores url when pressed backward
static Stack<String>
       backward_stack = new Stack<String>();     

// Function for when visit a url
static void visit_new_url(String url)
{
  // If current URL is empty
  if (current_state_url != "")
  {
    // Push into backward_stack
    backward_stack.Push(
             current_state_url);
  }

  // Set curr_state_url to url
  current_state_url = url;
}

// Function to handle state
// when the forward button
// is pressed
static void forward()
{
  // If current url is the last url
  if (forward_stack.Count == 0 ||
      current_state_url ==
      forward_stack.Peek())
  {
    Console.Write("Not Available\n");
    return;
  }

  // Otherwise
  else
  {
    // Push current state to the
    // backward stack
    backward_stack.Push(
             current_state_url);

    // Set current state to top
    // of forward stack
    current_state_url =
            forward_stack.Peek();

    // Remove from forward
    // stack
    forward_stack.Pop();
  }
}

// Function to handle state
// when the backward button
// is pressed
static void backward()
{
  // If current url is the
  // last url
  if (backward_stack.Count != 0 ||
      current_state_url ==
      backward_stack.Peek())
  {
    Console.Write("Not Available\n");
    return;
  }

  // Otherwise
  else
  {
    // Push current url to the
    // forward stack
    forward_stack.Push(
            current_state_url);

    // Set current url to top
    // of backward stack
    current_state_url =
            backward_stack.Peek();

    // Pop it from backward
    // stack
    backward_stack.Pop();
  }
}

// Function that performs the
// process of pressing forward
// and backward button in a
// Browser
static void simulatorFunction()
{
  // Current URL
  String url = "ajay.com";

  // Visit the current URL
  visit_new_url(url);

  // Print the current URL
  Console.Write("Current URL is: " +
                current_state_url +
                " \n");

  // New current URL
  url = "abc.com";

  // Visit the current URL
  visit_new_url(url);

  // Print the current URL
  Console.Write("Current URL is: " +
                current_state_url +
                " \n");

  // Pressed backward button
  backward();

  // Print the current URL
  Console.Write("Current URL after pressing" +
                " Backward button is: " +
                current_state_url + " \n");

  // Pressed forward button
  forward();

  // Print the current URL
  Console.Write("Current URL after pressing" +
                " Forward button is: " +
                current_state_url + " \n");

  // New current URL
  url = "nikhil.com";

  // Visit the current URL
  visit_new_url(url);

  // Print the current URL
  Console.Write("Current URL is: " +
                current_state_url +
                " \n");

  // Pressed forward button
  forward();

  // Print the current URL
  Console.Write("Current URL after pressing" +
                " Forward button is: " +
                current_state_url + " \n");
  // Pressed backward button
  backward();

  // Print the current URL
  Console.Write("Current URL after pressing" +
                " Backward button is: " +
                current_state_url + " \n");
}

// Driver Code
public static void Main(String[] args)
{
  // Function to simulate process of
  // pressing forward & backward button
  simulatorFunction();
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Stores the current
    // visiting page
    let current_state_url = "";

    // Stores url when pressed forward
    let forward_stack = [];

    // Stores url when pressed backward
    let backward_stack = []; 

    // Function for when visit a url
    function visit_new_url(url)
    {
      // If current URL is empty
      if (current_state_url != "")
      {
        // Push into backward_stack
        backward_stack.push(current_state_url);
      }

      // Set curr_state_url to url
      current_state_url = url;
    }

    // Function to handle state
    // when the forward button
    // is pressed
    function forward()
    {
      // If current url is the last url
      if (forward_stack.length == 0 ||
          current_state_url == forward_stack[forward_stack.length - 1])
      {
        document.write("Not Available" + "</br>");
        return;
      }

      // Otherwise
      else
      {
        // Push current state to the
        // backward stack
        backward_stack.push(current_state_url);

        // Set current state to top
        // of forward stack
        current_state_url = forward_stack[forward_stack.length - 1];

        // Remove from forward
        // stack
        forward_stack.pop();
      }
    }

    // Function to handle state
    // when the backward button
    // is pressed
    function backward()
    {
      // If current url is the
      // last url
      if (backward_stack.length != 0 ||
          current_state_url ==
          backward_stack[backward_stack.length - 1])
      {
        document.write("Not Available" + "</br>");
        return;
      }

      // Otherwise
      else
      {
        // Push current url to the
        // forward stack
        forward_stack.push(current_state_url);

        // Set current url to top
        // of backward stack
        current_state_url = backward_stack[backward_stack.length - 1];

        // Pop it from backward
        // stack
        backward_stack.pop();
      }
    }

    // Function that performs the
    // process of pressing forward
    // and backward button in a
    // Browser
    function simulatorFunction()
    {
      // Current URL
      let url = "ajay.com";

      // Visit the current URL
      visit_new_url(url);

      // Print the current URL
      document.write("Current URL is: " + current_state_url + "</br>");

      // New current URL
      url = "abc.com";

      // Visit the current URL
      visit_new_url(url);

      // Print the current URL
      document.write("Current URL is: " + current_state_url + "</br>");

      // Pressed backward button
      backward();

      // Print the current URL
      document.write("Current URL after pressing" + " Backward button is: " +
                    current_state_url + " </br>");

      // Pressed forward button
      forward();

      // Print the current URL
      document.write("Current URL after pressing" +
                    " Forward button is: " +
                    current_state_url + " </br>");

      // New current URL
      url = "nikhil.com";

      // Visit the current URL
      visit_new_url(url);

      // Print the current URL
      document.write("Current URL is: " +
                    current_state_url +
                    " </br>");

      // Pressed forward button
      forward();

      // Print the current URL
      document.write("Current URL after pressing" +
                    " Forward button is: " +
                    current_state_url + " </br>");
      // Pressed backward button
      backward();

      // Print the current URL
      document.write("Current URL after pressing" +
                    " Backward button is: " +
                    current_state_url + " </br>");
    }

    // Function to simulate process of
    // pressing forward & backward button
    simulatorFunction();

// This code is contributed by rameshtravel07.
</script>
```

**Output**

```
Current URL is: ajay.com 
Current URL is: abc.com 
Current URL after pressing Backward button is: ajay.com 
Current URL after pressing Forward button is: abc.com 
Current URL is: nikhil.com 
Not Available
Current URL after pressing Forward button is: nikhil.com 
Current URL after pressing Backward button is: abc.com 
```

**时间复杂度:** O(N)。
***辅助空间:** O(N)。*