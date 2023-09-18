# Agora Singling Handling (RTM)

Before starting the initialization process, we need to first set the credentials required, For this, we use the “setSessionCredential” function, which is responsible for setting the session credential , the user , the session and the channel name for the chat and the actions channel

```dart
channelChatName = "ChatChannel:${currentSessionCredential.sessionId}";
channelActionsName = "ActionsChannel:${currentSessionCredential.sessionId}";
```

## Initializing Signaling

The `initRTM` method is responsible for initializing the Agora RTM client and logging in to it by first

- Creating an instance of the Agora RTM client using the provided App ID.
- Logs in the client using the RTM token and user ID from the current session credentials.
- Create `onMessageReceived` callback that will be called when a message is received from the RTM client .
- Create an `onConnectionStateChanged2` callback that will be called when the connection state `RtmConnectionState` Event changes.
- Finally, a call to the `_createRtmChannel`  method to create the chat channel and the actions channel


??? abstract "Initializing Agora Singling (RTM) Flowchart"
    <iframe frameborder="0" style="width:100%;height:1296px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G12MHC7pqK8A4KRFD_TyCEbic-XgL8Khvg"></iframe>

### RTM Connection State Events

<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">State</th>
        <th style="text-align: left; padding: 10px;">Description</th>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Aborted</td>
        <td style="text-align: left; padding: 10px;">This means that the device is used in another session and will emit SignalingChanged(SignalingActionsdeviceUsed). 
        Our response to this situation is to inform the educator that their session is open on another device. Then, we will remove them from the first session and let them stay only in the last session they opened on their current device.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Disconnected or Reconnecting</td>
        <td style="text-align: left; padding: 10px;">This means that the connection is lost and will emit SignalingConnectionFailure(). It will show a toast with the message that the connection is lost, and the user can't send messages or actions.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Connected</td>
        <td style="text-align: left; padding: 10px;">This means that the connection is restored and will emit SignalingConnectionRestored(). It will show a toast with the message that the connection is restored, and the user can send messages or actions.</td>
    </tr>
</table>

??? info " `initRTM` Function Path"
    The `initRTM` function is located at the [`lib/features/sessions/presentation/logic/signaling/signaling_cubit.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/presentation/logic/signaling/signaling_cubit.dart&version=GBmaster) path.

#### Aborted State Handling

??? failure "The user Has Another open Account (RtmConnectionState.aborted)"
    <iframe frameborder="0" style="width:100%;height:482px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1Hii4C46QpKQ17_1LBUv9jKYV615zy-SI"></iframe>


## onChat Function

After creating the RTM chat and actions channal,now we need to listen for new members joining the channel and handles any recived text messages; For that we use the `onChat` Funciton which listens for `onMessageReceived` event which occurs when receiving a channel message.

Every time a message is recived we handle it by calling `handleReceivedMessage` 

1. It creates an instance of the MessageModel [`fullName`, `message`, `isFirstMessage` ] from the message object.
2. Checks if the message is the first message in the chat or not by checking if the message list is empty or the full name of the message is not equal to the first message's full name.
3. Then it inserts the message into the first index of the messages list and emits `MessageReceived()` event to notify the UI that a new message has been received.
