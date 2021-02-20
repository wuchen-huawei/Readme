English | [简体中文](./README_CN.md)

<p align="center">
<a href="https://www.huaweicloud.com/"><img width="600px" height="136px" src="https://console-static.huaweicloud.com/static/authui/20210202115135/public/custom/images/logo-en.svg"></a>
</p><br>

# Huawei Cloud Go Software Development Kit (Go SDK)

The Huawei Cloud Go SDK allows you to easily work with Huawei Cloud services such as Elastic Compute Service (ECS) and Virtual Private Cloud (VPC) without the need to handle API related tasks.

This document introduces how to obtain and use HuaweiCloud Go SDK.


## Requirements

- To use Huawei Cloud Go SDK, you must have Huawei Cloud account as well as the Access Key and Secret key of the Huawei Cloud account. You can create an AccessKey in the Huawei Cloud console. For more information, see [My Credentials](https://support.huaweicloud.com/en-us/usermanual-ca/en-us_topic_0046606340.html).

- To use Huawei Cloud Go SDK to access the APIs of specific service, please make sure you do have activated the service in [Huawei Cloud console](https://console.huaweicloud.com/console/?locale=zh-cn&region=cn-north-4#/home) if needed. 
  
- HuaweiCloud Go SDK requires go 1.14 or later. Run command `go version` to check the version of Go.


## Install Go SDK

Run the following commands to install Huawei Cloud Go SDK and related libraries:

``` bash
# Install the library of Huawei Cloud Go SDK
go get github.com/huaweicloud/huaweicloud-sdk-go-v3

# Install the dependent library
go get github.com/json-iterator/go
```

## Code Example

- The following example shows how to query a list of VPCs in a specific region, you need to substitute your real `{service} "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/{service}/{version}"` for `vpc "github.com/huaweicloud/huaweicloud-sdk-go-v3/services/vpc/v2"` in actual use, and initialize the client as `{service}.New{Service}Client`.
- Substitute the values for `{your ak string}`, `{your sk string}`, `{your endpoint string}` and `{your project id}`.

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


## Changelog

Detailed changes for each released version are documented in the [CHANGELOG.md](https://github.com/huaweicloud/huaweicloud-sdk-go-v3/blob/master/CHANGELOG.md). 


## User Manual [:top:]()
* [1  Client Configuration]()
    * [1.1  Default Configuration]()
    * [1.2  Network Proxy](#)
    * [1.3  Connection](#)
    * [1.4  SSL Certification](#14-SSL Certification)
* [2  Credentials Configuration](#)
    * [2.1  Use Permanent AK&SK]()
    * [2.2  Use Temporary AK&SK]()
* [3  Client Initialization]()
    * [3.1  Initialize with specified Endpoint]()
    * [3.2  Initialize with specified Region]()
* [4  Send Request and get response]()
    * [4.1  Exceptions]()
* [5  Troubleshooting ]
    * [5.1  Original HTTP Listener]()
    

### 1.  Client Configuration

#### 1.1  Default Configuration

``` go
// Use default configuration
httpConfig := config.DefaultHttpConfig()
```

#### 1.2  Network Proxy

``` go
// Use proxy if needed
httpConfig.WithProxy(config.NewProxy().
    WithSchema("http").
    WithHost("proxy.huaweicloud.com").
    WithPort(80).
    WithUsername("testuser").
    WithPassword("password"))))
```

#### 1.3 Connection

``` go
// seconds to wait for the server to send data before giving up
httpConfig.WithTimeout(30);
```

#### 1.4 SSL Certification

``` go
// Skip ssl certification checking while using https protocol if needed
httpConfig.WithIgnoreSSLVerification(true);
```

3. Initialize the credentials

    **Notice:**
    There are two types of HUAWEI CLOUD services, regional services and global services. 
    Global services currently only support BSS, DevStar, EPS, IAM, RMS.

    For Regional services' authentication, projectId is required. 
    For global services' authentication, domainId is required. 
    
    If you use {Service}Region to initialize {Service}Client, projectId/domainId supports automatic acquisition, you don't need to configure it when initializing Credentials.

    - `ak` is the access key ID for your account.
    - `sk` is the secret access key for your account.
    - `projectId` is the ID of your project depending on your region which you want to operate.
    - `domainId` is the account ID of HUAWEI CLOUD.
    - `securityToken` is the security token when using temporary AK/SK.

    3.1 Use permanent AK/SK
    
    ``` go
    # Regional Services
    auth := basic.NewCredentialsBuilder().
                WithAk(ak).
                WithSk(sk).
                WithProjectId(projectId).
                Build()
   
    # Global Services
    auth := global.NewCredentialsBuilder().
                WithAk(ak).
                WithSk(sk).
                WithDomainId(domainId).
                Build()
    ```
    
    3.2 Use temporary AK/SK
    
    It's preferred to obtain temporary access key, security key and security token first, which could be obtained through permanent access key and security key or through an agency.
    
    Obtaining a temporary access key token through permanent access key and security key, you could refer to document: https://support.huaweicloud.com/en-us/api-iam/iam_04_0002.html . The API mentioned in the document above corresponds to the method of createTemporaryAccessKeyByToken in IAM SDK.
    
    Obtaining a temporary access key and security token through an agency, you could refer to document: https://support.huaweicloud.com/en-us/api-iam/iam_04_0101.html . The API mentioned in the document above corresponds to the method of createTemporaryAccessKeyByAgency in IAM SDK.
    
    ``` go
    # Regional Services
    auth := basic.NewCredentialsBuilder().
                WithAk(ak).
                WithSk(sk).
                WithProjectId(projectId).
                WithSecurityToken(securityToken).
                Build()
   
    # Global Services
    auth := global.NewCredentialsBuilder().
                WithAk(ak).
                WithSk(sk).
                WithDomainId(domainId).
                WithSecurityToken(securityToken).
                Build()
    ```

4. Initialize the {Service}Client instance (Two ways)
        
    4.1 Specify Endpoint when initializing {Service}Client
    ``` go
    // Initialize specified New{Service}Client, take NewVpcClient for example
    client := vpc.NewVpcClient(
        vpc.VpcClientBuilder().
            WithEndpoint(endpoint).
            WithCredential(auth).
            WithHttpConfig(config.DefaultHttpConfig()).  
            Build())
    ```

    **where:**

    - `endpoint` is the service specific endpoints, see [Regions and Endpoints](https://developer.huaweicloud.com/intl/en-us/endpoint)

    4.2 Specify Region when initializing {Service}Client **(Recommended)**
    
    ``` go
    // Initialize specified New{Service}Client, take NewIamClient for example
    client := iam.NewIamClient(
        iam.IamClientBuilder().
            WithRegion(region.CN_NORTH_4).
            WithCredential(auth).
            WithHttpConfig(config.DefaultHttpConfig()).  
            Build())
    ```
    **where:**

    - If you use {Service}Region to initialize {Service}Client, projectId/domainId supports automatic acquisition, you don't need to configure it when initializing Credentials.
    - Multiple ProjectId situation is not supported.
    
5. Send a request and print response.

    ``` go
    // send request and print response, take interface of ListVpcs for example
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

6. Exceptions

    | Level 1 | Notice | 
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

7. Original HTTP Listener

    In some situation, you may need to debug your http requests, original http request and response information will be needed. The SDK provides a listener function to obtain the original encrypted http request and response information.

    > :warning:  Warning: The original http log information are used in debugging stage only, please do not print the original http header or body in the production environment. These log information are not encrypted and contain sensitive data such as the password of your ECS virtual machine or the password of your IAM user account, etc.

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
