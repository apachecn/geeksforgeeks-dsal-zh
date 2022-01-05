# Python |删除 IP 地址的前导零

> 原文:[https://www . geesforgeks . org/python-remove-前导零-ip-address/](https://www.geeksforgeeks.org/python-remove-leading-zeros-ip-address/)

给定一个 IP 地址，从 IP 地址中删除前导零。

**示例:**

```
Input : 100.020.003.400 
Output : 100.20.3.400

Input :001.200.001.004  
Output : 1.200.1.4

```

**方法 1:遍历并连接**

**方法**是将给定的字符串拆分为“.”然后将其转换为整数，去掉前导零，再将它们连接回字符串。要将字符串转换为整数，我们可以使用[int](https://www.geeksforgeeks.org/type-conversion-python/)，然后通过[str](https://www.geeksforgeeks.org/type-conversion-python/)将其转换回字符串，然后使用 join 函数将其连接回来。

```
# Python program to remove leading zeros 
# an IP address and print the IP

# function to remove leading zeros
def removeZeros(ip):

    # splits the ip by "."
    # converts the words to integeres to remove leading removeZeros 
    # convert back the integer to string and join them back to a string
    new_ip = ".".join([str(int(i)) for i in ip.split(".")])  
    return new_ip ;

# driver code   
# example1
ip ="100.020.003.400"  
print(removeZeros(ip))

# example2
ip ="001.200.001.004"
print(removeZeros(ip))
```

**输出:**

```
100.20.3.400
1.200.1.4

```

**方法二:[Regex](https://www.geeksforgeeks.org/regular-expression-python-examples-set-1/)T3】**

使用捕获组，匹配最后一个数字并复制它，防止所有数字被替换。

[regex \d](https://www.geeksforgeeks.org/regular-expression-python-examples-set-1/) 可以解释为:

*   **\d :** 匹配任意十进制数字

    ```
    **\d   Matches any decimal digit, this is equivalent
         to the set class [0-9].**
    ```

*   \b 允许您使用正则表达式执行“仅整句话”搜索，正则表达式的形式可以解释为:

    ```
    \b allows you to perform a "whole words only" search u
    sing a regular expression in the form of \bword\b
    ```

```
# Python program to remove leading zeros 
# an IP address and print the IP using regex
import re 

# function to remove leading zeros
def removeZeros(ip):
    new_ip = re.sub(r'\b0+(\d)', r'\1', ip)
    # splits the ip by "."
    # converts the words to integeres to remove leading removeZeros 
    # convert back the integer to string and join them back to a string

    return new_ip 

# driver code   
# example1
ip ="100.020.003.400"  
print(removeZeros(ip))

# example2
ip ="001.200.001.004"
print(removeZeros(ip))
```

**输出:**

```
100.20.3.400
1.200.1.4

```