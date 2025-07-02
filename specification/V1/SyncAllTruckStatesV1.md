# SyncAllTruckStatesV1

This message is sent by the Teleoepration when FMS and AHS initially connected.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | Client connection | Client Connection.<br/>To provide machine teleoperation states to `FMS` |

## Message Attributes

The `SyncAllTruckStatesV1` message consists of an array of the following object.

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"EquipmentId"` | EquipmentId | UUID | True | The vehicle identifier associated to the machine states
| `"Paused"` | [`True`, `False`] | Boolean | False | Determine whether the machine is paused |
| Additional keys allowed | 

>[!NOTE]
> This list is not exhaustive and more teleoperations can be added in the future.

## Examples
### Typical Message
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "SyncAllTruckStatesV1": [
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
  "SyncAllTruckStatesV1": [
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