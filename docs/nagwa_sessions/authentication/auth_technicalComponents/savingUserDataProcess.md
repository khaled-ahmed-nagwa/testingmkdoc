# Saving User Data Locally


## Process Steps

To save the user information to local storage, we are using `Hive` to store the information locally.

    1. we first use the `getSavedUsers` function to retrive the stored users locally
    2. Call the `verifyUsername` function from the remote data source to get the list of users that have the same username and password
    3. Add the users from the API response to the users from the local data source, then remove the duplicates from the list of users
    4. Check the index of the user that should be the first user in the list and if it is not the first user, we remove it from the list and add it to the first index
    5. Save the list of users in the local data source

## GetSavedUser

The `getSavedUsers` is used to get the saved users from the local database and return it as a list of UserEntity objects, it uses Hive to open the box and get the users objects from it, then it converts the users object to a list of UserEntity objects. and returns it.

## SaveUsers
The `saveUsers` is used to save the users in the local database, it uses Hive to open the box and save the users object in it. it converts the user's object to a list of JSON objects and saves it in the box. and returns true if the process is done successfully. 

!!! note "More information are coming in the next section regarding how we store and retrive users data locally"