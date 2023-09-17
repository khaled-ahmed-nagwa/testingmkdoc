# Upcoming and Running Sessions List

The educator has access to a centralized location where he can view a list of currently running and upcoming sessions. This list provides essential details such as the session name, date, and duration for each session.

??? abstract "Currently Running & Upcoming Sessions List Screen"
    <iframe frameborder="0" style="width:100%;height:342px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1uQN6ZUYZMBDspYHS8elasCcCgDmzMSMf"></iframe>

# Retrive Sessions List Flowchart

??? abstract "Getting Session’s List Flowchart"
    <iframe frameborder="0" style="width:100%;height:704px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G11m2W8uisabI7b9aShj4No0Z9qsAsdtJF"></iframe>

The `getSessions` function plays a crucial role in fetching a list of sessions that the student had registered for from our API `sessions/open`. This function communicates with the API and retrieves the necessary data about the sessions associated with the student's account. Once the data is obtained, it can be used to populate the centralized view, showing the educator all the relevant details.

<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
    <tr>
        <th style="width: 40%; text-align: left;">Function Name</th>
        <td style="width: 60%; text-align: left;">getSessions</td>
    </tr>
    <tr>
        <th style="width: 40%; text-align: left;">Function Required Parameters</th>
        <td style="width: 60%; text-align: left;">userId</td>
    </tr>
    <tr>
        <th style="width: 40%; text-align: left;">Function Return</th>
        <td style="width: 60%; text-align: left;">List of "sessions" that contains:
            <ul>
                <li>sessionId</li>
                <li>educatorId</li>
                <li>educatorName</li>
                <li>title</li>
                <li>startDate</li>
                <li>statusId</li>
                <li>statusName</li>
                <li>durationInMinutes</li>
                <li>subjectId</li>
                <li>subjectName</li>
                <li>fileId</li>
                <li>sessionProvider</li>
                <li>extension</li>
                <li>iconUrl</li>
                <li>studentsCount</li>
            </ul>
        </td>
    </tr>
</table>
</div>

## Fetch Sessions List API

<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
        <tr>
            <th style="text-align: left; padding: 10px;">API Endpoint</th>
            <td style="text-align: left; padding: 10px;">sessions/open</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">HTTP Method</th>
            <td style="text-align: left; padding: 10px;">GET</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Headers</th>
            <td style="text-align: left; padding: 10px;">api-version: "6"</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Query Parameters</th>
            <td style="text-align: left; padding: 10px;">
                <ul>
                    <li>userId</li>
                    <li>pageSize [Number of returned sessions (set it to a big number, ex. 100)]</li>
                    <li>pageNumber [Start index (set it to 1)]</li>
                </ul>
            </td>
        </tr>
    </table>
</div>

### Fetch Session List API Response

<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
        <caption style="font-size: 1.5em; font-weight: bold;">API Response (sessions/open)</caption>
        <tr>
            <th style="text-align: left; padding: 10px;">Key</th>
            <th style="text-align: left; padding: 10px;">Description</th>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">sessionId</td>
            <td style="text-align: left; padding: 10px;">Number that represents the ID of the session</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">educatorId</td>
            <td style="text-align: left; padding: 10px;">Number that represents the ID of the educator</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">title</td>
            <td style="text-align: left; padding: 10px;">String that represents the title of the session</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">educatorName</td>
            <td style="text-align: left; padding: 10px;">String that represents educator name</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">startDate</td>
            <td style="text-align: left; padding: 10px;">Date that represents the start date of the session</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">studentsCount</td>
            <td style="text-align: left; padding: 10px;">Number of the students who can attend session</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">studentsCountUnit</td>
            <td style="text-align: left; padding: 10px;"></td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">statusId</td>
            <td style="text-align: left; padding: 10px;">Number that represents session status Id</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">statusName</td>
            <td style="text-align: left; padding: 10px;">String represents the status of session ex. scheduled, In-Progress</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">statusNameLocalized</td>
            <td style="text-align: left; padding: 10px;"></td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">durationInMinutes</td>
            <td style="text-align: left; padding: 10px;">Number that represents session planned duration in minutes</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">durationInMinutesUnit</td>
            <td style="text-align: left; padding: 10px;"></td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">subjectId</td>
            <td style="text-align: left; padding: 10px;">Number that represents the subject ID</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">subjectName</td>
            <td style="text-align: left; padding: 10px;">String that represents subject name which session assigned to</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">sessionProvider</td>
            <td style="text-align: left; padding: 10px;">String represents session webRTC provider, in our case, its Agora</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">extension</td>
            <td style="text-align: left; padding: 10px;">Number represents the additional time that can be added to a session if the default duration is completed.</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">iconUrl</td>
            <td style="text-align: left; padding: 10px;">String that represents the session image URL</td>
        </tr>
        <tr>
            <td style="text-align: left; padding: 10px;">fileId</td>
            <td style="text-align: left; padding: 10px;">Number that represents the ID of the file that contains session materials (zip file id)</td>
        </tr>
    </table>
</div>
