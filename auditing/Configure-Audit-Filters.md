# Configure Audit Filters[¶](#configure-audit-filters "Permalink to this headline")
# 配置审计过滤器[¶](#configure-audit-filters "Permalink to this headline")

On this page
在本页

- [`--auditFilter` Option](#auditfilter-option)
- [Examples](#examples)
- [`--auditFilter` 选项](#auditfilter-option)
- [例子](#examples)


Auditing in MongoDB Atlas
MongoDB Atlas 中的审计

MongoDB Atlas supports auditing for all `M10` and larger clusters. 
MongoDB Atlas支持对所有M10更大的集群进行审计。
Atlas supports specifying a JSON-formatted audit filter as documented in [Configure Audit Filters](../configure-audit-filters/) and using the Atlas audit filter builder for simplified auditing configuration. 
Atlas支持指定“[配置审计过滤器](../configure-audit-filters/)”中所述的JSON格式的审计过滤器， 并使用Atlas审计过滤器构建器来简化审计配置。
To learn more, see the Atlas documentation for [Set Up Database Auditing](https://docs.atlas.mongodb.com/database-auditing) and [Configure a Custom Auditing Filter](https://docs.atlas.mongodb.com/tutorial/auditing-custom-filter).
要了解更多信息，请参阅Atlas文档中的“[设置数据库审计](https://docs.atlas.mongodb.com/database-auditing)和[配置自定义审计过滤器](https://docs.atlas.mongodb.com/tutorial/auditing-custom-filter)”。

[MongoDB Enterprise](https://www.mongodb.com/products/mongodb-enterprise-advanced?jmp=docs) supports [auditing](../../core/auditing/#auditing) of various operations.
[MongoDB 企业版](https://www.mongodb.com/products/mongodb-enterprise-advanced?jmp=docs)支持[审计](../../core/auditing/#auditing)各种操作。
When [enabled](../configure-auditing/), the audit facility, by default, records all auditable operations as detailed in [Audit Event Actions, Details, and Results](../../reference/audit-message/#audit-action-details-results).
启用审计功能会默认的记录所有可审计的操作，如[Audit Event Actions, Details, and Results](../../reference/audit-message/#audit-action-details-results)。
To specify which events to record, the audit feature includes the `--auditFilter` option.
`--auditFilter`选项允许我们指定那些事件需要被记录。

Note
注意

Starting in MongoDB 3.6, [`mongod`](../../reference/program/mongod/#bin.mongod "bin.mongod") and [`mongos`](../../reference/program/mongos/#bin.mongos "bin.mongos") bind to localhost by default. 
从mongoDB 3.6开始，[`mongod`](../../reference/program/mongod/#bin.mongod "bin.mongod") and [`mongos`](../../reference/program/mongos/#bin.mongos "bin.mongos")默认绑定localhost。
If the members of your deployment are run on different hosts or if you wish remote clients to connect to your deployment, you must specify `--bind_ip` or [`net.bindIp`](../../reference/configuration-options/#net.bindIp "net.bindIp"). 
如果你部署的实例运行在不同的主机上或者如果你希望远程客户端连接到部署实例，你必须指定`--bind_ip` or [`net.bindIp`](../../reference/configuration-options/#net.bindIp "net.bindIp"). 

For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).
更多信息，请查看[Localhost 绑定兼容性更改](../../release-notes/3.6-compatibility/#bind-ip-compatibility)。

Before you bind to other ip addresses, consider [enabling access control](../../administration/security-checklist/#checklist-auth) and other security measures listed in [Security Checklist](../../administration/security-checklist/) to prevent unauthorized access.
绑定到其他IP地址之前，请考虑启用[访问控制](../../administration/security-checklist/#checklist-auth)和[“安全性检查表”](../../administration/security-checklist/)中的列出的其他安全措施，以防止未经授权的访问。

## `--auditFilter` Option[¶](#auditfilter-option "Permalink to this headline")
## `--auditFilter` 选项[¶](#auditfilter-option "Permalink to this headline")

The `--auditFilter` option takes a string representation of a query document of the form:
--auditFilter`选项采用以下查询文档的字符串的表示形式：
copy

{ <field1>: <expression1>, ... }
复制

```js
{ <field1>: <expression1>, ... }
```

- The `<field>` can be [any field in the audit message](../../reference/audit-message/), including fields returned in the [param](../../reference/audit-message/#audit-action-details-results)document.
- `<field>`可以是[审计消息](../../reference/audit-message/)中的任何字段，包括[param](../../reference/audit-message/#audit-action-details-results)文档中返回的字段。
- The `<expression>` is a [query condition expression](../../reference/operator/query/#query-selectors).
- `<expression>`是一个[查询条件表达式](../../reference/operator/query/#query-selectors)。

To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.
指定一个审计过滤器，可以将过滤器文档括在单引号中使其转成字符串。

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.
在[配置文件](../../reference/configuration-options/)中指定审计过滤器，必须使用配置文件的YAML格式。

## Examples[¶](#examples "Permalink to this headline")
## 例子[¶](#examples "Permalink to this headline")

### Filter for Multiple Operation Types[¶](#filter-for-multiple-operation-types "Permalink to this headline")
### 筛选多种操作类型[¶](#filter-for-multiple-operation-types "Permalink to this headline")

The following example audits only the [`createCollection`](../../reference/privilege-actions/#createCollection "createCollection") and [`dropCollection`](../../reference/privilege-actions/#dropCollection "dropCollection") actions by using the filter:
以下示例通过使用过滤器仅审核[`createCollection`]和[`dropCollection`]操作：

copy
{ atype: { $in: ["createCollection", "dropCollection"] } }

复制
```js
{ atype: { $in: ["createCollection", "dropCollection"] } }
```

To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.
指定一个审计过滤器，可以将过滤器文档括在单引号中使其转成字符串。

copy
mongod --dbpath data/db --auditDestination file --auditFilter '{ atype: { $in: [ "createCollection", "dropCollection" ] } }' --auditFormat BSON --auditPath data/db/auditLog.bson

复制
```sh
mongod --dbpath data/db --auditDestination file --auditFilter '{ atype: { $in: [ "createCollection", "dropCollection" ] } }' --auditFormat BSON --auditPath data/db/auditLog.bson
```

Include additional options as required for your configuration. For instance, if you wish remote clients to connect to your deployment or your deployment members are run on different hosts, specify the `--bind_ip`. For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).
包括配置所需的其他选项。例如，如果您希望远程客户端连接到您的部署，或者您的部署成员在不同的主机上运行，​​请指定--bind_ip参数。有关更多信息，请参见[Localhost绑定兼容性更改](../../release-notes/3.6-compatibility/#bind-ip-compatibility)。

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.
在[配置文件](../../reference/configuration-options/)中指定审计过滤器，必须使用配置文件的YAML格式。

copy

storage:
dbPath: data/db
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: { \$in:[ "createCollection", "dropCollection"] } }'

复制

```yml
storage:
dbPath: data/db
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: { \$in:[ "createCollection", "dropCollection"] } }'
```

### Filter on Authentication Operations on a Single Database[¶](#filter-on-authentication-operations-on-a-single-database "Permalink to this headline")
### 筛选单个数据库上的身份验证操作[¶](#filter-on-authentication-operations-on-a-single-database "Permalink to this headline")


The `<field>` can include [any field in the audit message](../../reference/audit-message/). For authentication operations (i.e. `atype: "authenticate"`), the audit messages include a `db` field in the `param` document.
`<field>`可以包含[审计消息](../../reference/audit-message/)中的任何字段。对于身份认证操作(即，`atype: "authenticate"`)，审计消息中的param文档中包含‘db’字段。

The following example audits only the `authenticate` operations that occur against the `test` database by using the filter:
以下示例使用过滤器仅审核针对test数据库的`authenticate`操作。
copy

{ atype: "authenticate", "param.db": "test" }

复制

```js
{ atype: "authenticate", "param.db": "test" }
```
To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.
在[配置文件](../../reference/configuration-options/)中指定审计过滤器。

copy

mongod --dbpath data/db --auth --auditDestination file --auditFilter '{ atype: "authenticate", "param.db": "test" }' --auditFormat BSON --auditPath data/db/auditLog.bson

复制
```sh
mongod --dbpath data/db --auth --auditDestination file --auditFilter '{ atype: "authenticate", "param.db": "test" }' --auditFormat BSON --auditPath data/db/auditLog.bson
```

Include additional options as required for your configuration. For instance, if you wish remote clients to connect to your deployment or your deployment members are run on different hosts, specify the `--bind_ip`. For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).
包括配置所需的其他选项。例如，如果您希望远程客户端连接到您的部署，或者您的部署成员在不同的主机上运行，​​请指定--bind_ip参数。更多信息，请参见[Localhost绑定兼容性更改](../../release-notes/3.6-compatibility/#bind-ip-compatibility)。

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.
在[配置文件](../../reference/configuration-options/)中指定审计过滤器，必须使用配置文件的YAML格式。

copy
```yml
storage:
dbPath: data/db
security:
authorization: enabled
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: "authenticate", "param.db": "test" }'
```
复制
```yml
storage:
dbPath: data/db
security:
authorization: enabled
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: "authenticate", "param.db": "test" }'
```

To filter on all `authenticate` operations across databases, use the filter `{ atype: "authenticate" }`.
要过滤数据库中的所有‘authenticate’操作，请使用过滤器`{ atype: "authenticate" }`。

### Filter on Collection Creation and Drop Operations for a Single Database[¶](#filter-on-collection-creation-and-drop-operations-for-a-single-database "Permalink to this headline")
### 筛选单个数据库的集合创建和删除操作[¶](#filter-on-collection-creation-and-drop-operations-for-a-single-database "Permalink to this headline")

The `<field>` can include [any field in the audit message](../../reference/audit-message/). For collection creation and drop operations (i.e. `atype: "createCollection"` and `atype: "dropCollection"`), the audit messages include a namespace `ns` field in the `param` document.
`<field>`可以包含[审计消息](../../reference/audit-message/)中的任何字段。对于集合创建和删除操作(即，`atype: "createCollection"`和`atype: "dropCollection"`)，审计消息中的param文档中包含‘ns’字段。

The following example audits only the `createCollection` and `dropCollection` operations that occur against the `test` database by using the filter:

Note

The regular expression requires two backslashes (`\\`) to escape the dot (`.`).

copy

copied

{ atype: { \$in: \[ "createCollection", "dropCollection" \] }, "param.ns": /^test\\\./ } }

To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.

copy

copied

mongod --dbpath data/db --auth --auditDestination file --auditFilter '{ atype: { \$in: \[ "createCollection", "dropCollection" \] }, "param.ns": /^test\\\./ } }' --auditFormat BSON --auditPath data/db/auditLog.bson

Include additional options as required for your configuration. For instance, if you wish remote clients to connect to your deployment or your deployment members are run on different hosts, specify the `--bind_ip`. For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.


copy

copied

storage:
dbPath: data/db
security:
authorization: enabled
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: { \$in: \[ "createCollection", "dropCollection" \] }, "param.ns": /^test\\\./ } }'

### Filter by Authorization Role[¶](#filter-by-authorization-role "Permalink to this headline")

The following example audits operations by users with [`readWrite`](../../reference/built-in-roles/#readWrite "readWrite") role on the `test` database, including users with roles that inherit from [`readWrite`](../../reference/built-in-roles/#readWrite "readWrite"), by using the filter:

copy

copied

{ roles: { role: "readWrite", db: "test" } }

To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.

copy

copied

mongod --dbpath data/db --auth --auditDestination file --auditFilter '{ roles: { role: "readWrite", db: "test" } }' --auditFormat BSON --auditPath data/db/auditLog.bson

Include additional options as required for your configuration. For instance, if you wish remote clients to connect to your deployment or your deployment members are run on different hosts, specify the `--bind_ip`. For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.

copy

copied

storage:
dbPath: data/db
security:
authorization: enabled
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ roles: { role: "readWrite", db: "test" } }'

### Filter on Read and Write Operations[¶](#filter-on-read-and-write-operations "Permalink to this headline")

To capture [`read`](../../reference/built-in-roles/#read "read") and `write` operations in the audit, you must also enable the audit system to log authorization successes using the [`auditAuthorizationSuccess`](../../reference/parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") parameter. [\[1\]](#authorization-agnostic)

Note

Enabling [`auditAuthorizationSuccess`](../../reference/parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") degrades performance more than logging only the authorization failures.

The following example audits the [`find()`](../../reference/method/db.collection.find/#db.collection.find "db.collection.find()"), [`insert()`](../../reference/method/db.collection.insert/#db.collection.insert "db.collection.insert()"), [`remove()`](../../reference/method/db.collection.remove/#db.collection.remove "db.collection.remove()"), [`update()`](../../reference/method/db.collection.update/#db.collection.update "db.collection.update()"), [`save()`](../../reference/method/db.collection.save/#db.collection.save "db.collection.save()"), and [`findAndModify()`](../../reference/method/db.collection.findAndModify/#db.collection.findAndModify "db.collection.findAndModify()") operations by using the filter:

copy

copied

{ atype: "authCheck", "param.command": { \$in: \[ "find", "insert", "delete", "update", "findandmodify" \] } }

To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.

copy

copied

mongod --dbpath data/db --auth --setParameter auditAuthorizationSuccess=true --auditDestination file --auditFilter '{ atype: "authCheck", "param.command": { \$in: \[ "find", "insert", "delete", "update", "findandmodify" \] } }' --auditFormat BSON --auditPath data/db/auditLog.bson

Include additional options as required for your configuration. For instance, if you wish remote clients to connect to your deployment or your deployment members are run on different hosts, specify the `--bind_ip`. For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.

copy

copied

storage:
dbPath: data/db
security:
authorization: enabled
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: "authCheck", "param.command": { \$in: \[ "find", "insert", "delete", "update", "findandmodify" \] } }'
setParameter: { auditAuthorizationSuccess: true }

### Filter on Read and Write Operations for a Collection[¶](#filter-on-read-and-write-operations-for-a-collection "Permalink to this headline")

To capture [`read`](../../reference/built-in-roles/#read "read") and `write` operations in the audit, you must also enable the audit system to log authorization successes using the [`auditAuthorizationSuccess`](../../reference/parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") parameter. [\[1\]](#authorization-agnostic)

Note

Enabling [`auditAuthorizationSuccess`](../../reference/parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") degrades performance more than logging only the authorization failures.

The following example audits the [`find()`](../../reference/method/db.collection.find/#db.collection.find "db.collection.find()"), [`insert()`](../../reference/method/db.collection.insert/#db.collection.insert "db.collection.insert()"), [`remove()`](../../reference/method/db.collection.remove/#db.collection.remove "db.collection.remove()"), [`update()`](../../reference/method/db.collection.update/#db.collection.update "db.collection.update()"), [`save()`](../../reference/method/db.collection.save/#db.collection.save "db.collection.save()"), and [`findAndModify()`](../../reference/method/db.collection.findAndModify/#db.collection.findAndModify "db.collection.findAndModify()") operations for the collection `orders` in the database `test` by using the filter:

copy

copied

{ atype: "authCheck", "param.ns": "test.orders", "param.command": { \$in: \[ "find", "insert", "delete", "update", "findandmodify" \] } }

To specify an audit filter, enclose the filter document in single quotes to pass the document as a string.

copy

copied

mongod --dbpath data/db --auth --setParameter auditAuthorizationSuccess=true --auditDestination file --auditFilter '{ atype: "authCheck", "param.ns": "test.orders", "param.command": { \$in: \[ "find", "insert", "delete", "update", "findandmodify" \] } }' --auditFormat BSON --auditPath data/db/auditLog.bson

Include additional options as required for your configuration. For instance, if you wish remote clients to connect to your deployment or your deployment members are run on different hosts, specify the `--bind_ip`. For more information, see [Localhost Binding Compatibility Changes](../../release-notes/3.6-compatibility/#bind-ip-compatibility).

To specify the audit filter in a [configuration file](../../reference/configuration-options/), you must use the YAML format of the configuration file.

copy

copied

storage:
dbPath: data/db
security:
authorization: enabled
auditLog:
destination: file
format: BSON
path: data/db/auditLog.bson
filter: '{ atype: "authCheck", "param.ns": "test.orders", "param.command": { \$in: \[ "find", "insert", "delete", "update", "findandmodify" \] } }'
setParameter: { auditAuthorizationSuccess: true }

See also

[Configure Auditing](../configure-auditing/), [Auditing](../../core/auditing/), [System Event Audit Messages](../../reference/audit-message/)

\[1\]

_([1](#id1), [2](#id2))_ You can enable [`auditAuthorizationSuccess`](../../reference/parameters/#param.auditAuthorizationSuccess "auditAuthorizationSuccess") parameter without enabling `--auth`; however, all operations will return success for authorization checks.
