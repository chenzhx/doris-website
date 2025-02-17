---
{
    "title": "SET REPLICA STATUS",
    "language": "en"
}
---

<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->



## Description

This statement is used to set the state of the specified replica.

This command is currently only used to manually set the status of certain replicas to BAD, DROP or OK, allowing the system to automatically repair these replicas

grammar:

```sql
ADMIN SET REPLICA STATUS
        PROPERTIES ("key" = "value", ...);
```

 The following properties are currently supported:

1. "tablet_id": Required. Specify a Tablet Id.
2. "backend_id": Required. Specify Backend Id.
3. "status": Required. Specifies the state. Currently only "bad", "drop" or "ok" are supported

If the specified replica does not exist, or the status is already bad, it will be ignored.

> Note:
>
> A replica set to Bad, it will not be able to read or write. In addition, sometimes the setting may not working, when be report tablet ok, fe will auto change its status to ok. This operation may delete the replica immediately, so please operate with caution.
>
> A replica set to Drop, it can still be read and written. A healthy replica will be added to other machines first, and then this replica will be deleted. Compared with setting Bad, setting Drop is safer.

## Examples

 1. Set the replica status of tablet 10003 on BE 10001 to bad.

       ```sql
    ADMIN SET REPLICA STATUS PROPERTIES("tablet_id" = "10003", "backend_id" = "10001", "status" = "bad");
       ```

 2. Set the replica status of tablet 10003 on BE 10001 to drop.

       ```sql
    ADMIN SET REPLICA STATUS PROPERTIES("tablet_id" = "10003", "backend_id" = "10001", "status" = "drop");
       ```


 3. Set the replica status of tablet 10003 on BE 10001 to ok.

   ```sql
   ADMIN SET REPLICA STATUS PROPERTIES("tablet_id" = "10003", "backend_id" = "10001", "status" = "ok");
   ```

## Keywords

    ADMIN, SET, REPLICA, STATUS

## Best Practice

