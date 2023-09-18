# Ending Session

Once the educator finishes his session, he can press the end session button, which will end the session and inform all students that the session has ended.

??? abstract "End Session Button Screen"
    <iframe frameborder="0" style="width:100%;height:476px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1BzRXih_Q8be8ayPzJTM5tm8utA4qx7pm"></iframe>


## End Session API
<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">Ending Session API</th>
        <td></td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">API Endpoint</th>
        <td>sessions/end</td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">HTTP Method</th>
        <td>POST</td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">API Required Data</th>
        <td>
            <ul>
                <li>sessionId</li>
                <li>educatorId</li>
            </ul>
        </td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">API Headers</th>
        <td>api-version: 6</td>
    </tr>
</table>


## Updating Session Status

We need to update the data in Firestore; `updateSessionStatus` is responsible for that:
- it accesses a collection in the Firestore called `sessions_in_progress`.
- if the sessionStatus is ended, it will create a document name equal to the educatorId and set the data of the document to empty map.
  
- if the `sessionStatus` is ended, it will create a document name equal to the `educatorId` and set the data of the document to empty map.
  
!!! question "Why we need to update the session status in firebase?"
    We rely on firebase to listen to any changes in session wheter it's started / ended so that we can update the class sessions list in real-time without any delays.




??? info "`endSession` Function Path"
    The `endSession` function is located at the [`lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart&version=GBmaster) path.