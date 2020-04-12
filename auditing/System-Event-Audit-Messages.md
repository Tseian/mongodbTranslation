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

| `atype` | `param` | `result` | 
| :---: | :--- | :--- |
| `authenticate` | `{ user:` `<user name>, db: <database>, mechanism: <mechanism> }`| 0 - 成功 ；18 - 身份验证失败 |
|`authCheck`| `{ command: <name>, ns: <database>.<collection>, args: <command object> }；ns 字段可选；args 字段可能已编辑。` | 0 - 成功； 13 - 未授权执行该操作；默认情况下，审核系统仅记录授权失败。要使系统记录授权成功，请使用[审计授权成功](../parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess")参数。[[1]](#performance)
|[createCollection](../privilege-actions/#createCollection "createCollection") | `{ ns: <database>.<collection> }` | 0 - 成功 | 
| createDatabase | `{ ns: <database> }` |  0 - 成功 |
| [createIndex](../privilege-actions/#createIndex "createIndex") | `{ ns: <database>.<collection>, indexName: <index name>, indexSpec: <index specification> }` | 0 - 成功 |
| renameCollection | `{ old: <database>.<collection>, new: <database>.<collection> }` | 0 - 成功 |
| [dropCollection](../privilege-actions/#dropCollection "dropCollection") | `{ ns: <database>.<collection> }` | 0 - 成功 |
| [dropDatabase](../privilege-actions/#dropDatabase "dropDatabase") | `{ ns: <database> }` | 0 - 成功 |
| [dropIndex](../privilege-actions/#dropIndex "dropIndex") | `{ ns: <database>.<collection>, indexName: <index name> }` | 0 - 成功 |
| [createUser](../privilege-actions/#createUser "createUser") | `{ user: <user name>, db: <database>, customData: <document>, roles: [{ role: <role name>, db: <database> }, ... ] }；customData 字段是可选的` | 0 - 成功 |
| [dropUser](../privilege-actions/#dropUser "dropUser") | `{ user: <user name>, db: <database> }` | 0 - 成功 | 
| dropAllUsersFromDatabase | `{ db: <database> }` | 0 - 成功 |
| updateUser | `{ user: <user name>, db: <database>, passwordChanged: <boolean>, customData: <document>, roles: [ { role: <role name>, db: <database> }, ... ] }` |   customData 字段是可选的 | 0 - Success |
| grantRolesToUser | `{ user: <user name>, db: <database>, roles: [ { role: <role name>, db: <database> }, ...] }` | 0 - Success |
| revokeRolesFromUser | `{ user: <user name>, db: <database>, roles: [ { role: <role name>, db: <database> }, ... ] }` | 0 - Success |
| [createRole](../privilege-actions/#createRole "createRole") | `{ role: <role name>, db: <database>, roles: [ { role: <role name>, db: <database> }, ... ],privileges: [{ resource: <resource document>, actions: [ <action>, ... ]}, ... ] }`；roles和privileges字段是可选的。；For details on the resource document, see [Resource Document](../resource-document/#resource-document). For a list of actions, see [Privilege Actions](../privilege-actions/#security-user-actions).| 0 - Success |

`updateRole`

{
  role: <role name>,
  db: <database>,
  roles: \[
     {
       role: <role name>,
       db: <database>
     },
     ...
  \],
  privileges: \[
    {
      resource: <resource document>,
      actions: \[ <action>, ... \]
    },
    ...
  \]
}

The `roles` and the `privileges` fields are optional.

For details on the resource document, see [Resource Document](../resource-document/#resource-document). For a list of actions, see [Privilege Actions](../privilege-actions/#security-user-actions).

`0` \- Success

[`dropRole`](../privilege-actions/#dropRole "dropRole")

{
  role: <role name>,
  db: <database>
}

`0` \- Success

`dropAllRolesFromDatabase`

{ db: <database> }

`0` \- Success

`grantRolesToRole`

{
  role: <role name>,
  db: <database>,
  roles: \[
     {
       role: <role name>,
       db: <database>
     },
     ...
  \]
}

`0` \- Success

`revokeRolesFromRole`

{
  role: <role name>,
  db: <database>,
  roles: \[
     {
       role: <role name>,
       db: <database>
     },
     ...
  \]
}

`0` \- Success

`grantPrivilegesToRole`

{
  role: <role name>,
  db: <database>,
  privileges: \[
    {
      resource: <resource document>,
      actions: \[ <action>, ... \]
    },
    ...
  \]
}

For details on the resource document, see [Resource Document](../resource-document/#resource-document). For a list of actions, see [Privilege Actions](../privilege-actions/#security-user-actions).

`0` \- Success

`revokePrivilegesFromRole`

{
  role: <role name>,
  db: <database name>,
  privileges: \[
    {
      resource: <resource document>,
      actions: \[ <action>, ... \]
    },
    ...
  \]
}

For details on the resource document, see [Resource Document](../resource-document/#resource-document). For a list of actions, see [Privilege Actions](../privilege-actions/#security-user-actions).

`0` \- Success

`replSetReconfig`

{
  old: {
   _id: <replicaSetName>,
   version: <number>,
   ...
   members: \[ ... \],
   settings: { ... }
  },
  new: {
   _id: <replicaSetName>,
   version: <number>,
   ...
   members: \[ ... \],
   settings: { ... }
  }
}

For details on the replica set configuration document, see [Replica Set Configuration](../replica-configuration/).

`0` \- Success

[`enableSharding`](../privilege-actions/#enableSharding "enableSharding")

{ ns: <database> }

`0` \- Success

`shardCollection`

{
  ns: <database>.<collection>,
  key: <shard key pattern>,
  options: { unique: <boolean> }
}

`0` \- Success

[`addShard`](../privilege-actions/#addShard "addShard")

{
  shard: <shard name>,
  connectionString: <hostname>:<port>,
  maxSize: <maxSize>
}

When a shard is a replica set, the `connectionString` includes the replica set name and can include other members of the replica set.

`0` \- Success

[`removeShard`](../privilege-actions/#removeShard "removeShard")

{ shard: <shard name> }

`0` \- Success

[`shutdown`](../privilege-actions/#shutdown "shutdown")

{ }

Indicates commencement of database shutdown.

`0` \- Success

[`applicationMessage`](../privilege-actions/#applicationMessage "applicationMessage")

{ msg: <custom message string> }

See [`logApplicationMessage`](../command/logApplicationMessage/#dbcmd.logApplicationMessage "logApplicationMessage").

`0` - Success

[[1]](#id1) Enabling [`auditAuthorizationSuccess`](../parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") degrades performance more than logging only the authorization failures.

[[1]](#id1)启用[审计授权成功](../parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess")与仅记录授权失败相比，启用会使性能下降更多。

