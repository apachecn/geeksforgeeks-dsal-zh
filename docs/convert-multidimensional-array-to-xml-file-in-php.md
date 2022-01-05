# 在 PHP 中将多维数组转换为 XML 文件

> 原文:[https://www . geesforgeks . org/convert-多维-数组-xml-file-in-php/](https://www.geeksforgeeks.org/convert-multidimensional-array-to-xml-file-in-php/)

给定一个多维数组，任务是将这个数组转换成一个 XML 文件。要将多维数组转换为 xml 文件，请创建一个 XML 文件，并使用 appendChild()和 createElement()函数将数组元素添加到 XML 文件中。

**示例:**

*   首先，创建一个 PHP 多维数组，用于将该数组转换为 XML 文件格式。

    ```
    $array = array (
        'company' => 'Gfg',
        'employe' => array (
            '0' => array (
                'name' => 'Jatin Das',
                'age' => '34'
            ),
            '1' => array (
                'name' => 'Mohit Mal',
                'age' => '30'
            ),
            '2' => array (
                'name' => 'Shubham Jha',
                'age' => '24'
            ),
            '3' => array (
                'name' => 'Harsha Bhosle',
                'age' => '29'
            )
        )
    );
    ```

*   现在，您需要创建一个用户定义的函数 generatXML()。

    ```
    function generateXML($data) {

        $title = $data['company'];
        $rowCount = count($data['employe']);

        // Create the xml document
        $xmlDoc = new DOMDocument();

        $root = $xmlDoc -> appendChild($xmlDoc ->
                                createElement("geeks"));

        $root -> appendChild($xmlDoc -> 
                            createElement("title", $title));
        $root -> appendChild($xmlDoc -> 
                      createElement("totalRows", $rowCount));

        $tabUsers = $root -> appendChild($xmlDoc ->
                                createElement('rows'));

        foreach($data['employe'] as $user) {
            if (!empty($user)) {
                $tabUser = $tabUsers -> appendChild($xmlDoc -> 
                                       createElement('employe'));
                foreach($user as $key => $val) {
                    $tabUser -> appendChild($xmlDoc ->
                                      createElement($key, $val));
                }
            }
        }

        header("Content-Type: text/plain");

        // Make the output
        $xmlDoc -> formatOutput = true;

        // Save xml file
        $file_name = str_replace(' ', '_', $title) . '.xml';

        $xmlDoc -> save($file_name);

        // Return xml file name
        return $file_name;
    }
    ```

*   然后使用 **generateXML()** 函数，在其中传递数组数据，将数组转换成 PHP 中的 XML。

    ```
    generateXML($array);
    ```

*   **输出:**

    ```
    <geeks>
        <title>Gfg</title>
        <totalRows>4</totalRows>
        <rows>
            <employe>
                <name>Jatin Das</name>
                <age>34</age>
            </employe>
            <employe>
                <name>Mohit Mal</name>
                <age>30</age>
            </employe>
            <employe>
                <name>Shubham Jha</name>
                <age>24</age>
            </employe>
            <employe>
                <name>Harsha Bhosle</name>
                <age>29</age>
            </employe>
        </rows>
    </geeks>
    ```