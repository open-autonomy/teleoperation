# MachineTeleoperationStateV1

This message is sent by the Teleoperation when there are changes in machine teleoperation state.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | Machine teleoperation state changes | When a machine's state has been changed.<br/>To provide the teleoperation state of a machine to `FMS` |

## Message Attributes

The `MachineTeleoperationStateV1` message consists of the following object.

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"Paused"` | [`True`, `False`] | Boolean | False | Determine whether the machine is paused |
| Additional keys allowed | 

One or more machine teleoperation states can be sent in a message. At a minimum, the message must include the state that has changed.

>[!NOTE]
> The top-level message headers should contain the `EquipmentId`, indicating which AV the `MachineTeleoperationStateV1` message is for.

>[!NOTE]
> This list is not exhaustive and more teleoperations can be added in the future.

## Examples
### Typical Message
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
  "MachineTeleoperationStateV1": {
    "Paused": false
  }
}
```

### Extra Attributes
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
  "MachineTeleoperationStateV1": {
    "Paused": false,
    "Light": "On",
  }
}
```