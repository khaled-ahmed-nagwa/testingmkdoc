# Handling Voice Calls, Actions, and Text Chat

## Agora Overview

Agora Real-time messages Signaling (Was RTM) and Agora Voice Calls are two components of the Agora platform used for facilitating communication in real-time virtual learning environments

### Agora Voice Call

It enables the transfer of audio in real-time during online sessions. It allows participants, such as students and teachers, to engage in voice-based communication seamlessly.

### Agora Signaling (Agora RTM - Real-time messages)

communication protocol designed for facilitating chat messages and interactive actions in real-time virtual learning environments. It enables the transfer of text-based messages and supports various actions to enhance engagement and manage the session effectively. These actions include:

- Student Hand Raise: Students can virtually raise their hands, signaling their desire to speak or ask questions, and the teacher receives notifications.
-  Educator Audio Control: Educators can mute or unmute students' audio streams.
- Student Self-Mute/Unmute: Students can self-mute or unmute when granted permission by the educator.
- Disconnection/Reconnection Detection: Agora includes mechanisms to detect when educators or students disconnect or reconnect.
- Educator Student Removal: Educators have the authority to remove a student from the session when necessary.

!!! note "Agora RTM was the previous name for Agora Signaling, so when we refer to Agora Signaling or RTM, they are essentially the same."

#### Referance 
For more information about Agora, check out the official SDK documentation:

- [RtmClient | Signaling (previously RTM) SDK](https://api-ref.agora.io/en/signaling-sdk/web/1.x/classes/rtmclient.html).
- [Agora API Overview](https://api-ref.agora.io/en/voice-sdk/flutter/6.x/API/rtc_api_overview_ng.html).
- [Agora SDK](https://api-ref.agora.io/en/chat-sdk/flutter/1.x/agora_chat_sdk/agora_chat_sdk-library.html).
