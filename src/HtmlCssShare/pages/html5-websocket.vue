<template>
    <div>
        <pre>
        WebSocket 协议本质上是一个基于 TCP 的协议。
    
        为了建立一个 WebSocket 连接，客户端浏览器首先要向服务器发起一个 HTTP 请求，这个请求和通常的 HTTP 请求不同，包含了一些附加头信息，其中附加头信息"Upgrade: WebSocket"表明这是一个申请协议升级的 HTTP 请求，服务器端解析这些附加的头信息然后产生应答信息返回给客户端，客户端和服务器端的 WebSocket 连接就建立起来了，双方就可以通过这个连接通道自由的传递信息，并且这个连接会持续存在直到客户端或者服务器端的某一方主动的关闭连接。
        </pre>
        <a @click='WebSocketTest'>运行 WebSocket</a>
    </div>
</template>

<script>
    export default {
        data() {
            return {
    
            }
        },
        ready() {
    
        },
        methods: {
            WebSocketTest() {
                if ("WebSocket" in window) {
                    alert("您的浏览器支持 WebSocket!");
    
                    // 打开一个 web socket
                    var ws = new WebSocket("ws://localhost:9998/echo");
    
                    ws.onopen = function() {
                        // Web Socket 已连接上，使用 send() 方法发送数据
                        ws.send("发送数据");
                        alert("数据发送中...");
                    };
    
                    ws.onmessage = function(evt) {
                        var received_msg = evt.data;
                        alert("数据已接收...");
                    };
    
                    ws.onclose = function() {
                        // 关闭 websocket
                        alert("连接已关闭...");
                    };
                } else {
                    // 浏览器不支持 WebSocket
                    alert("您的浏览器不支持 WebSocket!");
                }
            }
        }
    }
</script>
<style>
    pre{
        white-space:pre-line;
    }
</style>