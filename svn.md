SVN CheatSheet
--------------

## Basics

```bash
svn checkout http://server.somewhere.com/repos/project_name/trunk/ project_name
cd project_name
svn status
svn up
svn diff file.txt
svn commit -m "A message"
svn commit -m "A message" thisfileonly.txt
```

## New Project

If a new project with directory `new_project` which contains the current
copy of the project code.  The following commands will import the project
to the server

```bash
cd new_project
# making server directories
svn mkdir --parents -m "Creating new project." http://server.somewhere.com/repos/new_project/trunk/
svn mkdir -m "Creating new project" http://server.somewhere.com/repos/new_project/tags/
svn mkdir -m "Creating new project" http://server.somewhere.com/repos/new_project/branches/
# Import current code
svn import -m "Import new project" . http://server.somewhere.com/repos/new_project/trunk/
```

## RCS

 * get - `svn propget svn:keywords file.txt`
 * set - `svn propset svn:keywords "Date Revision Author Id" file.txt`
 * edit - `svn propedit svn:keywords file.txt`

Once the RCS keywords are set on the file you can add them to the file.

```javascript
  this.version = "$Revision$";
```

which will become

```javascript
  this.version = "$Revision: 47592 $";
```

## Ignore

 * edit - `svn propedit svn:ignore file.txt`

```
target
*.log
```
