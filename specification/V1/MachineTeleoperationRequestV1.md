# MachineTeleoperationRequestV1

This message is sent by an operator or dispatching from the fleet management system to remotely command a autonomous vehicle to perform specific task.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `Teleoperation` | Operator or Dispatching requesting a vehicle to perform certain operation support by teleoperation | 1. A vehicle to perform the operation (rejects if cannot)|

## Message Attributes

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"Command"` | [`"Pause"`, `"Resume"`] | String | True | The command the operator or dispatching is requesting the vehicle to perform.
| `"RequestId"` | RequestId | UUID | True | A unique ID for to link the response message to the request mesage |

**NOTE**: the top-level message headers should contain the `EquipmentId` which is the vehicle that is requested to perform the command.

## Examples
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
  "MachineTeleoperationRequestV1": {
    "Command": "Pause",
    "RequestId": "123e4567-e89b-12d3-a456-426614174001"
  }
}
```
