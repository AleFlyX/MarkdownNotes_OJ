### .test
如果想要在字符串 The dog chased the cat 中匹配到 the 这个单词，可以使用如下正则表达式：/the/。 注意，正则表达式中不需要引号。

JavaScript 中有多种使用正则表达式的方法。 测试正则表达式的一种方法是使用 .test() 方法。 .test() 方法会把编写的正则表达式和字符串（即括号内的内容）匹配，如果成功匹配到字符，则返回 true，反之，返回 false。
~~~
let testStr = "freeCodeCamp";
let testRegex = /Code/;
testRegex.test(testStr);
test 方法会返回 true。
~~~

#### 匹配文字字符串
在上一个挑战中，使用正则表达式 /Hello/ 搜索到了字符串 Hello。 那个正则表达式在字符串中搜寻 Hello 的文字匹配。 下面是另一个在字符串中搜寻 Kevin 的示例：
~~~
let testStr = "Hello, my name is Kevin.";
let testRegex = /Kevin/;
testRegex.test(testStr);
test 方法会返回 true。
~~~

任何其他形式的 Kevin 都不会被匹配。 例如，正则表达式 /Kevin/ 不会匹配 kevin 或者KEVIN。
~~~
let wrongRegex = /kevin/;
wrongRegex.test(testStr);
此 test 调用将返回 false。
~~~

#### 同时用多种模式匹配文字字符串
使用正则表达式/coding/，你可以在其他字符串中查找coding。

这对于搜寻单个字符串非常有用，但仅限于一种匹配模式。 你可以使用 alternation 或 OR 操作符搜索多个模式： |

此操作符匹配操作符前面或后面的字符。 例如，如果你想匹配 yes 或 no，你需要的正则表达式是
~~~ 
 /yes|no/。
~~~


你还可以匹配多个规则，这可以通过添加更多的匹配模式来实现。 这些匹配模式将包含更多的 OR 操作符来分隔它们，比如
~~~ 
/yes|no|maybe/。
~~~

#### 匹配时忽略大小写
到目前为止，已经了解了如何用正则表达式来执行字符串的匹配。 但有时候，并不关注匹配字母的大小写。

大小写即大写字母和小写字母。 大写字母如 A、B 和 C。 小写字母如 a、b 和 c。

可以使用标志（flag）来匹配这两种情况。 标志有很多，不过这里我们只关注忽略大小写的标志——*i*。 可以通过将它附加到正则表达式之后来使用它。 这里给出使用该标志的一个实例 */ignorecase/i*。 这个字符串可以匹配字符串 ignorecase、igNoreCase 和 IgnoreCase。
~~~
编写正则表达式 fccRegex 以匹配 freeCodeCamp，忽略大小写。 正则表达式不应与任何缩写或带有空格的变体匹配。
let myString = "freeCodeCamp";
let fccRegex = /freecodecamp/i; // 修改这一行
let result = fccRegex.test(myString);
~~~

### 提取匹配项
到目前为止，只是检查了一个匹配模式是否存在于字符串中。 还可以使用 .match() 方法来提取找到的实际匹配项。

可以使用字符串来调用 .match() 方法，并在括号内传入正则表达式。

请看下面的举例：
~~~
"Hello, World!".match(/Hello/);
let ourStr = "Regular expressions";
let ourRegex = /expressions/;
ourStr.match(ourRegex);
这里第一个 match 将返回 ["Hello"] 第二个将返回 ["expressions"]。

请注意， .match 语法是目前为止一直使用的 .test 方法中的“反向”：

'string'.match(/regex/);
/regex/.test('string');

~~~

### 全局匹配
到目前为止，只能提取或搜寻一次模式匹配。
~~~
let testStr = "Repeat, Repeat, Repeat";
let ourRegex = /Repeat/;
testStr.match(ourRegex);
在这里 match 将返回 ["Repeat"]。

要多次搜索或提取模型，你可以使用全局搜索标志： g。

let repeatRegex = /Repeat/g;
testStr.match(repeatRegex);
这里 match 返回值 ["Repeat", "Repeat", 
"Repeat"]

~~~

### 用通配符匹配任何内容
有时不（或不需要）知道匹配模式中的确切字符。 如果要精确匹配到完整的单词，那出现一个拼写错误就会匹配不到。 幸运的是，可以使用通配符 . 来处理这种情况。

通配符 . 将匹配任何一个字符。 通配符也叫 dot 或 period。 可以像使用正则表达式中任何其他字符一样使用通配符。 例如，如果想匹配 hug、huh、hut 和 hum，可以使用正则表达式 /hu./ 匹配以上四个单词。
~~~
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr);
huRegex.test(hugStr);
上面的 test 都会返回 true。


exp:

完成正则表达式 unRegex 以匹配字符串 run、sun、fun、pun、nun 和 bun。 正则表达式中应该使用通配符。

let exampleStr = "Let's have fun with regular expressions!";
let unRegex = /.un/; // 修改这一行
let result = unRegex.test(exampleStr); //true

~~~

### 将单个字符与多种可能性匹配 .match(要匹配的char)
已经了解了文字匹配模式（/literal/）和通配符（/./）。 这是正则表达式的两种极端情况，一种是精确匹配，而另一种则是匹配所有。 在这两种极端情况之间有一个平衡选项。

可以使用字符集 （character classes）更灵活的匹配字符。 可以把字符集放在方括号（[ 和 ]）之间来定义一组需要匹配的字符串。

例如，如果想要匹配 bag、big 和 bug，但是不想匹配 bog。 可以创建正则表达式 /b[aiu]g/ 来执行此操作。 [aiu] 是只匹配字符 a、i 或者 u 的字符集。
~~~
let bigStr = "big";
let bagStr = "bag";
let bugStr = "bug";
let bogStr = "bog";
let bgRegex = /b[aiu]g/;  
bigStr.match(bgRegex);
bagStr.match(bgRegex);
bugStr.match(bgRegex);
bogStr.match(bgRegex);
按顺序排列，四次 match 调用将返回值 ["big"]、["bag"]、["bug"] 和 null。
~~~

### 匹配字母表中的字母
了解了如何使用字符集（character sets）来指定要匹配的一组字符串，但是有时需要匹配大量字符（例如，字母表中的每个字母）。 有一种写法可以让实现这个功能变得简短。

在字符集中，可以使用连字符（-）来定义要匹配的字符范围。

例如，要匹配小写字母 a 到 e，你可以使用 [a-e]。
~~~
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex);
batStr.match(bgRegex);
matStr.match(bgRegex);
按顺序排列，三次 match 调用将返回值 ["cat"]，["bat"] 和 null。
~~~

使用连字符（-）匹配字符范围并不仅限于*字母*。 它还可以匹配一系列数字。

例如，/[0-5]/ 匹配 0 和 5 之间的任意数字，包含 0 和 5。

此外，还可以在单个字符集中组合一系列字母和数字。
~~~

let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex);

~~~
 
### 匹配单个未指定的字符 "^"(非)
到目前为止，已经创建了一个想要匹配的字符集合，但也可以创建一个不想匹配的字符集合。 这些类型的字符集称为否定字符集（ negated character sets）。

要创建否定字符集，需要在开始括号后面和不想匹配的字符前面放置脱字符（即^）。

例如，/[^aeiou]/gi 匹配所有非元音字符。 注意，字符 .、!、[、@、/ 和空白字符等也会被匹配，该否定字符集仅排除元音字符。
~~~
let quoteSample = "3 blind mice.";
let myRegex = /[^aeiou0-9]/ig; 
let result =quoteSample.match(myRegex); 
~~~

### 匹配出现一次或多次的字符
有时，需要匹配出现一次或者连续多次的的字符（或字符组）。 这意味着它至少出现一次，并且可能重复出现。

可以使用 *+* 符号来检查情况是否如此。 记住，字符或匹配模式必须一个接一个地连续出现。 这就是说，字符必须一个接一个地重复。

#### 例如，*/a+/g* 会在 abc 中匹配到一个匹配项，并且返回 ["a"]。 因为 + 的存在，它也会在 aabc 中匹配到一个匹配项，然后返回 ["aa"]。
~~~
/a+/
~~~

如果它是检查字符串 abab，它将匹配到两个匹配项并且返回["a", "a"]，因为a字符不连续，在它们之间有一个b字符。 最后，因为在字符串 bcd 中没有 a，因此找不到匹配项。

### 匹配出现零次或多次的字符
上一次的挑战中使用了加号 + 来查找出现一次或多次的字符。 还有一个选项可以匹配出现零次或多次的字符。

执行该操作的字符叫做星号，即*。
~~~
let soccerWord = "gooooooooal!";
let gPhrase = "gut feeling";
let oPhrase = "over the moon";
let goRegex = /go*/;
soccerWord.match(goRegex);
gPhrase.match(goRegex);
oPhrase.match(goRegex);
按顺序排列，三次 match 调用将返回值 ["goooooooo"]，["g"] 和 null。


exp:
####################
在这个挑战里，chewieQuote 已经被初始化为 Aaaaaaaaaaaaaaaarrrgh!。 创建一个变量为 chewieRegex 的正则表达式，使用 * 在 chewieQuote 中匹配 A 及其之后出现的零个或多个a。 你的正则表达式不需要使用修饰符，也不需要匹配引号。

let chewieRegex = /Aa*/; 

let result = chewieQuote.match(chewieRegex);

~~~

### 用惰性匹配来查找字符 "?"
在正则表达式中，贪婪（greedy）匹配会匹配到符合正则表达式匹配模式的字符串的最长可能部分，并将其作为匹配项返回。 另一种方案称为懒惰（lazy）匹配，它会匹配到满足正则表达式的字符串的最小可能部分。

可以将正则表达式 /t[a-z]*i/ 应用于字符串 "titanic"。 这个正则表达式是一个以 t 开始，以 i 结束，并且中间有一些字母的匹配模式。

正则表达式默认是贪婪匹配，因此匹配返回为 ["titani"]。 它会匹配到适合该匹配模式的最大子字符串。

但是，你可以使用 ? 字符来将其变成懒惰匹配。 调整后的正则表达式 /t[a-z]*?i/ 匹配字符串 "titanic" 返回 ["ti"]。

**注意：**应该避免使用正则表达式解析 HTML，但是可以用正则表达式匹配 HTML 字符串。

### 匹配字符串的末尾  "$"

可以使用正则表达式的美元符号 $ 来搜寻字符串的结尾。
~~~
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding);
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding);
第一次 test 调用将返回 true, 而第二次调用将返回 false。

~~~

### 匹配所有的字母和数字  "\w"
在JavaScript的正则表达式（Regex）中，\w 是一个特殊字符类，用于匹配任何字母数字字符（包括下划线 _）。具体来说，\w 等同于 [A-Za-z0-9_]，即它可以匹配任何大写字母（A-Z）、小写字母（a-z）、数字（0-9）或下划线（_）。

~~~
let longHand = /[A-Za-z0-9_]+/;
let shortHand = /\w+/;
let numbers = "42";
let varNames = "important_var";
longHand.test(numbers);
shortHand.test(numbers);
longHand.test(varNames);
shortHand.test(varNames);
上面的 test 都会返回 true。

这些元字符缩写也被称为短语元字符 shorthand character classes。

~~~

### 匹配除了字母和数字的所有符号 "\W"
已经了解到可以使用缩写 \w 来匹配字母和数字 [A-Za-z0-9_]。 不过，有可能想要搜寻的匹配模式是非字母数字字符。

可以使用 \W 搜寻和 \w 相反的匹配模式。 注意，相反匹配模式使用大写字母。 此缩写与 [^A-Za-z0-9_] 是一样的。
~~~
let shortHand = /\W/;
let numbers = "42%";
let sentence = "Coding!";
numbers.match(shortHand);
sentence.match(shortHand);
第一次 match 调用将返回值 ["%"] 而第二次调用将返回 ["!"]。

~~~

#### 匹配所有数字 "\d"
已经了解了常见字符串匹配模式的元字符，如字母数字。 另一个常见的匹配模式是只寻找数字。

查找数字字符的缩写是 *\d*，注意是小写的 d。 这等同于元字符 [0-9]，它查找 0 到 9 之间任意数字的单个字符。

#### "\D" 
查找非数字字符的缩写是 \D。 这等同于字符串 [^0-9]，它查找不是 0 - 9 之间数字的单个字符。

### 匹配空白字符 "\s"
迄今为止的挑战包括匹配字母和数字。 还可以匹配字符之间的空格。

可以使用 *\s* 搜寻空格，其中 s 是小写。 此匹配模式将匹配空格、回车符、制表符、换页符和换行符。 可以认为这类似于元字符 [ \r\t\f\n\v]。
~~~
let whiteSpace = "Whitespace. Whitespace everywhere!"
let spaceRegex = /\s/g;
whiteSpace.match(spaceRegex);
这个 match 调用将返回 [" ", " "]。
~~~

#### 匹配非空白字符 "\S"
使用 \S 搜寻非空白字符，其中 s 是大写。 此匹配模式将不匹配空格、回车符、制表符、换页符和换行符。 可以认为这类似于元字符 [^ \r\t\f\n\v]。

### 指定匹配的上限和下限 {下限，上限}
回想一下，使用加号 + 查找一个或多个字符，使用星号 * 查找零个或多个字符。 这些都很方便，但有时需要匹配一定范围的匹配模式。

可以使用数量说明符（quantity specifiers）指定匹配模式的上下限。 数量说明符与花括号（{ 和 }）一起使用。 可以在花括号之间放两个数字，这两个数字代表匹配模式的上限和下限。

例如，要匹配出现 3 到 5 次字母 a 的在字符串 ah，正则表达式应为/a{3,5}h/。
~~~
let A4 = "aaaah";
let A2 = "aah";
let multipleA = /a{3,5}h/;
multipleA.test(A4);
multipleA.test(A2);
第一次 test 调用将返回 true，而第二次调用将返回 false。

~~~

#### 只指定匹配的下限
可以使用带有花括号的数量说明符来指定匹配模式的上下限。 但有时候只想指定匹配模式的下限而不需要指定上限。

为此，在第一个数字后面跟一个逗号即可。

例如，要匹配至少出现 3 次字母 a 的字符串 hah，正则表达式应该是 /ha{3,}h/。
~~~
let A4 = "haaaah";
let A2 = "haah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleA = /ha{3,}h/;
multipleA.test(A4);
multipleA.test(A2);
multipleA.test(A100);
按顺序排列，三次 test 调用将返回值 true，false 和 true。

~~~~

#### 指定匹配的确切数量
可以使用带有花括号的数量说明符来指定匹配模式的上下限。 但有时只需要特定数量的匹配。

要指定一定数量的匹配模式，只需在大括号之间放置一个数字。

例如，要只匹配字母 a 出现 3 次的单词hah，正则表达式应为/ha{3}h/。
~~~
let A4 = "haaaah";
let A3 = "haaah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleHA = /ha{3}h/;
multipleHA.test(A4);
multipleHA.test(A3);
multipleHA.test(A100);
按顺序排列，三次 test 调用将返回值 false，true 和 false。
~~~

### 检查全部或无 "?"
有时，想要搜寻的匹配模式可能有不确定是否存在的部分。 尽管如此，还是想检查它们。

为此，可以使用问号 ? 指定可能存在的元素。 这将检查前面的零个或一个元素。 可以将此符号视为前面的元素是可选的。

例如，美式英语和英式英语略有不同，可以使用问号来匹配两种拼写。
~~~
let american = "color";
let british = "colour";
let rainbowRegex= /colou?r/;
rainbowRegex.test(american);
rainbowRegex.test(british);
上面的 test 都会返回 true。
~~~

### 正向先行断言和负向先行断言
先行断言 （Lookaheads）是告诉 JavaScript 在字符串中向前查找的匹配模式。 当想要在同一个字符串上搜寻多个匹配模式时，这可能非常有用。

有两种先行断言：正向先行断言（positive lookahead）和负向先行断言（negative lookahead）。

正向先行断言会查看并确保搜索匹配模式中的元素存在，但实际上并不匹配。 正向先行断言的用法是 (?=...)，其中 ... 就是需要存在但不会被匹配的部分。

另一方面，负向先行断言会查看并确保搜索匹配模式中的元素不存在。 负向先行断言的用法是 (?!...)，其中 ... 是希望不存在的匹配模式。 如果负向先行断言部分不存在，将返回匹配模式的其余部分。

尽管先行断言有点儿令人困惑，但是这些示例会有所帮助。
~~~
let quit = "qu";
let noquit = "qt";
let quRegex= /q(?=u)/;
let qRegex = /q(?!u)/;
quit.match(quRegex);
noquit.match(qRegex);
这两次 match 调用都将返回 ["q"]。
~~~
先行断言的更实际用途是检查一个字符串中的两个或更多匹配模式。 这里有一个简单的密码检查器，密码规则是 3 到 6 个字符且至少包含一个数字：

~~~
let password = "abc123";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
checkPass.test(password);

~~~

### 检查混合字符组
有时候我们想使用正则表达式里的括号 () 来检查字符组。

如果想在字符串找到 Penguin 或 Pumpkin，可以用这个正则表达式：/P(engu|umpk)in/g。

然后使用 test() 方法检查 test 字符串里面是否包含字符组。

~~~
let testStr = "Pumpkin";
let testRegex = /P(engu|umpk)in/;
testRegex.test(testStr);
test 方法会返回 true。
~~~

### 使用捕获组重用模式
当你想要匹配一个像下面这样多次出现的单词，

let repeatStr = "row row row your boat";
你可以使用 /row row row/。但如果你不知道重复的特定单词，怎么办？ 捕获组 可以用于找到重复的子字符串。

捕获组是通过把要捕获的正则表达式放在括号中来构建的。 在这个例子里， 目标是捕获一个包含字母数字字符的词，所以捕获组是将 \w+ 放在括号中：/(\w+)/。

分组匹配的子字符串被保存到一个临时的“变量”， 可以使用同一正则表达式和反斜线及捕获组的编号来访问它（例如：\1）。 捕获组按其开头括号的位置自动编号（从左到右），从 1 开始。

下面的示例是匹配被空格隔开的两个相同单词：
~~~
let repeatRegex = /(\w+) \1 \1/;
repeatRegex.test(repeatStr); // Returns true
repeatStr.match(repeatRegex); // Returns ["row row row", "row"]
在字符串上调用 .match() 方法将返回一个数组，其中包含它最终匹配到的子字符串及其捕获组。
~~~


### 使用捕获组搜索和替换
搜索功能是很有用的。 但是，当搜索同时也执行更改（或替换）匹配文本的操作时，搜索功能就会显得更加强大。

可以在字符串上使用 .replace() 方法来搜索并替换字符串中的文本。 .replace() 的输入首先是想要搜索的正则表达式匹配模式。 第二个参数是用于替换匹配的字符串或用于执行某些操作的函数。
~~~
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
replace 调用将返回字符串 The sky is blue.。

你还可以使用美元符号（$）访问替换字符串中的捕获组。

"Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1');
调用 replace 将返回字符串 Camp Code。
~~~
