
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
`oldSchool.buildBlog ()`

- *http://oldschool.scripting.com/cluelessnewbie/*

`oldSchool.buildBlog (true)`

- *{*

<br/><br/>
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
`oldSchool.getCursorLink ()`

- *http://clueless.lucky.wtf/2021/11/14.html#a232957*

<br/><br/>
