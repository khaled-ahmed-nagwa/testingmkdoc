# Agora RTC Handling 

When we receive the `engineLoaded` event we start the process of initializing Agora RTC

???+ question "What is the engineLoaded Event"
    This event will be fired from the HTML rendering engine when the engine is fully loaded and ready for use. It serves as an indication that all necessary components have been initialized, and you can now start interacting with the engine and its functionalities.

## Setup Agora Voice SDK

Our first step will be setting up the the voice SDK engine and registering the event handler for the voice SDK engine events , for that we use the `setupVoiceSDKEngine` method the handle the setup process.

??? abstract "Setup Voice SDK Flowchart"
    <iframe frameborder="0" style="width:100%;height:962px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1KY1u8nsBwETs4Wy5jLwO_8P_siNk6S9f"></iframe>

??? info "`setupVoiceSDKEngine` Function Path"
    The `setupVoiceSDKEngine` function is located at the [`lib/features/sessions/presentation/logic/voice_calling/voice_call_cubit.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/presentation/logic/voice_calling/voice_call_cubit.dart&version=GBdevelopment) path.



### Join Agora Engine 

You can notice that inside the `setupVoiceSDKEngine` function, we call the a function called `joinAgoraEngine` in case if the user is eductor, inside this function we call the agoraStarted function inside the HTML rendering engine. `NagwaRenderingEngine.agoraStarted();`

!!! question "What is `agoraStarted` function ?"
    We call this function to send a message indicating to the HTML rendering engine that Agora has started. This action will trigger the agoraStarted message.





### Switch Between Members Types

The switch between the broadcaster and audience roles can be done by calling the `setClientRole` method of the Agora engine and passing the desired role as a parameter.and it Sets the user role and level in an interactive live streaming channel


!!! note "Agora engine is initialized with the channel profile set to `channelProfileLiveBroadcasting`, which is the profile when there are more than two users in the channel"

### Mute & UnMute Functionlity 

The mute and unmute microphone functionality can be done by calling the `muteLocalAudioStream` method of the Agora engine and passing the desired state as a parameter. the method stops or resumes publishing the local audio stream.
??? abstract "Mic Status Screenshot"
    <iframe frameborder="0" style="width:100%;height:279px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1y-zwR912AHIpelVMiguGpaeKw56iMiJC"></iframe>

??? warning " Access Microphone Permission"
    The process of setting up the Agora Voice SDK cannot begin without obtaining permission from the educator to access the microphone. A popup will appear requesting permission before proceeding.

    <iframe frameborder="0" style="width:100%;height:524px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1AGclcWIKRaRT7p8Luxt5RoaSAczzdWWO"></iframe>
 

## Join RTC Channel

After setting up the voice SDK, our next step is to join the RTC channal and setting the default audio route.


1. It set the default audio route to speakerphone by calling `agoraEngine.setDefaultAudioRouteToSpeakerphone(true)`
!!! info "If you want the default audio route to be the earpiece , change true to be false"
2. Gets the client role type  whether the user is a broadcaster or an audience member, and then sets the client role accordingly.
   

### Participant Types In Agora RTC

- `clientRoleAudience` : the default role for the user when he joins the channel, it means that the user can only listen to the voice of the broadcaster and cannot speak.
- `clientRoleBroadcaster` role means that the user can speak and listen to the voice of the broadcaster.


3. Call to join the channel is made with
   1. `token`: The token generated on our server for authentication.
   2.`channelId`: The channel name. This parameter signifies the channel in which users engage in real-time audio and video interaction
   2. `options`: The channel media options which containe many parameters , one of them is the clinet role type
   3. `UID`:The user ID. This parameter is used to identify the user in the channel for real-time audio and video interaction
4. Enable the local audio and the local audio stream is muted or unmuted depending on the microphone status of the user. 

??? abstract "Join RTC Flowchart"
    <iframe frameborder="0" style="width:100%;height:614px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1ccHpAfF8kkbKnI6KIT_fXmnqsyyT2W8Z"></iframe>

??? info "`join` Function Path"
    The `join` function is located at the [`lib/features/sessions/presentation/logic/voice_calling/voice_call_cubit.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/presentation/logic/voice_calling/voice_call_cubit.dart&version=GBdevelopment) path.

## Leaving the Channel

- The `leave` method serves the purpose of enabling an educator to exit the channel and free up the resources used by the Agora engine. When an educator decides to leave the channel, this process is initiated by invoking the `leaveChannel` method of the Agora engine, which ensures the user's disconnection from the session. 
- Additionally, the `release` method of the Agora engine is called to properly release all resources associated with the engine. After a successful method call, we can no longer use any method or callback in the SDK anymore. If we want to use the real-time communication functions again, you must call createAgoraRtcEngine and initialize to create a new RtcEngine instance

!!! tip "When we call `release` immediately after calling `leave`, the SDK does not trigger the onLeaveChannel callback."


## Switch Microphone State
The `switchMicrophone` function is used to switch the microphone status from muted to unmuted and vice versa.

- It first checks if the user is joined to the channel or not 
- If joined, it will set the isMicrophoneMuted variable to the new status, 
- then set the client role to the new status 
- Change the audio stream whether muted or not based on `isMuted` varible by calling the `muteLocalAudioStream` from the agora engine.

!!! info "The  `muteLocalAudioStream` stops or resumes publishing the local audio stream ,  as it takes a `mute` varible to spacify Whether to stop publishing the local audio stream: true : Stops publishing the local audio stream. false : (Default) Resumes publishing the local audio stream."
