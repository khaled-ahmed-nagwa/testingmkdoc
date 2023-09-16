# Getting Stored Users Locally

## Function Flowchart

???+ abstract "`getSavedUsers` Function Flowchart"
    <iframe frameborder="0" style="width:100%;height:1064px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1PR9L-koZaRPocA17bFDFK7afUB3n8GFJ"></iframe>

??? note "The `getSavedUsers` Function Path"
      the `getSavedUsers` is located at the [`lib/features/authentication/data/local/data_sources/authentication_local_data_source_impl.dart`](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/authentication/data/local/data_sources/authentication_local_data_source_impl.dart#:~:text=data_sources-,authentication_local_data_source_impl.dart,-authentication_local_data_source.dart) path.




### `getSavedUsers` Function Return

 <table>
    <tbody>
        <tr>
            <td>Function Return</td>
            <td>
                List of <code>UserEntity</code> objects that contains:
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
        </tr>
    </tbody>
</table>
 