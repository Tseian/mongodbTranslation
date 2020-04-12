# System Event Audit Messages[¶](#system-event-audit-messages "Permalink to this headline")
# 系统事件审计消息[¶](#system-event-audit-messages "Permalink to this headline")

On this page
在本页

*   [Audit Message](#audit-message)
*   [Audit Event Actions, Details, and Results](#audit-event-actions-details-and-results)
*   [审计消息](#audit-message)
*   [审计事件操作，详情和结果](#audit-event-actions-details-and-results)

Note
注意
Available only in [MongoDB Enterprise](http://www.mongodb.com/products/mongodb-enterprise-advanced?jmp=docs) and [MongoDB Atlas](https://cloud.mongodb.com/user#/atlas/login).
仅在[MongoDB 企业版](http://www.mongodb.com/products/mongodb-enterprise-advanced?jmp=docs)和[MongoDB Atlas](https://cloud.mongodb.com/user#/atlas/login)可用。

## Audit Message[¶](#audit-message "Permalink to this headline")
## 审计消息[¶](#audit-message "Permalink to this headline")

The [event auditing feature](../../core/auditing/) can record events in JSON format. To configure auditing output, see [Configure Auditing](../../tutorial/configure-auditing/).
该[事件审核功能](../../core/auditing/)可以记录JSON格式的事件。要配置审核输出，请参阅[配置审核](../../tutorial/configure-auditing/)。


The recorded JSON messages have the following syntax:
记录的JSON消息格式如下：

copy
```js
{
  atype: <String>,
  ts : { "$date": <timestamp> },
  local: { ip: <String>, port: <int> },
  remote: { ip: <String>, port: <int> },
  users : [ { user: <String>, db: <String> }, ... ],
  roles: [ { role: <String>, db: <String> }, ... ],
  param: <document>,
  result: <int>
}
```
复制
```js
{
  atype: <String>,
  ts : { "$date": <timestamp> },
  local: { ip: <String>, port: <int> },
  remote: { ip: <String>, port: <int> },
  users : [ { user: <String>, db: <String> }, ... ],
  roles: [ { role: <String>, db: <String> }, ... ],
  param: <document>,
  result: <int>
}
```

| Field | Type | Description | 
|:---:|:---:|:---:|
| `atype` | string | Action type. See [Audit Event Actions, Details, and Results](#audit-action-details-results).

`ts` document Document that contains the date and UTC time of the event, in ISO 8601 format.

`local` document Document that contains the local `ip` address and the `port` number of the running instance.

`remote` document Document that contains the remote `ip` address and the `port` number of the incoming connection associated with the event.

`users` array Array of user identification documents. Because MongoDB allows a session to log in with different user per database, this array can have more than one user. Each document contains a `user` field for the username and a `db` field for the authentication database for that user.

`roles` array Array of documents that specify the [roles](../../core/authorization/) granted to the user. Each document contains a `role` field for the name of the role and a `db` field for the database associated with the role.

`param` document Specific details for the event. See [Audit Event Actions, Details, and Results](#audit-action-details-results).

`result` integer Error code. See [Audit Event Actions, Details, and Results](#audit-action-details-results).

| 字段 | 类型 | 描述|
|:---:|:---:|:---|
|`atype` | string | 操作类型. 详情请看[审计事件操作，详情和结果](#audit-action-details-results). |
|`ts`| document| 文档包含日期和UTC时间格式为ISO 8601 |
|`local`| document | 文档包含运行实例本地IP和端口 |
|`remote`| document | 文档包含与事件相关的传入连接的远程ip和端口号 |
|`users` | array | 数组包含一组用户识别文档。由于MongoDB允许会话以每个数据库的不同用户身份登录，因此该数组可以包含多个用户。每个文档都包含user字段记录用户名和db字段记录验证该用户的数据库名 |
|`roles`| array | 数组包含文档，用于指定授予用户的角色。每个文档包含一个role字段记录角色名和一个db字段记录与该角色相关的数据库名 |
| `param` | document | 事件的详细信息。请看[审计事件操作，详情和结果](#audit-action-details-results). |
|`result` | integer | 错误码。请看[审计事件操作，详情和结果](#audit-action-details-results). |

## Audit Event Actions, Details, and Results[¶](#audit-event-actions-details-and-results "Permalink to this headline")
## 审计事件操作，详情和结果[¶](#audit-event-actions-details-and-results "Permalink to this headline")
The following table lists for each `atype` or action type, the associated `param` details and the `result` values, if any.
下表列出了每种atype或操作类型，相关的param详细信息和result值(如果有)。

[[1]](#id1) Enabling [`auditAuthorizationSuccess`](../parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") degrades performance more than logging only the authorization failures.

[[1]](#id1)启用[审计授权成功](../parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess")与仅记录授权失败相比，启用会使性能下降更多。

