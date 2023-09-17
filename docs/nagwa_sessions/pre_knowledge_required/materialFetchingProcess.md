# Fetching Material Process 

## Fetching URL of the Session Material

After Checking the unavailability of the material on the local device, we start the process of downloading it, First, we need to retrieve the material specified in the session; this is done by using the `getDownloadMaterialUrl` function, which is responsible for calling our session endpoint and retrieving the URL of associated material as a string, based on the `fileId` and `userId` of the session material.


<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
        <tr>
            <th style="text-align: left; padding: 10px;">API Endpoint</th>
            <td style="text-align: left; padding: 10px;">sessions/downloadurl</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">HTTP Method</th>
            <td style="text-align: left; padding: 10px;">Get</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Headers</th>
            <td style="text-align: left; padding: 10px;">api-version: "6"</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Query Parameters</th>
            <td style="text-align: left; padding: 10px;">
                <ul>
                    <li>fileID</li>
                    <li>userID</li>
                </ul>
            </td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">API Response</th>
            <td style="text-align: left; padding: 10px;">url</td>
        </tr>
    </table>
</div>

### Getting The URL Of Session Material Function



??? abstract "Fetch URl of Session Material Flowchart"
    <iframe frameborder="0" style="width:100%;height:464px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1bbGfdEzf6GFrH9-YoAvhmt4E36zOZva5"></iframe>



<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">
        <tr>
            <th style="text-align: left; padding: 10px;">Function Name</th>
            <td style="text-align: left; padding: 10px;">getDownloadMaterialUrl</td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">Required Parameters</th>
            <td style="text-align: left; padding: 10px;">
                <ul>
                    <li>DownloadSessionParams</li>
                    <li>fileId</li>
                    <li>userId</li>
                    <li>sessionId</li>
                </ul>
            </td>
        </tr>
        <tr>
            <th style="text-align: left; padding: 10px;">Function Return</th>
            <td style="text-align: left; padding: 10px;">String that represents the URL</td>
        </tr>
    </table>
</div>

??? info "`getDownloadMaterialUrl` Function Path"
    The `getDownloadMaterialUrl` function is located at the [`lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart#:~:text=sessions-,sessions_remote_data_source_impl.dart,-sessions_remote_data_source.dart) path.

## Download Session Material 

After Getting the download URL of the material from the previous step, our next step will be to start downloading and saving the material locally.

For that, you can find that the `downloadSessionMaterial` function is responsible for downloading the session material. This is done by:

1. Calling the `getDownloadMaterialUrl` function to get the download URL of the session material.
   
2. Then the download URL is used to download the session material using the dio package.
      -  While downloading the session material, the onLoadingProgress function is called to update the download progress. and the function saves the downloaded session material in the temporary directory of the device
3. Finallt, The function returns the path of the downloaded session material.

### Download Session Material Flowchart

??? abstract "Download Flowchart"
    <iframe frameborder="0" style="width:100%;height:494px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1QqlrAZkvw_LQBJxG9emceIOkCBB6c4JS"></iframe>


<table width="100%" style="border-collapse: collapse;">
    <tr>
        <th style="width: 50%; text-align: left;">Function Name</th>
        <td style="width: 50%; text-align: left;">downloadSessionMaterial</td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Required Parameters</th>
        <td style="width: 50%; text-align: left;">
            <ul>
                <li><code>DownloadSessionParams</code>: contains the <code>fileId</code> and <code>userId</code> of the session material.</li>
                <li><code>Function(double progress)</code>: a callback function that takes a double value as a parameter. It's used to update the progress of the download.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Function Return</th>
        <td style="width: 50%; text-align: left;">String that describes the material local path</td>
    </tr>
</table>



??? info "`downloadSessionMaterial` Function Path"
    The `getDownloadMaterialUrl` function is located at the [`lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/data/data_sources/sessions/sessions_remote_data_source_impl.dart#:~:text=sessions-,sessions_remote_data_source_impl.dart,-sessions_remote_data_source.dart) path.