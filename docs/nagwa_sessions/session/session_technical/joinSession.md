# Session Joining 

If anything happens that causes the educator to exit the session, even if they accidentally close the app, they can see the list of session cards when they open the app again. The card will have a **Continue** button. Once they click the button, we will call the `sessions/join` API to retrieve the required data needed to rejoin the running session.


!!! note "The join session button is only available if the session is already started and still running."


!!! tip "The session will not be completely ended and students will still be able to join unless: The educator presses the end session button OR The session reached its end date."

### Join Session API

<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
        <tr>
            <th style="text-align: left; padding: 10px;">Joining Session API</th>
            <td style="text-align: left; padding: 10px;"></td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Endpoint</th>
            <td style="text-align: left; padding: 10px;">sessions/join</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Query Parameters</th>
            <td style="text-align: left; padding: 10px;">clientType</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">HTTP Method</th>
            <td style="text-align: left; padding: 10px;">POST</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Required Data</th>
            <td style="text-align: left; padding: 10px;">
                <ul>
                    <li>userId</li>
                    <li>sessionId</li>
                </ul>
            </td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Headers</th>
            <td style="text-align: left; padding: 10px;">api-version: 7</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Response</th>
            <td style="text-align: left; padding: 10px;">
                <ul>
                    <li>actualStartDate</li>
                    <li>rtcToken</li>
                    <li>rtmToken</li>
                    <li>sessionId</li>
                </ul>
            </td>
        </tr>
    </table>
</div>


#### Return Parameters From the API

<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">Return Parameter</th>
        <th style="text-align: left; padding: 10px;">Data Type</th>
        <th style="text-align: left; padding: 10px;">Description</th>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">rtcToken</td>
        <td style="text-align: left; padding: 10px;">String</td>
        <td style="text-align: left; padding: 10px;">Web RTC token, only populated if the WebRTC session provider is ‘Agora’</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">actualStartDate</td>
        <td style="text-align: left; padding: 10px;">Long</td>
        <td style="text-align: left; padding: 10px;">Time when the educator started the session in Unix time</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">rtmToken</td>
        <td style="text-align: left; padding: 10px;">String</td>
        <td style="text-align: left; padding: 10px;">Web RTM token, for supporting chat during sessions</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">sessionId</td>
        <td style="text-align: left; padding: 10px;">Number</td>
        <td style="text-align: left; padding: 10px;">ID of the session</td>
    </tr>
</table>


## Join Session Flowchart

??? abstract "Joining Session Flowchart"
    <iframe frameborder="0" style="width:100%;height:914px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1etG9uI7bzIWvvCVfrMJ0heo-5MdPmujl"></iframe>

<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">Function Name</th>
        <td style="text-align: left; padding: 10px;">joinSession</td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">Function Required Parameters</th>
        <td style="text-align: left; padding: 10px;">
            <ul>
                <li>userId: Number (ID of the user who wants to join the session)</li>
                <li>sessionId: Number (ID of the session)</li>
            </ul>
        </td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">Function Return Parameters</th>
        <td style="text-align: left; padding: 10px;">
            <ul>
                <li>startedSessionDuration</li>
                <li>rtcToken</li>
                <li>rtmToken</li>
                <li>sessionId</li>
            </ul>
        </td>
    </tr>
</table>

------

??? info "`joinSession` Function Path"
    The `joinSession` function is located at the [`lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart&version=GBmaster) path.