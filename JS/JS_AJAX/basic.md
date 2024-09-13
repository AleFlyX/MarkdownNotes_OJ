AJAX（Asynchronous JavaScript and XML）是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。它允许网页的异步通信，即网页可以在不中断用户与网页交互的情况下，与服务器交换数据并更新部分网页内容。AJAX 技术不是单一的技术，而是多种技术的组合，包括：

1. **HTML**：用于构建网页内容。
2. **CSS**：用于美化网页的样式。
3. **JavaScript**：用于实现网页的交互性。
4. **XMLHttpRequest**：AJAX 的核心，用于在后台与服务器交换数据。虽然名字中包含 XML，但它可以发送和接收任何类型的数据（包括文本和 JSON）。
5. **DOM（文档对象模型）**：用于动态地访问和更新网页的内容。

### AJAX 的基本工作流程

1. **创建 XMLHttpRequest 对象**：首先，需要创建一个 XMLHttpRequest 对象，这个对象用于在客户端与服务器之间发送请求和接收响应。

2. **配置请求**：设置请求的方法和 URL（例如，GET 或 POST，以及请求的 URL）。

3. **发送请求**：通过 XMLHttpRequest 对象的 `send()` 方法发送请求到服务器。

4. **处理响应**：设置回调函数来处理服务器返回的响应。通常，在 XMLHttpRequest 对象的 `onreadystatechange` 事件中设置回调函数，该函数检查请求的状态（`readyState`），并在状态为 4（已完成）时处理响应数据。

### 示例代码

以下是一个简单的 AJAX 请求示例，使用 GET 方法从服务器获取数据：

```

var xhr = new XMLHttpRequest(); // 创建 XMLHttpRequest 对象
xhr.open('GET', 'example.txt', true); // 配置请求（方法、URL、异步）

// 设置回调函数
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 请求已完成，且响应状态码为 200
        console.log(xhr.responseText); // 处理响应数据
    }
};

xhr.send(); // 发送请求
```

### 注意事项

- **异步性**：AJAX 请求是异步进行的，这意味着 JavaScript 代码会继续执行，而不会等待服务器响应。因此，处理响应的代码必须放在回调函数中。
- **跨域问题**：出于安全考虑，浏览器对跨域请求有严格的限制。如果需要跨域请求数据，通常需要使用 CORS（跨源资源共享）或 JSONP（仅限 GET 请求）等技术。
- **错误处理**：AJAX 请求可能会因为网络问题、服务器错误等原因失败。因此，应该在 AJAX 请求中添加错误处理逻辑。
- **现代替代方案**：虽然 XMLHttpRequest 仍然广泛使用，但现代 JavaScript 提供了更简洁、更强大的 API 来处理 HTTP 请求，如 Fetch API 和 Axios。这些 API 提供了更简单的语法和更丰富的功能。

# XMLHttpRequest 
- open
- send
- onreadystate
- status

## open send
### open(method,url,async)
- method:请求类型（如POST或GET）
- url:文件在服务器上的位置
- async:是否异步（true异步，false同步）

### send(string)
	
将请求发送到服务器。
- string：仅用于 POST 请求


~~~
xmlhttp.open("GET","ajax_info.txt",true);
xmlhttp.send();
~~~  

## GET 还是 POST？
与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：

- 不愿使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

# 服务器响应
- responseText：获得字符串形式的响应数据。
- responseXML：获得 XML 形式的响应数据。
~~~
document.getElementById('Div').innerHTML=xmlhttp.responseText;
~~~


## onreadystatechange 事件
~~~
xmlHttp.onreadystate

xmlHttp.status
~~~  
xmlHttp.onreadystate：
- 0: 请求未初始化
- 1: 服务器连接已建立
- 2: 请求已接收
- 3: 请求处理中
- 4: 请求已完成，且响应已就绪

*注意： onreadystatechange 事件被触发 4 次（0 - 4）, 分别是： 0-1、1-2、2-3、3-4，对应着 readyState 的每个变化。*

xmlHttp.status：
- 200:'OK'
- 404:Not Found
例如：
~~~
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
~~~




