# Canceling Session

!!! danger "Canceling Session Is Not Currently Enabled"
    Currently , the cancel session feature is not included in the application

The educator can cancel the session anytime before it starts and it will be removed from the student session list 


??? abstract "Cancel Session Button"
    <iframe frameborder="0" style="width:100%;height:372px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1S2jc3n5cS6xD_oempYK-c4loIEl5IvD1"></iframe>


## Cancel Session API 

<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: center; padding: 10px;">Canceling Session API</th>
        <td width="30%"></td>
        <td></td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">API Endpoint</th>
        <td>sessions/cancel</td>
        <td></td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">HTTP Method</th>
        <td>POST</td>
        <td></td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">API Required Data</th>
        <td>
            <ul>
                <li>educatorId</li>
                <li>sessionId</li>
            </ul>
        </td>
        <td></td>
    </tr>
    <tr>
        <th style="text-align: left; padding: 10px;">API Headers</th>
        <td>api-version: 6</td>
        <td></td>
    </tr>
</table>


??? info "`cancelSession` Function Path"
    The `cancelSession` function is located at the [`lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart&version=GBmaster) path.