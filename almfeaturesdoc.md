## Github

##### Sync Calls:
This library lets you support asynchronous calls through channels

##### Callback Support:
According to the requirement of Planner the best way is to have Asynchronous requests.
The Github Go library have a quite good support to do it through channels and function callback as well.

##### Query:
The query passed is passed as “is:open is:issue user:arquillian author:aslakknutsen”

##### Individual Lookup:
Individual lookup related to public repo we don’t need any ID for key but to access and query the private repository we will be needing the personal access token of the user and to authenticate the app as explained further in the Auth section.

##### Collect Sample Data:
http://www.tegdesign.com/querying-github-api-golang-find-magento-repositories/

##### Auth models:
To use GitHub API from Go we can use github.com/google/go-github package. GitHub, like many other sites, uses OAuth 2.0 protocol for authentication. There are few packages for Go that implement OAuth. read this sample.
Short intro to OAuth for GitHub
* To access private info about the user via the API in your web app you need to authenticate your app against GitHub website.
* First, you need to register your application with GitHub (under Developer applications). You provide description of the app, including a callback url (we’ll get back to that). GitHub creates client id and client secret that you’ll need to provide to OAuth libraries (and keep them secret).
* The flow of OAuth is:
the user is on your website and clicks “login with GitHub” link
you redirect the user to GitHub’s authorization page. In that url you specify desired access level and a random secret
the user authorizes your app by clicking on a link
GitHub redirects to a callback url on your website (which you provided when registering the app with GitHub)
in the url handler, extract “secret” and “code” args
you have to check that the secret is the same as the one you sent to GitHub (security measure that prevents forgery)
* you call another GitHub url to exchange code for access token
Access token is what you use to authenticate your API calls.

##### Notes on callback url
callback url is defined when the ap is registered. This is a problem for testing, because your app might use different hosts for development or production. One option is to create different apps for testing and production, with different callback urls. OAuth protocol allows providing callback url as an argument when calling authorization page (and oauth2 library allows setting it as oauth2.Config.RedirectURL) but GitHub has restrictions and doesn’t allow changing host.
Using personal access token
If you want to access someone else’s GitHub info, you need to authorize your app with GitHub as described above. If you want to access your own account, you can generate a personal access token.
For querying a public repository, no auth level is required


##### Required auth levels for different interactions
* Query: for public repo no auth required, for private repos required
* Lookup: Same as querying but for repository app needs to authenticate the user
* Callback: Same as Query and lookup.


## Trello

##### Sync calls only
Go Library for trello supports Asynchronous calls through channels

##### Callback support
According to the requirement of Planner the best way is to have Asynchronous requests. And using go channels will solve this issue or function callback is also supported by the library.

##### Query
Query is given as the boardId and the list name we want to    search.
>listName: ‘Epic Backlog’,  
>boardId: ‘nlLwlKoz’

##### Individual lookup
Lookup through API key can get all its related credentials as the query we have for a particular user for a boardId and a listName

##### Collect sample data
 Doc for usage of Library https://godoc.org/github.com/VojtechVitek/go-trello    

##### Auth models:
Using the Trello object, we need to authenticate the user.
* This is done with the Trello.authenticate method. This method will automatically trigger the OAuth flow and return back a token. This token will be specific to your Application ID and the user who is executing the flow.
* It's important to understand that the Authentication Token gives application the ability to make calls on behalf of your user, from their context. This token grants access to the authenticated user's boards, lists, Cards, and other settings, depending on the permissions you requested in the authenticate method.

##### Required auth levels for different interactions
* Query : For querying public boards only username is needed. Other than that API key is needed
* Lookup : Same as Querying, API Key and token are needed for the private boards.
* Callback: Username, API key and token are needed.
