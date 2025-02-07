# Open-Autonomy Teleoperation Interface Definition

This section defines the requirements, use cases and message schematics for the Teleoperation interface.

> ### [AsyncAPI Specification](./specification/asyncapi.yaml)
> Defines the Teleoperation message schematics and protocols used

>### [Message Flow - Sequence Diagram](./diagram/sequence_diagrams.md)
> Defines when the Teleoperation messages should be used

## Introduction
This repo is dedicated in documenting the Teleoperation interfrace for the Open-Autonomy family

### Purpose of Teleoperation interface
The purpose of Teleoperation interface is to provide and define capbility for Fleet Management System (FMS) to send teleoperation command request to the Autonomous Haulage System (AHS), and to have AHS send machines' teleoperation states back to the FMS.

#### Official Open-Autonomy Supported Teleoperation Command
> Available for the `command` property value in the `MachineTeleoperationRequestV1` request.
> | Command | Description |
> | ------- | ----------- |
> | Pause   | To pause an equipment's current operation |
> | Resume  | To resume a paused equipment's operation | 

#### Official Open-Autonomy Supported Teleoperation State
> State property keys that are reserved in the `MachineTeleoperationRequestV1` message.
> | Key | Type | Values | Description |
> | --- | ---- | ------ | ----------- |
> | Puased | Boolean | [True, False] | A boolean state property that is used to define define whether the equipment is paused or not|

### Audience
- Autonomy integrators ( typically miners )
- Autonomous truck suppliers ( Engineering / Developers )
- Fleet Management suppliers ( Engineering / Developers )

### What is Teleoperation?
Teleoperation in the context of Open-Autonomy is the ability to remotely command equipment to perform action.

### Limitations
Despite the definition that teleoperation is to provide ability to remotely command equipment to perform action. It should not be used for safety critical action/command of the equipment.<br>
This Includes the following:
- Positional movement of equipment

Additionally, the teleoperation interface definition is not to be used for all equipment operation states and actions. It should only record and send equipment states that are relavent to the supported teleoperation command.