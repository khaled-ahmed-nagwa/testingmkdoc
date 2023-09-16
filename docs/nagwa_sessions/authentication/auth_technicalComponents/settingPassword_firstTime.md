# Setting Password For The First Time 1️⃣

When an educator logs into the application for the first time after registering, they will need to enter their email address and initial password. Once their email address and password are verified, they will be prompted to create a new password that will become their account password.

??? info "Setting Password For the First Time Screen"
    <iframe frameborder="0" style="width:100%;height:602px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Completing%20Creation%20Account%20Process%20(Setting%20Password).drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D11cRdu6v3Eyut5xlw1Y4uK5oVPKzsrfsN%26export%3Ddownload"></iframe>

## **Setting Password API**

| **Resetting Password API**     |                     |
|--------------------------------|---------------------|
| **API Endpoint**               | `users/reset-password-confirmation` |
| **HTTP Method**                | `POST` |
| **API Required Data** |  `token` <br>  `password` |
