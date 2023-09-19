# Login Process: Validating Username

## Process Overview

After logging into the application, the user will be routed to the username (email) input screen. This is the first screen that the user sees when they open the app for the first time or after logging out. The page asks the user to enter their username, and after clicking the `Continue` button, it will check the validity of the entered username.

- If the entered username is not registered to the app, an error message will be displayed informing the user that the email is not registered on the portal.
- If a student username was entered, an error message will be shown indicating that this account is not authorized to access the app.
- If the account is already logged in to the app, an alert dialog will be shown that asks the educator if he wants to switch to that account.

!!! note "Checking If User Exsits 🔍 ?"

    Checking if an account exists on a local device is done by calling the `isUserExistByUsername` method,
    which checks the local storage (Hive) for the entered username.

## Username Verification Function Flowchart

??? abstract "Username Verification Flowchart 👨‍💻"
    <iframe frameborder="0" style="width:100%;height:784px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1nkVlIPxS3NM1A49sghDv6IWSwSlzI4Qw"></iframe>



<table border= 10px>
  <caption><code>usernameLogin</code> Function</caption>
  <thead>
    <tr>
      <th>Variable</th>
      <th>Parameters</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Function Required Parameters</td>
      <td><code>username</code></td>
      <td>String</td>
    </tr>
    <tr>
      <td>Function Return Parameters</td>
      <td>
        - <code>portalID</code><br>
        - <code>userID</code><br>
        - <code>needPasswordReset</code><br>
        - <code>resetToken</code><br>
        - <code>isPhoneVerified</code><br>
        - <code>status</code><br>
        - <code>roles</code>
      </td>
      <td>
        String<br>
        int<br>
        Bool<br>
        String<br>
        Bool<br>
        int<br>
        List of Strings
      </td>
    </tr>
  </tbody>
</table>


 
## Username Verification API
 
 <table>
  <caption>API Endpoint Details</caption>
  <thead>
    <tr>
      <th>Category</th>
      <th>Name</th>
      <th>Data Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>API Endpoint</td>
      <td>users/verification</td>
      <td></td>
    </tr>
    <tr>
      <td>API Query Parameters</td>
      <td>username</td>
      <td></td>
    </tr>
    <tr>
      <td>HTTP Method</td>
      <td>GET</td>
      <td></td>
    </tr>
    <tr>
      <td rowspan="11">API Response</td>
      <td>result</td>
      <td>A list that contains the following</td>
    </tr>
    <tr>
      <td> - portalID</td>
      <td>int</td>
    </tr>
    <tr>
      <td>- userID</td>
      <td>int</td>
    </tr>
    <tr>
      <td>- needPasswordReset</td>
      <td>bool</td>
    </tr>
    <tr>
      <td>- resetToken</td>
      <td>string</td>
    </tr>
    <tr>
      <td>- isPhoneVerified</td>
      <td>bool</td>
    </tr>
    <tr>
      <td>- status</td>
      <td>int</td>
    </tr>
    <tr>
      <td>- roles</td>
      <td>list</td>
    </tr>
    <tr>
      <td>- accountStatus</td>
      <td>String</td>
    </tr>
    <tr>
      <td>- suffix</td>
      <td>String</td>
    </tr>
    <tr>
      <td>- portalType</td>
      <td>int</td>
    </tr>
  </tbody>
</table>

!!! example "Allowed Roles to Access The Application"
    You may have noticed that the username verification API returns a 'roles' list. This list contains the roles associated with the username within the portal. Currently, the allowed roles are limited to ```' teacher', 'tutor', and 'assistant' ``` Any other role will not grant access to continue logging into the application.


## Login Screenshots

??? info "Inserting Username Screen"
    <iframe frameborder="0" style="width:100%;height:552px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Inserting%20Username%20Screen.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D11Bgz435T5lFyEso23yVLZYY9_H-HNYll%26export%3Ddownload"></iframe>

??? info "Different Validation Messages"
    <iframe frameborder="0" style="width:100%;height:542px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Different%20Validation%20Messages.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1nd6Cg1oWdhKJcbr0yMkMEt8fr3BqjDYp%26export%3Ddownload"></iframe>
