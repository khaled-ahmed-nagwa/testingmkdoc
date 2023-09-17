# Fetching HTML Rendering Engine


When an educator log with his account into the application, a function is called to check if the engine exsist locally or not. If not, the engine is downloaded in the background. So in the case of an educator who has started a session immediately after installing the application, a download progress bar is displayed, and he will need to wait for the download to finish before he can start the session.

!!! note "The engine is only downloaded once and stored in local storage."

## Fetch All Engines List

To retrieve a list of engines, we use the `getEngineDetails` function. This function makes an HTTP GET request to our `Engines/GetAll`  API endpoint to retrieve a list of engine details. The function returns the results as a list of “EngineDetailsEntity” objects that containes the name and md5 of engines.  

!!! warning "The list which returned from `Engines/GetAll` endpoint does not include the URL to download the engine, so we need to find a way to get this URL."

<div style="text-align: center;">
    <table width="100%" style="margin: 0 auto;">
        <thead>
            <tr>
                <th>Fetch All Engines API</th>
                <th>                   </th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>API Endpoint</td>
                <td><code>Engines/GetAll</code></td>
            </tr>
              <tr>
                <td>HTTP Method</td>
                <td><code>Get</code></td>
            </tr>
                <tr>
                <td>API Respone</td>
                <td> A List that containes: <br> -  <code>name</code> <br> - <code>md5</code> <td>
            </tr>
        </tbody>
    </table>
</div>

??? abstract "Fetching List of All Engines Flowchart"
    <iframe frameborder="0" style="width:100%;height:764px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1QckVkVoPLv9hloCUY_v7Q2qX_7wkgkhT"></iframe>

??? info "`getEngineDetails` Function Path"
    The `getEngineDetails` function is located at the [`lib/features/sessions/data/data_sources/engine/engine_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/Nagwa%20Sessions%20For%20Educators/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/engine/engine_remote_data_source_impl.dart&_a=contents&version=GBmaster) path.

--------------------------------------

## Fetching Single Engine Details

After fetching a list of all engines, we need to get the **URL** of a specific engine. To do this, we use the `getEngine` function to call the `Engines/GetEngine` API endpoint. We provide the engine name as a parameter to the function, and **the function returns the URL of the engine**.

<div style="text-align: center;">
    <table width="100%" style="margin: 0 auto;">
        <thead>
            <tr>
                <th>Fetch Single Engine API</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>API Endpoint</td>
                <td><code>Engines/GetEngine</code></td>
            </tr>
            <tr>
                <td>HTTP Method</td>
                <td><code>GET</code></td>
            </tr>
            <tr>
                <td>Query Parameter</td>
                <td><code>name</code></td>
            </tr>
            <tr>
                <td>API Response</td>
                <td><code>name</code><br><code>url</code><br><code>md5</code></td>
            </tr>
        </tbody>
    </table>
</div>

??? abstract "Fetching Details of a Single Engine Flowchart "
    <iframe frameborder="0" style="width:100%;height:604px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1st1DcnF0cuIdkqEApNydjA_ziv8a8n0P"></iframe>

??? info "`getEngine` Function Path"
    The `getEngine` function is located at the [`lib/features/sessions/data/data_sources/engine/engine_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/Nagwa%20Sessions%20For%20Educators/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/engine/engine_remote_data_source_impl.dart&_a=contents&version=GBmaster) path.
    