---
layout: default
title: 错误码列表
nav_order: 5
has_children: false
permalink: docs/errorcode
---

# 错误码对照表 
{: .no_toc }



{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 统一错误码

| HTTP | 命名                    | 描述                                                         |
| :--- | :---------------------- | :----------------------------------------------------------- |
| 200  | **OK**                  | 没有错误                                                     |
| 400  | **INVALID_ARGUMENT**    | 客户端指定了无效的参数。 检查错误消息和错误详细信息以获取更多信息。 |
| 400  | **FAILED_PRECONDITION** | 请求不能在当前系统状态下执行，例如删除非空目录。             |
| 400  | **OUT_OF_RANGE**        | 客户端指定了无效的范围。                                     |
| 401  | **UNAUTHENTICATED**     | 由于遗失，无效或过期的OAuth令牌而导致请求未通过身份验证。    |
| 403  | **PERMISSION_DENIED**   | 客户端没有足够的权限。这可能是因为OAuth令牌没有正确的范围，客户端没有权限，或者客户端项目尚未启用API。 |
| 404  | **NOT_FOUND**           | 找不到指定的资源，或者该请求被未公开的原因（例如白名单）拒绝。 |
| 409  | **ABORTED**             | 并发冲突，例如读-修改-写冲突。                               |
| 409  | **ALREADY_EXISTS**      | 客户端尝试创建的资源已存在。                                 |
| 429  | **RESOURCE_EXHAUSTED**  | 资源配额达到速率限制。 客户端应该查找google.rpc.QuotaFailure错误详细信息以获取更多信息。 |
| 499  | **CANCELLED**           | 客户端取消请求                                               |
| 500  | **DATA_LOSS**           | 不可恢复的数据丢失或数据损坏。 客户端应该向用户报告错误。    |
| 500  | **UNKNOWN**             | 未知的服务器错误。 通常是服务器错误。                        |
| 500  | **INTERNAL**            | 内部服务错误。 通常是服务器错误。                            |
| 501  | **NOT_IMPLEMENTED**     | 服务器未实现该API方法。                                      |
| 503  | **UNAVAILABLE**         | 暂停服务。通常是服务器已经关闭。                             |
| 504  | **DEADLINE_EXCEEDED**   | 已超过请求期限。如果重复发生，请考虑降低请求的复杂性。       |