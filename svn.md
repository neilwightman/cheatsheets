SVN CheatSheet
--------------

## Basics

```bash
svn checkout http://server.somewhere.com/dir/project_name/trunk/ project_name
cd project_name
svn status
svn up
svn diff file.txt
svn commit -m "A message"
svn commit -m "A message" thisfileonly.txt
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
