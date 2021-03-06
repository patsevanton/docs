---
editable: false
---

# SecurityGroupService



| Call | Description |
| --- | --- |
| [Get](#Get) |  |
| [List](#List) |  |
| [Create](#Create) |  |
| [Update](#Update) |  |
| [UpdateRules](#UpdateRules) |  |
| [UpdateRule](#UpdateRule) | update rule description or labels |
| [Delete](#Delete) |  |
| [Move](#Move) |  |
| [ListOperations](#ListOperations) |  |

## Calls SecurityGroupService {#calls}

## Get {#Get}



**rpc Get ([GetSecurityGroupRequest](#GetSecurityGroupRequest)) returns ([SecurityGroup](../security_group.proto#SecurityGroup))**

### GetSecurityGroupRequest {#GetSecurityGroupRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false


### SecurityGroup {#SecurityGroup}

Field | Description
--- | ---
id | **string**<br> 
folder_id | **string**<br> 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br> 
status | enum **Status**<br> <ul><li>`UPDATING`: updating is a long operation because we must update all instances in SG</li><ul/>
rules[] | **[SecurityGroupRule](../security_group.proto#SecurityGroupRule)**<br> 
default_for_network | **bool**<br> 


### SecurityGroupRule {#SecurityGroupRule}

Field | Description
--- | ---
id | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
direction | enum **Direction**<br>Required.  false<ul><ul/>
ports | **[PortRange](../security_group.proto#PortRange)**<br> 
protocol_name | **string**<br>null value means any protocol values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml 
protocol_number | **int64**<br> 
target | **oneof:** `cidr_blocks`, `security_group_id` or `predefined_target`<br>
&nbsp;&nbsp;cidr_blocks | **[CidrBlocks](../security_group.proto#CidrBlocks)**<br> 
&nbsp;&nbsp;security_group_id | **string**<br> 
&nbsp;&nbsp;predefined_target | **string**<br> 


### PortRange {#PortRange}

Field | Description
--- | ---
from_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.
to_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.


### CidrBlocks {#CidrBlocks}

Field | Description
--- | ---
v4_cidr_blocks[] | **string**<br> 
v6_cidr_blocks[] | **string**<br> 


## List {#List}



**rpc List ([ListSecurityGroupsRequest](#ListSecurityGroupsRequest)) returns ([ListSecurityGroupsResponse](#ListSecurityGroupsResponse))**

### ListSecurityGroupsRequest {#ListSecurityGroupsRequest}

Field | Description
--- | ---
folder_id | **string**<br>Required.  false
page_size | **int64**<br> 
page_token | **string**<br> 
filter | **string**<br> 


### ListSecurityGroupsResponse {#ListSecurityGroupsResponse}

Field | Description
--- | ---
security_groups[] | **[SecurityGroup](../security_group.proto#SecurityGroup1)**<br> 
next_page_token | **string**<br> 


### SecurityGroup {#SecurityGroup}

Field | Description
--- | ---
id | **string**<br> 
folder_id | **string**<br> 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br> 
status | enum **Status**<br> <ul><li>`UPDATING`: updating is a long operation because we must update all instances in SG</li><ul/>
rules[] | **[SecurityGroupRule](../security_group.proto#SecurityGroupRule1)**<br> 
default_for_network | **bool**<br> 


### SecurityGroupRule {#SecurityGroupRule}

Field | Description
--- | ---
id | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
direction | enum **Direction**<br>Required.  false<ul><ul/>
ports | **[PortRange](../security_group.proto#PortRange1)**<br> 
protocol_name | **string**<br>null value means any protocol values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml 
protocol_number | **int64**<br> 
target | **oneof:** `cidr_blocks`, `security_group_id` or `predefined_target`<br>
&nbsp;&nbsp;cidr_blocks | **[CidrBlocks](../security_group.proto#CidrBlocks1)**<br> 
&nbsp;&nbsp;security_group_id | **string**<br> 
&nbsp;&nbsp;predefined_target | **string**<br> 


### PortRange {#PortRange}

Field | Description
--- | ---
from_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.
to_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.


### CidrBlocks {#CidrBlocks}

Field | Description
--- | ---
v4_cidr_blocks[] | **string**<br> 
v6_cidr_blocks[] | **string**<br> 


## Create {#Create}



**rpc Create ([CreateSecurityGroupRequest](#CreateSecurityGroupRequest)) returns ([operation.Operation](#Operation))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[CreateSecurityGroupMetadata](#CreateSecurityGroupMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[SecurityGroup](../security_group.proto#SecurityGroup2)<br>

### CreateSecurityGroupRequest {#CreateSecurityGroupRequest}

Field | Description
--- | ---
folder_id | **string**<br>Required.  false
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br>Required.  false
rule_specs[] | **[SecurityGroupRuleSpec](#SecurityGroupRuleSpec)**<br> 


### SecurityGroupRuleSpec {#SecurityGroupRuleSpec}

Field | Description
--- | ---
description | **string**<br> 
labels | **map<string,string>**<br> 
direction | **[SecurityGroupRule.Direction](../security_group.proto#SecurityGroupRule2)**<br>Required.  false
ports | **[PortRange](../security_group.proto#PortRange2)**<br> 
protocol | **oneof:** `protocol_name` or `protocol_number`<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol
&nbsp;&nbsp;protocol_name | **string**<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol 
&nbsp;&nbsp;protocol_number | **int64**<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol 
target | **oneof:** `cidr_blocks`, `security_group_id` or `predefined_target`<br>
&nbsp;&nbsp;cidr_blocks | **[CidrBlocks](../security_group.proto#CidrBlocks2)**<br> 
&nbsp;&nbsp;security_group_id | **string**<br> 
&nbsp;&nbsp;predefined_target | **string**<br> 


### PortRange {#PortRange}

Field | Description
--- | ---
from_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.
to_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.


### CidrBlocks {#CidrBlocks}

Field | Description
--- | ---
v4_cidr_blocks[] | **string**<br> 
v6_cidr_blocks[] | **string**<br> 


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[CreateSecurityGroupMetadata](#CreateSecurityGroupMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[SecurityGroup](../security_group.proto#SecurityGroup2)>**<br>if operation finished successfully. 


### CreateSecurityGroupMetadata {#CreateSecurityGroupMetadata}

Field | Description
--- | ---
security_group_id | **string**<br> 


### SecurityGroup {#SecurityGroup}

Field | Description
--- | ---
id | **string**<br> 
folder_id | **string**<br> 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br> 
status | enum **Status**<br> <ul><li>`UPDATING`: updating is a long operation because we must update all instances in SG</li><ul/>
rules[] | **[SecurityGroupRule](../security_group.proto#SecurityGroupRule2)**<br> 
default_for_network | **bool**<br> 


## Update {#Update}



**rpc Update ([UpdateSecurityGroupRequest](#UpdateSecurityGroupRequest)) returns ([operation.Operation](#Operation1))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[UpdateSecurityGroupMetadata](#UpdateSecurityGroupMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[SecurityGroup](../security_group.proto#SecurityGroup3)<br>

### UpdateSecurityGroupRequest {#UpdateSecurityGroupRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false
update_mask | **[google.protobuf.FieldMask](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/field-mask)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
rule_specs[] | **[SecurityGroupRuleSpec](#SecurityGroupRuleSpec1)**<br>all existing rules will be replaced with given list 


### SecurityGroupRuleSpec {#SecurityGroupRuleSpec}

Field | Description
--- | ---
description | **string**<br> 
labels | **map<string,string>**<br> 
direction | **[SecurityGroupRule.Direction](../security_group.proto#SecurityGroupRule2)**<br>Required.  false
ports | **[PortRange](../security_group.proto#PortRange3)**<br> 
protocol | **oneof:** `protocol_name` or `protocol_number`<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol
&nbsp;&nbsp;protocol_name | **string**<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol 
&nbsp;&nbsp;protocol_number | **int64**<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol 
target | **oneof:** `cidr_blocks`, `security_group_id` or `predefined_target`<br>
&nbsp;&nbsp;cidr_blocks | **[CidrBlocks](../security_group.proto#CidrBlocks3)**<br> 
&nbsp;&nbsp;security_group_id | **string**<br> 
&nbsp;&nbsp;predefined_target | **string**<br> 


### PortRange {#PortRange}

Field | Description
--- | ---
from_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.
to_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.


### CidrBlocks {#CidrBlocks}

Field | Description
--- | ---
v4_cidr_blocks[] | **string**<br> 
v6_cidr_blocks[] | **string**<br> 


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[UpdateSecurityGroupMetadata](#UpdateSecurityGroupMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[SecurityGroup](../security_group.proto#SecurityGroup3)>**<br>if operation finished successfully. 


### UpdateSecurityGroupMetadata {#UpdateSecurityGroupMetadata}

Field | Description
--- | ---
security_group_id | **string**<br> 


### SecurityGroup {#SecurityGroup}

Field | Description
--- | ---
id | **string**<br> 
folder_id | **string**<br> 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br> 
status | enum **Status**<br> <ul><li>`UPDATING`: updating is a long operation because we must update all instances in SG</li><ul/>
rules[] | **[SecurityGroupRule](../security_group.proto#SecurityGroupRule2)**<br> 
default_for_network | **bool**<br> 


## UpdateRules {#UpdateRules}



**rpc UpdateRules ([UpdateSecurityGroupRulesRequest](#UpdateSecurityGroupRulesRequest)) returns ([operation.Operation](#Operation2))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[UpdateSecurityGroupMetadata](#UpdateSecurityGroupMetadata1)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[SecurityGroup](../security_group.proto#SecurityGroup4)<br>

### UpdateSecurityGroupRulesRequest {#UpdateSecurityGroupRulesRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false
deletion_rule_ids[] | **string**<br> 
addition_rule_specs[] | **[SecurityGroupRuleSpec](#SecurityGroupRuleSpec2)**<br> 


### SecurityGroupRuleSpec {#SecurityGroupRuleSpec}

Field | Description
--- | ---
description | **string**<br> 
labels | **map<string,string>**<br> 
direction | **[SecurityGroupRule.Direction](../security_group.proto#SecurityGroupRule2)**<br>Required.  false
ports | **[PortRange](../security_group.proto#PortRange4)**<br> 
protocol | **oneof:** `protocol_name` or `protocol_number`<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol
&nbsp;&nbsp;protocol_name | **string**<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol 
&nbsp;&nbsp;protocol_number | **int64**<br>values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml null value means any protocol 
target | **oneof:** `cidr_blocks`, `security_group_id` or `predefined_target`<br>
&nbsp;&nbsp;cidr_blocks | **[CidrBlocks](../security_group.proto#CidrBlocks4)**<br> 
&nbsp;&nbsp;security_group_id | **string**<br> 
&nbsp;&nbsp;predefined_target | **string**<br> 


### PortRange {#PortRange}

Field | Description
--- | ---
from_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.
to_port | **int64**<br> Acceptable values are 0 to 65535, inclusive.


### CidrBlocks {#CidrBlocks}

Field | Description
--- | ---
v4_cidr_blocks[] | **string**<br> 
v6_cidr_blocks[] | **string**<br> 


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[UpdateSecurityGroupMetadata](#UpdateSecurityGroupMetadata1)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[SecurityGroup](../security_group.proto#SecurityGroup4)>**<br>if operation finished successfully. 


### UpdateSecurityGroupMetadata {#UpdateSecurityGroupMetadata}

Field | Description
--- | ---
security_group_id | **string**<br> 


### SecurityGroup {#SecurityGroup}

Field | Description
--- | ---
id | **string**<br> 
folder_id | **string**<br> 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br> 
status | enum **Status**<br> <ul><li>`UPDATING`: updating is a long operation because we must update all instances in SG</li><ul/>
rules[] | **[SecurityGroupRule](../security_group.proto#SecurityGroupRule2)**<br> 
default_for_network | **bool**<br> 


## UpdateRule {#UpdateRule}

update rule description or labels

**rpc UpdateRule ([UpdateSecurityGroupRuleRequest](#UpdateSecurityGroupRuleRequest)) returns ([operation.Operation](#Operation3))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[UpdateSecurityGroupRuleMetadata](#UpdateSecurityGroupRuleMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[SecurityGroupRule](../security_group.proto#SecurityGroupRule2)<br>

### UpdateSecurityGroupRuleRequest {#UpdateSecurityGroupRuleRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false
rule_id | **string**<br>Required.  false
update_mask | **[google.protobuf.FieldMask](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/field-mask)**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[UpdateSecurityGroupRuleMetadata](#UpdateSecurityGroupRuleMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[SecurityGroupRule](../security_group.proto#SecurityGroupRule2)>**<br>if operation finished successfully. 


### UpdateSecurityGroupRuleMetadata {#UpdateSecurityGroupRuleMetadata}

Field | Description
--- | ---
security_group_id | **string**<br> 
rule_id | **string**<br> 


### SecurityGroupRule {#SecurityGroupRule}

Field | Description
--- | ---
id | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
direction | enum **Direction**<br>Required.  false<ul><ul/>
ports | **[PortRange](../security_group.proto#PortRange5)**<br> 
protocol_name | **string**<br>null value means any protocol values from https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml 
protocol_number | **int64**<br> 
target | **oneof:** `cidr_blocks`, `security_group_id` or `predefined_target`<br>
&nbsp;&nbsp;cidr_blocks | **[CidrBlocks](../security_group.proto#CidrBlocks5)**<br> 
&nbsp;&nbsp;security_group_id | **string**<br> 
&nbsp;&nbsp;predefined_target | **string**<br> 


## Delete {#Delete}



**rpc Delete ([DeleteSecurityGroupRequest](#DeleteSecurityGroupRequest)) returns ([operation.Operation](#Operation4))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[DeleteSecurityGroupMetadata](#DeleteSecurityGroupMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty)<br>

### DeleteSecurityGroupRequest {#DeleteSecurityGroupRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[DeleteSecurityGroupMetadata](#DeleteSecurityGroupMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty)>**<br>if operation finished successfully. 


### DeleteSecurityGroupMetadata {#DeleteSecurityGroupMetadata}

Field | Description
--- | ---
security_group_id | **string**<br> 


## Move {#Move}



**rpc Move ([MoveSecurityGroupRequest](#MoveSecurityGroupRequest)) returns ([operation.Operation](#Operation5))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[MoveSecurityGroupMetadata](#MoveSecurityGroupMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[SecurityGroup](../security_group.proto#SecurityGroup5)<br>

### MoveSecurityGroupRequest {#MoveSecurityGroupRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false
destination_folder_id | **string**<br>Required.  false


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[MoveSecurityGroupMetadata](#MoveSecurityGroupMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[SecurityGroup](../security_group.proto#SecurityGroup5)>**<br>if operation finished successfully. 


### MoveSecurityGroupMetadata {#MoveSecurityGroupMetadata}

Field | Description
--- | ---
security_group_id | **string**<br> 


### SecurityGroup {#SecurityGroup}

Field | Description
--- | ---
id | **string**<br> 
folder_id | **string**<br> 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br> 
name | **string**<br> 
description | **string**<br> 
labels | **map<string,string>**<br> 
network_id | **string**<br> 
status | enum **Status**<br> <ul><li>`UPDATING`: updating is a long operation because we must update all instances in SG</li><ul/>
rules[] | **[SecurityGroupRule](../security_group.proto#SecurityGroupRule3)**<br> 
default_for_network | **bool**<br> 


## ListOperations {#ListOperations}



**rpc ListOperations ([ListSecurityGroupOperationsRequest](#ListSecurityGroupOperationsRequest)) returns ([ListSecurityGroupOperationsResponse](#ListSecurityGroupOperationsResponse))**

### ListSecurityGroupOperationsRequest {#ListSecurityGroupOperationsRequest}

Field | Description
--- | ---
security_group_id | **string**<br>Required.  false
page_size | **int64**<br> 
page_token | **string**<br> 


### ListSecurityGroupOperationsResponse {#ListSecurityGroupOperationsResponse}

Field | Description
--- | ---
operations[] | **[operation.Operation](#Operation6)**<br> 
next_page_token | **string**<br> 


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)**<br>The normal response of the operation in case of success. If the original method returns no data on success, such as Delete, the response is [google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty). If the original method is the standard Create/Update, the response should be the target resource of the operation. Any method that returns a long-running operation should document the response type, if any. 


