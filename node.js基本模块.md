### node.js基本模块
服务器程序没有浏览器程序的安全限制，服务器程序必须能接收网络请求，读写文件，处理二进制内容
#### node.js

- global唯一的全局对象
- progress代表当前node.js进程
- node.js由事件驱动执行的单线程模型：调用progress.nextTick()在下一次事件响应中执行代码
- exit可以在程序即将退出时执行某个函数：
    ```
    process.on（‘exit’，function（code）{
    console.log('about to exit with code: ' + code);
    }）
    ```
    - 1. fs模块
            内置的文件系统模块，负责读写文件，同时提供了同步和异步方法
            - 异步读取文件
            ```
                var fs = require('fs');
                fs.readFile('sample.txt','utf-8',function(err,data){
                    if(err){
                        console.log(err)	//报错
                    }else{
                        console.log(data)	//正常
                    }
                })
            ```
            - 同步读取文件（少用）
            ```
                var fs = require('fs');
                var data = fs.readFileSync('sample.txt','uft-8');
                console.log(data)
            ```
            - 写文件

                fs.writeFile()实现
            - 获取文件大小，创建时间等信息

                可以使用fs.stat()
    - 2. stream

        支持流这种数据结构
        ```
        var fs = require('fs');
        var rs = fs.createReadStream('sample.txt','utf-8');
        //表示流的数据可以读取
        rs.on('data',function(chunk){
            //...
        })
        //表示流已经到达末尾了
        rs.on('end',function(){
            //...
        })
        //表示出错了
        rs.on('error',function(){
            //...
        })
        ```
    - 3. http
        应用程序不直接处理http协议，而是操作http模块提供的request和response
        
        用node.js实现一个http服务器程序：
        ```
        vat http= require('http');	//导入http模块
        var server = http.createSever(function(request,response){
        console.log(request.method + ':' + request.url);
        response.writeHead(200,{'Content-type':'text/html'});
        response.end('<h1>hello world</h1>');
        });
        server.listen（8080） //服务器监听8080端口
        ```
    - 4. crypto
        
        目的是为了提供通用的加密和哈希算法。用纯JavaScript代码实现这些功能不是不可能，但速度会非常慢。

        Nodejs用C/C++实现这些算法后，通过cypto这个模块暴露为JavaScript接口，这样用起来方便，运行速度也快。
- http协议：服务器和浏览器之间的传输协议
    
    //http格式包含header、body（可选）
    - model：封装业务逻辑相关的数据和处理方法
    - view：视图，负责数据的展示
    - controller：用于控制应用程序的流程，处理用户的行为和数据上的改变

        - mvc：在controller中响应view的事件调用model的接口对数据进行操作，一旦model发生变化便通知相关视图进行更新

            缺点：每个事件都流经controller，会导致模型变得臃肿

            mvc中controller和view一般是一一对应的，控制器与视图之间的联系过于紧密导致controller复用性降低
        - mvp：controller/presenter负责业务逻辑、model管理数据、view负责显示
（           mvp是mvc的改良版）