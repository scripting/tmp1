
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
undefined

undefined

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
undefined

undefined

## file.readWholeFile
#### Syntax
file.readWholeFile (path)

#### What it does
Reads the file at the indicated path and returns its contents as a string. 

#### Returns
The contents of the file, as a string.

#### Example
undefined

## file.delete
#### Syntax
file.delete (path)

#### What it does
Tries to delete both a private file or a public one at the indicated path. It's an error if neither file exists. 

#### Returns
undefined

#### Example
undefined

undefined

undefined

## file.getFileInfo
#### Syntax
file.getFileInfo (path)

#### Params
path is a string, the location to a file being stored on the server.

#### Returns
Information about the file, including: its size in bytes, when it was created, last read, last modified, and whether it's public or private.

If the file is public, urlPublic, the address of the file, is included. 

#### Example
undefined

undefined

## file.makeFilePublic
#### Syntax
file.makeFilePublic (path)

#### What it does
Makes the file public if it is private. 

#### Returns
The public URL of the file. 

#### Example
undefined

undefined

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
undefined

undefined

