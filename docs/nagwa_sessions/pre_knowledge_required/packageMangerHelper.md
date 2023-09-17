# Package Manager Heplper

The `PackageManagerHelper` class contains the needed information to download and get packages. To simplify the management of engine-related packages in our app, we have developed a package manager helper. This class is responsible for handling tasks such as downloading and managing packages on the local device. In our implementation, we utilize Hive for local storage and Dio for network requests.


## Getting Package

The `getPackage` method is used to download and extract any required packages for starting the session. If the package is already stored locally and its stored MD5 hash matches the MD5 returned from the API, it will not be downloaded again. Instead, it will be obtained from the local path stored in Hive.
!!! note "Hive is used to store package-related data, such as the path, URL, Hive key, MD5 hash, and package ID if available."

### Getting Package Flowchart

??? abstract "Get Package Flowchart"
    <iframe frameborder="0" style="width:100%;height:984px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1RLSYUTTIKBkYSL-FEDdtSrbpkHZ7oCnO"></iframe>

### Get Package Function

<table width="100%" style="border-collapse: collapse;">
    <tr>
        <th style="width: 50%; text-align: left;">Function Name</th>
        <td style="width: 50%; text-align: left;">getPackage</td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Description</th>
        <td style="width: 50%; text-align: left;">This function is used to download a package. It takes the following parameters and returns a boolean value indicating whether the package was successfully downloaded or not.</td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Parameters</th>
        <td style="width: 50%; text-align: left;">
            <strong>packageDetails</strong> (object): An object that contains the following properties:
            <ul>
                <li>url: The URL of the package.</li>
                <li>md5: The MD5 checksum of the package.</li>
                <li>packageId: The identifier of the package.</li>
                <li>hiveKey: The hive key associated with the package.</li>
                <li>localPath: The local path where the package will be saved.</li>
            </ul>
            <strong>onLoadingProgress</strong> (callback): A callback function that is called every time a chunk of data is received during the download.
        </td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Return Value</th>
        <td style="width: 50%; text-align: left;">
            <strong>boolean</strong>: Returns true if the package is successfully downloaded, otherwise returns false.
        </td>
    </tr>
</table>

??? info "`getPackage` Function Path"
    The `getPackage` function is located at the [`lib/core/helpers/package_manager_helper.dar`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/core/helpers/package_manager_helper.dart#:~:text=localization_helper.dart-,package_manager_helper.dart,-path_helper.dart) path.

----------------------------------------------------

## Downloading a Package

 If a package is not stored locally, it is downloaded from the URL provided by the API. The 'downloadPackage' function is responsible for downloading the file from the given URL and saving it to a temporary directory. It also includes an optional progress callback The callback is called every time a chunk of data is received. This function returns a String that represents the path to the downloaded package file.

### Download Package Flowchart

??? abstract "Download Package Flowchart"
    <iframe frameborder="0" style="width:100%;height:634px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1ld5Z_5Rl2v7MI6i_iyW2aqWH7JNHXVgy"></iframe>

### Download Package Function
<table width="100%" style="border-collapse: collapse;">
    <tr>
        <th style="width: 50%; text-align: left;">Function Name</th>
        <td style="width: 50%; text-align: left;">downloadPackage</td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Required Parameters</th>
        <td style="width: 50%; text-align: left;">
            <ul>
                <li>downloadingUrl</li>
                <li>fileName</li>
                <li>onLoadingProgress: callback that is called every time a chunk of data is received.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <th style="width: 50%; text-align: left;">Function Return</th>
        <td style="width: 50%; text-align: left;">String that represents the path of the downloaded file.</td>
    </tr>

</table>



??? info "`downloadPackage` Function Path"
    The `downloadPackage` function is located at the [`lib/core/helpers/package_manager_helper.dar`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/core/helpers/package_manager_helper.dart#:~:text=localization_helper.dart-,package_manager_helper.dart,-path_helper.dart) path.