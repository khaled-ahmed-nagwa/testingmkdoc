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

### Handling Recived Messages: `onChat` Function

After creating the RTM chat channal,now we need to listen for new members joining the channel and handles any recived text messages; For that we use the `onChat` Funciton which listens for `onMessageReceived` event which occurs when receiving a channel message.

Every time a message is recived we handle it by calling `handleReceivedMessage`

1. It creates an instance of the MessageModel [`fullName`, `message`, `isFirstMessage` ] from the message object.
2. Checks if the message is the first message in the chat or not by checking if the message list is empty or the full name of the message is not equal to the first message's full name.
3. Then it inserts the message into the first index of the messages list and emits `MessageReceived()` event to notify the UI that a new message has been received.

??? example "handleReceivedMessage Function"
    ```dart linenums="1"
    void handleReceivedMessage(Map<String, dynamic> messageObj) {
    final messageModel = MessageModel.fromJson(messageObj);
    final bool isFirst =
        messages.isEmpty || messageModel.fullName != messages.first.fullName;
    messageModel.isFirstMessage = isFirst;
    messages.insert(0, messageModel);
    isAllMessagesRead = false;
    emit(MessageReceived());
    }
    ```

### Handling Recived Actions: `onActions` Function

After creating the RTM action channal, now we need to join the channel and listen to the incoming messages on it , For that we use the `onAction` function which joins a channel and listens for incoming messages [`onMessageReceived` event], then calls a function to handle the received actions.

!!! tip " [Actions list (Numbers & Describtion)](../../pre_knowledge_required/agoraDetails.md/#agora-actions-numbers)"

Every time a message is recived we handle it by calling `handleReceivedActions` function.

1. This function takes a map of strings and dynamic as an argument, then creates an `ActionModel` object that containes [`signalingAction`, `userId`, `username`] from the map. then it checks the type of action and performs certain actions based on the result
   1. If the action is a reset action, the function `reset()` is called to reset the signaling.
   2.  If it's raiseHand, it will emit `signalinguserRaiseHandStatusChanged` with the `studentId` and `isHandRaised` = true
   3.  Otherwise, it will emit `SignalingChanged(actionModel.signalingAction)`


??? example "handleRecivedActions Function"
    ```dart linenums="1"
    void handleReceivedActions(Map<String, dynamic> actionObj) {
    final actionModel = ActionModel.fromJson(actionObj);
    if (actionModel.signalingAction == SignalingActions.reset) {
      emit(SignalingReset(studentId: int.parse(actionModel.userId)));
    } else if (actionModel.signalingAction == SignalingActions.raiseHand) {
      emit(
        SignalingUserRaiseHandStatusChanged(
          studentId: int.parse(actionModel.userId),
          isHandRaised: true,
        ),
      );
    }
    if (actionModel.signalingAction != SignalingActions.reset) {
      emit(SignalingChanged(actionModel.signalingAction));
    }
    } 
    ```


In additon to the previous uses of the function , `onActions` also listen for any changes in members state (`onMemberJoined` event), and emit `SignalingUserOnlineStatusChanged` with the online status and student ID.

### Sending Action: `sendAction` function

To facilitate the sending of actions we use the `sendAction` function to send an action to the RTM channel
1. Creates an action object, which contains the following:
   1. Text that represents the action type.
   2. user ID
   3. message type
   4. timestamp
   5. offline status
2. Call the `sendMessage2()` function on the RTM channel object with the action object as an argument the message object is as follows
    ```dart linenums="1"
    messageObj = {
      "text": jsonEncode({
        "a": signalingAction.type,
        "si": studentId?.toString() ?? user.userID.toString(),
      }),
      "messageType": 1,
      "ts": 0,
      "offline": false,
    };
    ```

### Disabling Chat Functionality

As you know that the eductor has the authority to disable chat functionality , to handles this we call the `updateChatStatus` function which runs `NagwaRenderingEngine.updateChatStatus($isEnabled)`  function in the webview which enables or disables the chat and emits the `DrawingRefresh`
!!! note "Use the `updateChatStatus` function if you want to update the chat status and enable or disable it. By calling this function false, you can disable the chat feature, and with true, you can enable it again."

!!! warning "In case the educator has internet connection issues, the chat functionality will be disabled."

??? abstract "Enable & Disable Button Screenshot"
    <iframe frameborder="0" style="width:100%;height:527px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1nO62RfRG--q7V76PijiawiazlNXo4SQm"></iframe>

#### Chat Status Handler

The HTML rendering engine sends an `chatStatusUpdated` event when the chat status is updated (enabled / disabled). So we use the `chatstatusHandler` function which is a javascript callback which checks if the chat is enabled or not and change the isChatEnabled value, the 

### Closing RTM Channel
Upon finishing the session or exiting from it, a function is called to logout the eductor from all channels joined. The `close()` function is responsible for releasing resources and logging out the user from the chat and action channels
- First, it leaves the chat channel, then releases it
- then it leaves the action channel, then releases it
- then it logout from the RTM client, then releases  
