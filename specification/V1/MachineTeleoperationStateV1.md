# MachineTeleoperationStateV1

This message is sent by the Teleoepration when there are changes in machine teleoperation state.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | Machine teleoperation state changes | When a machines state has been changed.<br/>To provide machine teleoperation states to `FMS` |

## Message Attributes

The `MachineTeleoperationStateV1` message consists of the following object.

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"Paused"` | [`True`, `False`] | Boolean | False | Determine whether the machine is paused |
| Additional keys allowed | 

>[!NOTE]
> The top-level message headers should contain the `EquipmentId`, indicating which AV the `MachineTeleoperationStateV1` message is for.

**NOTE**: Additional state properties that are not officially mentioned in the above attributes table may not be supported by AHS and FMS. Should the *additional keys* be supported and handled, will be implementation specific of the AHS and FMS vendor.

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