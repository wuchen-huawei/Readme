# 0.0.33-rc 2021-02-07

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that request sends fail when the data type of request body is `string`.
- __Change__
  - None

### HuaweiCloud SDK IMS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Interface `ListOsVersions` adjustment: change the data type of `os_bit` which is the property of response of the
    interface from string to integer.

### HuaweiCloud SDK Live

- __Features__
  - Support more interfaces: ListLiveSampleLogs, CreateDomain, DeleteDomain, UpdateDomain, ShowDomain,
    CreateDomainMapping, DeleteDomainMapping
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK MRS

- __Features__
  - Support `MapReduce Service`.
- __Bug Fix__
  - None
- __Change__
  - None

# 0.0.32-rc 2021-01-30

### HuaweiCloud SDK DDS

- __Features__
  - Support more interfaces: `ListApiVersion`, `ShowApiVersion`,`SetAuditlogPolicy`, `ShowAuditlogPolicy`
    , `ListAuditlogs`.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK DNS

- __Features__
  - Support `Domain Name Service`.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ECS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Change interface name from `UpdateAutoTerminateTimeServer` to `UpdateServerAutoTerminateTime`.

### HuaweiCloud SDK EVS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Interface `CinderCreateVolume` is supported to specify the id of dedicated storage pool using
    property `OS-SCH-HNT:scheduler_hints`.
  - Modify property type of `allocated` of class `QuotaDetails` from `String` to `Integer`.

### HuaweiCloud SDK IAM

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Increases the property `access_mode` of response class of interface `ShowUser`.

## 0.0.31-rc 2021-01-25

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - The default value of `DefaultTimeout` is set to 120 seconds.

### HuaweiCloud SDK BSS

- __Features__
  - Support more interface: ListOrderDiscounts.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK DNS

- __Features__
  - Support `Domain Name Service`.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ECS

- __Features__
  - Support more interface: `UpdateAutoTerminateTimeServer`.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.30-rc 2021-01-15

### HuaweiCloud SDK Core

- __Features__
  - Support function `ValueOf` to get region information.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CloudBuild

- __Features__
  - Support more interface: `ShowListHistory`.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK DGC

- __Features__
  - Support more interfaces: `Job` related interfaces, `Script` related interfaces, `Resource` related interfaces.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK IAM

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Modify the data type of response field `is_domain_owner` from string to boolean of interface `ShowUser`
    and `CreateUser`.

### HuaweiCloud SDK Live

- __Features__
  - Support more interface: `ListLiveStreamsOnline`.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK RDS

- __Features__
  - Support more interfaces: ShowOffSiteBackupPolicy, SetOffSiteBackupPolicy, ListOffSiteBackups,
    ListOffSiteRestoreTimes, ListOffSiteRestoreTimes
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK SWR

- __Features__
  - Support `Software Repository for Container` service.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.29-beta 2020-12-31

### HuaweiCloud SDK BMS

- __Features__
  - None
- __Bug Fix__
  - Fix the problem of interface: ListBareMetalServers.
  - Fix the problem of interface: ListBareMetalServerDetails.
  - Modify interface fields: ShowBaremetalServerInterfaceAttachments.
- __Change__
  - None

### HuaweiCloud SDK CloudIDE

- __Features__
  - Support more interface: ShowAccountStatus.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK DCS

- __Features__
  - None
- __Bug Fix__
  - Modify the interface return data type to prevent deserialization failure:
    - ListSlowlog: change data type of `Tags` from Tag to ResourceTag.
    - ListInstances: change data type of `duration` from int32 to string.
    - ShowBigkeyScanTaskDetails: change data type of `db` from int32 to string.
    - ShowHotkeyTaskDetails: change data type of `db` from int32 to string.
- __Change__
  - None

### HuaweiCloud SDK DGC

- __Features__
  - Support `Data Lake Governance Center` service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK DIS

- __Features__
  - Support `Data Ingestion Service`.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK RDS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Interface modification: response type of interface `CreateInstance` adjustment.

### HuaweiCloud SDK SMN

- __Features__
  - None
- __Bug Fix__
  - Modify the request parameters of interface `PublishMessage` from Object to Map<String, String>
- __Change__
  - None

## 0.0.28-beta 2020-12-28

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix response exception when using temporary AK/SK.
- __Change__
  - None

### HuaweiCloud SDK DCS

- __Features__
  - None
- __Bug Fix__
  - Change property type of `port` from string to integer.
- __Change__
  - None

## 0.0.27-beta 2020-12-25

### HuaweiCloud SDK DCS

- __Features__
  - None
- __Bug Fix__
  - Fix the problem of compilation failure in Mac OS.
- __Change__
  - Query parameter in interface `ListInstances` modification: id → instance_id.

### HuaweiCloud SDK DDS

- __Features__
  - Support Document Database Service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK Kafka

- __Features__
  - None
- __Bug Fix__
  - Fix the problem of compilation failure in Mac OS.
- __Change__
  - None

### HuaweiCloud SDK RabbitMQ

- __Features__
  - None
- __Bug Fix__
  - Fix the problem of compilation failure in Mac OS.
- __Change__
  - None

### HuaweiCloud SDK RMS

- __Features__
  - Support more interfaces: `Resources` related interfaces and `Region` related interfaces.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.26-beta 2020-12-23

### HuaweiCloud SDK Core

- __Features__
  - Support Endpoint Resolver: it's supported to use {Service}Region when initializing {ServiceClient} which can
    automatically backfill endpoint. After choosing a region, the projectId/domainId will be backfilled automatically.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK BSS

- __Features__
  - Support more interfaces: ListMeasureUnits.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CES

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Update interface: ShowMetricData

### HuaweiCloud SDK Live

- __Features__
  - Support more interfaces: ShowStreamPortrait.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK MPC

- __Features__
  - Support more interfaces: QualityEnhanceTemplate related interfaces and MergeChannelsTask related interfaces.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK RDS

- __Features__
  - Support Relational Database Service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK SMN

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Update field type in message_template_name.

## 0.0.25-beta 2020-12-15

### HuaweiCloud SDK CCE

- __Features__
  - Support Cloud Container Engine service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ELB

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that sending request to interface `CreateListener` returns empty response.
  - Fix the problem that sending request to interface `CreateListener` returns response with wrong type.
- __Change__
  - None

### HuaweiCloud SDK FunctionGraph

- __Features__
  - Support more interfaces: UpdateFunctionReservedInstances.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK NAT

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that using interface `BatchCreateNatGatewayDnatRules` failed.
- __Change__
  - None

## 0.0.24-beta 2020-12-04

### HuaweiCloud SDK SMN

- __Features__
  - Support Simple Message Notification service.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.23-beta 2020-11-30

### HuaweiCloud SDK BCS

- __Features__
  - Support BlockChain Service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK BMS

- __Features__
  - Support Bare Metal Server service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK BSS

- __Features__
  - Support more interfaces: ListUsageTypes, ModPeriodToOnDemand.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CBR

- __Features__
  - Support more interfaces: MigrateVaultResource
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CES

- __Features__
  - Support more interfaces:
  - ListEvents
  - ListEventDetail
  - CreateResourceGroup
  - UpdateResourceGroup
  - DeleteResourceGroup
  - ListResourceGroup
  - UpdateAlarm
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK DCS

- __Features__
  - Support Distributed Cache Service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ECS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - [Issue 21](https://github.com/huaweicloud/huaweicloud-sdk-java-v3/issues/21) Open related interface.

### HuaweiCloud SDK FunctionGraph

- __Features__
  - Support FunctionGraph service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK IAM

- __Features__
  - Support more interfaces.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK Live

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Name of service client modification: LiveAPIClient → LiveClient.

## 0.0.22-beta 2020-11-17

### HuaweiCloud SDK AS

- __Features__
  - None
- __Bug Fix__
  - [Issue 8](https://github.com/huaweicloud/huaweicloud-sdk-go-v3/issues/8) Fix the problem that creating scaling
    policy failed.
- __Change__
  - None

### HuaweiCloud SDK DMS

- __Features__
  - Support Distributed Message Services, provide Kafka premium instances and RabbitMQ premium instances with dedicated
    resources.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ECS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Property adjustment:  increase property `dry_run` in interfaces `CreatePostPaidServers` and `CreateServers` which
    means whether parameters will be checked before sending real requests.

### HuaweiCloud SDK NAT

- __Features__
  - Support NAT Gateway service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK VPC

- __Features__
  - Support more interfaces: interfaces related to Network ACLs.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.21-beta 2020-11-11

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Update core code from [Pull requests #11](https://github.com/huaweicloud/huaweicloud-sdk-go-v3/pull/11).
- __Change__
  - None

### HuaweiCloud SDK CBR

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Interface adjustment: property `object_type` in interface `CreateVault` support key `turbo`.
  - Interface adjustment: property `description` in interface `UpdatePolicy` is removed.

### HuaweiCloud SDK CES

- __Features__
  - Add examples of interface response and adjust some filed description.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CloudPipeline

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Modify the name of generated Client class: devcloudpipeline_client → cloudPipeline_client
  - Modify the name of generated Meta class: devcloudpipeline_meta → cloudPipeline_meta

### HuaweiCloud SDK DevStar

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Modify interface parameters and adjust sample code.

## 0.0.20-beta 2020-11-02

### HuaweiCloud SDK CES

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Interface adjustment: property `alarm_type` in class `CreateAlarmRequestBody` support key `RESOURCE_GROUP`.
  - Interface adjustment: property `meta_data` in class `ListAlarmHistoriesResponse` only returns total number of alarm
    histories.

### HuaweiCloud SDK ELB

- __Features__
  - None
- __Bug Fix__
  - Modify wrong parameter in class `CreateL7ruleRequestBody`.
- __Change__
  - None

## 0.0.19-beta 2020-10-31

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix: fix the problem that when query parameter contains enumerated variables the request will fail.
  - [Issue 7](https://github.com/huaweicloud/huaweicloud-sdk-go-v3/issues/7) resolve the problem of using json.Marshal()
    returns object{}.
- __Change__
  - None

### HuaweiCloud SDK CBR

- __Features__
  - Support more interfaces: interfaces related to `TAG`.
- __Bug Fix__
  - [Issue 17](https://github.com/huaweicloud/huaweicloud-sdk-java-v3/issues/17) fix the problem of interface:
    ListBackups.
- __Change__
  - None

### HuaweiCloud SDK CTS

- __Features__
  - Support more interface: ListQuotas
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK EPS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Adjust interfaces' names, replace abbreviations of `EP` with `EnterpriseProject`, the involved interfaces are:

  1. ListEP → ListEnterpriseProject
  2. CreateEP → CreateEnterpriseProject
  3. ShowEP → ShowEnterpriseProject
  4. ModifyEP → ModifyEnterpriseProject
  5. EnableEP → EnableEnterpriseProject
  6. ShowEPQuota → ShowEnterpriseProjectQuota
  7. ShowResourceBindEP → ShowResourceBindEnterpriseProject
  8. DisableEP → DisableEnterpriseProject

### HuaweiCloud SDK Iam

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Adjust interfaces' names, the involved interfaces are:

  1. KeystoneCreateUserTokenByPasswordAndMFA → KeystoneCreateUserTokenByPasswordAndMfa
  2. CreateUnscopeTokenByIDPInitiated → CreateUnscopeTokenByIdpInitiated

### HuaweiCloud SDK ProjectMan

- __Features__
  - Support more interfaces: iteration information, user information, project members, project information, project
    indicators, project statistics, etc.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.18-beta 2020-10-20

### HuaweiCloud SDK ELB

- __Features__
  - Support more interfaces of version v2.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.17-beta 2020-10-14

### HuaweiCloud SDK BSS

- __Features__
  - Partner center supports exporting product catalog prices.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK Live

- __Features__
  - Support more interfaces of version v2 of Live.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.16-beta 2020-10-12

### HuaweiCloud SDK CTS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Delete deprecated interfaces of version v1.

### HuaweiCloud SDK DevStar

- __Features__
  - None
- __Bug Fix__
  - Modify the credential type of DevStarClient: the correct credential type is GlobalCredentials.
- __Change__
  - None

## 0.0.15-beta 2020-09-30

### HuaweiCloud SDK AS

- __Features__
  - Support Auto Scaling service.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.14-beta 2020-09-24

### HuaweiCloud SDK BSS

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that the class `BssClient` cannot be loaded.
- __Change__
  - None

### HuaweiCloud SDK EIP

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Interface `ListPublicips` adjustment: enterprise_project_id does not support multi-value query.

## 0.0.13-beta 2020-09-16

### HuaweiCloud SDK ECS

- __Features__
  - None
- __Bug Fix__
  - Fix parameter type of interfaces.
- __Change__
  - None

### HuaweiCloud SDK BSS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Update interfaces.

### HuaweiCloud SDK EIP

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that not support transfer multiple values.
- __Change__
  - None

### HuaweiCloud SDK ELB

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that some parameters are wrong.
- __Change__
  - None

### HuaweiCloud SDK IMS

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Adjust descriptions of interfaces.

### HuaweiCloud SDK Live

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Adjust descriptions of banned interface.

## 0.0.12.1-beta 2020-09-16

### HuaweiCloud SDK ECS

- __Features__
  - None
- __Bug Fix__
  - Fix parameter type of interfaces.
- __Change__
  - None

### HuaweiCloud SDK All

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - When the optional parameter type is list, the parameter type will be changed to a pointer, for example, []string
    to *[]string

## 0.0.12-beta 2020-09-11

### HuaweiCloud SDK KPS

- __Features__
  - Support KPS service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK EVS

- __Features__
  - Support EVS service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CBR

- __Features__
  - None
- __Bug Fix__
  - Fix response value type definition errors.
- __Change__
  - None

## 0.0.11-beta 2020-09-09

### HuaweiCloud SDK CBR

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that resources related interfaces have wrong data type.
- __Change__
  - None

### HuaweiCloud SDK VPC

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that security group related interfaces have wrong data type.
- __Change__
  - None

## 0.0.10-beta 2020-09-04

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that the enumeration code cannot be generated for integer enumeration parameters without format
    defined in yaml.
- __Change__
  - Modify User Agent of Http Request header.

## 0.0.9-beta 2020-08-28

### HuaweiCloud SDK CloudPipeline

- __Features__
  - Support CloudPipeline service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK EIP

- __Features__
  - Support more APIs: tags related APIs and shared bandwidth related APIs.
- __Bug Fix__
  - Interface BatchCreateBandwidth: modify field billing_info.
- __Change__
  - None

### HuaweiCloud SDK IAM

- __Features__
  - Support more APIs: consistency of console related APIs.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ProjectMan

- __Features__
  - Support Project Management service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK VPC

- __Features__
  - Support more APIs: security group, security group rules, available IP count related APIs.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.8-beta 2020-08-25

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - None
- __Change__
  - Change optional enum variable type to pointer.

### HuaweiCloud SDK ELB

- __Features__
  - Support Elastic Load Balance service.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.7-beta 2020-08-20

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix the problem that some enum variables are unreadable.
- __Change__
  - Add 'E' as prefix to enum Variables which start with '_'.

## 0.0.6-beta 2020-08-20

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix the problem of missing the imports when the struct contains enum variables.
- __Change__
  - None

## 0.0.5-beta 2020-08-19

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix the deserialization failure of enum variables.
  - Fix the deserialization failure of error response in some scenarios.
- __Change__
  - None

## 0.0.4-beta 2020-08-18

### HuaweiCloud SDK Core

- __Features__
  - None
- __Bug Fix__
  - Fix the problem of missing default values of Go basic type when serializing.
- __Change__
  - None

## 0.0.3-beta 2020-08-14

### HuaweiCloud SDK APIG

- __Features__
  - Support API Gateway service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK BSS

- __Features__
  - Support Business Support System.
- __Bug Fix__
  - None
- __Change__
  - None

## 0.0.2-beta 2020-8-11

### HuaweiCloud SDK Core

- __Features__
  - Support temporary AK/SK authentication mode.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CBR

- __Features__
  - Support Cloud Backup and Recovery service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK CloudIDE

- __Features__
  - Support Cloud IDE service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK ECS

- __Features__
  - Support Elastic Cloud Server service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK EIP

- __Features__
  - Support Elastic IP service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK EVS

- __Features__
  - Support Elastic Volume Service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK IMS

- __Features__
  - Support Image Management Service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK Live

- __Features__
  - Support Live service.
- __Bug Fix__
  - None
- __Change__
  - None

### HuaweiCloud SDK MPC

- __Features__
  - Support Media Processing Center.
- __Bug Fix__
  - None
- __Change__
  - None

## 3.0.1-beta 2020-07-30

### First Release

- __Supported Services__
  - Classroom
  - Cloud Trace Service(CTS)
  - DevStar
  - Enterprise Project Management Service(EPS)
  - Identity and Access Management(IAM)
  - Tag Management Service(TMS)
  - Virtual Private Cloud(VPC)
