SVN CheatSheet
--------------

## Basics

```bash

```

## RCS

 * get - `svn propget svn:keywords file.txt`
 * set - `svn propset svn:keywords "Date Revision Author Id" file.txt`
 * edit - `svn propedit svn:keywords file.txt`

Once the RCS keywords are set no the file you can add them to the file.

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
