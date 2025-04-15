# MachineTeleoperationStateV1

This message is sent by the Teleoepration when FMS and AHS initially connected or changes in machine teleoperation state changes

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | Client connection or machine teleoperation state changes | Normally Nothing.<br/>To provide machine teleoperation states to `FMS` |

## Message Attributes

The `MachineTeleoperationStateV1` message consist an array of the following object.

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"EquipmentId"` | EquipmentId | UUID | True | The vehicle identifier associated to the machine states
| `"Paused"` | [`True`, `False`] | Boolean | False | Determine whether the machine is paused |
| Additional keys allowed | 

**NOTE**: Additional state properties that are not officially mentioned in the above attributes table may not be supported by AHS and FMS. Should the *additional keys* be supported and handled, will be implementation specific of the AHS and FMS vendor.

## Examples
### Typical Message
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "MachineTeleoperationStateV1": [
    {
      "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
      "Paused": false
    },
    {
      "EquipmentId": "123e4567-e89b-12d3-a456-426614174001",
      "Paused": true
    }
  ]
}
```

### Extra Attributes
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "MachineTeleoperationStateV1": [
    {
      "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
      "Paused": false,
      "Light": "On",
    },
    {
      "EquipmentId": "123e4567-e89b-12d3-a456-426614174001",
      "Paused": true
    },
    {
      "EquipmentId": "123e4567-e89b-12d3-a456-426614174002",
      "Paused": true,
      "Light": "Off"
    }
  ]
}
```