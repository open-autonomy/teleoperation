# MachineTeleoperationExceptionV1

This message is sent by AHS to indicate that the vehicle that is performing a teleoperation command had hit an errored.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS` | A vehcile errored while performing a requested teleoperation action | Normally Nothing. |

## Message Attributes

| Key | Value | Format | Required | Description |
| --- | :---: | :---: | :---: | --- |
| `"Reason"` | ReasonEnum | String | True | Exception reason enumeration
| `"Detail"` | | String | True | Human readable exception message |

**NOTE**: the top-level message headers should contain the `EquipmentId` which is the vehicle that is requested to perform the command.

## Examples
```JSON
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2021-09-01T12:00:00Z",
  "EquipmentId": "123e4567-e89b-12d3-a456-426614174000",
  "MachineTeleoperationExceptionV1": {
    "Reason": "Fallen",
    "Detail": "I've fallen and cannot get up"
  }
}
```
