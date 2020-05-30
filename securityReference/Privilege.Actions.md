# Privilege Actions

On this page

- [Query and Write Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#query-and-write-actions)
- [Database Management Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#database-management-actions)
- [Deployment Management Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#deployment-management-actions)
- [Change Stream Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#change-stream-actions)
- [Replication Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#replication-actions)
- [Sharding Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#sharding-actions)
- [Server Administration Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#server-administration-actions)
- [Session Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#session-actions)
- [Free Monitoring Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#free-monitoring-actions)
- [Diagnostic Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#diagnostic-actions)
- [Internal Actions](https://docs.mongodb.com/manual/reference/privilege-actions/#internal-actions)

Privilege actions define the operations a user can perform on a [resource](https://docs.mongodb.com/manual/reference/resource-document/#resource-document). A MongoDB [privilege](https://docs.mongodb.com/manual/core/authorization/#privileges) comprises a [resource](https://docs.mongodb.com/manual/reference/resource-document/#resource-document) and the permitted actions. This page lists available actions grouped by common purpose.

MongoDB provides built-in roles with pre-defined pairings of resources and permitted actions. For lists of the actions granted, see [Built-In Roles](https://docs.mongodb.com/manual/reference/built-in-roles/). To define custom roles, see [Create a User-Defined Role](https://docs.mongodb.com/manual/tutorial/manage-users-and-roles/#create-user-defined-role).

## Query and Write Actions

- `find`

  User can perform the following commands, and their equivalent helper methods:[`aggregate`](https://docs.mongodb.com/manual/reference/command/aggregate/#dbcmd.aggregate) for all [pipeline operations](https://docs.mongodb.com/manual/reference/operator/aggregation/) **except** [`$collStats`](https://docs.mongodb.com/manual/reference/operator/aggregation/collStats/#pipe._S_collStats), [`$out`](https://docs.mongodb.com/manual/reference/operator/aggregation/out/#pipe._S_out), and [`$indexStats`](https://docs.mongodb.com/manual/reference/operator/aggregation/indexStats/#pipe._S_indexStats).[`checkShardingIndex`](https://docs.mongodb.com/manual/reference/command/checkShardingIndex/#dbcmd.checkShardingIndex)[`count`](https://docs.mongodb.com/manual/reference/command/count/#dbcmd.count)[`dataSize`](https://docs.mongodb.com/manual/reference/command/dataSize/#dbcmd.dataSize)[`distinct`](https://docs.mongodb.com/manual/reference/command/distinct/#dbcmd.distinct)[`filemd5`](https://docs.mongodb.com/manual/reference/command/filemd5/#dbcmd.filemd5)[`find`](https://docs.mongodb.com/manual/reference/command/find/#dbcmd.find)[`geoSearch`](https://docs.mongodb.com/manual/reference/command/geoSearch/#dbcmd.geoSearch)[`getLastError`](https://docs.mongodb.com/manual/reference/command/getLastError/#dbcmd.getLastError)[`getMore`](https://docs.mongodb.com/manual/reference/command/getMore/#dbcmd.getMore)[`killCursors`](https://docs.mongodb.com/manual/reference/command/killCursors/#dbcmd.killCursors), provided that the cursor is associated with a currently authenticated user.[`listCollections`](https://docs.mongodb.com/manual/reference/command/listCollections/#dbcmd.listCollections)[`listIndexes`](https://docs.mongodb.com/manual/reference/command/listIndexes/#dbcmd.listIndexes)[`mapReduce`](https://docs.mongodb.com/manual/reference/command/mapReduce/#dbcmd.mapReduce) with the `{out: inline}` option.[`resetError`](https://docs.mongodb.com/manual/reference/command/resetError/#dbcmd.resetError)Required for the query portion of the [`mapReduce`](https://docs.mongodb.com/manual/reference/command/mapReduce/#dbcmd.mapReduce) command and [`db.collection.mapReduce`](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#db.collection.mapReduce) helper method when [outputting to a collection](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#mapreduce-out-mtd).Required for the query portion of the [`findAndModify`](https://docs.mongodb.com/manual/reference/command/findAndModify/#dbcmd.findAndModify) command and [`db.collection.findAndModify`](https://docs.mongodb.com/manual/reference/method/db.collection.findAndModify/#db.collection.findAndModify) helper method.Required on the *source* collection for the [`cloneCollectionAsCapped`](https://docs.mongodb.com/manual/reference/command/cloneCollectionAsCapped/#dbcmd.cloneCollectionAsCapped) and [`renameCollection`](https://docs.mongodb.com/manual/reference/command/renameCollection/#dbcmd.renameCollection) commands and the [`db.collection.renameCollection()`](https://docs.mongodb.com/manual/reference/method/db.collection.renameCollection/#db.collection.renameCollection) helper method.For MongoDB 4.0.6+:If the user does not have the [`listDatabases`](https://docs.mongodb.com/manual/reference/privilege-actions/#listDatabases) privilege action, users can run the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command to return a list of databases for which the user has privileges (including databases for which the user has privileges on specific collections) if the command is run with `authorizedDatabases` option unspecified or set to `true`.For MongoDB 4.0.5:If the user does not have the [`listDatabases`](https://docs.mongodb.com/manual/reference/privilege-actions/#listDatabases) privilege action, users can run the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command to return a list of databases for which the user has the [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) action privilege if the command is run with `authorizedDatabases` option unspecified or set to `true`.For MongoDB 4.0.0-4.0.4:If the user does not have the [`listDatabases`](https://docs.mongodb.com/manual/reference/privilege-actions/#listDatabases) privilege action, users can run the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command to return a list of databases for which the user has the [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) action privilege.Apply this action to database or collection resources.

- `insert`

  User can perform the following commands and their equivalent methods:[`insert`](https://docs.mongodb.com/manual/reference/command/insert/#dbcmd.insert)[`create`](https://docs.mongodb.com/manual/reference/command/create/#dbcmd.create)Required for the output portion of the [`mapReduce`](https://docs.mongodb.com/manual/reference/command/mapReduce/#dbcmd.mapReduce) command and [`db.collection.mapReduce()`](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#db.collection.mapReduce) helper method when [outputting to a collection](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#mapreduce-out-mtd).Required for the [`aggregate`](https://docs.mongodb.com/manual/reference/command/aggregate/#dbcmd.aggregate) command and [`db.collection.aggregate()`](https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#db.collection.aggregate) helper method when using the [`$out`](https://docs.mongodb.com/manual/reference/operator/aggregation/out/#pipe._S_out) pipeline operator.Required for the [`update`](https://docs.mongodb.com/manual/reference/command/update/#dbcmd.update) and [`findAndModify`](https://docs.mongodb.com/manual/reference/command/findAndModify/#dbcmd.findAndModify) commands and equivalent helper methods when used with the `upsert` option.Required on the *destination* collection for the following commands and their helper methods:[`cloneCollection`](https://docs.mongodb.com/manual/reference/command/cloneCollection/#dbcmd.cloneCollection)[`cloneCollectionAsCapped`](https://docs.mongodb.com/manual/reference/command/cloneCollectionAsCapped/#dbcmd.cloneCollectionAsCapped)[`renameCollection`](https://docs.mongodb.com/manual/reference/command/renameCollection/#dbcmd.renameCollection)Apply this action to database or collection resources.

- `remove`

  User can perform the [`delete`](https://docs.mongodb.com/manual/reference/command/delete/#dbcmd.delete) command and equivalent helper method.Required for the write portion of the [`findAndModify`](https://docs.mongodb.com/manual/reference/command/findAndModify/#dbcmd.findAndModify) command and [`db.collection.findAndModify()`](https://docs.mongodb.com/manual/reference/method/db.collection.findAndModify/#db.collection.findAndModify) method.Required for the [`mapReduce`](https://docs.mongodb.com/manual/reference/command/mapReduce/#dbcmd.mapReduce) command and [`db.collection.mapReduce()`](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#db.collection.mapReduce) helper method when you specify the `replace` action when [outputting to a collection](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#mapreduce-out-mtd).Required for the [`aggregate`](https://docs.mongodb.com/manual/reference/command/aggregate/#dbcmd.aggregate) command and [`db.collection.aggregate()`](https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#db.collection.aggregate) helper method when using the [`$out`](https://docs.mongodb.com/manual/reference/operator/aggregation/out/#pipe._S_out) pipeline operator.Apply this action to database or collection resources.

- `update`

  User can perform the [`update`](https://docs.mongodb.com/manual/reference/command/update/#dbcmd.update) command and equivalent helper methods.Required for the [`mapReduce`](https://docs.mongodb.com/manual/reference/command/mapReduce/#dbcmd.mapReduce) command and [`db.collection.mapReduce()`](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#db.collection.mapReduce) helper method when [outputting to a collection](https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/#mapreduce-out-mtd) without specifying the `replace` action.Required for the [`findAndModify`](https://docs.mongodb.com/manual/reference/command/findAndModify/#dbcmd.findAndModify) command and [`db.collection.findAndModify()`](https://docs.mongodb.com/manual/reference/method/db.collection.findAndModify/#db.collection.findAndModify) helper method.Apply this action to database or collection resources.

- `bypassDocumentValidation`

  *New in version 3.2.*Users can bypass [document validation](https://docs.mongodb.com/manual/core/schema-validation/) on commands and methods that support the `bypassDocumentValidation` option. The following commands and their equivalent methods support bypassing document validation:[`aggregate`](https://docs.mongodb.com/manual/reference/command/aggregate/#dbcmd.aggregate)[`applyOps`](https://docs.mongodb.com/manual/reference/command/applyOps/#dbcmd.applyOps)[`cloneCollection`](https://docs.mongodb.com/manual/reference/command/cloneCollection/#dbcmd.cloneCollection) on the *destination* collection[`findAndModify`](https://docs.mongodb.com/manual/reference/command/findAndModify/#dbcmd.findAndModify)[`insert`](https://docs.mongodb.com/manual/reference/command/insert/#dbcmd.insert)[`mapReduce`](https://docs.mongodb.com/manual/reference/command/mapReduce/#dbcmd.mapReduce)[`update`](https://docs.mongodb.com/manual/reference/command/update/#dbcmd.update)Apply this action to database or collection resources.

- `useUUID`

  *New in version 3.6.*User can execute the following commands using a UUID as if it were a namespace:[`find`](https://docs.mongodb.com/manual/reference/command/find/#dbcmd.find)[`listIndexes`](https://docs.mongodb.com/manual/reference/command/listIndexes/#dbcmd.listIndexes)For example, this privilege authorizes a user to run the following command which executes a [`find`](https://docs.mongodb.com/manual/reference/command/find/#dbcmd.find) command on a collection with the given UUID. In order to be successful, this operation also requires that the user is authorized to execute the `find` command on the collection namespace corresponding to the given UUID.copycopied`db.runCommand({find: UUID("123e4567-e89b-12d3-a456-426655440000")}) `For more information on collection UUIDs, see [Collections](https://docs.mongodb.com/manual/core/databases-and-collections/#collections).Apply this action to the `cluster` resource.

## Database Management Actions

- `changeCustomData`

  User can change the custom information of any user in the given database. Apply this action to database resources.

- `changeOwnCustomData`

  Users can change their own custom information. Apply this action to database resources. See also [Change Your Password and Custom Data](https://docs.mongodb.com/manual/tutorial/change-own-password-and-custom-data/).

- `changeOwnPassword`

  Users can change their own passwords. Apply this action to database resources. See also [Change Your Password and Custom Data](https://docs.mongodb.com/manual/tutorial/change-own-password-and-custom-data/).

- `changePassword`

  User can change the password of any user in the given database. Apply this action to database resources.

- `createCollection`

  User can perform the [`db.createCollection()`](https://docs.mongodb.com/manual/reference/method/db.createCollection/#db.createCollection) method. Apply this action to database or collection resources.

- `createIndex`

  Provides access to the [`db.collection.createIndex()`](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#db.collection.createIndex) method and the [`createIndexes`](https://docs.mongodb.com/manual/reference/command/createIndexes/#dbcmd.createIndexes) command. Apply this action to database or collection resources.

- `createRole`

  User can create new roles in the given database. Apply this action to database resources.

- `createUser`

  User can create new users in the given database. Apply this action to database resources.

- `dropCollection`

  User can perform the [`db.collection.drop()`](https://docs.mongodb.com/manual/reference/method/db.collection.drop/#db.collection.drop) method. Apply this action to database or collection resources.

- `dropRole`

  User can delete any role from the given database. Apply this action to database resources.

- `dropUser`

  User can remove any user from the given database. Apply this action to database resources.

- `enableProfiler`

  User can perform the [`db.setProfilingLevel()`](https://docs.mongodb.com/manual/reference/method/db.setProfilingLevel/#db.setProfilingLevel) method. Apply this action to database resources.

- `grantRole`

  User can grant any role in the database to any user from any database in the system. Apply this action to database resources.

- `killCursors`

  Starting in MongoDB 4.2, users can always kill their own cursors, regardless of whether the users have the privilege to [`killCursors`](https://docs.mongodb.com/manual/reference/privilege-actions/#killCursors). As such, the [`killCursors`](https://docs.mongodb.com/manual/reference/privilege-actions/#killCursors) privilege has no effect in MongoDB 4.2+.In MongoDB 3.6.3 through MongoDB 4.0.x, users require [`killCursors`](https://docs.mongodb.com/manual/reference/privilege-actions/#killCursors) privilege to kill their own curors when access control is enabled. Cursors are associated with the users at the time of cursor creation. Apply this action to collection resources.

- `killAnyCursor`

  *New in version 3.6.3.*User can kill **any** cursor, even cursors created by other users. Apply this action to collection resources.

- `revokeRole`

  User can remove any role from any user from any database in the system. Apply this action to database resources.

- `setAuthenticationRestriction`

  *New in version 3.6.*User can specify the [authenticationRestrictions](https://docs.mongodb.com/manual/reference/command/createUser/#create-user-auth-restrictions) field in the `user` document when running the following commands:[createUser](https://docs.mongodb.com/manual/reference/command/createUser/)[updateUser](https://docs.mongodb.com/manual/reference/command/updateUser/)User can specify the `authenticationRestrictions` field in the `role` document when running the following commands:[createRole](https://docs.mongodb.com/manual/reference/command/createRole/)[updateRole](https://docs.mongodb.com/manual/reference/command/updateRole/)NOTEThe following built-in roles grant this privilege:The [`userAdmin`](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdmin) role provides this privilege on the database that the role is assigned.The [`userAdminAnyDatabase`](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdminAnyDatabase) role provides this privilege on all databases.Transitively, the [`restore`](https://docs.mongodb.com/manual/reference/built-in-roles/#restore) and [`root`](https://docs.mongodb.com/manual/reference/built-in-roles/#root) roles also provide this privilege.Apply this action to database resources.

- `unlock`

  User can perform the [`db.fsyncUnlock()`](https://docs.mongodb.com/manual/reference/method/db.fsyncUnlock/#db.fsyncUnlock) method. Apply this action to the `cluster` resource.

- `viewRole`

  User can view information about any role in the given database. Apply this action to database resources.

- `viewUser`

  User can view the information of any user in the given database. Apply this action to database resources.

## Deployment Management Actions

- `authSchemaUpgrade`

  User can perform the `authSchemaUpgrade` command. Apply this action to the `cluster` resource.

- `cleanupOrphaned`

  User can perform the [`cleanupOrphaned`](https://docs.mongodb.com/manual/reference/command/cleanupOrphaned/#dbcmd.cleanupOrphaned) command. Apply this action to the `cluster` resource.

- `cpuProfiler`

  User can enable and use the CPU profiler. Apply this action to the `cluster` resource.

- `inprog`

  User can use the [`db.currentOp()`](https://docs.mongodb.com/manual/reference/method/db.currentOp/#db.currentOp) method to return information on pending and active operations. Apply this action to the `cluster` resource.*Changed in version 3.2.9:* Even without the [`inprog`](https://docs.mongodb.com/manual/reference/privilege-actions/#inprog) privilege, on [`mongod`](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) instances, users can view their own operations by running `db.currentOp( { "$ownOps": true } )`.

- `invalidateUserCache`

  Provides access to the [`invalidateUserCache`](https://docs.mongodb.com/manual/reference/command/invalidateUserCache/#dbcmd.invalidateUserCache) command. Apply this action to the `cluster` resource.

- `killop`

  User can perform the [`db.killOp()`](https://docs.mongodb.com/manual/reference/method/db.killOp/#db.killOp) method. Apply this action to the `cluster` resource.*Changed in version 3.2.9:* Even without the [`killop`](https://docs.mongodb.com/manual/reference/privilege-actions/#killop) privilege, on [`mongod`](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) instances, users can kill their own operations.

- `planCacheRead`

  User can run the following operations:[`$planCacheStats`](https://docs.mongodb.com/manual/reference/operator/aggregation/planCacheStats/#pipe._S_planCacheStats) aggregation stage.[`planCacheListPlans`](https://docs.mongodb.com/manual/reference/command/planCacheListPlans/#dbcmd.planCacheListPlans) command and [`PlanCache.getPlansByQuery()`](https://docs.mongodb.com/manual/reference/method/PlanCache.getPlansByQuery/#PlanCache.getPlansByQuery) method.[`planCacheListQueryShapes`](https://docs.mongodb.com/manual/reference/command/planCacheListQueryShapes/#dbcmd.planCacheListQueryShapes) command and the [`PlanCache.listQueryShapes()`](https://docs.mongodb.com/manual/reference/method/PlanCache.listQueryShapes/#PlanCache.listQueryShapes) method.Apply this action to database or collection resources.

- `planCacheWrite`

  User can perform the [`planCacheClear`](https://docs.mongodb.com/manual/reference/command/planCacheClear/#dbcmd.planCacheClear) command and the [`PlanCache.clear()`](https://docs.mongodb.com/manual/reference/method/PlanCache.clear/#PlanCache.clear) and [`PlanCache.clearPlansByQuery()`](https://docs.mongodb.com/manual/reference/method/PlanCache.clearPlansByQuery/#PlanCache.clearPlansByQuery) methods. Apply this action to database or collection resources.

- `storageDetails`

  User can perform the `storageDetails` command. Apply this action to database or collection resources.

## Change Stream Actions

- `changeStream`

  User with [`changeStream`](https://docs.mongodb.com/manual/reference/privilege-actions/#changeStream) and [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) on the specific collection, all non-`system` collections in a specifc database, or all non-`system` collections across all databases can open [change stream cursor](https://docs.mongodb.com/manual/changeStreams/) for that resource.

## Replication Actions

- `appendOplogNote`

  User can append notes to the oplog. Apply this action to the `cluster` resource.

- `replSetConfigure`

  User can configure a replica set. Apply this action to the `cluster` resource.

- `replSetGetConfig`

  User can view a replica set’s configuration. Provides access to the [`replSetGetConfig`](https://docs.mongodb.com/manual/reference/command/replSetGetConfig/#dbcmd.replSetGetConfig) command and [`rs.conf()`](https://docs.mongodb.com/manual/reference/method/rs.conf/#rs.conf) helper method.Apply this action to the `cluster` resource.

- `replSetGetStatus`

  User can perform the [`replSetGetStatus`](https://docs.mongodb.com/manual/reference/command/replSetGetStatus/#dbcmd.replSetGetStatus) command. Apply this action to the `cluster` resource.

- `replSetHeartbeat`

  User can perform the `replSetHeartbeat` command. Apply this action to the `cluster` resource.

- `replSetStateChange`

  User can change the state of a replica set through the [`replSetFreeze`](https://docs.mongodb.com/manual/reference/command/replSetFreeze/#dbcmd.replSetFreeze), [`replSetMaintenance`](https://docs.mongodb.com/manual/reference/command/replSetMaintenance/#dbcmd.replSetMaintenance), [`replSetStepDown`](https://docs.mongodb.com/manual/reference/command/replSetStepDown/#dbcmd.replSetStepDown), and [`replSetSyncFrom`](https://docs.mongodb.com/manual/reference/command/replSetSyncFrom/#dbcmd.replSetSyncFrom) commands. Apply this action to the `cluster` resource.

- `resync`

  User can perform the `resync` command. Apply this action to the `cluster` resource.

## Sharding Actions

- `addShard`

  User can perform the [`addShard`](https://docs.mongodb.com/manual/reference/command/addShard/#dbcmd.addShard) command. Apply this action to the `cluster` resource.

- `clearJumboFlag`

  *Available starting in 4.2.3 and 4.0.15*Required to clear a chunk’s jumbo flag using the [`clearJumboFlag`](https://docs.mongodb.com/manual/reference/command/clearJumboFlag/#dbcmd.clearJumboFlag) command. Apply this action to database or collection resources.Included in the [`clusterManager`](https://docs.mongodb.com/manual/reference/built-in-roles/#clusterManager) built-in role.

- `enableSharding`

  APPLICABLE RESOURCESThe action can apply to either:[Database](https://docs.mongodb.com/manual/reference/resource-document/#resource-specific-db) or [collection](https://docs.mongodb.com/manual/reference/resource-document/#resource-specific-db-collection) resource to enable sharding for a database or shard a collection.[Cluster](https://docs.mongodb.com/manual/reference/resource-document/#resource-specific-collection) resource to perform various shard zone operations (Starting in version 4.2.2, 4.0.14, 3.6.16).ResourcesDescription[Database](https://docs.mongodb.com/manual/reference/resource-document/#resource-specific-db) or[Collection](https://docs.mongodb.com/manual/reference/resource-document/#resource-specific-db-collection)Grants users privileges to perform the following operations:Enable sharding on a database using the [`enableSharding`](https://docs.mongodb.com/manual/reference/command/enableSharding/#dbcmd.enableSharding) command, andShard a collection using the [`shardCollection`](https://docs.mongodb.com/manual/reference/command/shardCollection/#dbcmd.shardCollection) command.[Cluster](https://docs.mongodb.com/manual/reference/resource-document/#resource-specific-collection)*Starting in version 4.2.2, 4.0.14, 3.6.16*Grants users privileges to perform the following shard zone operations:[`addShardToZone`](https://docs.mongodb.com/manual/reference/command/addShardToZone/#dbcmd.addShardToZone)[`updateZoneKeyRange`](https://docs.mongodb.com/manual/reference/command/updateZoneKeyRange/#dbcmd.updateZoneKeyRange)[`removeShardFromZone`](https://docs.mongodb.com/manual/reference/command/removeShardFromZone/#dbcmd.removeShardFromZone)You can also perform these shard zone operations if you have [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find)/[`update`](https://docs.mongodb.com/manual/reference/privilege-actions/#update) actions on the appropriate collections in the `config` database. Refer to the specific operations for details.

- `flushRouterConfig`

  User can perform the [`flushRouterConfig`](https://docs.mongodb.com/manual/reference/command/flushRouterConfig/#dbcmd.flushRouterConfig) command. Apply this action to the `cluster` resource.

- `getShardMap`

  User can perform the [`getShardMap`](https://docs.mongodb.com/manual/reference/command/getShardMap/#dbcmd.getShardMap) command. Apply this action to the `cluster` resource.

- `getShardVersion`

  User can perform the [`getShardVersion`](https://docs.mongodb.com/manual/reference/command/getShardVersion/#dbcmd.getShardVersion) command. Apply this action to database resources.

- `listShards`

  User can perform the [`listShards`](https://docs.mongodb.com/manual/reference/command/listShards/#dbcmd.listShards) command. Apply this action to the `cluster` resource.

- `moveChunk`

  User can perform the [`moveChunk`](https://docs.mongodb.com/manual/reference/command/moveChunk/#dbcmd.moveChunk) command. In addition, user can perform the [`movePrimary`](https://docs.mongodb.com/manual/reference/command/movePrimary/#dbcmd.movePrimary) command provided that the privilege is applied to an appropriate database resource. Apply this action to database or collection resources.

- `removeShard`

  User can perform the [`removeShard`](https://docs.mongodb.com/manual/reference/command/removeShard/#dbcmd.removeShard) command. Apply this action to the `cluster` resource.

- `shardingState`

  User can perform the [`shardingState`](https://docs.mongodb.com/manual/reference/command/shardingState/#dbcmd.shardingState) command. Apply this action to the `cluster` resource.

- `splitChunk`

  User can perform the [`splitChunk`](https://docs.mongodb.com/manual/reference/command/splitChunk/#dbcmd.splitChunk) command and the [`mergeChunks`](https://docs.mongodb.com/manual/reference/command/mergeChunks/#dbcmd.mergeChunks) command. Apply this action to database or collection resources.

- `splitVector`

  User can perform the [`splitVector`](https://docs.mongodb.com/manual/reference/command/splitVector/#dbcmd.splitVector) command. Apply this action to database or collection resources.

## Server Administration Actions

- `applicationMessage`

  User can perform the [`logApplicationMessage`](https://docs.mongodb.com/manual/reference/command/logApplicationMessage/#dbcmd.logApplicationMessage) command. Apply this action to the `cluster` resource.

- `closeAllDatabases`

  User can perform the `closeAllDatabases` command. Apply this action to the `cluster` resource.

- `collMod`

  User can perform the [`collMod`](https://docs.mongodb.com/manual/reference/command/collMod/#dbcmd.collMod) command. Apply this action to database or collection resources.

- `compact`

  User can perform the [`compact`](https://docs.mongodb.com/manual/reference/command/compact/#dbcmd.compact) command. Apply this action to database or collection resources.

- `connPoolSync`

  User can perform the [`connPoolSync`](https://docs.mongodb.com/manual/reference/command/connPoolSync/#dbcmd.connPoolSync) command. Apply this action to the `cluster` resource.

- `convertToCapped`

  User can perform the [`convertToCapped`](https://docs.mongodb.com/manual/reference/command/convertToCapped/#dbcmd.convertToCapped) command. Apply this action to database or collection resources.

- `dropConnections`

  User can perform the [`dropConnections`](https://docs.mongodb.com/manual/reference/command/dropConnections/#dbcmd.dropConnections) command. Apply this action to the `cluster` resource.

- `dropDatabase`

  User can perform the [`dropDatabase`](https://docs.mongodb.com/manual/reference/command/dropDatabase/#dbcmd.dropDatabase) command. Apply this action to database resources.

- `dropIndex`

  User can perform the [`dropIndexes`](https://docs.mongodb.com/manual/reference/command/dropIndexes/#dbcmd.dropIndexes) command. Apply this action to database or collection resources.

- `forceUUID`

  *New in version 3.6.*User can create a collection with a user-defined [collection UUID](https://docs.mongodb.com/manual/core/databases-and-collections/#collections-uuids) using the [`applyOps`](https://docs.mongodb.com/manual/reference/command/applyOps/#dbcmd.applyOps) command.Apply this action to the `cluster` resource.

- `fsync`

  User can perform the [`fsync`](https://docs.mongodb.com/manual/reference/command/fsync/#dbcmd.fsync) command. Apply this action to the `cluster` resource.

- `getParameter`

  User can perform the [`getParameter`](https://docs.mongodb.com/manual/reference/command/getParameter/#dbcmd.getParameter) command. Apply this action to the `cluster` resource.

- `hostInfo`

  Provides information about the server the MongoDB instance runs on. Apply this action to the `cluster` resource.

- `logRotate`

  User can perform the [`logRotate`](https://docs.mongodb.com/manual/reference/command/logRotate/#dbcmd.logRotate) command. Apply this action to the `cluster` resource.

- `reIndex`

  User can perform the [`reIndex`](https://docs.mongodb.com/manual/reference/command/reIndex/#dbcmd.reIndex) command. Apply this action to database or collection resources.

- `renameCollectionSameDB`

  Allows the user to rename collections on the current database using the [`renameCollection`](https://docs.mongodb.com/manual/reference/command/renameCollection/#dbcmd.renameCollection) command. Apply this action to database resources.Additionally, the user must either *have* [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) on the source collection or *not have* [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) on the destination collection.If a collection with the new name already exists, the user must also have the [`dropCollection`](https://docs.mongodb.com/manual/reference/privilege-actions/#dropCollection) action on the destination collection.

- `setParameter`

  User can perform the [`setParameter`](https://docs.mongodb.com/manual/reference/command/setParameter/#dbcmd.setParameter) command. Apply this action to the `cluster` resource.

- `shutdown`

  User can perform the [`shutdown`](https://docs.mongodb.com/manual/reference/command/shutdown/#dbcmd.shutdown) command. Apply this action to the `cluster` resource.

- `touch`

  User can perform the `touch` command. Apply this action to the `cluster` resource.

## Session Actions

- `impersonate`

  *New in version 3.6.*User can perform the [`killAllSessionsByPattern`](https://docs.mongodb.com/manual/reference/command/killAllSessionsByPattern/#dbcmd.killAllSessionsByPattern) command with `users` and `roles` pattern. Apply this action to the `cluster` resource.To run [`killAllSessionsByPattern`](https://docs.mongodb.com/manual/reference/command/killAllSessionsByPattern/#dbcmd.killAllSessionsByPattern) command, users must also have [`killAnySession`](https://docs.mongodb.com/manual/reference/privilege-actions/#killAnySession) privileges on the cluster resource.

- `listSessions`

  *New in version 3.6.*User can perform the [`$listSessions`](https://docs.mongodb.com/manual/reference/operator/aggregation/listSessions/#pipe._S_listSessions) operation or [`$listLocalSessions`](https://docs.mongodb.com/manual/reference/operator/aggregation/listLocalSessions/#pipe._S_listLocalSessions) operation for all users or specified user(s). Apply this action to the `cluster` resource.

- `killAnySession`

  *New in version 3.6.*User can perform the [`killAllSessions`](https://docs.mongodb.com/manual/reference/command/killAllSessions/#dbcmd.killAllSessions) and the [`killAllSessionsByPattern`](https://docs.mongodb.com/manual/reference/command/killAllSessionsByPattern/#dbcmd.killAllSessionsByPattern) command. Apply this action to the `cluster` resource.SEE ALSO[`impersonate`](https://docs.mongodb.com/manual/reference/privilege-actions/#impersonate)

## Free Monitoring Actions

- `checkFreeMonitoringStatus`

  User with this action on the `cluster` resource can check the status of [Free Monitoring](https://docs.mongodb.com/manual/administration/free-monitoring/).*New in version 4.0.*

- `setFreeMonitoring`

  User with this action on the `cluster` resource can enable or disable [Free Monitoring](https://docs.mongodb.com/manual/administration/free-monitoring/).*New in version 4.0.*

## Diagnostic Actions

- `collStats`

  User can perform the [`collStats`](https://docs.mongodb.com/manual/reference/command/collStats/#dbcmd.collStats) command. Apply this action to database or collection resources.

- `connPoolStats`

  User can perform the [`connPoolStats`](https://docs.mongodb.com/manual/reference/command/connPoolStats/#dbcmd.connPoolStats) and [`shardConnPoolStats`](https://docs.mongodb.com/manual/reference/command/shardConnPoolStats/#dbcmd.shardConnPoolStats) commands. Apply this action to the `cluster` resource.

- `cursorInfo`

  User can perform the [`cursorInfo`](https://docs.mongodb.com/manual/reference/command/cursorInfo/#dbcmd.cursorInfo) command. Apply this action to the `cluster` resource.

- `dbHash`

  User can perform the [`dbHash`](https://docs.mongodb.com/manual/reference/command/dbHash/#dbcmd.dbHash) command. Apply this action to database or collection resources.

- `dbStats`

  User can perform the [`dbStats`](https://docs.mongodb.com/manual/reference/command/dbStats/#dbcmd.dbStats) command. Apply this action to database resources.

- `getCmdLineOpts`

  User can perform the [`getCmdLineOpts`](https://docs.mongodb.com/manual/reference/command/getCmdLineOpts/#dbcmd.getCmdLineOpts) command. Apply this action to the `cluster` resource.

- `getLog`

  User can perform the [`getLog`](https://docs.mongodb.com/manual/reference/command/getLog/#dbcmd.getLog) command. Apply this action to the `cluster` resource.

- `indexStats`

  User can perform the `indexStats` command. Apply this action to database or collection resources.*Changed in version 3.0:* MongoDB 3.0 removes the `indexStats` command.

- `listDatabases`

  User can perform the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command. Apply this action to the `cluster` resource.For MongoDB 4.0.6+:If the user does not have the [`listDatabases`](https://docs.mongodb.com/manual/reference/privilege-actions/#listDatabases) privilege action, users can run the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command to return a list of databases for which the user has privileges (including databases for which the user has privileges on specific collections) if the command is run with `authorizedDatabases` option unspecified or set to `true`.For MongoDB 4.0.5:If the user does not have the [`listDatabases`](https://docs.mongodb.com/manual/reference/privilege-actions/#listDatabases) privilege action, users can run the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command to return a list of databases for which the user has the [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) action privilege if the command is run with `authorizedDatabases` option unspecified or set to `true`.For MongoDB 4.0.0-4.0.4:If the user does not have the [`listDatabases`](https://docs.mongodb.com/manual/reference/privilege-actions/#listDatabases) privilege action, users can run the [`listDatabases`](https://docs.mongodb.com/manual/reference/command/listDatabases/#dbcmd.listDatabases) command to return a list of databases for which the user has the [`find`](https://docs.mongodb.com/manual/reference/privilege-actions/#find) action privilege.

- `listCollections`

  User can perform the [`listCollections`](https://docs.mongodb.com/manual/reference/command/listCollections/#dbcmd.listCollections) command. Apply this action to database resources.NOTEStarting in version 4.0, user without the required privilege can run the [`listCollections`](https://docs.mongodb.com/manual/reference/command/listCollections/#dbcmd.listCollections) command with **both** `authorizedCollections` and `nameOnly` options set to `true`. In this case, the command returns just the name and type of the collection(s) to which the user has privileges.

- `listIndexes`

  User can perform the [`listIndexes`](https://docs.mongodb.com/manual/reference/command/listIndexes/#dbcmd.listIndexes) command. Apply this action to database or collection resources.

- `netstat`

  User can perform the [`netstat`](https://docs.mongodb.com/manual/reference/command/netstat/#dbcmd.netstat) command. Apply this action to the `cluster` resource.

- `serverStatus`

  User can perform the [`serverStatus`](https://docs.mongodb.com/manual/reference/command/serverStatus/#dbcmd.serverStatus) command. Apply this action to the `cluster` resource.

- `validate`

  User can perform the [`validate`](https://docs.mongodb.com/manual/reference/command/validate/#dbcmd.validate) command. Apply this action to database or collection resources.

- `top`

  User can perform the [`top`](https://docs.mongodb.com/manual/reference/command/top/#dbcmd.top) command. Apply this action to the `cluster` resource.

## Internal Actions

- `anyAction`

  Allows any action on a resource. **Do not** assign this action unless it is absolutely necessary.

- `internal`

  Allows internal actions. **Do not** assign this action unless it is absolutely necessary.