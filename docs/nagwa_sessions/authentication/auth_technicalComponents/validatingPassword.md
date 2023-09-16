# Login Process (Validating Password)

## Overview

After ensuring the existence & authentication of the username in the [previous step](login_validatingUsername.md###ProcessOverview), the educator will be routed to insert his account password

## Inserting Password Screenshots

??? example "Inserting Password Screenshot"
    <iframe frameborder="0" style="width:100%;height:372px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Insert%20Password%20Screen.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1muTeuGmw27Hw7bLXktg-yFyw31beI_up%26export%3Ddownload"></iframe>

??? example "Incorrect Password Error ⚠️ Screenshot"
    <iframe frameborder="0" style="width:100%;height:512px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1IrxL1ibhUWJMchIFPwf-INrgLw23If6U"></iframe>

## Flowchart

??? abstract "Verify Username & Password Function Flowchart"
    <iframe frameborder="0" style="width:100%;height:832px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G17uMp3KGEVW6tsI8kP7NAELv4HFR-e9eo"></iframe>

## Verify Username & Password API

<table>
  <tr>
    <th>Verify Username & Password API</th>
    <th></th>
  </tr>
  <tr>
    <td>API Endpoint</td>
    <td><code>users/login</code></td>
  </tr>
  <tr>
    <td>HTTP Method</td>
    <td><code>POST</code></td>
  </tr>
  <tr>
    <td>API Required Data</td>
    <td>
      <ul>
        <li><code>loginName </code> </li>
        <li><code>password</code> </li>
        <li><code>portalId</code> </li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>API Response</td>
    <td><code> result</code>  list that contains the following:  
    <ul>
      <li><code>portalID </code> </li>
        <li><code>code</code> </li>
        <li><code>userName</code> </li>
        <li><code>firstName</code> </li>
        <li><code>lastName</code> </li>
        <li><code>accountStatus</code> </li>
         <li><code>status</code> </li>
         <li><code>country</code> </li>
         <li><code>language</code> </li>
         <li><code>phoneNumber</code> </li>
         <li><code>dialCode</code> </li>
         <li><code>roles</code> </li>

    </ul>
    </td>
  </tr>
</table>


 
## `verifyUsername` Function
 
<table>
    <caption>verifyUsername Function</caption>
    <tr>
        <th>Function Required Parameters</th>
        <td>
            <ul>
                <li>userId</li>
                <li>username</li>
                <li>password</li>
                <li>portalId</li>
            </ul>
        </td>

        <td>
            <ul>
                <li>Int</li>
                <li>String</li>
                <li>String</li>
                <li>Int</li>
            </ul>
        </td>

    </tr>
    <tr>
        <th>Function Return Parameters</th>
        <td>
            List of `UserEntity` Object that contain
            <ul>
                <li>userID</li>
                <li>portalId</li>
                <li>username</li>
                <li>firstName</li>
                <li>lastName</li>
                <li>status</li>
                <li>roles</li>
                <li>phoneNumber</li>
                <li>countryPhoneCode</li>
                <li>language</li>
                <li>country</li>
                <li>portalType</li>
                <li>imageUrl</li>
                <li>portalCurrency</li>
                <li>portalTimeZone</li>
            </ul>
        </td>

        <td>
            List of Objects
            <ul>
                <li>Int</li>
                <li>Int</li>
                <li>String</li>
                <li>String</li>
                <li>String</li>
                <li>Int</li>
                <li>List</li>
                <li>String</li>
                <li>String</li>
                <li>String</li>
                <li>String</li>
                <li>Int</li>
                <li>String</li>
                <li>String</li>
                <li>String</li>
            </ul>
        </td>

    </tr>
</table>

??? note "`verifyUsername` Function Path"
      the `verifyUsername` is located at the [`lib/features/authentication/data/remote/data_sources/authentication_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/authentication/data/remote/data_sources/authentication_remote_data_source_impl.dart#:~:text=data_sources-,authentication_remote_data_source_impl.dart,-authentication_remote_data_source.dart) path.

You can notice that inside the `verifyUsername` function, a call to the `_getUserPortalInfo` function is made to retrieve the full list of the user portal information.
 
## Get User Portal Information API 

 <table>
    <caption>Get User Portal Information API</caption>
    <thead>
        <tr>
            <th>Field</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>API Endpoint</td>
            <td>user/UserInfo/$userId</td>
        </tr>
        <tr>
            <td>HTTP Method</td>
            <td>GET</td>
        </tr>
        <tr>
            <td>API Headers</td>
            <td>api-version: 1</td>
        </tr>
        <tr>
            <td colspan="1"><strong>API Response</strong></td>
                        <td>result (containes the following)</td>  

         </tr>
        <tr>
            <td>portalInfo</td>
            <td>A list that contains the following:
            
                <ul>
                    <li>portalId</li>
                    <li>clusterId</li>
                    <li>title</li>
                    <li>subtitleLanguage</li>
                    <li>language</li>
                    <li>country</li>
                    <li>countryTitle</li>
                    <li>logoExtension</li>
                    <li>logoURL</li>
                    <li>videosSubtitle</li>
                    <li>timeZone</li>
                    <li>timeZoneDisplayName</li>
                    <li>isActive</li>
                    <li>priceCountry</li>
                    <li>portalCurrency</li>
                    <li>isPaid</li>
                    <li>type</li>
                    <li>nextType</li>
                    <li>pricePerStudent</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>userInfo</td>
            <td>A list that contains the following:
                <ul>
                    <li>portalID</li>
                    <li>code</li>
                    <li>userName</li>
                    <li>firstName</li>
                    <li>lastName</li>
                    <li>accountStatus</li>
                    <li>status</li>
                    <li>country</li>
                    <li>language</li>
                    <li>phoneNumber</li>
                    <li>countryPhoneCode</li>
                    <li>roles</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>



??? example "Response From the `user/UserInfo/$userId` API"
    ```json
        {
          "success": true,
          "resultCode": 200,
          "errorCode": null,
          "result": {
              "portalInfo": {
                  "portalId": 129139714843,
                  "clusterId": 0,
                  "title": "Nagwa Classes",
                  "subtitleLanguage": null,
                  "language": "ar",
                  "country": "eg",
                  "countryTitle": "مصر",
                  "logoExtension": ".png",
                  "logoURL": "https://s3.amazonaws.com/files-portals.nagwa.com/images/portals-logo/129139714843.png",
                  "videosSubtitle": null,
                  "timeZone": "Arab Standard Time",
                  "timeZoneDisplayName": "(UTC+03:00) Arabian Standard Time (Riyadh)",
                  "isActive": "1",
                  "priceCountry": "eg",
                  "portalCurrency": "EGP",
                  "isPaid": false,
                  "type": 4,
                  "nextType": null,
                  "pricePerStudent": 20.00
              },
              "userInfo": {
                  "portalID": 129139714843,
                  "code": 496182456783,
                  "userName": "teacher.dina.ali@gmail.com",
                  "firstName": "Teacher Dina",
                  "lastName": "Ali",
                  "accountStatus": "Active",
                  "status": 1,
                  "country": "eg",
                  "language": "ar",
                  "phoneNumber": null,
                  "countryPhoneCode": null,
                  "gradeId": 0,
                  "token": null,
                  "roles": [
                      "Teacher"
                  ]
              }
          },
          "errors": []
      }
    
    ```