English | [简体中文](./README_CN.md)

<p align="center">
<a href="https://www.huaweicloud.com/"><img width="600px" height="136px" src="https://console-static.huaweicloud.com/static/authui/20210202115135/public/custom/images/logo-en.svg"></a>
</p>

# Huawei Cloud Python Software Development Kit (Python SDK)

The Huawei Cloud Python SDK allows you to easily work with Huawei Cloud services such as Elastic Compute Service (ECS)
and Virtual Private Cloud (VPC) without the need to handle API related tasks.

This document introduces how to obtain and use Huawei Cloud Python SDK.

## Requirements

- To use Huawei Cloud Python SDK, you must have Huawei Cloud account as well as the Access Key and Secret Key of the
  Huawei Cloud account. You can create an Access Key in the Huawei Cloud console. For more information,
  see [My Credentials](https://support.huaweicloud.com/en-us/usermanual-ca/en-us_topic_0046606340.html).

- To use Huawei Cloud Python SDK to access the APIs of specific service, please make sure you do have activated the
  service in [Huawei Cloud console](https://console.huaweicloud.com/?locale=en-us) if needed.

- Huawei Cloud Python SDK requires **Python 3** or later, Run command `python --version` to check the version of Python.

## Install Python SDK

You could use **pip** or **source code** to install dependencies.

You must install `huaweicloudsdkcore` library no matter which product/service development kit you need to use. Take
using VPC SDK for example, you need to install `huaweicloudsdkcore` library and `huaweicloudsdkvpc` library:

- Use python pip

```bash
# Install the core library
pip install huaweicloudsdkcore

# Install the VPC management library
pip install huaweicloudsdkvpc
```

- Install from source code

```bash
# Install the core library
cd huaweicloudsdkcore-${version}
python setup.py install

# Install the VPC management library
cd huaweicloudsdkvpc-${version}
python setup.py install
```

## Code example

- The following example shows how to query a list of VPC in a specific region, you need to substitute your
  real `{Service}Client` for `VpcClient` in actual use.
- Substitute the values for `{your ak string}`, `{your sk string}`, `{your endpoint string}` and `{your project id}`.

``` python
# coding: utf-8


from huaweicloudsdkcore.auth.credentials import BasicCredentials
from huaweicloudsdkcore.exceptions import exceptions
from huaweicloudsdkcore.http.http_config import HttpConfig
# import specified service library huaweicloudsdk{service}, take vpc for example
from huaweicloudsdkvpc.v2 import *


def list_vpc(client):
    try:
        request = ListVpcsRequest(limit=1)
        response = client.list_vpcs(request)
        print(response)
    except exceptions.ClientRequestException as e:
        print(e.status_code)
        print(e.request_id)
        print(e.error_code)
        print(e.error_msg)


if __name__ == "__main__":
    ak = "{your ak string}"
    sk = "{your sk string}"
    endpoint = "{your endpoint}"
    project_id = "{your project id}"

    config = HttpConfig.get_default_config()
    config.ignore_ssl_verification = True
    credentials = BasicCredentials(ak, sk, project_id)

    vpc_client = VpcClient.new_builder() \
        .with_http_config(config) \
        .with_credentials(credentials) \
        .with_endpoint(endpoint) \
        .build()

    list_vpc(vpc_client)
```

## Changelog

Detailed changes for each released version are documented in
the [CHANGELOG.md](https://github.com/huaweicloud/huaweicloud-sdk-python-v3/blob/master/CHANGELOG.md).

## User Manual [:top:](#huawei-cloud-python-software-development-kit-python-sdk)

* [1. Client Configuration](#1-client-configuration-top)
    * [1.1  Default Configuration](#11-default-configuration-top)
    * [1.2  Network Proxy](#12-network-proxy-top)
    * [1.3  Connection](#13-connection-top)
    * [1.4  SSL Certification](#14-ssl-certification-top)
* [2. Credentials Configuration](#2-credentials-configuration-top)
    * [2.1  Use Permanent AK&SK](#21-use-permanent-aksk-top)
    * [2.2  Use Temporary AK&SK](#22-use-temporary-aksk-top)
* [3. Client Initialization](#3-client-initialization-top)
    * [3.1  Initialize the client with specified Endpoint](#31-initialize-the-serviceclient-with-specified-endpoint-top)
    * [3.2  Initialize the client with specified Region (Recommended)](#32-initialize-the-serviceclient-with-specified-region-recommended-top)
* [4. Send Requests and Handle Responses](#4-send-requests-and-handle-responses-top)
    * [4.1  Exceptions](#41-exceptions-top)
* [5. Use Asynchronous Client](#5-use-asynchronous-client-top)
* [6. Troubleshooting](#6-troubleshooting-top)
    * [6.1 Access Log](#61-access-log-top)
    * [6.2 Original HTTP Listener](#62-original-http-listener-top)

### 1. Client Configuration [:top:](#user-manual-top)

#### 1.1 Default Configuration [:top:](#user-manual-top)

``` python
#  Use default configuration
config = HttpConfig.get_default_config()
```

#### 1.2 Network Proxy [:top:](#user-manual-top)

``` python
# Use Proxy if needed
config.proxy_protocol = 'http'
config.proxy_host = 'proxy.huaweicloud.com'
config.proxy_port = 80
config.proxy_user = 'username'
config.proxy_password = 'password'
```

#### 1.3 Connection [:top:](#user-manual-top)

``` python
# The default connection timeout is 60 seconds, the default read timeout is 120 seconds. You could specify a unified timeout by using config.timeout=timeout, or specify timeout separately config.timeout=(connect timeout, read timeout)
config.timeout = 120
```

#### 1.4 SSL Certification [:top:](#user-manual-top)

``` python
# Skip ssl certifaction checking while using https protocol if needed
config.ignore_ssl_verification = True
# Server ca certification if needed
config.ssl_ca_cert = ssl_ca_cert
```

### 2. Credentials Configuration [:top:](#user-manual-top)

There are two types of Huawei Cloud services, `regional` services and `global` services.

Global services contain BSS, DevStar, EPS, IAM, RMS, TMS.

For `regional` services' authentication, project_id is required. For `global` services' authentication, domain_id is
required.

**Parameter description**:

- `ak` is the access key ID for your account.
- `sk` is the secret access key for your account.
- `project_id` is the ID of your project depending on your region which you want to operate.
- `domain_id` is the account ID of Huawei Cloud.
- `security_token` is the security token when using temporary AK/SK.

#### 2.1 Use Permanent AK&SK [:top:](#user-manual-top)

``` python
# Region services
basic_credentials = BasicCredentials(ak, sk, project_id)

# Global services
global_credentials = GlobalCredentials(ak, sk, domain_id)
```

**Notice**: project_id/domain_id supports **automatic acquisition** in version `3.0.26-beta` or later, if you want to
use this feature, it's required to build your client instance with method `with_region()`, detailed example could refer
to [3.2 Initialize the client with specified Region](#32-initialize-the-serviceclient-with-specified-region-recommended-top)
.

#### 2.2 Use Temporary AK&SK [:top:](#user-manual-top)

It's required to obtain temporary access key, security key and security token first, which could be obtained through
permanent access key and security key or through an agency.

Obtaining a temporary access key token through permanent access key and security key, you could refer to
document: https://support.huaweicloud.com/en-us/api-iam/iam_04_0002.html . The API mentioned in the document above
corresponds to the method of `CreateTemporaryAccessKeyByToken` in IAM SDK.

Obtaining a temporary access key and security token through an agency, you could refer to
document: https://support.huaweicloud.com/en-us/api-iam/iam_04_0101.html . The API mentioned in the document above
corresponds to the method of `CreateTemporaryAccessKeyByAgency` in IAM SDK.

``` python
# Region services
basic_credentials = BasicCredentials(ak, sk, project_id).with_security_token(security_token)

# Global services
global_credentials = GlobalCredentials(ak, sk, domain_id).with_security_token(security_token)
```

### 3. Client Initialization [:top:](#user-manual-top)

There are two ways to initialize the {Service}Client, you could choose one you preferred.

#### 3.1 Initialize the {Service}Client with specified Endpoint [:top:](#user-manual-top)

``` python
# Initialize specified service client instance, take VpcClient for example
client = VpcClient.new_builder() \
    .with_http_config(config) \
    .with_credentials(basic_credentials) \
    .with_endpoint(endpoint) \
    .build()
```

**where:**

- `endpoint` varies by services and regions,
  see [Regions and Endpoints](https://developer.huaweicloud.com/intl/en-us/endpoint) to obtain correct endpoint.

#### 3.2 Initialize the {Service}Client with specified Region **(Recommended)** [:top:](#user-manual-top)

``` python
# dependency for region module
from huaweicloudsdkiam.v3.region.iam_region import IamRegion

# domain_id could be unassigned in this situation
global_credentials = GlobalCredentials(ak, sk)

# initialize specified service client instance, take IamClient for example
client = IamClient.new_builder() \
    .with_http_config(config) \
    .with_credentials(global_credentials) \
    .with_region(IamRegion.CN_NORTH_4) \
    .build()
```

**Notice:**

- If you use {Service}Region to initialize {Service}Client, project_id/domain_id supports automatic acquisition, you
  don't need to configure it when initializing Credentials.
- Multiple project_id situation is not supported.

### 4. Send Requests and Handle Responses [:top:](#user-manual-top)

``` python
# Initialize a request and print response, take interface of ListVpcs for example
request = ListVpcsRequest(limit=1)

response = client.list_vpcs(request)
print(response)
```

#### 4.1 Exceptions [:top:](#user-manual-top)

| Level 1 | Notice | Level 2 | Notice |
| :---- | :---- | :---- | :---- |
| ConnectionException | Connection error | HostUnreachableException | Host is not reachable |
| | | SslHandShakeException | SSL certification error |
| RequestTimeoutException | Request timeout | CallTimeoutException | timeout for single request |
| | | RetryOutageException | no response after retrying |
| ServiceResponseException | service response error | ServerResponseException | server inner error, http status code: [500,] |
| | | ClientRequestException | invalid request, http status code: [400? 500) |

``` python
# handle exceptions
try:
    request = ListVpcsRequest(limit=1)
    response = client.list_vpcs(request)
    print(response)
except exception.ServiceResponseException as e:
    print(e.status_code)
    print(e.request_id)
    print(e.error_code)
    print(e.error_msg)
```

### 5. Use Asynchronous Client [:top:](#user-manual-top)

``` python
# Initialize asynchronous client, take VpcAsyncClient for example
client = VpcAsyncClient.new_builder() \
    .with_http_config(config) \
    .with_credentials(basic_credentials) \
    .with_endpoint(endpoint) \
    .build()

# send asynchronous request
request = ListVpcsRequest(limit=1)
response = client.list_vpcs_async(request)

# get asynchronous response
print(response.result())
```

### 6. Troubleshooting [:top:](#user-manual-top)

SDK supports `Access` log and `Debug` log which could be configured manually.

#### 6.1 Access Log [:top:](#user-manual-top)

SDK supports print access log which could be enabled by manual configuration, the log could be output in console or
specified files.

For example:

``` python
# Initialize specified service client instance, take VpcClient for example
client = VpcClient.new_builder() \
    .with_http_config(config) \
    .with_credentials(basic_credentials) \
    .with_endpoint(endpoint) \
    .with_file_log(path="test.log", log_level=logging.INFO) \  # Write log files
    .with_stream_log(log_level=logging.INFO) \                 # Write log to console
    .build()
```

**where:**

- `with_file_log`:
    - `path` means log file path.
    - `log_level` means log level, default is INFO.
    - `max_bytes` means size of single log file, the default value is 10485760 bytes.
    - `backup_count` means count of log file, the default value is 5.
- `with_stream_log`:
    - `stream` means stream object, the default value is sys.stdout.
    - `log_level` means log level, the default value is INFO.

After enabled log, the SDK will print the access log by default, every request will be recorded in console like:

```shell script
2020-06-16 10:44:02,019 4568 HuaweiCloud-SDK http_handler.py 28 INFO "GET https://vpc.cn-north-1.myhuaweicloud.com/v1/0904f9e1f100d2932f94c01f9aa1cfd7/vpcs" 200 11 0:00:00.543430 b5c927ffdab8401e772e70aa49972037
```

The format of access log is:

``` python
%(asctime)s %(thread)d %(name)s %(filename)s %(lineno)d %(levelname)s %(message)s
```

#### 6.2 Original HTTP Listener [:top:](#user-manual-top)

In some situation, you may need to debug your http requests, original http request and response information will be
needed. The SDK provides a listener function to obtain the original encrypted http request and response information.

> :warning:  Warning: The original http log information is used in debugging stage only, please do not print the original http header or body in the production environment. These log information is not encrypted and contains sensitive data such as the password of your ECS virtual machine, or the password of your IAM user account, etc. When the response body is binary content, the body will be printed as "***" without detailed information.

``` python
import logging
from huaweicloudsdkcore.http.http_handler import HttpHandler


def response_handler(**kwargs):
    logger = kwargs.get("logger")
    response = kwargs.get("response")
    request = response.request

    base = "> Request %s %s HTTP/1.1" % (request.method, request.path_url) + "\n"
    if len(request.headers) != 0:
        base = base + "> Headers:" + "\n"
        for each in request.headers:
            base = base + "    %s : %s" % (each, request.headers[each]) + "\n"
    base = base + "> Body: %s" % request.body + "\n\n"

    base = base + "< Response HTTP/1.1 %s " % response.status_code + "\n"
    if len(response.headers) != 0:
        base = base + "< Headers:" + "\n"
        for each in response.headers:
            base = base + "    %s : %s" % (each, response.headers[each],) + "\n"
    base = base + "< Body: %s" % response.content
    logger.debug(base)


if __name__ == "__main__":
    client = VpcClient.new_builder() \
        .with_http_config(config) \
        .with_credentials(basic_credentials) \
        .with_stream_log(log_level=logging.DEBUG) \
        .with_http_handler(HttpHandler().add_response_handler(response_handler)) \
        .with_endpoint(endpoint) \
        .build()
```

**Notice:**

HttpHandler supports method `add_request_handler` and `add_response_handler`.
