# Resource Action



## Request

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x06 | Run |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | No | [Stream identifier](../definitions.md#stream-identifier). If set, the target endpoint should answer to the run message. If not, it should not send back any response. |
| **Method** | 0x02 | varint |  | GET, POST, PUT DELETE, START_STREAM, STOP\_STREAM_ |
| **Resource**  | 0x02 |  | Yes | [Resource identifier](../definitions.md#resource-identifier). |
|  |  |  |  |  |
| **Payload** | 0x03 |  | No | The payload sent to the target resource. |
|  |  |  |  |  |
| **Parameters** | 0x04 |  | No | [Resource parameters](../definitions.md#resource-parameters) to be supplied while executing  the resource. |

