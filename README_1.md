[English](./README.md) | 简体中文

<p align="center">
<a href="https://www.huaweicloud.com/"><img width="360px" height="120px" src="https://console-static.huaweicloud.com/static/authui/20210202115135/public/custom/images/logo.svg"></a>
</p>

<h3></h3>

# 华为云开发者 Go 软件开发工具包 （Go SDK）

欢迎使用华为云 Go SDK。

华为云 Go SDK 让您无需关心请求细节即可快速使用弹性云服务器、虚拟私有云等多个华为云服务。

这里将向您介绍如何获取并使用华为云 Go SDK 。

## 使用前提

 - 要使用华为云 Go SDK ，您需要拥有云账号以及该账号对应的 Access Key（AK）和 Secret Access Key（SK）。 请在华为云控制台“我的凭证-访问密钥”页面上创建和查看您的 AK&SK 。更多信息请查看[访问密钥](https://support.huaweicloud.com/usermanual-ca/zh-cn_topic_0046606340.html)。

 - 要使用华为云 Go SDK 访问指定服务的 API ，您需要确认已在[华为云控制台](https://console.huaweicloud.com/console/?locale=zh-cn&region=cn-north-4#/home)开通当前服务。

 - 华为云 Go SDK 支持 go 1.14 及以上版本，可执行 `go version` 检查当前 Go 的版本信息。

## SDK 获取和安装

使用 go get 安装华为云 Go SDK ，执行如下命令安装华为云 Go SDK 库以及相关依赖库：

```bash
# 安装华为云 Go SDK 库
go get github.com/huaweicloud/huaweicloud-sdk-go-v3

# 安装依赖
go get github.com/json-iterator/go
```


## 代码示例

- 使用如下代码在特定 Region 下创建 VPC ，实际使用中请将 `vpc "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2"` 替换为您使用的产品/服务相应的 `{service} "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/{service}/{version}"`，且初始化为{service}.New{Service}Client。
- 调用前请根据实际情况替换如下变量： `{your ak string}`、`{your sk string}`、`{your endpoint string}` 以及 `{your project id}`。

``` go
package main

import (
    "fmt"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/core/auth/basic"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/core/config"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/core/httphandler"
    vpc "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2/model"
    "net/http"
)

func RequestHandler(request http.Request) {
    fmt.Println(request)
}

func ResponseHandler(response http.Response) {
    fmt.Println(response)
}

func main() {
    client := vpc.NewVpcClient(
        vpc.VpcClientBuilder().
            WithEndpoint("{your endpoint}").
            WithCredential(
                basic.NewCredentialsBuilder().
                    WithAk("{your ak string}").
                    WithSk("{your sk string}").
                    WithProjectId("{your project id}").
                    Build()).
            WithHttpConfig(config.DefaultHttpConfig().
                WithIgnoreSSLVerification(true).
                WithHttpHandler(httphandler.
                    NewHttpHandler().
                        AddRequestHandler(RequestHandler).
                        AddResponseHandler(ResponseHandler))).
            Build())

    request := &model.ListVpcsRequest{}
    response, err := client.ListVpcs(request)
    if err == nil {
        fmt.Println("%+v\n",response.Vpc)
    } else {
        fmt.Println(err)
    }
}
```


## 在线调试

[API Explorer](https://apiexplorer.developer.huaweicloud.com/apiexplorer/overview) 提供API检索及平台调试，支持全量快速检索、可视化调试、帮助文档查看、在线咨询。


## 变更日志

每个版本的详细更改记录可在[变更日志](https://github.com/huaweicloud/huaweicloud-sdk-go-v3/blob/master/CHANGELOG_CN.md)中查看。


## 用户手册 [:top:](#华为云开发者-go-软件开发工具包-go-sdk)
<details>
  <summary>1. 客户端连接参数</summary>
    <details>
      <summary>1.1  默认配置</summary>
      <pre><code>// 使用默认配置
httpConfig := config.DefaultHttpConfig()</pre></code>
    </details>
    <details>
      <summary>1.2  网络代理</summary>
      <pre><code>// 根据需要配置网络代理
httpConfig.WithProxy(config.NewProxy().
  WithSchema("http").
  WithHost("proxy.huaweicloud.com").
  WithPort(80).
  WithUsername("testuser").
  WithPassword("password"))))</pre></code>
    </details>
    <details>
      <summary>1.3  超时配置</summary>
      <pre><code>httpConfig.WithTimeout(120);</pre></code>
    </details>
    <details>
      <summary>1.4  SSL 配置</summary>
      <pre><code>// 根据需要配置是否跳过SSL证书校验
httpConfig.WithIgnoreSSLVerification(true);</pre></code>
    </details>
</details>
