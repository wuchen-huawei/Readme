[English](./README.md) | 简体中文

[目录](#华为云开发者-go-软件开发工具包-go-sdk)
  * [在线调试](#在线调试)
  * [前提条件](#前提条件)
  * [SDK 获取和安装](#sdk-获取和安装)
  * [开始使用](#开始使用)
    * [1. 导入依赖模块](#1-导入依赖模块)
    * [2. 配置客户端属性](#2-配置客户端属性)
    * [3. 初始化认证信息](#3-初始化认证信息)
    * [4. 初始化客户端（两种方式）](#4-初始化客户端两种方式)
    * [5. 发送请求并查看响应](#5-发送请求并查看响应)
    * [6. 异常处理](#6-异常处理)
    * [7. 原始Http侦听器](#7-原始Http侦听器)
  * [代码示例](#代码示例)

# 华为云开发者 Go 软件开发工具包 （Go SDK）

欢迎使用华为云 Go SDK。

华为云 Go SDK 让您无需关心请求细节即可快速使用弹性云服务器、虚拟私有云等多个华为云服务。

这里将向您介绍如何获取并使用华为云 Go SDK 。

## 在线调试

[API Explorer](https://apiexplorer.developer.huaweicloud.com/apiexplorer/overview) 提供API检索及平台调试，支持全量快速检索、可视化调试、帮助文档查看、在线咨询。


## 前提条件

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

## 开始使用

以使用虚拟私有云VPC SDK为例，您需要使用模块 `github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2` ：

### 1. 导入依赖模块

``` go
import (
    "fmt"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/core/auth/basic"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/core/config"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/core/httphandler"
    vpc "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2"
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2/model"
    region "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2/region"
    "net/http"
)
```

### 2. 配置客户端属性

#### 2.1 默认配置

``` go
// 使用默认配置
httpConfig := config.DefaultHttpConfig()
```

#### 2.2 网络代理（可选）

 ``` go
 // 根据需要配置网络代理
 httpConfig.WithProxy(config.NewProxy().
     WithSchema("http").
     WithHost("proxy.huaweicloud.com").
     WithPort(80).
     WithUsername("testuser").
     WithPassword("password"))))
 ```

#### 2.3 超时配置（可选）

``` go
httpConfig.WithTimeout(120);
```

#### 2.4 SSL配置（可选）

``` go
// 根据需要配置是否跳过SSL证书校验
httpConfig.WithIgnoreSSLVerification(true);
```

### 3. 初始化认证信息

**说明**：华为云服务存在两种部署方式，Region 级服务和 Global 级服务。

Global级服务当前仅支持 BSS, DevStar, EPS， IAM， RMS。

Region级服务仅需要提供projectId。Global级服务需要提供domainId。

- `ak` 华为云账号 Access Key 。
- `sk` 华为云账号 Secret Access Key 。
- `projectId` 云服务所在项目 ID ，根据你想操作的项目所属区域选择对应的项目 ID 。
- `domainId` 华为云账号ID 。
- `securityToken` 采用临时AK/SK认证场景下的安全票据。

#### 3.1 使用永久 AK 和 SK
    
``` go
// Region级服务
basicAuth := basic.NewCredentialsBuilder().
            WithAk(ak).
            WithSk(sk).
            WithProjectId(projectId).
            Build()

// Global级服务
globalAuth := global.NewCredentialsBuilder().
            WithAk(ak).
            WithSk(sk).
            WithDomainId(domainId).
            Build()
```
**说明**：`0.0.26-beta` 及以上版本支持通过永久 AK&SK 回填 projectId/domainId ，需要在初始化客户端时配合 `WithRegion()` 方法使用，代码示例详见 [4.2 指定Region方式（推荐）](#4-2-指定Region方式推荐)。
    
#### 3.2 使用临时 AK 和 SK

首先需要获得临时 AK、SK 和 SecurityToken ，可以从永久 AK&SK 获得，或者通过委托授权获得。

- 通过永久 AK&SK 获得可以参考文档：https://support.huaweicloud.com/api-iam/iam_04_0002.html ，对应 IAM SDK 中的 `CreateTemporaryAccessKeyByToken` 方法。

- 通过委托授权获得可以参考文档：https://support.huaweicloud.com/api-iam/iam_04_0101.html, 对应 IAM SDK 中的 `CreateTemporaryAccessKeyByAgency` 方法。

临时 AK&SK&SecurityToken 获取成功后，可使用如下方式初始化认证信息：

``` go
// Region级服务
basicAuth := basic.NewCredentialsBuilder().
            WithAk(ak).
            WithSk(sk).
            WithProjectId(projectId).
            WithSecurityToken(securityToken).
            Build()

// Global级服务
globalAuth := global.NewCredentialsBuilder().
            WithAk(ak).
            WithSk(sk).
            WithDomainId(domainId).
            WithSecurityToken(securityToken).
            Build()
```

### 4. 初始化客户端（两种方式）

#### 4.1 指定云服务Endpoint方式

``` go
// 初始化指定云服务的客户端 New{Service}Client ，以初始化 NewVpcClient 为例
client := vpc.NewVpcClient(
    vpc.VpcClientBuilder().
        WithEndpoint(endpoint).
        WithCredential(basicAuth).
        WithHttpConfig(config.DefaultHttpConfig()).  
        Build())
```

**说明:**
`endpoint` 华为云各服务应用区域和各服务的终端节点，详情请查看[地区和终端节点](https://developer.huaweicloud.com/endpoint)。
    
#### 4.2 指定Region方式 **（推荐）**

``` go
import (
    // 增加region依赖
    "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/iam/v3/region"
)

globalAuth := global.NewCredentialsBuilder().
            WithAk(ak).
            WithSk(sk).
            // 可不填 domainId
            Build()

// 初始化指定云服务的客户端 New{Service}Client ，以初始化 NewIamClient 为例
client := iam.NewIamClient(
    iam.IamClientBuilder().
        WithRegion(region.CN_NORTH_4).
        WithCredential(globalAuth).
        WithHttpConfig(config.DefaultHttpConfig()).  
        Build())
```
   
**说明：**

- 指定 Region 方式创建客户端场景，支持自动获取用户的regionId以及domainId，认证Credential中无需再次指定。

- 不适用于`多 ProjectId `场景。

### 5. 发送请求并查看响应.

``` go
// 初始化请求,，以调用接口 ListVpcs 为例
request := &model.ListVpcsRequest{
    Body: &model.ListVpcsRequestBody{
        Vpc: &model.ListVpcsOption{
            limit: 1,
        },
    },
}

response, err := client.ListVpcs(request)
if err == nil {
    fmt.Printf("%+v\n",response.Vpc)
} else {
    fmt.Println(err)
}
```

### 6. 异常处理

| 一级分类 | 一级分类说明 |
| :---- | :---- | 
| ServiceResponseError | service response error |
| url.Error | connect endpoint error |

``` go
response, err := client.ListVpcs(request)
if err == nil {
    fmt.Println(response)
} else {
    fmt.Println(err)
}
```

### 7. 原始 Http 侦听器

在某些场景下可能对业务发出的Http请求进行Debug，需要看到原始的Http请求和返回信息，SDK提供侦听器功能来获取原始的为加密的Http请求和返回信息。

> :warning:  Warning: 原始信息打印仅在debug阶段使用，请不要在生产系统中将原始的Http头和Body信息打印到日志，这些信息并未加密且其中包含敏感数据，例如所创建虚拟机的密码，IAM用户的密码等;

``` go
func RequestHandler(request http.Request) {
    fmt.Println(request)
}

func ResponseHandler(response http.Response) {
    fmt.Println(response)
}

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
