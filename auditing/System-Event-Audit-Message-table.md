
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