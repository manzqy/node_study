## 根据不同路径返回不同内容

~~~js
// 此页面是用来向浏览器端响应整个html页面的
// 1. 引入http核心模块
var http = require('http')
var fs = require('fs')
// 2. 创建服务器对象
var server = http.createServer()
// 3. 监听端口
server.listen(3000,  () => {
  console.log('server is running at http://127.0.0.1:3000');
})
// 4. 注册事件，监听请求
server.on('request', (req, res) => {
  // http://192.168.110.89:3000/
  // http://192.168.110.89:3000/favicon.ico
  // req.url可以用来获取浏览器端发送过来请求中的路径，确切的说是用于获取端口号后面的路径
  // req.method 可以用来获取浏览器端的请求方式
  var url = req.url;
  var method = req.method
  if(method=='GET' && url == '/index.html'){
    fs.readFile(__dirname+'/views/index.html','utf-8',(err,data)=>{
      if(err) return console.log(err.message);
      res.end(data)
    })
  }else if(method=='GET' && url=='/about.html'){
    fs.readFile(__dirname + '/views/about.html', 'utf-8', (err, data) => {
      if (err) return console.log(err.message);
      res.end(data)
    })
  }else if(method=='GET' && url=='/register.html'){
    fs.readFile(__dirname + '/views/register.html', 'utf-8', (err, data) => {
      if (err) return console.log(err.message);
      res.end(data)
    })
  }else {
    res.end('404')
    // 前后端的数据格式只有两种
  }
})
~~~

