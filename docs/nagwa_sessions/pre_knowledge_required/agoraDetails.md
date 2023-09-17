# Agora 

## Signaling Overview
A message is broadcast to all users in the same channel when a user sends a message. The message structure is as follows: {n: user full name, m: user message}, The n field represents the full name of the user who sent the message, while the m field contains the actual message content.
To manage the messages and actions, we have two channels 

1. Messages Channel: Used for transferring chat messages, its name should be `ChatChannel:${currentSessionCredential.sessionId}`.
2. Actions Channel: Used for transferring actions, its name should be `ActionsChannel:${currentSessionCredential.sessionId}`.

### Agora Actions Numbers

<table width="100%" style="border-collapse: collapse;">
    <tr>
        <th style="width: 20%; text-align: left;">Action Number</th>
        <th style="width: 80%; text-align: left;">Action Description</th>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">1</td>
        <td style="width: 80%; text-align: left;">The student raised his hand in order to seek permission to speak

</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">2</td>
        <td style="width: 80%; text-align: left;">Educator unmuted a student with ID </td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">3</td>
        <td style="width: 80%; text-align: left;">The educator muted student with ID.</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">4</td>
        <td style="width: 80%; text-align: left;">The educator ended the session</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">5</td>
        <td style="width: 80%; text-align: left;">Educator away, meaning that he is having internet connection issues or   left the session </td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">6</td>
        <td style="width: 80%; text-align: left;">The educator is now back </td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">7</td>
        <td style="width: 80%; text-align: left;">willTerminateApp</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">8</td>
        <td style="width: 80%; text-align: left;">Reset session to normal state by resetting speaking and raising hand actions if a student was speaking and had a connection problem or if the educator left and came back</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">12</td>
        <td style="width: 80%; text-align: left;">The student muted himself, it’s sent by the student </td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">13</td>
        <td style="width: 80%; text-align: left;">The student unmuted himself; it's sent by the student</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">14</td>
        <td style="width: 80%; text-align: left;">The eductor kicked out students from the session</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">15</td>
        <td style="width: 80%; text-align: left;">Indicates that the student has an active account and is currently running the session on another device.</td>
    </tr>
</table>


## Agora Voice Call (RTC)
To provide the educator with real-time voice communication with the students, we first set the user-needed credentials, We pass the current session credential and the user ID of the active user to the `setSessionCredential` method of the `voiceCallCubit`. This allows the voice call feature to authenticate the user and establish a connection for the session.

By default, when an educator joins a session, permission is requested from him to allow microphone access. Once permission is granted,  his microphone becomes open and he has the flexablilty to turn it off /on.
