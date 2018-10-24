### WebSocket

在浏览器和服务器之间建立一个不受限的双向通信的通道（全双工通信），服务器可以在任意时刻发送消息给浏览器
```
（
    轮询：浏览器通过JavaScript启动一个定时器，固定的间隔给服务器发请求，询问服务器有没有新消息
    缺点：实时性不够  频繁请求会给服务器带来压力	
 ）
```
websocket连接由浏览器发起，因为请求协议是一个标准的http协议：
```
GET ws://localhost:3000/ws/chat HTTP/1.1
Host: localhost
Upgrade: websocket	//表示此链接将要转化成websocket连接
Connection: Upgrade
Origin: http://localhost:3000
Sec-WebSocket-Key: client-random-string
Sec-WebSocket-Version: 13
```
http协议建立在TCP协议上的，TCP协议本身上全双工通信，但http协议的请求-应答机制限制了全双工通信
```
使用websocket：
/ 导入WebSocket模块:
const WebSocket = require('ws');

// 引用Server类:
const WebSocketServer = WebSocket.Server;

// 实例化:
const wss = new WebSocketServer({
    port: 3000
});
```