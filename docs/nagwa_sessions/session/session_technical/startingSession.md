# Starting Session

When it’s session time, the start button located on the session card becomes active, and the  educator can click the "Start" button to begin the session. Once they click the button, we call our “sessions/start” endpoint to start the session and make it visible to the class students so that they can join the session.


## Starting Session API
<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
        <tr>
            <th style="text-align: left; padding: 10px;">Starting Session API</th>
            <td style="text-align: left; padding: 10px;"></td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Endpoint</th>
            <td style="text-align: left; padding: 10px;">sessions/start</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">HTTP Method</th>
            <td style="text-align: left; padding: 10px;">POST</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Required Data</th>
            <td style="text-align: left; padding: 10px;">
                <ul>
                    <li>educatorId</li>
                    <li>sessionId</li>
                </ul>
            </td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Headers</th>
            <td style="text-align: left; padding: 10px;">api-version:6</td>
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

---------------------

## Starting Session Flowchart

??? abstract "Start Session Flowchart"
    <iframe frameborder="0" style="width:100%;height:674px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1o17h3xDyChuyljgdglymFuCZmfIxYc7K"></iframe>


### Starting Session Function 

<table width="100%" style="border-collapse: collapse;">
    <tr>
        <th style="text-align: left; padding: 10px;">Function Name</th>
        <td style="text-align: left; padding: 10px;">startSession</td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">Function Required Parameters</th>
        <td style="text-align: left; padding: 10px;">
            <ul>
                <li>educatorId</li>
                <li>sessionId</li>
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

???+ failure "If the class has no students enrolled, then the educator cannot start the session"
    <iframe frameborder="0" style="width:100%;height:542px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1qIFCq9VEZQkqy9FSrNR9jZzRfDBYk-N_"></iframe>


??? info "`startSession` Function Path"
    The `startSession` function is located at the [`ib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart&version=GBmaster) path.


## Creating Session Notifier
Upon calling the start API, a call to `createSessionNotifier` method is used to create a notifier for the session in progress it requires the (`educatorId`, `sessionId`) to create the notifier.

1. It creates an instance of the collection "sessions_in_progress" in the Firestore database.
2. It creates a document name equal to the (educatorId) and sets the data of the document to the `sessionNotifierParams` which are the (educatorId, sessionId and the status of the session) which in this case is `in_progress`.


