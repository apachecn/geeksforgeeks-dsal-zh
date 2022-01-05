# 什么是网络爬虫，在哪里使用？

> 原文:[https://www . geeksforgeeks . org/什么是网络爬虫以及在哪里使用/](https://www.geeksforgeeks.org/what-is-a-webcrawler-and-where-is-it-used/)

**网络爬虫**是一个**机器人**，从互联网上下载内容并进行索引。这个机器人的主要目的是了解互联网上不同的网页。这类机器人大多由搜索引擎操作。通过将[搜索算法](https://www.geeksforgeeks.org/searching-algorithms/)应用于网络爬虫收集的数据，搜索引擎可以提供相关链接作为对用户请求的响应。在本文中，让我们讨论如何实现网络爬虫。

网络爬虫是[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)算法的一个非常重要的应用。这个想法是，整个互联网可以用一个有向图来表示:

*   带顶点->域/网址/网站。
*   边->连接。

**示例:**

![](img/baf808dcd460e2777e956fc619f71617.png)

**方法:**该算法工作背后的思想是解析网站的原始 HTML，并在获得的数据中寻找其他 URL。如果有网址，则将其添加到[队列](https://www.geeksforgeeks.org/queue-data-structure/)中，并以广度优先搜索方式访问它们。

> **注意:**由于代理问题，此代码在联机 IDE 上将不起作用。尝试在本地计算机上运行。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate the WebCrawler

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.URL;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

// Class Contains the functions
// required for WebCrowler
class WebCrowler {

    // To store the URLs in the
    / /FIFO order required for BFS
    private Queue<String> queue;

    // To store visited URls
    private HashSet<String>
        discovered_websites;

    // Constructor for initializing the
    // required variables
    public WebCrowler()
    {
        this.queue
            = new LinkedList<>();

        this.discovered_websites
            = new HashSet<>();
    }

    // Function to start the BFS and
    // discover all URLs
    public void discover(String root)
    {
        // Storing the root URL to
        // initiate BFS.
        this.queue.add(root);
        this.discovered_websites.add(root);

        // It will loop until queue is empty
        while (!queue.isEmpty()) {

            // To store the URL present in
            // the front of the queue
            String v = queue.remove();

            // To store the raw HTML of
            // the website
            String raw = readUrl(v);

            // Regular expression for a URL
            String regex
                = "https://(\\w+\\.)*(\\w+)";

            // To store the pattern of the
            // URL formed by regex
            Pattern pattern
                = Pattern.compile(regex);

            // To extract all the URL that
            // matches the pattern in raw
            Matcher matcher
                = pattern.matcher(raw);

            // It will loop until all the URLs
            // in the current website get stored
            // in the queue
            while (matcher.find()) {

                // To store the next URL in raw
                String actual = matcher.group();

                // It will check whether this URL is
                // visited or not
                if (!discovered_websites
                         .contains(actual)) {

                    // If not visited it will add
                    // this URL in queue, print it
                    // and mark it as visited
                    discovered_websites
                        .add(actual);
                    System.out.println(
                        "Website found: "
                        + actual);

                    queue.add(actual);
                }
            }
        }
    }

    // Function to return the raw HTML
    // of the current website
    public String readUrl(String v)
    {

        // Initializing empty string
        String raw = "";

        // Use try-catch block to handle
        // any exceptions given by this code
        try {
            // Convert the string in URL
            URL url = new URL(v);

            // Read the HTML from website
            BufferedReader be
                = new BufferedReader(
                    new InputStreamReader(
                        url.openStream()));

            // To store the input
            // from the website
            String input = "";

            // Read the HTML line by line
            // and append it to raw
            while ((input
                    = br.readLine())
                   != null) {
                raw += input;
            }

            // Close BufferedReader
            br.close();
        }

        catch (Exception ex) {
            ex.printStackTrace();
        }

        return raw;
    }
}

// Driver code
public class Main {

    // Driver Code
    public static void main(String[] args)
    {
        // Creating Object of WebCrawler
        WebCrowler web_crowler
            = new WebCrowler();

        // Given URL
        String root
            = "https:// www.google.com";

        // Method call
        web_crowler.discover(root);
    }
}
```

**输出:**

```
Website found: https://www.google.com
Website found: https://www.facebook.com
Website found: https://www.amazon.com
Website found: https://www.microsoft.com
Website found: https://www.apple.com
```

**应用:**这类网络爬虫用于获取网页的重要参数，如:

1.  经常访问的网站有哪些？
2.  网络整体有哪些重要的网站？
3.  社交网络上的有用信息:脸书、推特等。
4.  一群人中谁最受欢迎？
5.  谁是公司里最重要的软件工程师？