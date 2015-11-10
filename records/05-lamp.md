# Web系统概论培训记录（5）

------



###PHP基础知识指导（2015.11.09）
记录人：曾祥意

###课前
主要是针对上周js实现计算器的情况作了一些说明
####整体情况
- js代码整体情况写的不错，代码规范性做得比较好
- 计算器输入的情况有很多，需要考虑清楚，如计算器连续输入情况，比如输入：1+2 - ，按下等号后应该输出3

####细节问题
- **文件分离**: 在HTML中可以使用 &lt;style>&lt;/style>标签，嵌入CSS代码，也可以使用&lt;script>&lt;/script>, 嵌入JS代码。类似的，可以在JS中使用innerHTML属性嵌入HTML代码，也可以访问style对象修改样式。但是考虑到代码的调试和维护性，不建议让HTML，CSS，JS代码过于紧密，应该将三者分离出来，各司其职。比如：&lt; button onclick = "cal()">可以改为js绑定事件；js修改样式，可以改为设置多个class，在JS中用切换class等。
- **泛化特化**：在计算器的设计中，按键可分为num，operation，equal这些类，由于它们都是按键，在大小，边框样式，边距等样式都是一样的，不同样式可能只是背景颜色而已，这就表明它们在样式上有公共的性质，但又有各自的特殊之处，所以可以考虑使用类似于cal-button的类，公共样式只用书写一次，特殊的样式再各自设置。
- **Camel命名法**：当变量名或函式名是由一个或多个单字连结在一起，而构成的唯一识别字时，第一个单词以小写字母开始；第二个单词的首字母大写或每一个单词的首字母都采用大写字母，例如：myFirstName、myLastName. 函数命名根据完成的动作命名：动词＋名词，例如：calculateResult
- **避免无意义标签**：有的时候在写程序时，会遇到很多可能出现的状态，因此会设置一些标志变量，用来标记程序当前的状态。这种情况考虑用STATE_OPERATION代替0，1之类没有意义的变量的书写，这样可以加强程序的可读性。
- **其他问题**：书写说明文档和注释是一种很好的习惯，可以帮助别人更轻松理解自己的代码，也方便自己以后的查看。commit提交说明要附上几句简单有意义的话，避免无意义的说明。

------

###正式讲课
由刘文哲学长主讲
[课程PPT地址](images/elwg后台培训第一讲.pdf)


### LAMP简介
- Linux + Apache + Mysql + PHP/Python是一组常见的搭建动态网站或者服务器的开源软件，共同组成了一个强大的web应用程序平台。
- PHP是一种脚本语言，可以内嵌到HTML中，十分方便。
```
    <body>
        <?php 
        echo "Hello world!";
        ?>
    </body>
```

------


###PHP语法
- PHP标签
PHP的标记 <?php 和 ?> 如果文件内容是纯PHP代码，最好在文件末尾删除结束标记。
```
    <?php
    echo "Hello world!";
    
    //somecode
    -------------------------------------------------------

    <p>something</p>
    <?php echo 'Hello world!'; ?>
    <p>another thing</p>
    
```

- 数据类型
PHP是一种弱数据类型，声明时无须指定类型。PHP支持8种类型，boolen（布尔型）、integer（整型）、float（浮点型）、string（字符串）、array（数组）、object（对象）、resource（资源）、NULL（无类型）。用var_dump()来查看变量的值和类型，用echo来输出值。
PHP可以转换数据类型，有自动转换和强制转换

```
    //自动转换
    $foo = 5 . "10 eggs";
    echo $foo;//输出"510 eggs"
    
    $foo = 5 + "10";
    echo $foo; //输出 15

    //强制转换  
    var_dump((int)$foo); //类型为int
```

- 比较运算符
'==' 和 '===' 的区分，'=='会忽略两个值的类型，但'===' 除了值相等还会比较两个值的类型。
```
    $a = 5;
    var_dump($a == '5');//reture true
    var_dump($a == 5);//reture true
    var_dump($a === '5');//reture false
    var_dump($a === 5);//reture true
    
    //strpos函数是字符串查找函数，返回第一次出现待查字符串出现的位置

    //返回0，不会进入if语句
    if(strpos('abcd', 'a')){
    }
    
    //返回0, 不严格等于false，会进入if语句
    if(strpos('abcd', 'a') !== false){
    }

```

- 字符串的表示
单引号：不会对字符串里的特殊字符和变量进行解析
双引号：会对字符串里的特殊字符，如换行符和变量名进行解析
Nowdoc结构：和单引号功能一样，不过更加适合表示多行的字符串，不需要用字符串连接符。
Heredoc结构：和双引号功能一样，不过更加适合表示多行的字符串，不需要用字符串连接符。

```
    $single_quotes = 'this is a simple string';
    
    $price  = 6.5;
    //$price会解析为6.5，\n会解析为换行符
    $double_quotes = "the apple cost $price dollars.\n it's too expenseve!";
    
    $str = <<<'EDO'
    this is a example of string
    using nowdoc sytax
    EDO;

    //$a 会解析为字符串"heredoc"
    $a = 'heredoc';
    $str = <<<EDO
    this is a example of string
    using $a sytax
    EDO;
```
####思考题
如果一段文本中不包含需要解析的字符串，是选择单引号还是双引号？
解答：理论上单引号和双引号都可以选择，但是双引号会有一个解析的过程，从系统运行的效率来看，此时应该选择单引号。
-  常量定义
```
    define("SAMPLE_CONSTANTS", 'sample_value')
```

- 全局变量
PHP中有许多预定义变量都是超全局的，意味着它们在一个脚本的全部作用域都可见，如 $_GET。GET变量是获取浏览器地址栏提交的信息，与之对应的POST变量是获取表单提交的信息。

- PHP扩展
PHP有很多扩展，在需要实现一个功能之前，可以查看PHP是否已经实现了相应扩张，也可以自己写扩展。

- 连接数据库
推荐使用mysqli或者PDO来取代mysql扩展
**注意**: 数据库插入数据要谨慎，不能太相信用户的输入，接受用户的数据之前要先过滤！

-------

###Apache和Nginx服务器
- Linux基本命令
 - cd(切换文件路径)，ls(列出当前文件)
 - yum(安装更新包)
 - vim(文本编辑器)
 
- apache服务器的安装和配置（windows用户推荐）
- nginx+php-fpm服务器的安装和配置（Linux用户推荐）

--------
 
###mysql
- 关系型数据库，基本单元：表，列；类似于对象和属性的关系。
- 设计规范：三范式，字段尽量不要冗余，适当的冗余可以提高查询效率。
- 主键：
>主关键字(primary key)是表中的一个或多个字段，它的值用于唯一地标识表中的某一条记录。在两个表的关系中，主关键字用来在一个表中引用来自于另一个表中的特定记录。主关键字是一种唯一关键字，表定义的一部分。一个表不能有多个主关键字，并且主关键字的列不能包含空值。主关键字是可选的，并且可在 CREATE TABLE 或 ALTER TABLE 语句中定义。

- 数据类型：整数类型(tinyint, smallint, middleint, int, bigint), 浮点型(double, float), 字符串(char, varchar), 长文本(text), 日期(datetime)
**说明**: 在选用数据类型的时候，要根据数据可能的最大范围来选择，例如表示年龄的时候，用tinyint就足够了。char和varchar的区别在于char是定长，varchar是变长。

------

###代码规范
- 命名规范：同js一样，遵循Camel命名法，类要大写开头，以示区别，函数变量小写开头。
- 缩进和空格：四空格
- 保持代码风格一致

