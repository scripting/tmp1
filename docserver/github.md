
# github verbs
## github.connectViaOauth
#### Syntax
github.connectViaOauth ()

#### Params
None

#### What it does
Initiates an Oauth login with GitHub. 

When it's done, you will have an "access token" in local storage on the computer you're using.

The access token allows you to use the other GitHub verbs. 

#### Note
This verb does not work in Electric Drummer yet. But you can use the other GitHub verbs if you copy the access token from web Drummer into localStorage on the Electric Drummer. Here's a <a href="http://scripting.com/drummer/blog/2021/11/11/204101.html?title=githubScriptingInElectricDrummer">blog post</a> that explains what to do step by step.

#### Returns
true

#### Example
undefined

undefined

## github.disconnect
#### Syntax
github.disconnect ()

#### Params
None

#### What it does
Removes the local access token, effectively logging you off GitHub. 

The GitHub verbs will not work on this machine after calling github.disconnect.

#### Returns
true

#### Example
undefined

## github.download
#### Syntax
github.download (username, repository, path)

#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

The third string is a path to the object you want to download. 

#### Returns
A JavaScript object with information about the file, including its contents. 

#### Examples
undefined

undefined

## github.getAccessToken
#### Syntax
github.getAccessToken ()

#### Params
None.

#### Returns
The access token if you're logged in, undefined if not. 

#### Example
undefined

## github.getDirectory
#### Syntax
github.getDirectory (username, repository, path)

#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

The third string is a path to the directory you want a list of. 

#### Returns
A JavaScript object containing information about all the files in the directory. 

#### Examples
undefined

undefined

## github.getUserInfo
#### Syntax
github.getUserInfo (string)

#### Params
The string, which is optional, is the username of the account you want the information of. 

#### Returns
If the username is not provided, github.getUserInfo returns a JavaScript object containing the user info for the current logged-in user. 

#### Examples
undefined

undefined

## github.upload
#### Syntax
github.upload (username, repository, path, data, message)

#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

The third string is a path to the object you want to upload. 

The fourth string is the data of the file to be created by the upload.

The fifth string is the "commit message" that is displayed next to the object in GitHub. It it is not supplied, the server generates a random slogan for the commit message. 

#### Returns
All the information GitHub returns about the upload.

#### Examples
undefined

