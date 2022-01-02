
# clock verbs
### clock.now
#### Syntax
#### Returns
### clock.waitSeconds
#### Syntax
#### Parameters
#### Returns
#### Notes

# date verbs
### date.convertToTimeZone
#### Syntax
#### Params
The date param is the date you want to convert to a different time zone. 

The string says how far from GMT and in what direction the other time zone is. For example -5 would be the string for the east coast of the United States, meaning five hours earlier than GMT. "0" is GMT. This param is optional, if not specified it is "0".

#### Returns
The date, expressed in the indicated time zone. 

If x is a date returned by this routine, you can use the JavaScript date functions to get components of a time, getHours, getMinutes, etc and they will return the correct values for the indicated time zone.

### date.dayGreaterThanOrEqual
#### Syntax
#### Params
#### Returns
#### Notes
### date.netStandardString
#### Syntax
#### Params
#### Returns
#### Notes
This is the format that's required for RSS feeds, OPML files and mail protocols. 

### date.sameDay
#### Syntax
#### Params
#### Returns
### date.sameMonth
#### Syntax
#### Params
#### Returns
### date.secondsSince
#### Syntax
#### Params
#### Returns
#### Notes
### date.tomorrow
#### Syntax
#### Params
#### Returns
### date.yesterday
#### Syntax
#### Params
#### Returns

# daytona verbs
### daytona.ping
#### Syntax
#### Params
The first param is the URL of a public outline containing the content you want to be included in your Daytona index.

#### What it does
#### Returns
#### Note
### daytona.query
#### Syntax
#### Params
The first param is a string that contains the string you want to search for.

#### Returns
### daytona.resetMyIndex
#### Syntax
#### Param
#### Returns
#### What it does
#### Note
### daytona.removeOutlineRefs
#### Syntax
#### Params
The first param is the address of the public outline that you want removed from your Daytona index.

#### What it does
#### Returns

# dialog verbs
### dialog.alert
#### Syntax
#### Params
#### Returns
### dialog.ask
#### Syntax
#### Params
All parameters are strings.

prompt is displayed over the text box, it's the question the user is meant to answer.

default is the initial string in the text box.

#### What it does
A dialog with a text box and two buttons appears. The buttons are labeled Cancel and OK.

The user can enter text to replace the default text, and then press Cancel or OK.

#### Returns
### dialog.confirm
#### Syntax
#### Params
#### Returns
### dialog.about
#### Syntax
#### Params
#### What it does
#### Returns

# dns verbs
### dns.getDomainName
#### Syntax
#### Returns
#### Common error
#### Example
### dns.getDottedId
#### Syntax
#### Returns
#### Common error
#### Bug

# drummer verbs
### drummer.productname
#### Syntax
#### Params
#### Returns
#### Notes
At first it might seem silly to have a verb that tells your script the name of the Drummer app, but these things do change sometimes. 

For example, there was a scripting language in the Fargo app, and it's possible someone might run one of its scripts here. 

fargo.version is implemented here, so you can find out that this isn't Fargo anymore, if your script cares. 

### drummer.productnameForDisplay
#### Syntax
#### Params
#### Returns
### drummer.runScript
#### Syntax
#### Params
#### Returns
#### Notes
The script text runs but I was hoping the value would be returned, but it's not.

### drummer.subscribeToOutline
#### Syntax
#### Params
#### What it does
#### Returns
#### Notes
If the outline has a &lt;urlUpdateSocket> head element, Drummer will request updates from the server, and will automatically update the outline when the outline changes.

### drummer.version
#### Syntax
#### Params
#### Returns
### drummer.useStylesheet
#### Syntax
#### Params
#### What it does
#### Returns
#### Notes

# file verbs
### file.exists
#### Syntax
#### Params
#### Action
#### Returns
#### Notes
### file.writeWholeFile
#### Syntax
#### What it does
#### Returns
#### Note
### file.readWholeFile
#### Syntax
#### What it does
#### Returns
### file.delete
#### Syntax
#### What it does
#### Returns
### file.getFileInfo
#### Syntax
#### Params
#### Returns
Information about the file, including: its size in bytes, when it was created, last read, last modified, and whether it's public or private.

### file.makeFilePublic
#### Syntax
#### What it does
#### Returns
### file.getFileHierarchy
#### Syntax
#### What it does
Returns a JavaScript object that describes the user's file hierarchy.

There are two top-level branches, Private files and Public files. Unless you have explicitly made a file public, all files are private. 

Under each is the hierarchy, as they are stored in the file system on the server. For each folder there is a  whenCreated and a whenModified value, and an object called subs, which contains the files and any sub-folders.

#### Returns
#### Notes
This feature is based on the <a href="https://github.com/scripting/folderToJson">folderToJson</a> package.


# github verbs
### github.connectViaOauth
#### Syntax
#### Params
#### What it does
Initiates an Oauth login with GitHub. 

When it's done, you will have an "access token" in local storage on the computer you're using.

#### Note
#### Returns
### github.disconnect
#### Syntax
#### Params
#### What it does
Removes the local access token, effectively logging you off GitHub. 

#### Returns
### github.download
#### Syntax
#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

#### Returns
### github.getAccessToken
#### Syntax
#### Params
#### Returns
### github.getDirectory
#### Syntax
#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

#### Returns
### github.getUserInfo
#### Syntax
#### Params
#### Returns
### github.upload
#### Syntax
#### Params
The first two strings identify a GitHub repository. The first is the username, and the second is the name of the repository in the user's GitHub account. 

The third string is a path to the object you want to upload. 

The fourth string is the data of the file to be created by the upload.

#### Returns

# http verbs
### http.client
#### Syntax
#### Parameters
options is a JavaScript structure that defines the request. 

#### Returns
#### Breakage
#### Notes
This is meant to be a complete HTTP client that's accessible to Drummer programmers.  

In its first release in November 2021, it is far from complete. But it gives you a lot more power than the simpler <a href="http://docserver.scripting.com/?verb=http.readUrl">http.readUrl</a>. Most important probably is that http.client can do requests other than GET.

The options struct is what you would pass to a <a href="https://www.w3schools.com/jquery/ajax_ajax.asp">jQuery AJAX call</a>. Here's a list of values it looks for: 

<i>type -- the HTTP method, such as GET, POST, HEAD. </i>
<i>url -- the address the request is directed to</i>
<i>data -- the data that is passed in the body of the request. </i>
There's a new endpoint in <a href="https://www.npmjs.com/package/daveappserver">daveappserver</a> that acts as the proxy server for this verb. It is deployed at drummer.scripting.com.

### http.readUrl
#### Syntax
#### Parameters
The string is the http address of the page you want to read. 

#### Returns
#### Notes
If you want to access a resource on the local machine, or one that is inaccessible to drummer.scripting.com for some reason, you must not use the proxy server. 

### http.derefUrl
#### Syntax
#### Parameters
#### Returns
#### Notes

# oldSchool verbs
### oldSchool.buildBlog
#### Syntax
#### Params
#### What it does
#### Returns
### oldSchool.getCursorLink
#### Syntax
#### Params
#### Returns
The URL of the rendering of the bar cursor headline, if it's part of a blog. 

The file must have a head-level <i>urlBlogWebsite</i> attribute, if not oldSchool.getCursorLink returns undefined. 

#### Note

# opml verbs
### opml.parse
#### Syntax
#### Params
#### What it does
#### Returns
### opml.stringify
#### Syntax
#### Params
#### Returns
### opml.attributes.addGroup
#### Syntax
#### Params
The string is the name of an OPML file in the user's Drummer account.

#### What it does
The value of the object replaces is added to the file-level attributes in the OPML file.

#### Returns
### opml.attributes.deleteOne
#### Syntax
#### Params
The first string is the name of an OPML file in the user's Drummer account.

#### What it does
Drummer deletes the named attribute in the file, if it exists.

#### Returns
### opml.attributes.exists
#### Syntax
#### Params
The first string is the name of an OPML file in the user's Drummer account.

#### Returns
### opml.attributes.getAll
#### Syntax
#### Params
#### Returns
### opml.attributes.getOne
#### Syntax
#### Params
The first string is the name of an OPML file in the user's Drummer account.

#### Returns
The value of the named attribute.

### opml.attributes.makeEmpty
#### Syntax
#### Params
#### What it does
#### Returns
### opml.attributes.setAll
#### Syntax
#### Params
The string is the name of an OPML file in the user's Drummer account.

#### What it does
The value of the object replaces all file-level attributes in the OPML file.

#### Returns
### opml.attributes.setOne
#### Syntax
#### Params
The first string is the name of an OPML file in the user's Drummer account.

The second string is the name of an attribute.

#### What it does
Drummer sets the value of the named attribute in the file.

#### Returns
### opml.getCurrentObject
#### Syntax
#### Params
#### Returns
#### Note
### opml.getCurrentOpml
#### Syntax
#### Params
#### Returns
### opml.getMarkdown
#### Syntax
#### Params
#### Returns
#### Notes
This is markdown text for publishing, not for interop with outliners. 

We add two newlines at the end of the text of every outline node.

We generate nothing for indentation, you can use that in your writing in any way that suits you.

### opml.getHeaders
#### Syntax
#### Params
#### Returns
### opml.setHeaders
#### Syntax
#### Params
#### Returns
#### Notes
The headers are not replaced by this call, it's additive. 


# base64 verbs
### base64.encode
#### Syntax
#### Params
#### Returns
### base64.decode
#### Syntax
#### Params
#### Returns

# rss verbs
### rss.readFeed
#### Syntax
#### Params
#### Returns
#### Note

# speaker verbs
### speaker.beep
#### Syntax
#### What it does
#### Notes
#### Returns

# string verbs
### string.addCommas
#### Syntax
#### Params
#### Returns
### string.addPeriodAtEnd
#### Syntax
#### Params
#### Returns
#### Notes
It's a complicated and somewhat quirky algorithm. 

First we call string.trimWhitespace to remove any spaces or newlines at the beginning and end of the string.

Then, if the string ends with a period, comma, question mark, quote, colon, semicolon or exclamation point, we do nothing. Putting a period after these characters would usually be incorrect. 

### string.beginsWith
#### Syntax
#### Params
The first param is a string that might begin with the second param.

#### Returns
### string.bumpUrlString
#### Syntax
#### Params
#### Returns
#### Notes
The first string it returns is 1, then 2, then it runs through the alphabet. After z it returns 00, then 01.

### string.contains
#### Syntax
#### What it does
Determines if one string contains another.

#### Returns
### string.countFields
#### Syntax
#### Params
#### Returns
#### Examples
string.countFields ("scripting.com/2003/08/12.html", "/")

string.countFields ("Do you know the way to San Jose?", " ")

### string.dayOfWeekToString
#### Syntax
#### Param
#### Returns
#### Errors
#### Example
### string.decodeXml
#### Syntax
#### Params
#### Returns
#### Notes
We look for four strings: &amp;lt; &amp;gt; &amp;amp; and &amp;apos; and convert them to < > & and '.

### string.delete
#### Syntax
#### Params
The first parameter is a string that you want to delete characters from. 

The second parameter is the 1-based location of the first character to delete.

#### Returns
#### Notes
If you try to delete more characters than are present, it deletes as many as it can.

### string.encodeHtml
#### Syntax
#### Params
#### Returns
#### Notes
If you try to delete more characters than are present, it deletes as many as it can.

### string.endsWith
#### Syntax
#### Params
The first string is the one we're looking in.

The second is what we're looking for in the string.

#### Returns
### string.extensionToMimeType
#### Syntax
#### Params
#### Returns
Returns a <a href="https://en.wikipedia.org/wiki/Media_type#Common_examples_[10]">media type</a> corresponding to the extension of the file. 

For example, if the extension is .html, it returns text/html. 

#### Note
### string.filledString
#### Syntax
#### Params
The first parameter is a string which will be replicated.

#### Returns
### string.formatDate
#### Syntax
#### Params
The first parameter is a JavaScript date object. 

The second parameter is a string containing a format spec, following <a href="https://man7.org/linux/man-pages/man3/strftime.3.html">strftime</a> standard.

#### Returns
#### Notes
All three parameters are optional.

If the date is not specified, the current date-time is used.

If the format is not specified, we use "%c".

### string.getRandomPassword
#### Syntax
#### Params
#### Returns
### string.hashMD5
#### Syntax
#### Params
#### Returns
#### Notes
### string.innerCaseName
#### Syntax
#### Params
#### Returns
#### Notes
### string.insert
#### Syntax
#### Params
#### Returns
#### Bugs
### string.isAlpha
#### Syntax
#### Params
#### Returns
True if it's an alphabetic character, false otherwise.

#### Notes
#### Examples
string.isAlpha ("x")

string.isAlpha ("1")

string.isAlpha ("#")

### string.isNumeric
#### Syntax
#### Params
#### Returns
True if it's a numeric character, false otherwise.

#### Notes
#### Examples
string.isNumeric ("4")

string.isNumeric ("g")

string.isNumeric ("#")

### string.isPunctuation
#### Syntax
#### Params
#### Returns
True if it's a punctuation character, false otherwise.

#### Notes
If the string is longer than one character, it returns true if the first character is numeric, false otherwise.

#### Bugs
#### Examples
string.isPunctuation (" ")

string.isPunctuation (".")

### string.isWhitespace
#### Syntax
#### Params
#### Returns
True if it's a whitespace character, false otherwise.

#### Notes
#### Examples
string.isWhitespace (" ")

string.isWhitespace ("\n")

### string.lastField
#### Syntax
#### Params
#### Returns
A string with the contents of the last specified field in the string, with fields determined by the character.

#### Bugs
#### Examples
string.lastField ("scripting.com/2003/08/12.html", "/")

string.lastField ("oh the buzzing of the bees", " ")

### string.lower
#### Syntax
#### What it does
#### Returns
#### Example
### string.maxStringLength
#### Syntax
#### Params
The first parameter is a string that you want to be sure isn't longer than the number in the second parameter.

flWholeWordAtEnd is an optional boolean param. If true, we don't leave a broken word at the end of the string. Defaults to true. 

#### Returns
### string.markdownProcess
#### Syntax
#### Params
#### Returns
#### Notes
### string.mid
#### Syntax
#### Params
The first parameter is a string that you want to get characters from. 

The second parameter is the 1-based location of the first character to copy.

#### Returns
#### Notes
If you try to delete copy characters than are present, it copies as many as it can.

#### Example
string.mid ("123456789", 3, 1)

### string.monthToString
#### Syntax
#### Param
#### Returns
#### Examples
string.monthToString (0)

### string.multipleReplaceAll
#### Syntax
#### Params
s is a string.

replaceTable is an object, where the name of each property is a string to search for, and its value is what you want it replaced with. 

flCaseSensitive, a boolean, determines if the search is case-sensitive. It's optional, if undefined, it defaults to false. 

startCharacters is an optional string, if specified we only look at text within the first string that begins with these characters.

#### Returns
#### Example
### string.nthField
#### Syntax
#### Params
s is a string, ch is a 1-character string, n is a number.

#### Returns
#### Example
### string.padWithZeros
#### Syntax
#### Params
number is a number you want padded with zeros.

#### Returns
#### Notes
#### Examples
string.padWithZeros (1200, 5)

### string.popExtension
#### Syntax
#### Params
#### Returns
#### Example
### string.popLastField
#### Syntax
#### Params
#### Returns
#### Notes
#### Examples
string.popLastField ("myDiary.html", ".") + ".json"

### string.popTrailing
#### Syntax
#### Params
#### Returns
#### Example
### string.randomSnarkySlogan
#### Syntax
#### Params
#### Returns
#### Notes
### string.replaceAll
#### Syntax
#### Params
#### Returns
#### Example
### string.stripMarkup
#### Syntax
#### Params
#### Returns
### string.trimLeading
#### Syntax
#### Params
#### Returns
#### Example
### string.trimTrailing
#### Syntax
#### Params
#### Returns
#### Example
### string.trimWhitespace
#### Syntax
#### Params
#### Returns
#### Notes
#### Example
string.trimWhitespace ("  All the whitespace is a problem.    ")

### string.upper
#### Syntax
#### What it does
#### Returns
#### Example

# tab verbs
### tab.getPublicUrl
#### Syntax
#### What it does
If the outline in the current tab in the outliner is public, returns the HTTP address of the file. 

#### Returns
### tab.openFile
#### Syntax
#### Params
The first string is the name of an existing outline file.  

#### What it does
#### Returns
#### Common error
### tab.openInstantOutline
#### Syntax
#### Params
The first string is the URL of an instant outline descriptor file.  

#### What it does
#### Returns
#### Bug

# webBrowser verbs
### webBrowser.openUrl
#### Syntax
#### Params
#### What it does
#### Returns
