suWebsocket概述

本模块封装了的原生WebSocket通信，支持ws、wss协议。

Websocket简介

WebSocket使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在WebSocket API中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。

suWebsocket 模块概述

服务端和客户端双向通信 自定义心跳数据和间隔时间

模块接口

listener
websocket消息监听：连接断开，接收消息等事件。

listener(callback(ret, err))

callback(ret, err)

ret：

类型：JSON 对象
内部字段：
{
    status: 1   //数字类型；1
    type: "receive"    //字段串类型:
                    receive 接收消息
                    closed 连接断开
}
err：

类型：JSON 对象
内部字段：
{
    status: 0     //数字类型；
}
示例代码
```
var suWebsocket = api.require('suWebsocket');
suWebsocket.listener(function (ret, err) {
    alert(JSON.stringify(ret) + "  " + JSON.stringify(err));
})
```

可用性

Android系统

可提供的1.0.0及更高版本

open
websocket连接

params

url：

类型：字符串
描述：（必填项）websocket的连接地址：如：ws://192.168.1.5:8887。
pingTime：

类型：整型

描述：(可选项）心跳间隔，单位秒，设置大于0时起效果。
默认值：5
pingData：

类型：字符串

描述：（可选项）心跳数据，配合pingTime 使用。
默认值："ping"
open({params}, callback(ret, err))

callback(ret, err)

ret：

类型：JSON 对象
内部字段：
{
    status: 1      //数字类型；1，连接成功
}
err：

类型：JSON 对象
内部字段：
{
    status: 0     //数字类型；
                    //错误码：
                    //0（连接失败）
                    //-1（已连接成功,不用重复连接），
}
示例代码

var suWebsocket = api.require('suWebsocket');
suWebsocket.open({
    url : "ws://192.168.1.5:8887"
}, function (ret, err) {
    alert(JSON.stringify(ret) + "  " + JSON.stringify(err));
});
可用性

Android系统

可提供的1.0.0及更高版本

send
客户端发送消息

send({params}, callback(ret, err))

params

data：

类型：字符串
描述：（必填项）发送的消息内容。
callback(ret, err)

ret：

类型：JSON 对象
内部字段：
{
    status: 1   //数字类型；1
    messaage: "发送成功"
}
err：

类型：JSON 对象
内部字段：
{
    status: 0     //数字类型；0
    message: "发送失败"
}
示例代码

var suWebsocket = api.require('suWebsocket');
suWebsocket.send({
    data: '这是客户端发送的数据'
}, function (ret, err) {
    alert(JSON.stringify(ret) + "  " + JSON.stringify(err));
});
可用性

Android系统

可提供的1.0.0及更高版本

close
关闭连接

close(callback(ret, err))

callback(ret, err)

ret：

类型：JSON 对象
内部字段：
{
    status: 1   //数字型；关闭成功
    message: "关闭成功"
}
err：

类型：JSON 对象
内部字段：
{
    status: 0     //数字类型；关闭失败
    message: "关闭失败"
}
示例代码

var suWebsocket = api.require('suWebsocket');
suWebsocket.close(function (ret, err) {
    alert(JSON.stringify(ret) + "  " + JSON.stringify(err));
});
可用性

Android系统

可提供的1.0.0及更高版本

connectState
获取连接状态

connectState(callback(ret, err))

callback(ret, err)

ret：

类型：JSON 对象
内部字段：
{
    status: 1   //数字类型；1||0
    state: 'NOT_YET_CONNECTED'//连接状态:
               //NOT_YET_CONNECTED 还没有连接
               //OPEN 打开状态
               //CLOSING 正在关闭
               //CLOSED 已关闭
}
示例代码

var suWebsocket = api.require('suWebsocket');
suWebsocket.connectState(function (ret, err) {
    alert(JSON.stringify(ret) + "  " + JSON.stringify(err));
});
可用性

Android系统
