# Teleoperation Sequence Diagrams

The following sections describes when the messages should be sent during the lifecycle of the teleoperation messages between the Fleet Management System (FMS) and the Autonomous Haulage System (AHS).

### Language
| Acronyms | Extend Name |
| -------- | ----------- |
| AHS      | Autonomous Haulage System |
| AHT      | Autonomous Haul Truck |
| AV       | Autonomous Vehicle (interchangeable with AHT) |
| FMS      | Fleet Management System |

> ## On Connect
> When the FMS connects to the AHS via WebSocket connection, AHS shall send the AHTs' Machine Teleoperation State to the FMS.
> ```mermaid
> %% On Connect Sequence
> sequenceDiagram 
>    FMS->AHS: WebSocket Connection
>   par AHS to AHT_1
>        AHS ->>+ AHT_1: Get AV status / state
>        AHT_1 -->>- AHS: MachineTeleoperationStateV1
>    and AHS to AHT_2
>        AHS ->>+ AHT_2: Get AV status / state
>        AHT_2 -->>- AHS: MachineTeleoperationStateV1
>    and AHS to ... AHT_n
>        AHS ->>+ ... AHT_n: Get AV status / state
>        ... AHT_n -->>- AHS: MachineTeleoperationStateV1
>    end
>    AHS --) FMS: MachineTeleoperationStateV1[]
>    Note right of ... AHT_n: AHTs and AVs are interchangable terminology
> ```
> See [On Connect Sequence Diagram](./teleoperation-on-connect-sequence.svg) if above mermaid code cannot be rendered.

> ## Command Accepted
> When the FMS sends a teleoperation request to the AHS through a REST endpoint and the request is accepted by AHT.
> The following shall happen in sequential,
> 1.  AHS shall response to the REST request with 202 Accepted, if capabable of processing the command and send to the vehicle.
> 2. The AHS shall send back teleoperation response message to FMS when AHT accepted the command via the WebSocket.
> 3. Finally AHS shall sent back the teleoperation state if there are changes to the state after actioning via the WebSocket.
> ```mermaid
> %% Teleoperation Command Request Accepted Sequence
> sequenceDiagram
>   participant FMS
>   participant AHS
>   participant AHT_1
>   participant AHT_2
>   participant ... AHT_n
>   note over FMS, ... AHT_n: On Connect Sequence
>   FMS ->>+ AHS: POST MachineTeleoperationRequestV1 for AHT_1
>   AHS -->> FMS: Accepted POST MachineTeleoperationRequestV1 for AHT_1
>   AHS ->>+ AHT_1: Send MachineTeleoperationRequestV1
>   AHT_1 -->>- AHS: Accepted MachineTeleoperationRequestV1
>   AHS -)- FMS: AHT_1 Accepted Command with MachineTeleoperationResponseV1
>   alt Machine Not at final state of Command
>     Note over FMS, AHT_1: AHT_1 Actioning Command...
>     AHT_1 ->> AHS: MachineTeleoperationStateV1 with State Changed
>     AHS -) FMS: AHT_1 MachineTeleoperationStateV1 with State Changed  
>   else Machine Already ste final state of Command
>     Note over FMS, AHT_1: No MachineTeleoperationStateV1 message will be sent
>   end
> ```
> See [Command Accepted Sequence Diagram](./teleoperation-command-accepted-sequence.svg) if above mermaid code cannot be rendered.

> ## Command Rejected
> When the FMS sends a teleoperation request to the AHS through a REST > endpoint and the request is rejected.
> Two different parties can reject the request.
> 1. The AHS rejects the REST reqest, [4xx, 5xx]. <br/>
> AHS not able to proceed with sending command to equipment. <br/>
> In example:
>     - Malform Request
>     - Server Error
> 2. AHS accepts REST request **BUT** AHT rejects the request from AHS, then AHS shall response with a teleoperation response message that ATS reject the request and the reason behind rejection via the WebSocket.
> ```mermaid
> %% Teleoperation Command Request Rejected Sequence
> sequenceDiagram
>   participant FMS
>   participant AHS
>   participant AHT_1
>   participant AHT_2
>   participant ... AHT_n
>   note over FMS, ... AHT_n: On Connect Sequence
>   alt AHS Rejects Command
>     FMS ->>+ AHS: POST MachineTeleoperationRequestV1 for AHT_1
>     AHS -->>- FMS: Rejected POST MachineTeleoperationRequestV1 for AHT_1
>   else AHS Accepcts Command But AHT Rejects Command
>     FMS ->>+ AHS: POST MachineTeleoperationRequestV1 for AHT_1
>     AHS -->> FMS: Accepted POST MachineTeleoperationRequestV1 for AHT_1
>     AHS ->>+ AHT_1: Send MachineTeleoperationRequestV1
>     AHT_1 -->>- AHS: Rejected MachineTeleoperationRequestV1
>     AHS -)- FMS: AHT_1 Rejected Command with MachineTeleoperationResopnseV1
>   end
> ```
> See [Command Rejected Sequence Diagram](./teleoperation-command-rejected-sequence.svg) if above mermaid code cannot be rendered.

> ## Exception Occurred
> When the FMS sends a teleoperation request to the AHS through a REST endpoint and the request is accepted, However, error occurred when actioning the reques. <br/>
> Then the following shall happen:
> 1. AHT reports error back to AHS
> 2. AHS sends teleoperation exception message to FMS via the WebSocket
> 3. AHS sends teleopeation state message to FMS via the WebSocket if changes to the AHT teleoperation state.
> 
> ```mermaid
> %% Exception Occured During Action of Teleoperation Command
> sequenceDiagram
>   participant FMS
>   participant AHS
>   participant AHT_1
>   participant AHT_2
>   participant ... AHT_n
>   note over FMS, ... AHT_n: On Connect Sequence
>   FMS ->>+ AHS: POST MachineTeleoperationRequestV1 for AHT_1
>   AHS -->> FMS: Accepted POST MachineTeleoperationRequestV1 for AHT_1
>   AHS ->>+ AHT_1: Send MachineTeleoperationRequestV1
>   AHT_1 -->>- AHS: Accepted MachineTeleoperationRequestV1
>   AHS -)- FMS: AHT_1 Accepted Command with MachineTeleoperationResponseV1
>   break
>     note over FMS, AHT_1: Exception occured when actioning
>     AHT_1 -->> AHS: Exception
>     AHS -) FMS: Send MachineTeleoperationExceptionV1 of the occurred exception
> Note right of FMS: Propose to have a new message MachineTeleoperationExceptionV1 for sending exceptions
>     AHS -) FMS: Send MachineTeleoperationStateV1    
>   end
> ```
> See [Exception Occurred Sequence Diagram](./teleoperation-exception-occurred-sequence.svg) if above mermaid code cannot be rendered.

**NOTE** AHS shall sent machine teleoperation state whenever there's a state change on the AHT.