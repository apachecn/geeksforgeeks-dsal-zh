# 解析 Java 中的 Apache 访问日志

> 原文：[https://www.geeksforgeeks.org/parsing-apache-access-log-in-java/](https://www.geeksforgeeks.org/parsing-apache-access-log-in-java/)

Web 服务器日志，用于维护页面请求的历史记录，通常记录在文件末尾。 通常会添加有关请求的信息，包括客户端 IP 地址，请求日期/时间，请求的页面，HTTP 代码，服务的字节，用户代理和引荐来源网址。

给定一个 Web 服务器日志记录，找到具有成功响应的 IP 地址成功 HTTL 响应的总数（200 个代码）。

例子：

```
Input : Sample Access Log
192.168.1.2 - - [17/Sep/2013:22:18:19 -0700] "GET /abc HTTP/1.1" 404 201
192.168.1.2 - - [17/Sep/2013:22:18:19 -0700] "GET /favicon.ico HTTP/1.1" 200 1406
192.168.1.2 - - [17/Sep/2013:22:18:27 -0700] "GET /wp/ HTTP/1.1" 200 5325
192.168.1.2 - - [17/Sep/2013:22:18:27 -0700] "GET /wp/wp-content/themes/twentytwelve/style.css?ver=3.5.1 HTTP/1.1" 200 35292
192.168.1.3 - - [17/Sep/2013:22:18:27 -0700] "GET /wp/wp-content/themes/twentytwelve/js/navigation.js?ver=1.0 HTTP/1.1" 200 863

Output :
192.168.1.3 1
192.168.1.2 3

```

先决条件： [Java 正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)

```
// Java program to count the no. of IP address
// count for successful http response 200 code.
import java.io.*;
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
class FindSuccessIpCount {
public static void findSuccessIpCount(String record)
{
// Creating a regular expression for the records
final String regex = "^(\\S+) (\\S+) (\\S+) " +
"\\[([\\w:/]+\\s[+\\-]\\d{4})\\] \"(\\S+)" +
" (\\S+)\\s*(\\S+)?\\s*\" (\\d{3}) (\\S+)" ;
final Pattern pattern = Pattern.compile(regex, Pattern.MULTILINE);
final Matcher matcher = pattern.matcher(record);
// Creating a Hashmap containing string as
// the key and integer as the value.
HashMap<String, Integer> countIP = new HashMap<String, Integer>();
while (matcher.find()) {
String IP = matcher.group( 1 );
String Response = matcher.group( 8 );
int response = Integer.parseInt(Response);
// Inserting the IP addresses in the
// HashMap and maintaining the frequency
// for each HTTP 200 code.
if (response == 200 ) {
if (countIP.containsKey(IP)) {
countIP.put(IP, countIP.get(IP) + 1 );
}
else {
countIP.put(IP, 1 );
}
}
}
// Printing the hashmap
for (Map.Entry entry : countIP.entrySet()) {
System.out.println(entry.getKey() + " " + entry.getValue());
}
[HTG11 1] }
public static void main(String[] args)
{
final String log = "123.123.123.123 - - [26/Apr/2000:00:23:48 -0400] \"GET /pics/wpaper.gif HTTP/1.0\" 200 6248 \"http:// www.jafsoft.com/asctortf/\" \"Mozilla/4.05 (Macintosh; I; PPC)\"\n"
+ "123.123.123.123 - - [26/Apr/2000:00:23:47 -0400] \"GET /asctortf/ HTTP/1.0\" 200 8130 \"http:// search.netscape.com/Computers/Data_Formats/Document/Text/RTF\" \"Mozilla/4.05 (Macintosh; I; PPC)\"\n"
+ "123.123.123.124 - - [26/Apr/2000:00:23:48 -0400] \"GET /pics/5star2000.gif HTTP/1.0\" 200 4005 \"http:// www.jafsoft.com/asctortf/\" \"Mozilla/4.05 (Macintosh; I; PPC)\"\n"
+ "123.123.123.123 - - [26/Apr/2000:00:23:50 -0400] \"GET /pics/5star.gif HTTP/1.0\" 404 1031 \"http:// www.jafsoft.com/asctortf/\" \"Mozilla/4.05 (Macintosh; I; PPC)\"\n"
+ "123.123.123.126 - - [26/Apr/2000:00:23:51 -0400] \"GET /pics/a2hlogo.jpg HTTP/1.0\" 200 4282 \"http:// www.jafsoft.com/asctortf/\" \"Mozilla/4.05 (Macintosh; I; PPC)\"\n"
+ "123.123.123.123 - - [26/Apr/2000:00:23:51 -0400] \"GET /cgi-bin/newcount?jafsof3&width=4&font=digital&noshow HTTP/1.0\" 200 36 \"http:// www.jafsoft.com/asctortf/\" \"Mozilla/4.05 (Macintosh; I; PPC)\"\n" ;
findSuccessIpCount(log);
}
}
```

**Output:**

```
123.123.123.126 1
123.123.123.124 1
123.123.123.123 3

```



* * *

* * *



