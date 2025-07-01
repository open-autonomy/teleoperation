# MachineTeleoperationResponseV1

This message is sent by AHS to determine if the vehicle accepted the corresponding machine teleoperation response message.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS` | `MachineTeleoperationRequestV1` message | Normally Nothing. |

## Message Attributes

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"Response"` | [`Accepted`, `Rejected`] | String | True | The command the operator or dispatching is requesting the vehicle to perform.
| `"Reason"` | ReasonEnum | String | False | Response rejection reason enumeration
| `"RequestId"` | RequestId | UUID | True | A unique ID for to link the response message to the request mesage |
| `"Detail"` | `""` | String | False | Human readable rejection response message |

**NOTE**: the top-level message headers should contain the `EquipmentId` which is the vehicle that is requested to perform the command.

## Examples
### Accepted
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
  "MachineTeleoperationResponseV1": {
    "Response": "Accepted",
    "RequestId": "123e4567-e89b-12d3-a456-426614174001"
  }
}
```

### Rejected
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
  "MachineTeleoperationResponseV1": {
    "Response": "Rejected",
    "Reason": "CommandCannotBeExecuted",
    "RequestId": "123e4567-e89b-12d3-a456-426614174001",
    "Detail": "Command cannot be executed due to safety reasons"
  }
}
```