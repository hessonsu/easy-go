# easy-go
easy-go集成了自封装的各种easy系列包应用的项目，为方便各种场景应用能快速开发，作为示例性项目仅提供参考

- 集成easy-gin
- 集成easy-logrus
- 集成swagger
- 配置方便
- 更多功能计划后续集成，以方便使用（常用web开发：orm, redis, mongodb, jwt, auth2等）

### 在线预览地址 
[easy-go-demo](http://47.115.33.58:8078/swagger/index.html)

### 使用介绍
```
package main

import (
	"fmt"
	"os"
	"os/signal"
	"syscall"

	"github.com/ajdwfnhaps/easy-go/plugin/web"
)

func main() {

	//使用 easy-gin
	web.UseEasyGinPlugin("conf/config.toml")
	handleSignal()
}

func handleSignal() {
	c := make(chan os.Signal)
	signal.Notify(c, syscall.SIGHUP, syscall.SIGINT, syscall.SIGTERM, syscall.SIGQUIT)
	select {
	case <-c:
		fmt.Println("服务退出")
	}
}

```

[详细代码参考](main.go)

### easy-gin 介绍
[了解更多](https://github.com/ajdwfnhaps/easy-gin)


### config.toml

```
#版本号
version="1.0.0"

# 运行模式(debug:调试,test:测试,release:正式)
run_mode = "debug"

# 静态站点目录(也可以启动服务时使用-www指定)
www = ""

# http配置
[http]
# http监听地址
host = "0.0.0.0"
# http监听端口
port = 8078
# 证书路径
cert_file = ""
# 证书密钥
key_file = ""
# http优雅关闭等待超时时长(单位秒)
shutdown_timeout = 30


# 日志配置
[log]
# 应用编号
app_no=100101
# 应用名称
app_name="样例Api服务"
# 日志级别(1:fatal 2:error,3:warn,4:info,5:debug)
log_level = 5
# 日志格式（支持输出格式：text/json）
format = "json"
# 日志输出(支持：stdout/stderr/file/multi)
# output = "multi"
# 指定日志输出的文件路径
output_file = "logs/app"
# 是否禁用自定义时间戳显示
disable_custom_timestamp = false
# 是否禁用行号信息显示(WarnLevel以上才会显示)
disable_line_hook = false
# 设置保留天数
log_file_max_age = 7
# 设置每天分割日志文件
log_file_rotation_time = 86400
# 设置日志文件名规则
log_file_path_format = ".%Y-%m-%d.log"

# swagger文档
[swagger]
on=1
title = "Swagger Example API"
description="swagger文档描述 demo 测试服务接口介绍"
version="1.0"
#host=""
base_path="/"
schemes=["http"]

# 跨域请求
[cors]
# 是否启用
enable = false
# 允许跨域请求的域名列表(*表示全部允许)
allow_origins = ["*"]
# 允许跨域请求的请求方式列表
allow_methods = ["GET","POST","PUT","DELETE","PATCH"]
# 允许客户端与跨域请求一起使用的非简单标头的列表
allow_headers = []
# 请求是否可以包含cookie，HTTP身份验证或客户端SSL证书等用户凭据
allow_credentials = true
# 可以缓存预检请求结果的时间（以秒为单位）
max_age = 7200


```


**运行效果如下图：**
![text](https://github.com/ajdwfnhaps/easy-gin/blob/master/pics/swagger.png)

### docker 部署
1. 执行build-linux-amd64.bat,可在windows系统下交叉编译发布linux amd64架构的二进制文件
2. 上传的相应linux服务器相应目录
3. docker run

```
docker run --privileged=true --name easy-go-demo -p 8078:8078 -v /home/mwr/go-prj/easy-go-demo:/app -w /app/  -e TZ='Asia/Shanghai' -d alpine:latest /app/./easy-go
```

### todo列表：
- orm集成(gorm, xorm)
- nosql集成(redis, mongodb)
- mq使用
- mqtt集成

### 扩展
- easy-logrus包
- easy-tool包
- mqtt包
- tcp server包
- 服务治理相关包
- Golang学习文档整理.bk

