
# clock verbs
## clock.now
#### Syntax
clock.now ()

#### Returns
A JavaScript date object with the current date and time. 

#### Example
clock.now ()

> *Tue Mar 16 2021 14:31:39 GMT-0400 (Eastern Daylight Time)*

## clock.waitSeconds
#### Syntax
clock.waitSeconds (number)

#### Parameters
The number is the number of seconds it waits. It doesn't have to be a whole number (integer). 

#### Returns
The number of seconds it waited. 

#### Notes
The waiting is done via a JavaScript <a href="https://www.w3schools.com/jsref/met_win_settimeout.asp">setTimeout</a> call. 

#### Examples
clock.waitSeconds (1)

> *1.005*

clock.waitSeconds (1.3)

> *1.3*

clock.waitSeconds (random (1, 3))

> *2.005*


# date verbs
## date.convertToTimeZone
#### Syntax
date.convertToTimeZone (date, string)

#### Params
The date param is the date you want to convert to a different time zone. 

The string says how far from GMT and in what direction the other time zone is. For example -5 would be the string for the east coast of the United States, meaning five hours earlier than GMT. "0" is GMT. This param is optional, if not specified it is "0".

The string param does not have to represent a whole hour. For example Central Indian Time is "+5:30".

#### Returns
The date, expressed in the indicated time zone. 

If x is a date returned by this routine, you can use the JavaScript date functions to get components of a time, getHours, getMinutes, etc and they will return the correct values for the indicated time zone.

This is a core routine for building blogs that might be published by software running in a time zone different from the author of the blog. 

#### Examples
date.convertToTimeZone (clock.now (), "+5:30").toLocaleString ()

> *11/15/2021, 8:45:29 PM*

## date.dayGreaterThanOrEqual
#### Syntax
date.dayGreaterThanOrEqual (d1, d2)

#### Params
Both parameters are JavaScript date objects. 

#### Returns
true if the first date is on the same day as the second, or if the first date is later than the second. 

#### Notes
This verb is useful in determining which version of software you're running, if you have the publication date of a new version. Also useful to see if a timer has expired. 

#### Example
date.dayGreaterThanOrEqual (clock.now (), "November 22, 2018")

> *true*

## date.netStandardString
#### Syntax
date.netStandardString (date)

#### Params
date is a JavaScript date object.

#### Returns
A <a href="https://tools.ietf.org/html/rfc822">RFC 822</a> version of the date. 

#### Notes
This is the format that's required for RSS feeds, OPML files and mail protocols. 

It's a human and machine readable way of expressing of dates. 

#### Examples
date.netStandardString (clock.now ())

> *Sun, 14 Mar 2021 16:28:56 GMT*

date.netStandardString ("12/5/97; 9:03:15 PM")

> *Sat, 06 Dec 1997 04:03:15 GMT*

## date.sameDay
#### Syntax
date.sameDay (d1, d2)

#### Params
Both parameters are JavaScript date objects. 

#### Returns
true if the dates are on the same day, false otherwise.

#### Examples
date.sameDay ("March 12, 2021", "February 12, 2021")

> *false*

date.sameDay ("March 12, 2021", "March 12, 2021")

> *true*

## date.sameMonth
#### Syntax
date.sameMonth (d1, d2)

#### Params
Both parameters are JavaScript date objects. 

#### Returns
true if the dates are in the same month, false otherwise.

#### Examples
date.sameMonth ("March 12, 2021", "February 12, 2021")

> *false*

date.sameMonth ("March 12, 2021", "March 30, 2021")

> *true*

## date.secondsSince
#### Syntax
date.secondsSince (date)

#### Params
date is a JavaScript date object.

#### Returns
The number of seconds since the date. 

#### Notes
Useful when you want to know how long something took. 

#### Example
date.secondsSince ("March 14, 2020")

> *31580389.57*

## date.tomorrow
#### Syntax
date.tomorrow (date)

#### Params
date is a JavaScript date object.

#### Returns
The result of adding 24 hours from the date.

#### Example
date.tomorrow (clock.now ())

> *Mon Mar 15 2021 12:21:22 GMT-0400 (Eastern Daylight Time)*

## date.yesterday
#### Syntax
date.yesterday (date)

#### Params
date is a JavaScript date object.

#### Returns
The result of subtracting 24 hours from the date.

#### Example
date.yesterday (clock.now ())

> *Sat Mar 13 2021 11:21:02 GMT-0500 (Eastern Standard Time)*


# daytona verbs
## daytona.ping
#### Syntax
daytona.ping (urlOutline, collection)

#### Params
The first param is the URL of a public outline containing the content you want to be included in your Daytona index.

The second param is optional and defaults to "drummeruser." For most users that's the only value that will work.

#### What it does
Queues an indexing of the outline. It will usually take a minute or more for Daytona to index the outline. 

#### Returns
A message saying it worked, if it did. 

#### Note
Simply updating the outline is enough to get it to be reindexed, so in most cases you will not have to do the ping from a script.

#### Example
daytona.ping ("http://drummer.scripting.com/cluelessnewbie/blog.opml")

> *all is good*

## daytona.query
#### Syntax
daytona.query (query, collection)

#### Params
The first param is a string that contains the string you want to search for.

The second param is the collection you want to search in. It can be scriptingnews, drummerdocs or drummeruser.  It's optional, if not present the default value is drummeruser.

#### Returns
The result of the query in a JavaScript object.

#### Example
daytona.query ("BBC")

> *[*

## daytona.resetMyIndex
#### Syntax
daytona.resetMyIndex (collection)

#### Param
The param is the collection you want to search in. It can be scriptingnews, drummerdocs or drummeruser. It's optional, if not present the default value is drummeruser. For most users, the only value that will work is drummeruser. 

#### Returns
true

#### What it does
Deletes all index entries for the indicated collection. You're basically saying you want to start over with the index. Then you can either make changes to the outlines you want to include in the index to get them re-indexed, or use the daytona.ping verb. 

#### Note
daytona.removeOutlineRefs is more selective, it only removes references to one outline, not all of them. 

#### Example
daytona.resetMyIndex ()

> *true*

## daytona.removeOutlineRefs
#### Syntax
daytona.removeOutlineRefs (urlOutline, collection)

#### Params
The first param is the address of the public outline that you want removed from your Daytona index.

The second param is the collection you want it removed from. It can be scriptingnews, drummerdocs or drummeruser.  It's optional, if not present the default value is drummeruser.

#### What it does
Deletes all index entries for the indicated outline, so you can start over with the outline. We will do this with our blog.opml files when we archive the outline, removing all index references for the blog.opml file. If you don't, there will be double-references for posts that were archived, and even worse the ones that come from blog.opml won't be there if you click through the Eye icon to see the context. 

#### Returns
true

#### Example
daytona.removeOutlineRefs ("http://drummer.scripting.com/cluelessnewbie/blog.opml")

> *true*


# dialog verbs
## dialog.alert
#### Syntax
dialog.alert (string)

#### Params
The string is displayed in a dialog with a single button, OK.

#### Returns
The value undefined.

#### Example
dialog.alert ("It's sunny outside.")

> *undefined*

## dialog.ask
#### Syntax
dialog.ask (prompt, default, placeholder)

#### Params
All parameters are strings.

prompt is displayed over the text box, it's the question the user is meant to answer.

default is the initial string in the text box.

placeholder is a string that appears in the text box when it's empty.

#### What it does
A dialog with a text box and two buttons appears. The buttons are labeled Cancel and OK.

The user can enter text to replace the default text, and then press Cancel or OK.

If the user clicks Cancel, dialog.ask returns the value undefined. If the user clicks OK, it returns the string that's in the text box, as modified by the user. 

#### Returns
The string the user entered if they pressed OK, or the value undefined if Cancel.

#### Example
dialog.ask ("Favorite color?", "blue", "A color like blue or red goes here.")

> *orange*

## dialog.confirm
#### Syntax
dialog.confirm (string)

#### Params
The string is displayed in a dialog with two buttons, Cancel and OK.

#### Returns
A boolean, true if the user clicked OK, false if Cancel.

#### Example
dialog.confirm ("Really erase all files on your computer?")

> *true*

## dialog.about
#### Syntax
dialog.about (string1, string2)

#### Params
The first string is the text of an OPML file. The second string is the title of the dialog, which is optional. 

#### What it does
Displays the outline in a dialog, with the title at the top. 

#### Returns
undefined.

#### Example
dialog.about (http.readUrl ("http://scripting.com/states.opml"), "States outline")

> *undefined*


# dns verbs
## dns.getDomainName
#### Syntax
dns.getDomainName (dottedid)

#### Returns
The domain name associated with the dotted id. This is often referred to as "reverse DNS."

#### Common error
There is no domain associated with the provided dotted id.

#### Example
dns.getDomainName ("52.217.74.35") 

> *s3-website-us-east-1.amazonaws.com*

#### Limits
It only returns one domain name, but there might be more than one domain mapped to a given IP address. 

## dns.getDottedId
#### Syntax
dns.getDottedId (name)

#### Returns
Return the dotted id associated with the name. This is often referred to as "DNS lookup."

#### Common error
The domain is not defined. 

#### Bug
When there's an error, the error message is undefined.

#### Example
dns.getDottedId ("scripting.com")

> *52.217.103.83*

dns.getDottedId ("feedbase.io")

> *157.230.11.43*

dns.getDottedId ("asdfasdf.wtf")

> *208.113.174.22*


# drummer verbs
## drummer.productname
#### Syntax
drummer.productname ()

#### Params
None

#### Returns
The name of the Drummer app.

#### Notes
At first it might seem silly to have a verb that tells your script the name of the Drummer app, but these things do change sometimes. 

For example, there was a scripting language in the Fargo app, and it's possible someone might run one of its scripts here. 

fargo.version is implemented here, so you can find out that this isn't Fargo anymore, if your script cares. 

When you've been doing this for a long time, the value of these kinds of hooks become apparent. 

#### Examples
drummer.productname ()

> *"drummer"*

## drummer.productnameForDisplay
#### Syntax
drummer.productnameForDisplay ()

#### Params
None

#### Returns
The name of the Drummer app in a form suitable for displaying in a dialog, or other kind of message to the user.

#### Examples
drummer.productnameForDisplay ()

> *"Drummer"*

## drummer.runScript
#### Syntax
drummer.runScript (string)

#### Params
The string is a bit of JavaScript code.

#### Returns
undefined.

#### Notes
The script text runs but I was hoping the value would be returned, but it's not.

In the second example below, nothing happens. 

#### Examples
drummer.runScript ("dialog.alert (\"Hello World\")")

> *undefined*

drummer.runScript ("100 * 12")

> *undefined*

## drummer.subscribeToOutline
#### Syntax
drummer.subscribeToOutline (string)

#### Params
The string is the URL of an OPML file.

#### What it does
The outline opens in a new tab, or if it's already open, Drummer brings the tab to the front.

#### Returns
true.

#### Notes
If the outline has a &lt;urlUpdateSocket> head element, Drummer will request updates from the server, and will automatically update the outline when the outline changes.

See the <a href="https://github.com/scripting/instantOutlines">instantOutlines project</a> for examples and code for this protocol. 

#### Examples
drummer.subscribeToOutline ("http://scripting.com/states.opml")

> *true*

## drummer.version
#### Syntax
drummer.version ()

#### Params
None

#### Returns
The current version of the Drummer software.

#### Examples
drummer.version ()

> *2.0.6*

## drummer.useStylesheet
#### Syntax
drummer.useStylesheet (string)

#### Params
The string is the URL of an CSS style sheet file.

#### What it does
Applies the style sheet to Drummer.

#### Returns
true.

#### Notes
We're using this <a href="https://stackoverflow.com/questions/14028113/load-different-css-stylesheet-with-javascript">Stack Overflow piece</a> as guidance. 

#### Example
drummer.useStylesheet ("http://scripting.com/misc/darkmodestyles.css")

> *true*


# file verbs
## file.exists
#### Syntax
file.exists (path)

#### Params
path points to a file in the remote file system.

#### Action
Determines if the file exists

#### Returns
True if it exists, false otherwise

#### Notes
If you try to read a file that doesn't exist, for example, your script will fail. If your application can work even if a file doesn't exist, then you should use this verb to see if it exists. 

#### Examples
file.exists ("prefs.json")

file.exists ("meaningOfLife.js")

## file.writeWholeFile
#### Syntax
file.writeWholeFile (path, text)

#### What it does
Creates a new private file, or overwrites an existing file, at the indicated path, with the contents of the second parameter.  It creates any folders needed to store the file if they don't exist. 

#### Returns
true.

#### Note
Files are, by default, private. If you want to create a public file, first create the private file then call file.makeFilePublic.

#### Examples
file.writeWholeFile ("hello.txt", "Hello World")

> *true*

file.writeWholeFile ("code/alert.js", "dialog.alert ('Yo')") 

> *true*

## file.readWholeFile
#### Syntax
file.readWholeFile (path)

#### What it does
Reads the file at the indicated path and returns its contents as a string. 

#### Returns
The contents of the file, as a string.

#### Example
file.readWholeFile ("hello.txt") 

> *Hello World*

## file.delete
#### Syntax
file.delete (path)

#### What it does
Tries to delete both a private file or a public one at the indicated path. It's an error if neither file exists. 

#### Returns
undefined

#### Example
file.writeWholeFile ("deleteme.txt", "It's even worse than it appears.")

> *true*

file.readWholeFile ("deleteme.txt")

> *It's even worse than it appears.*

file.delete ("deleteme.txt")

> *undefined*

## file.getFileInfo
#### Syntax
file.getFileInfo (path)

#### Params
path is a string, the location to a file being stored on the server.

#### Returns
Information about the file, including: its size in bytes, when it was created, last read, last modified, and whether it's public or private.

If the file is public, urlPublic, the address of the file, is included. 

#### Example
file.getFileInfo ("states.opml") 

> *{*

file.getFileInfo ("scratchpad.opml")

> *{*

## file.makeFilePublic
#### Syntax
file.makeFilePublic (path)

#### What it does
Makes the file public if it is private. 

#### Returns
The public URL of the file. 

#### Example
file.makeFilePublic ("hello.txt")

> *http://drummer.scripting.com/davewiner/hello.txt*

http.readUrl ("http://drummer.scripting.com/davewiner/hello.txt")

> *Hello World*

## file.getFileHierarchy
#### Syntax
file.getFileHierarchy ()

#### What it does
Returns a JavaScript object that describes the user's file hierarchy.

There are two top-level branches, Private files and Public files. Unless you have explicitly made a file public, all files are private. 

Under each is the hierarchy, as they are stored in the file system on the server. For each folder there is a  whenCreated and a whenModified value, and an object called subs, which contains the files and any sub-folders.

For each file, in addition to creation and modification dates, ctChars is the size of the file.

#### Returns
A JavaScript object as explained above.

#### Notes
This feature is based on the <a href="https://github.com/scripting/folderToJson">folderToJson</a> package.

And the Outline file hierarchy command in the Tools menu is built on file.getFileHierarchy. 

#### Example
file.getFileHierarchy ()

> *{*

console.log (jsonStringify (file.getFileHierarchy ()))

> *undefined*


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
github.connectViaOauth ()

> *true*

localStorage.githubAccessToken //this is where you access token is stored

> *1234567890123456789012345678901234567890*

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
github.disconnect ()

> *true*

## github.download
#### Syntax
github.download (username, repository, path)

#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

The third string is a path to the object you want to download. 

#### Returns
A JavaScript object with information about the file, including its contents. 

#### Examples
base64.decode (github.download ("scripting", "Scripting-News", "/blog/stories/2020/02/15/a142106.md").content)

> *Questions for all Democratic candidates, esp <a href="http://scripting.com/2020/02/14/141155.html?title=presidentBloombergReallyADemocrat">Bloomberg</a>. Do you feel the president is above the law? If you are elected, will you use the new powers Trump has taken for himself? What will you do if Trump refuses to leave?*

github.download ("scripting", "Scripting-News", "/blog/stories/2020/02/15/a142106.md").size

> *319*

## github.getAccessToken
#### Syntax
github.getAccessToken ()

#### Params
None.

#### Returns
The access token if you're logged in, undefined if not. 

#### Example
github.getAccessToken ()

> *1234567890123456789012345678901234567890*

## github.getDirectory
#### Syntax
github.getDirectory (username, repository, path)

#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

The third string is a path to the directory you want a list of. 

#### Returns
A JavaScript object containing information about all the files in the directory. 

#### Examples
github.getDirectory ("scripting", "tmp1")

> *[*

github.getDirectory ("scripting", "Scripting-News", "/blog/opml/2017")

> *[*

## github.getUserInfo
#### Syntax
github.getUserInfo (string)

#### Params
The string, which is optional, is the username of the account you want the information of. 

#### Returns
If the username is not provided, github.getUserInfo returns a JavaScript object containing the user info for the current logged-in user. 

#### Examples
github.getUserInfo ()

> *{*

github.getUserInfo ("octocat")

> *{*

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
github.upload ("scripting", "tmp1", "hello.txt", "Hello World")

> *{*


# http verbs
## http.client
#### Syntax
http.client (options, boolean)

#### Parameters
options is a JavaScript structure that defines the request. 

boolean indicates whether it uses a proxy server (true) or the request is made from the browser (false).

#### Returns
What the HTTP request returns.

#### Breakage
There will be breakage. If you want to use this now, be prepared to adjust your code later, and participate in the <a href="https://github.com/scripting/drummerRFC/issues/6">thread</a> on the RFC site. As long as this alert is here, assume your apps that use this verb will break.

#### Notes
This is meant to be a complete HTTP client that's accessible to Drummer programmers.  

In its first release in November 2021, it is far from complete. But it gives you a lot more power than the simpler <a href="http://docserver.scripting.com/?verb=http.readUrl">http.readUrl</a>. Most important probably is that http.client can do requests other than GET.

The options struct is what you would pass to a <a href="https://www.w3schools.com/jquery/ajax_ajax.asp">jQuery AJAX call</a>. Here's a list of values it looks for: 

> *type -- the HTTP method, such as GET, POST, HEAD. *

> *url -- the address the request is directed to*

> *data -- the data that is passed in the body of the request. *

> *params -- a JavaScript object containing the search params for the request. *

There's a new endpoint in <a href="https://www.npmjs.com/package/daveappserver">daveappserver</a> that acts as the proxy server for this verb. It is deployed at drummer.scripting.com.

It's named after the Frontier verb <a href="http://docserver.userland.com/tcp/httpClient">tcp.httpClient</a>, which had a very long param list. In this version I opted for a struct instead. The intention is to do all that the Frontier verb does in this verb, in Drummer.

#### Examples
http.client ({url: "http://drummer.scripting.com/now"}, true)

> *Fri Nov 05 2021 13:05:15 GMT-0400 (Eastern Daylight Time)*

## http.readUrl
#### Syntax
http.readUrl (string, boolean)

#### Parameters
The string is the http address of the page you want to read. 

The boolean indicates whether you want to go through a proxy server for the request. It's optional, and it's default value is true.

#### Returns
It makes an HTTP request and returns to the caller what the request returns. 

#### Notes
If you want to access a resource on the local machine, or one that is inaccessible to drummer.scripting.com for some reason, you must not use the proxy server. 

If you can make the request without using the proxy server it will be faster, and conserves resources. 

#### Examples
http.readUrl ("http://scripting.com/rss.xml", false).length

> *73700*

http.readUrl ("http://scripting.com/rss.xml", false).length

> *73700*

http.readUrl ("http://localhost:1410/now", false)

> *Mon Aug 09 2021 16:35:28 GMT-0400 (Eastern Daylight Time)*

## http.derefUrl
#### Syntax
http.derefUrl (string)

#### Parameters
The string is a shortened http address. In other words and address that points to another address.  

#### Returns
If the address is not a shortened url, it returns the address itself. If it is, it returns the address that it points to.

#### Notes
9/17/2021 by DW -- it does not work in the case that the address is not a shortened url. Not sure why, no time to investigate at this time. 

#### Examples
http.derefUrl ("https://tinyurl.com/yvfkvaps")

> *http://scripting.com/*

http.derefUrl ("https://scripting.com/")

> *http://scripting.com/*


# oldSchool verbs
## oldSchool.buildBlog
#### Syntax
oldSchool.buildBlog (boolean)

#### Params
The boolean, which is options, says whether or not you want all the data returned by Old School to be returned by this verb.

#### What it does
Calls drummercms.scripting.com telling it to build the user's Old School blog. 

#### Returns
The web address of the user's blog if the boolean is false, otherwise all the data Old School returns in the form of a JavaScript object.

#### Example
oldSchool.buildBlog ()

> *http://oldschool.scripting.com/cluelessnewbie/*

oldSchool.buildBlog (true)

> *{*

## oldSchool.getCursorLink
#### Syntax
oldSchool.getCursorLink ()

#### Params
None.

#### Returns
The URL of the rendering of the bar cursor headline, if it's part of a blog. 

The file must have a head-level <i>urlBlogWebsite</i> attribute, if not oldSchool.getCursorLink returns undefined. 

If the cursor points into a titled post, the URL points to the specific line in the post the cursor points to.

#### Note
This functionality is wired into the Eye icon.

#### Example
oldSchool.getCursorLink ()

> *http://clueless.lucky.wtf/2021/11/14.html#a232957*


# opml verbs
## opml.parse
#### Syntax
opml.parse (string)

#### Params
The string is OPML text. 

#### What it does
Parses the text and returns a standard JavaScript object representing the outline.

#### Returns
A JavaScript object representing the outline.

#### Example
opml.parse (file.readWholeFile ("hello.opml"))

> *{*

## opml.stringify
#### Syntax
opml.stringify (object)

#### Params
object is a JavaScript object representing an outline. 

#### Returns
The OPML text for the object. 

#### Example
opml.stringify (opml.parse (file.readWholeFile ("hello.opml")))

> *&lt;?xml version="1.0" encoding="ISO-8859-1"?>*

> *&lt;opml version="2.0">*

## opml.attributes.addGroup
#### Syntax
opml.attributes.addGroup (string, object)

#### Params
The string is the name of an OPML file in the user's Drummer account.

The object is a collection of attributes in the form of a JavaScript object.

#### What it does
The value of the object replaces is added to the file-level attributes in the OPML file.

Any previous attributes that are not in the object are not changed, and are still there.  

#### Returns
The attributes of the file after the opml.attributes.setAll call.

#### Example
opml.attributes.addGroup ("tmp.opml", {school: "Bronx Science", gpa: 3.5, major: "Art History"})

> *{*

## opml.attributes.deleteOne
#### Syntax
opml.attributes.deleteOne (string, string)

#### Params
The first string is the name of an OPML file in the user's Drummer account.

The second string is the name of an attribute.

#### What it does
Drummer deletes the named attribute in the file, if it exists.

If the attribute doesn't exist, it is not an error.

#### Returns
The attributes of the file after the opml.attributes.deleteOne call.

#### Example
opml.attributes.deleteOne ("tmp.opml", "height")

> *{*

## opml.attributes.exists
#### Syntax
opml.attributes.exists (string, string)

#### Params
The first string is the name of an OPML file in the user's Drummer account.

The second string is the name of an attribute.

#### Returns
true if the attribute exists in the file, false otherwise.

#### Examples
opml.attributes.exists ("tmp.opml", "major")

> *true*

opml.attributes.exists ("tmp.opml", "minor")

> *false*

## opml.attributes.getAll
#### Syntax
opml.attributes.getAll (string)

#### Params
The string is the name of an OPML file in the user's Drummer account.

#### Returns
All the elements of the &lt;head> section of the OPML file for the outline. 

#### Example
opml.attributes.getAll ("scratchpad.opml")

> *{*

## opml.attributes.getOne
#### Syntax
opml.attributes.getOne (string, string)

#### Params
The first string is the name of an OPML file in the user's Drummer account.

The second string is the name of an attribute.

#### Returns
The value of the named attribute.

If the attribute doesn't exist, the value returned is the JavaScript value undefined.

#### Example
opml.attributes.getOne ("tmp.opml", "name")

> *Bjorn Barker*

opml.attributes.getOne ("tmp.opml", "hometown")

> *undefined*

## opml.attributes.makeEmpty
#### Syntax
opml.attributes.makeEmpty (string)

#### Params
The first string is the name of an OPML file in the user's Drummer account.

#### What it does
Drummer deletes all the named attributes in the file.

#### Returns
The attributes of the file after the opml.attributes.deleteOne call.

#### Example
opml.attributes.makeEmpty ("tmp.opml")

> *{ }*

## opml.attributes.setAll
#### Syntax
opml.attributes.setAll (string, object)

#### Params
The string is the name of an OPML file in the user's Drummer account.

The object is a collection of attributes in the form of a JavaScript object.

#### What it does
The value of the object replaces all file-level attributes in the OPML file.

The object should contain only name-value pairs. 

#### Returns
The attributes of the file after the opml.attributes.setAll call.

#### Example
opml.attributes.setAll ("tmp.opml", {name: "Bjorn Barker", age: 32})

> *true*

## opml.attributes.setOne
#### Syntax
opml.attributes.setOne (string, string, value)

#### Params
The first string is the name of an OPML file in the user's Drummer account.

The second string is the name of an attribute.

value is a JavaScript string, or a value that can be coerced to a string. 

#### What it does
Drummer sets the value of the named attribute in the file.

The attribute might exist, in which case its value is overwritten, or it is created.

#### Returns
The attributes of the file after the opml.attributes.setOne call.

#### Example
opml.attributes.setOne ("tmp.opml", "height", 5.5 * 12)

> *{*

## opml.getCurrentObject
#### Syntax
opml.getCurrentObject ()

#### Params
None.

#### Returns
A JavaScript object with all the data contained in the current outline, accessible directly in JavaScript code.

#### Note
It does what opml.getCurrentOpml does, except instead of returning OPML text, it returns the same information as a JavaScript object. 

#### Example
opml.getCurrentObject ()

> *{*

## opml.getCurrentOpml
#### Syntax
opml.getCurrentOpml ()

#### Params
None.

#### Returns
The text returned is exactly what would be saved as OPML for the current outline. 

#### Example
opml.getCurrentOpml ()

> *&lt;?xml version="1.0"?>*

> *&lt;opml version="2.0">*

## opml.getMarkdown
#### Syntax
opml.getMarkdown (opmltext)

#### Params
opmltext is a string containing text in OPML format.

#### Returns
The markdown-from-outline algorithm that was implemented in Old School.

#### Notes
This is markdown text for publishing, not for interop with outliners. 

We add two newlines at the end of the text of every outline node.

We generate nothing for indentation, you can use that in your writing in any way that suits you.

We respect the <i>flSinglespaceMarkdown</i> attribute. When it's present and true, we only add one newline for the subs. We also generate an extra newline at the end of the subs. 

#### Example
Here's the example outline:

> *Foods I like*

Bagels has a flSinglespaceMarkdown attribute with the value true.

We ran this script.

> *console.log (opml.getMarkdown (op.getCursorOpml (false)))*

Which generated this text.

> *Cheese*

> *<br>*

> *Bagels*

> *<br>*

> *Everything*

> *Sesame*

> *Plain*

> *<br>*

> *Sauces*

## opml.getHeaders
#### Syntax
opml.getHeaders ()

#### Params
None.

#### Returns
All the elements of the &lt;head> section of the OPML file for the current outline. 

#### Example
opml.getHeaders ()

> *{     "title": "verbDocs",     "dateCreated": "Mon, 22 Mar 2021 16:14:46 GMT",     "dateModified": "Wed, 07 Apr 2021 15:45:15 GMT",     "expansionState": "5,6,7,9,11,13,17",     "lastCursor": "13",     "ownerTwitterScreenName": "davewiner",     "ownerName": "Dave Winer",     "ownerId": "http://twitter.com/davewiner",     "urlUpdateSocket": "ws://test.littleoutliner.com:1230/",     "longTitle": "",     "description": "" }*

## opml.setHeaders
#### Syntax
opml.setHeaders (object)

#### Params
The parameter is a JavaScript object containing the new values for the &lt;head> section of the OPML file for the current outline.

#### Returns
undefined.

#### Notes
The headers are not replaced by this call, it's additive. 

There is currently no way, from a script, to delete a head element.

#### Example
var headers = opml.getHeaders ();

headers.someRandomValue = number.random (1, 1000);

opml.setHeaders (headers);


# base64 verbs
## base64.encode
#### Syntax
base64.encode (string)

#### Params
The string is some text or data that you want to encode using the <a href="https://en.wikipedia.org/wiki/Base64">base64</a> algorithm.

#### Returns
The base64 encoding of the string.

#### Example
base64.encode ("Hello Dolly")

> *SGVsbG8gRG9sbHk=*

## base64.decode
#### Syntax
base64.decode (string)

#### Params
The string is <a href="https://en.wikipedia.org/wiki/Base64">base64</a>-encoded text.

#### Returns
The string that's decoded from the base64 encoded text.

#### Example
base64.decode ("SGVsbG8gRG9sbHk=")

> *Hello Dolly*

base64.decode (base64.encode ("It's a wonderful day in the neighborhood."))

> *It's a wonderful day in the neighborhood.*


# rss verbs
## rss.readFeed
#### Syntax
rss.readFeed (url)

#### Params
The url is the address of an RSS feed. 

#### Returns
A JavaScript object with the contents of the feed.

#### Note
It can handle most versions of RSS and Atom. 

#### Example
rss.readFeed ("http://scripting.com/rss.xml")

> *{*


# speaker verbs
## speaker.beep
#### Syntax
speaker.beep ()

#### What it does
Makes a standard beep sound on the computer's speaker.

#### Notes
It's useful for confirming an operation was done, or otherwise to attract the user's attention. 

#### Returns
undefined

#### Example
speaker.beep () === undefined

> *true*


# string verbs
## string.addCommas
#### Syntax
string.addCommas (number)

#### Params
The param is a large number that can be made easier to read by adding commas to it.

#### Returns
A string.

#### Examples
string.addCommas (11709445200)

> *11,709,445,200*

string.addCommas (12)

> *12*

string.addCommas ("abcdefghijklmnopqrstuvwxyz")

> *abcdefghijklmnopqrstuvwxyz*

## string.addPeriodAtEnd
#### Syntax
string.addPeriodAtEnd (string)

#### Params
string is a sentence that may not have a period at the end. 

#### Returns
The string, possibly with a period added at the end. 

#### Notes
It's a complicated and somewhat quirky algorithm. 

First we call string.trimWhitespace to remove any spaces or newlines at the beginning and end of the string.

Then, if the string ends with a period, comma, question mark, quote, colon, semicolon or exclamation point, we do nothing. Putting a period after these characters would usually be incorrect. 

Used in Radio3 to pre-process a linkblog post. 

#### Examples
string.addPeriodAtEnd ("I like ice cream")

> *I like ice cream.*

string.addPeriodAtEnd ("What is your favorite flavor?")

> *What is your favorite flavor?*

## string.beginsWith
#### Syntax
string.beginsWith (s, possibleBeginning, flUnicase)

#### Params
The first param is a string that might begin with the second param.

flUnicase, a boolean, is optional. If true the search is done regardless of the case of the characters. If true the match doesn't have to be exact regarding the case of the characters, so "hooray" will match "Hooray" or "hOOrAy" if flUnicase is true.

#### Returns
true if the string begins with the other, false if it doesn't.

#### Example
string.beginsWith ("hooray for hollywood", "hoo")

> *true*

## string.bumpUrlString
#### Syntax
string.bumpUrlString (string)

#### Params
string either undefined or the result of having called string.bumpUrlString. 

#### Returns
The next string in the sequence, as in a URL shortener application.

#### Notes
The first string it returns is 1, then 2, then it runs through the alphabet. After z it returns 00, then 01.

It can be used in implementing a URL shortener, to generate a sequence of strings, that can be used as aliases for another perhaps longer string. 

#### Examples
string.bumpUrlString (undefined)

> *1*

string.bumpUrlString ("z")

> *00*

string.bumpUrlString ("zz")

> *000*

string.bumpUrlString ("ZZ") //not case-sensitive

> *000*

## string.contains
#### Syntax
string.contains (s, whatItMightContain, flUnicase) returns boolean

#### What it does
Determines if one string contains another.

The third parameter, flUnicase, is optional, it defaults to true. 

#### Returns
true if the string contains the other, false if it doesn't.

#### Example
dialog.alert (string.contains ("http://november.com", "november")) //displays true

## string.countFields
#### Syntax
string.countFields (s, ch)

#### Params
s is a string, ch is a 1-character string.

#### Returns
The number of fields in the string, with fields determined by the character.

#### Examples
string.countFields ("scripting.com/2003/08/12.html", "/")

> *4*

string.countFields ("Do you know the way to San Jose?", " ")

> *8*

string.countFields ("Come hear Uncle John's Band.", "/")

> *1*

#### See also
string.nthField

string.lastField

## string.dayOfWeekToString
#### Syntax
string.dayOfWeekToString (number)

#### Param
A number between 0 and 6. 0 corresponds to Sunday, 6 to Saturday.

#### Returns
A string like "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" or the empty string. 

#### Errors
If the number is out of range it returns the empty string.

#### Example
string.dayOfWeekToString (3)

> *Wednesday*

#### See also
string.monthToString

## string.decodeXml
#### Syntax
string.decodeXml (string)

#### Params
A string that may include encoded XML.

#### Returns
The decoded version of the string.

#### Notes
We look for four strings: &amp;lt; &amp;gt; &amp;amp; and &amp;apos; and convert them to < > & and '.

At some point it may make sense to look for other strings. 

#### Examples
string.decodeXml ("&amp;lt;script&amp;gt;")

> *&lt;script>*

string.decodeXml ("Lennon &amp;amp; McCartney")

> *Lennon & McCartney*

## string.delete
#### Syntax
string.delete (string, index, count)

#### Params
The first parameter is a string that you want to delete characters from. 

The second parameter is the 1-based location of the first character to delete.

The third parameter is the number of characters to delete.

#### Returns
The result of deleting the characters from the string. 

#### Notes
If you try to delete more characters than are present, it deletes as many as it can.

If you try to delete starting past the end of the string, you end up deleting nothing.

#### Example
string.delete ("123456789", 3, 1)

> *12456789*

string.delete ("123456789", 2, 1000)

> *1*

string.delete ("123456789", 100, 3)

> *123456789*

## string.encodeHtml
#### Syntax
string.encodeHtml (string)

#### Params
A string that possibly contains HTML markup. 

#### Returns
The result of encoding angle brackets and quotes.  

#### Notes
If you try to delete more characters than are present, it deletes as many as it can.

If you try to delete starting past the end of the string, you end up deleting nothing.

#### Examples
string.encodeHtml ("Still diggin!")

> *Still diggin!*

string.encodeHtml ("I <b>love</b> a parade")

> *I &#60;b&#62;love&#60;/b&#62; a parade*

## string.endsWith
#### Syntax
string.endsWith (string1, string2, boolean)

#### Params
The first string is the one we're looking in.

The second is what we're looking for in the string.

The boolean says if the search is unicase (it's optional, if not present it's true).

#### Returns
True if the first string ends with the second. 

#### Examples
string.endsWith ("Hooray for Hollywood", "wood")

> *true*

string.endsWith ("Hooray for Hollywood", "Wood", false)

> *false*

string.endsWith ("Hooray for Hollywood", "wheat")

> *false*

## string.extensionToMimeType
#### Syntax
string.extensionToMimeType (string)

#### Params
The string is a path to a file.

#### Returns
Returns a <a href="https://en.wikipedia.org/wiki/Media_type#Common_examples_[10]">media type</a> corresponding to the extension of the file. 

For example, if the extension is .html, it returns text/html. 

If there is no extension or the extension isn't recognized, it returns undefined.

#### Note
string.extensionToMimeType calls the <a href="https://github.com/scripting/utils/blob/master/daveutils.js#L1182">daveutils</a> function httpExt2MIME. 

#### Examples
string.extensionToMimeType ("ideas.html")

> *text/html*

string.extensionToMimeType ("config.json")

> *application/json*

string.extensionToMimeType ("config.js")

> *application/javascript*

string.extensionToMimeType ("profile.png")

> *image/png*

string.extensionToMimeType ("profile.jpg")

> *image/jpeg*

## string.filledString
#### Syntax
string.filledString (character, count)

#### Params
The first parameter is a string which will be replicated.

The second parameter is the number of times it will be replicated.

#### Returns
A string containing a number of copies of the first parameter. 

#### Examples
string.filledString ("p", 10)

> *pppppppppp*

string.filledString ("123 ", 10)

> *123 123 123 123 123 123 123 123 123 123 *

string.filledString ("\t", 3)

> *   *

## string.formatDate
#### Syntax
string.formatDate (date, format, timezone)

#### Params
The first parameter is a JavaScript date object. 

The second parameter is a string containing a format spec, following <a href="https://man7.org/linux/man-pages/man3/strftime.3.html">strftime</a> standard.

The third parameter says what timezone you want the date to be in. 0 is GMT, -4 in US/Eastern. 

#### Returns
A string, representing the date, in the format specified, in the indicated timezone.

#### Notes
All three parameters are optional.

If the date is not specified, the current date-time is used.

If the format is not specified, we use "%c".

If the timezone is not specified, we use the timezone that the machine that ran the script is in.

#### Examples
string.formatDate (clock.now (), "%B")

> *March*

string.formatDate ()

> *Sun Mar 14 2021 11:24:53 GMT-0400 (Eastern Daylight Time)*

string.formatDate (clock.now (), "%l:%M %p")

> *11:21 AM*

string.formatDate (undefined, "%A, %B %e, %Y at %l:%M %p") + "."

> *Sunday, March 14, 2021 at 11:27 AM.*

## string.getRandomPassword
#### Syntax
string.getRandomPassword (count)

#### Params
count is the number of characters that will be in the random string that's generated.

#### Returns
A string of random characters.

#### Examples
string.getRandomPassword (20)

> *26mxjiulbv2br8jaeutj*

string.getRandomPassword (20)

> *pv8snpjvmbl4np4kh4mt*

## string.hashMD5
#### Syntax
string.hashMD5 (string)

#### Params
The string is the input to the <a href="https://en.wikipedia.org/wiki/MD5">MD5 encryption</a> algorithm.

#### Returns
The encrypted version of the string. 

#### Notes
You can tell with a lot of confidence that the sender who uses this function has a copy of the string without transmitting it. 

#### Examples
string.hashMD5 ("Spring forward, fall back.")

> *26d37b732af2a3caf47a0b2c9789a0ce*

string.hashMD5 ("It's even worse than it appears")

> *d7adfe509535ad6de49a8baf0fbf7a3d*

## string.innerCaseName
#### Syntax
string.innerCaseName (string)

#### Params
A string that contains words separated by spaces. 

#### Returns
The innerCase version of the string, which means capitalize the first letter after every space, then remove the spaces.

#### Notes
It's useful for creating a file name or URL from a title. 

#### Examples
string.innerCaseName ("The story of my life") + ".mp3"

> *theStoryOfMyLife.mp3*

## string.insert
#### Syntax
string.insert (source, dest, ix)

#### Params
source is a string that will be inserted into dest, also a string, and the 1-based index ix.

#### Returns
The result of the insertion.

#### Bugs
Behavior is unpredictable if ix is less than zero. 

#### Examples
string.insert ("Bull ", "My name is Mancuso.", 11)

> *My name is Bull Mancuso.*

string.insert ("Hello ", " from Hollywood", 1)

> * Hello from Hollywood*

## string.isAlpha
#### Syntax
string.isAlpha (ch)

#### Params
ch is a 1-character string.

#### Returns
True if it's an alphabetic character, false otherwise.

Alphabetic characters are A-Z and a-z.

#### Notes
If the string is longer than one character, it returns true if the first character is alphabetic, false otherwise.

#### Examples
string.isAlpha ("x")

> *true*

string.isAlpha ("1")

> *false*

string.isAlpha ("#")

> *false*

string.isAlpha ("123abc")

> *false*

#### See also
string.isNumeric

string.isWhitespace

string.isPunctuation

## string.isNumeric
#### Syntax
string.isNumeric (ch)

#### Params
ch is a 1-character string.

#### Returns
True if it's a numeric character, false otherwise.

Numeric characters are 0-9.

#### Notes
If the string is longer than one character, it returns true if the first character is numeric, false otherwise.

#### Examples
string.isNumeric ("4")

> *true*

string.isNumeric ("g")

> *false*

string.isNumeric ("#")

> *false*

string.isNumeric ("123abc")

> *true*

#### See also
string.isAlpha

string.isWhitespace

string.isPunctuation

## string.isPunctuation
#### Syntax
string.isPunctuation (ch)

#### Params
ch is a 1-character string.

#### Returns
True if it's a punctuation character, false otherwise.

Punctuation characters all characters that are not alpha, numeric or whitespace characters.

#### Notes
If the string is longer than one character, it returns true if the first character is numeric, false otherwise.

This function can in some cases be used to see if you need to add a period at the end of a sentence. 

#### Bugs
Admittedly, its definition is weird, it would probably be better to enumerate the characters that are punctuation, for example, period, comma, colon, semicolon. 

#### Examples
string.isPunctuation (" ")

> *false*

string.isPunctuation (".")

> *true*

string.isPunctuation (",")

> *true*

#### See also
string.isAlpha

string.isWhitespace

string.isNumeric

string.isPunctuation

string.trimWhitespace

## string.isWhitespace
#### Syntax
string.isWhitespace (ch)

#### Params
ch is a 1-character string.

#### Returns
True if it's a whitespace character, false otherwise.

Whitespace characters are " ", "\r", "\n", "\t" (i.e. blank, return, newline and tab).

#### Notes
If the string is longer than one character, it returns true if the first character is numeric, false otherwise.

#### Examples
string.isWhitespace (" ")

> *true*

string.isWhitespace ("\n")

> *true*

string.isWhitespace ("*")

> *false*

#### See also
string.isAlpha

string.isWhitespace

string.isNumeric

string.isPunctuation

string.trimWhitespace

## string.lastField
#### Syntax
string.lastField (s, ch)

#### Params
s is a string, ch is a 1-character string.

#### Returns
A string with the contents of the last specified field in the string, with fields determined by the character.

If ch doesn't appear in the string, it returns the whole string.

#### Bugs
If ch contains more than one character, the results are not easily specified.

#### Examples
string.lastField ("scripting.com/2003/08/12.html", "/")

> *12.html*

string.lastField ("oh the buzzing of the bees", " ")

> *bees*

string.lastField ("oh the buzzing of the bees", "123")

> *oh the buzzing of the bees*

#### See also
string.nthField

string.countFields

## string.lower
#### Syntax
string.lower (s) returns string

#### What it does
Converts the string to lower case. 

#### Returns
The lower case version of the string.

#### Example
dialog.alert (string.lower ("Everyone Do The Hamster Dance!"))

#### See also
string.upper

## string.maxStringLength
#### Syntax
string.maxStringLength (string, maxlength, flWholeWordAtEnd, flAddElipses)

#### Params
The first parameter is a string that you want to be sure isn't longer than the number in the second parameter.

flWholeWordAtEnd is an optional boolean param. If true, we don't leave a broken word at the end of the string. Defaults to true. 

flAddElipses is an optional boolean. If true, we add three periods at the end of the string. Defaults to true.

#### Returns
A string that is not longer than the indicated length.

#### Examples
string.maxStringLength ("I have a long story I would like to tell you. It begins like this.", 35)

> *I have a long story I would like ...*

string.maxStringLength ("You know nothing Jon Snow." , 80)

> *You know nothing Jon Snow.*

## string.markdownProcess
#### Syntax
string.markdownProcess (string)

#### Params
The string contains markdown text that you want to be converted to HTML.

#### Returns
The HTML rendering of the string.

#### Notes
We use <a href="https://github.com/StackExchange/pagedown">Pagedown</a>, the Markdown processor used on Stack Exchange. 

#### Examples
string.markdownProcess ("It's **even** worse than it appears.")

> *<p>It's <strong>even</strong> worse than it appears.</p>*

string.markdownProcess ("I read [Scripting News](http://scripting.com/).")

> *<p>I read <a href="http://scripting.com/">Scripting News</a>.</p>*

string.markdownProcess ("* one\n* two\n* three\n")

> *<ul>*

## string.mid
#### Syntax
string.mid (string, ix, ct)

#### Params
The first parameter is a string that you want to get characters from. 

The second parameter is the 1-based location of the first character to copy.

The third parameter is the number of characters to copy.

#### Returns
The result of extracting the characters from the string. 

#### Notes
If you try to delete copy characters than are present, it copies as many as it can.

If you try to copy starting past the end of the string, you end up copying nothing.

#### Example
string.mid ("123456789", 3, 1)

> *3*

string.mid ("123456789", 2, 1000)

> *23456789*

#### See also
string.delete

string.insert

## string.monthToString
#### Syntax
string.monthToString (number)

#### Param
A number between 0 and 11. 0 corresponds to January, 11 to December.

#### Returns
A string like "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December" or undefined. 

#### Examples
string.monthToString (0)

> *January*

string.monthToString (100)

> *undefined*

#### See also
string.dayOfWeekToString

## string.multipleReplaceAll
#### Syntax
string.multipleReplaceAll (s, replaceTable, flCaseSensitive, startCharacters, endCharacters)

#### Params
s is a string.

replaceTable is an object, where the name of each property is a string to search for, and its value is what you want it replaced with. 

flCaseSensitive, a boolean, determines if the search is case-sensitive. It's optional, if undefined, it defaults to false. 

startCharacters is an optional string, if specified we only look at text within the first string that begins with these characters.

endCharacters, also optional, if specified, we only look at text within the first string that ends with these characters.

#### Returns
A string, the result of the replacements.

#### Example
string.multipleReplaceAll ("This house costs $293,000.", {"house": "apartment", "293,000": "534,287"}) 

> *This apartment costs $534,287.*

#### See also
string.replaceAll

## string.nthField
#### Syntax
string.nthField (s, ch, n)

#### Params
s is a string, ch is a 1-character string, n is a number.

n is 1-based, i.e. the first field is 1, not 0.

#### Returns
A string with the contents of the specified field, with fields determined by the character.

#### Example
string.nthField ("scripting.com/2003/08/12.html", "/", 3)

> *08*

#### See also
string.lastField

string.countFields

## string.padWithZeros
#### Syntax
string.padWithZeros (number, ct)

#### Params
number is a number you want padded with zeros.

ct is the number of places you want the number padded to.

#### Returns
The padded version of the number as a string.

#### Notes
It's useful if you want all strings produced by the code to be the same length, regardless how large the numbers are.

#### Examples
string.padWithZeros (1200, 5)

> *01200*

string.padWithZeros (1, 4) + ".html"

> *0001.html*

#### See also
string.delete

string.insert

## string.popExtension
#### Syntax
string.popExtension (s)

#### Params
s is a string.

#### Returns
If the string has an extension, like .txt or .png, we return the string without the extension.

#### Example
string.popExtension ("myAffadavit.txt")

> *myAffadavit*

#### See also
string.popLastField

string.popTrailing

## string.popLastField
#### Syntax
string.popLastField (s, ch)

#### Params
s is a string, ch is a 1-character string.

#### Returns
A string without the last field, as determined by the character, used as a delimiter.

#### Notes
Useful if you want to replace the suffix of a file name with another suffix.

#### Examples
string.popLastField ("myDiary.html", ".") + ".json"

> *myDiary.json*

string.popLastField ("scripting.com/2021/03/13", "/")

> *scripting.com/2021/03*

#### See also
string.nthField

string.countFields

string.lastField

## string.popTrailing
#### Syntax
string.popTrailing (s, ch)

#### Params
s is a string, ch is a 1-character string.

#### Returns
A string without instances of the character at the end of the string

#### Example
string.popTrailing ("get rid of the dots please.........", ".")

> *get rid of the dots please*

#### See also
string.popLastField

string.popExtension

## string.randomSnarkySlogan
#### Syntax
string.randomSnarkySlogan ()

#### Params
None.

#### Returns
A slogan from Dave's collection. 

#### Notes
This is mostly for fun. Truthfully it's <i>only</i> for fun. Heh. ;-)

#### Examples
string.randomSnarkySlogan ()

> *People return to places that send them away.*

string.randomSnarkySlogan ()

> *This aggression will not stand.*

string.randomSnarkySlogan ()

> *All of this has happened before and all of this will happen again.*

string.randomSnarkySlogan ()

> *It's even worse than it appears.*

## string.replaceAll
#### Syntax
string.replaceAll (s, searchFor, replaceWith)

#### Params
All three parameters are strings.

#### Returns
The result of replacing all occurrences of the second string with the third, in the first. 

#### Example
string.replaceAll ("raise your hand if you're happy", " ", "---")

> *raise---your---hand---if---you're---happy*

#### See also
string.multipleReplaceAll

## string.stripMarkup
#### Syntax
string.stripMarkup (string)

#### Params
A string that might contain HTML markup.

#### Returns
The string without the HTML markup.

#### Example
string.stripMarkup ("Sometimes <b>you</b> don't <i>want</i> the <u>markup</u>.")

> *Sometimes you don't want the markup.*

## string.trimLeading
#### Syntax
string.trimLeading (string, ch)

#### Params
First parameter is a string, the second parameter is a 1-character string. 

#### Returns
The string without instances of the character at the beginning of the string. 

#### Example
string.trimLeading ("$$$$$We don't need the dollar signs at the beginning of this string.", "$")

> *We don't need the dollar signs at the beginning of this string.*

#### See also
string.trimTrailing

## string.trimTrailing
#### Syntax
string.trimTrailing (string, ch)

#### Params
First parameter is a string, the second parameter is a 1-character string. 

#### Returns
The string without instances of the character at the end of the string. 

#### Example
string.trimTrailing ("We don't need the question marks at the end of this string.?????", "?")

> *We don't need the question marks at the end of this string.*

#### See also
string.trimLeading

## string.trimWhitespace
#### Syntax
string.trimWhitespace (string)

#### Params
A string that might have whitespace at the beginning and/or end.

#### Returns
The string without whitespace characters at the beginning and end. 

#### Notes
Use this verb to allow comparisons between names or identifiers that might have whitespace around them. 

#### Example
string.trimWhitespace ("  All the whitespace is a problem.    ")

> *All the whitespace is a problem.*

string.trimWhitespace ("   Alice   ") == "Alice"

> *true*

#### See also
string.trimLeading

## string.upper
#### Syntax
string.upper (s) returns string

#### What it does
Converts the string to upper case. 

#### Returns
The upper case version of the string.

#### Example
dialog.alert (string.upper ("It's even worse than it appears."))

#### See also
string.lower


# tab verbs
## tab.getPublicUrl
#### Syntax
tab.getPublicUrl () returns string

#### What it does
If the outline in the current tab in the outliner is public, returns the HTTP address of the file. 

If the outline is private, returns undefined.

#### Returns
A web address or undefined.

#### Example
dialog.alert (tab.getPublicUrl ())

> *undefined*

## tab.openFile
#### Syntax
tab.openFile (string, string)

#### Params
The first string is the name of an existing outline file.  

The second string is optional, it's the title you want to appear in the tab. If not specified, the outline's title is displayed in the tab.

#### What it does
If the file is already open in a tab, that tab comes to the front. If not, and the file exists, it opens in a new tab. 

#### Returns
true

#### Common error
The file does not exist.

#### Examples
tab.openFile ("hello3.opml") 

> *true*

tab.openFile ("hello3.opml", "My Favorite File") 

> *true*

## tab.openInstantOutline
#### Syntax
tab.openInstantOutline (string, string)

#### Params
The first string is the URL of an instant outline descriptor file.  

The second string is optional, it's the title you want to appear in the tab. If not specified, the outline's title is displayed in the tab.

#### What it does
If the outline is already open in a tab, that tab comes to the front. If not, and the file exists, it opens in a new tab. 

#### Returns
true.

#### Bug
It has no way to report an error, if it couldn't open the outline, it still returns true.

#### Examples
tab.openInstantOutline ("http://instantoutliner.com/o0", "The states outline") 

> *true*


# webBrowser verbs
## webBrowser.openUrl
#### Syntax
webBrowser.openUrl (string)

#### Params
The string is a web address.

#### What it does
Opens the web page in a new browser tab or window.

#### Returns
true.

#### Example
webBrowser.openUrl ("http://scripting.com/") 

> *true*

