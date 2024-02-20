## Spotify - API Testing

### Introduction
Spotify Web API enables the creation of applications that can interact with Spotify's streaming service, such as retrieving content metadata, getting recommendations, creating and 
managing playlists, or controlling playback.

The Spotify Web API provides a wide range of functionality for developers, including:
- Retrieve data from your favourite artist, album or show.
- Search for Spotify content.
- Control and interact with the playback, play and resume, Seek to a position or retrieve your queue.
- Manage your personal library, by creating a new playlist and adding your favourite tracks to it.
- Get recommendations based on the music you listen the most.
- And much more! You can find a complete list of available endpoints in the API Reference.

### Getting started with Web API - request an access token
The access token is a string which contains the credentials and permissions that can be used to access a given resource (e.g artists, albums or tracks) or user's data (e.g your profile or your playlists).
1. Firstly, you need to create a new Spotify account.

2. Login to the Spotify Developer Dashboard, click on the Create an app button and enter the following information(just example):
- App Name: My App
- App Description: API testing
- Redirect URL: `http://itfactory/callback`
- Finally, check the Developer Terms of Service checkbox and tap on the Create button. This app provides the Client ID and Client Secret needed to request an access token.

3. Get your Client_ID and Client Secret:
- Go to the Dashboard
- Click on the name of the app you have just created (My App)
- Click on the Settings button -> The Client ID can be found here. The Client Secret can be found behind the View client secret link.

4. Open the Postman app, creat a new collection with the name Spotify, and create a new POST request:
- In the Access Token URL field enter the link `https://accounts.spotify.com/api/token`
- on the Body tab set the application/x-www-form-urlencoded value, and fill in the key-value parameter section with the following details:
  - Content-Type = application/x-www-form-urlencoded
  - grant_type = client_credentials
  - client_id = 'your-client-id'
  - client_secret = 'your-client-secret'
       
The response will return an access token valid for 1 hour.

### Request authorization
In order to get/update/delete information about a user, we need to get an authorization. Authorization refers to the process of granting a user or application access permissions to Spotify data and features.
The access to the protected resources is determined by one or several scopes. Scopes enable your application to access specific functionality (e.g. read a playlist, modify your library or just streaming) on
behalf of a user. The set of scopes you set during the authorization, determines the access permissions that the user is asked to grant.
Once the authorization is granted, the authorization server issues an access token, which is used to make API calls on behalf the user or application.
Open the Postman app and create a new POST request:
- In the Access Token URL field enter the link `https://accounts.spotify.com/api/token`
- Click on authorization and select from the dropdown type OAuth 2.0 and fill in the fields below
- Callback URL -> the link you used when creating your app in Dashboard (example: `http://itfactory/callback`)
- Auth URL -> `https://accounts.spotify.com/authorize`
- Access Token URL -> `https://accounts.spotify.com/api/token`
- Client ID -> your-client-id
- Client Secret -> your-client-secret
- Scope -> user-read-private user-library-read user-library-modify
- Click on the GET NEW ACCESS TOKEN button
The token has been created, the response will return an authorization token valid for 60 minutes.


### Types of requests
HTTP methods supported by this API are GET, POST, PUT, PATCH, and DELETE. In this section, you can explore and perform tests on various types of operations supported by the Spotify Web API. 
Some examples include:
- **GET**	-> Retrieves resources - information about artist, albums, playlist,etc
- **POST** ->	Creates resources - new playlists, add tracks, etc
- **PUT** ->	Changes and/or replaces resources or collections - update existing data,modify playlists, etc
- **DELETE** ->	Deletes resources - remove playlists, tracks, etc

### Tests used for validation
I send responses to some endpoints, to get information for an album, for multiple albums identified by their Spotify IDs, information about an album’s tracks, information for a single artist identified by their
unique Spotify ID, information for several artists based on their Spotify IDs, detailed profile information about the current user (including the current user's username), a list of the albums saved in the 
current Spotify user's 'Your Music' library, save and remove one or more albums to the current user's 'Your Music' library, and check if one or more albums is already saved in the current Spotify user's 
'Your Music' library.

- `https://api.spotify.com/v1/albums/{id}`
- `https://api.spotify.com/v1/artists/{id}`
- `https://api.spotify.com/v1/artists/{id}/albums`
- `https://api.spotify.com/v1/artists/{id}/top-tracks`
- `https://api.spotify.com/v1/albums/{id}/tracks`
- `https://api.spotify.com/v1/me`
- `https://api.spotify.com/v1/me/albums`

### Tests performed

#### 1. Create token
   - HTTP method for request: POST
   - Request description: Create a token valid for 1 hour
   - Response status code: 200 OK
     Below you can find a screenshot of the JavaScript tests:
     ![createtoken](https://github.com/anettabako91/postman/blob/main/createtoken_tests_results.png)

#### 2. Get an artist

   - HTTP method for request: GET
   - Request description: Get Spotify catalog information for a single artist identified by their unique Spotify ID.
   - Response status code: 200 OK
     
     API request and response:
     
     ![getanartist](https://github.com/anettabako91/postman/blob/main/getanartist_get.png)
  
   
     JavaScript Tests:
     
     ![getanartist_tests](https://github.com/anettabako91/postman/blob/main/getanartist_tests.png)
     
     ![getanartist_results](https://github.com/anettabako91/postman/blob/main/getanartist_results.png)

#### 3. Get current user's profile

   - HTTP method for request: GET
   - Request description: Get detailed profile information about the current user (including the current user's username).
   - Response status code: 200 OK
  
     API request and response:
     
     ![getuserprofile](https://github.com/anettabako91/postman/blob/main/getuser'sprofile_get.png)
     
     JavaScript Tests:
     
     ![getuserprofile_tests](https://github.com/anettabako91/postman/blob/main/getuser'sprofile_tests.png)
     
     ![getuserprofile_results](https://github.com/anettabako91/postman/blob/main/getuser'sprofile_results.png)

#### 4. Get user's saved albums

   - HTTP method for request: GET
   - Request description: Get a list of the albums saved in the current Spotify user's 'Your Music' library.
   - Response status code: 200 OK

     JavaScript Tests:

     ![getuser'ssavedalbums_tests](https://github.com/anettabako91/postman/blob/main/getuser'ssavedalbums_tests.png)
     
     ![getuser'ssavedalbums_results](https://github.com/anettabako91/postman/blob/main/getuser'sprofile_tests.png)
  
#### 5. Save album for current user

   - HTTP method for request: PUT
   - Request description: Save one or more albums to the current user's 'Your Music' library.
   - Response status code: 200 OK

     API request and response

     ![savealbumforcurrentuser_put](https://github.com/anettabako91/postman/blob/main/save_albumforcurrentuser_put.png)

     JavaScript Tests:

     ![savealbumforcurrentuser_tests](https://github.com/anettabako91/postman/blob/main/savealbumforcurrentuser_tests.png)
     
     ![savealbumforcurrentuser_results](https://github.com/anettabako91/postman/blob/main/savealbumforcurrentuser_results.png)
     
#### 6. Delete user's saved album

   - HTTP method for request: DELETE
   - Request description: Remove one or more albums from the current user's 'Your Music' library.
   - Response status code: 200 OK
  
     API request and response

     ![deleteuser'ssavedalbum_delete](https://github.com/anettabako91/postman/blob/main/deleteuser'ssavedalbums_delete.png)

#### 7. Check user's saved album

   - HTTP method for request: GET
   - Request description: Check if one or more albums is already saved in the current Spotify user's 'Your Music' library.
   - Response status code: 200 OK
  
     API request and response

     ![checkuser'ssavedalbum](https://github.com/anettabako91/postman/blob/main/checkuser'ssavedalbum_get.png)

     JavaScript Tests

     ![checkuser'ssavedalbum_testandresult](https://github.com/anettabako91/postman/blob/main/checkuser'ssavedalbum_tests_results.png)
  
#### 8. Check user's saved album with a Spotify ID that is not among the saved ones

   - HTTP method for request: GET
   - Request description: Check if the response is false if an album is not saved in the current Spotify user's 'Your Music' library.
   - Response status code: 200 OK
  
     API request and response

     ![checkuser'ssavedalbum_invalidid](https://github.com/anettabako91/postman/blob/main/checkuser'ssavedalbum_invalidid_request.png)

     JavaScript Tests

     ![checkuser'ssavedalbuminvalidid_testandresult](https://github.com/anettabako91/postman/blob/main/checkuser'ssavedalbum_invalidid_testsandresults.png)


#### 9. Create playlist

  - HTTP method for request: POST
  - Request description: Create a playlist for a Spotify user. (The playlist will be empty until you add tracks.) Each user is generally limited to a maximum of 11000 playlists
  - Response status code: 201 Created
  
  API request and response

  ![createnewplaylist](https://github.com/anettabako91/postman/blob/main/createplaylist_post.png)

  JavaScript Tests

  ![createnewplaylist_tests](https://github.com/anettabako91/postman/blob/main/createplaylist_tests.png)
  ![createnewplaylist_results](https://github.com/anettabako91/postman/blob/main/createplaylist_testresults.png)

  After creating one more new playlist, I also found a bug - the album description was not saved according to the data provided by me. You can see below the new request, tests and results

  ![createnewplaylist](https://github.com/anettabako91/postman/blob/main/createplaylist_newrequest.png)

  ![testsandresults](https://github.com/anettabako91/postman/blob/main/createnewplaylist_testandresult.png)
      
  
#### 10. Change playlist details

  - HTTP method for request: PUT
  - Request description: Change a playlist's name and public/private state. (The user must, of course, own the playlist.)
  - Response status code: 200 OK
   
  API request and response for getting playlist details

  ![getdetails](https://github.com/anettabako91/postman/blob/main/getplaylist_old.png)

  API request and response for changing playlist details

  ![changedetails](https://github.com/anettabako91/postman/blob/main/changeplaylistdetails.png)

  API request and response for getting the updated details

  ![newdetails](https://github.com/anettabako91/postman/blob/main/getplaylistnew.png)

  JavaScript Tests

  ![testsandresults](https://github.com/anettabako91/postman/blob/main/changeplaylistdetails_testsandresults.png)

### Execution report for the Spotify collection

Below you can find the execution report that was generated through the Postman collection runner:

![runcollection](https://github.com/anettabako91/postman/blob/main/runcollection.png)

[Here](https://github.com/anettabako91/postman/blob/main/SpotifyAPI.postman_test_run.json) you can find the exported results in json file.

The collection was also run through newman directly from the terminal, you can see the results below: (in the meantime the test regarding the response time in 'Change playlist details' passed and it is no longer an error)

![newman_run](https://github.com/anettabako91/postman/blob/main/runcollection_newman.png)

### Conclusion

A comprehensive set of 37 tests was created, covering various functionalities in the Spotify Web API. Tests included GET, POST, PUT and DELETE HTTP methods for an extensive coverage.
All the collection was successfully executed using Postman's runner and Newman. Detailed execution report was generated, providing information about each test case's perfomance and status.


