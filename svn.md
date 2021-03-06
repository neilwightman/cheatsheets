SVN CheatSheet
--------------

## Basics

### Checkout

```bash
svn checkout http://yourserver.com/repos/project_name/trunk/ project_name
cd project_name
```
### Update

```bash
# Check status (svn help status - shows help about what the letters mean) 
svn status

# Update to HEAD
svn up
# Update to revision 30
svn update -r 30
```

### Diff

```bash
# Diff local changes to BASE
svn diff file.txt
# Diff a single change to the file at rev 1234
svn diff -c 1234 file.txt
# Diff local file to a rev 1234
svn diff -r 1234 file.txt
# Diff file.txt from rev 3000 to 3500 (file must exist at rev 3000 + 3500)
svn diff -r 3000:3500 file.txt
svn diff -r 3000:3500 http://yourserver.com/repos/project_name/file.txt
```

### Undelete

```bash
# Svn log to find revision file was deleted at
svn log -v
# Svn up to the revision before to recover files (rev of delete -1)
svn up -r 47870 file1.txt file2.txt
```

## Commit

```bash
# Commit all changes pending (svn status)
svn commit -m "A message"
# Commit only thisfileonly.txt
svn commit -m "A message" thisfileonly.txt
```

### Merge

```bash
cd branch/
# merge a single change from trunk to your branch
svn merge -c 12345 http://yourserver.com/repos/new_project/trunk/ .
```

```bash
cd branch/
# undo a specific change on trunk
svn merge -c -12345 .
```

```bash
# revert project directory to version 268
svn merge -r HEAD:268 .
```

### Revert

```bash
# undo local modifications to foo.c
svn revert foo.c
```

### Conflicts

```bash
$ svn update
Updating '.':
Conflict discovered in 'foo.c'.
Select: (p) postpone, (df) diff-full, (e) edit,
        (mc) mine-conflict, (tc) theirs-conflict,
        (s) show all options: p
C    foo.c
Updated to revision 5.
Summary of conflicts:
  Text conflicts: 1
$ svn resolve --accept theirs-conflict foo.c
Resolved conflicted state of 'foo.c'
$
```

## New Project

If a new project with directory `new_project` which contains the current
copy of the project code.  The following commands will import the project
to the server.

```bash
cd new_project
# making server directories
svn mkdir --parents -m "Creating new project." http://yourserver.com/repos/new_project/trunk/
svn mkdir -m "Creating new project" http://yourserver.com/repos/new_project/tags/
svn mkdir -m "Creating new project" http://yourserver.com/repos/new_project/branches/
# Import current code (all of it)
svn import -m "Import new project" . http://yourserver.com/repos/new_project/trunk/
# Checkout project from the server
cd ..
mv new_project new_project_old
svn checkout http://yourserver.com/repos/new_project/trunk/ new_project
```

*Warning* : the folder you do the import from is not placed under version control!

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

## Branch

 * tag - `svn copy http://yourserver.com/repos/new_project/trunk/ http://yourserver.com/repos/new_project/tags/release-1.0 -m "Tagging release 1.0"`
 * branch - `svn copy http://yourserver.com/repos/new_project/trunk/ http://yourserver.com/repos/new_project/branche/dev-1.x -m "Create branch 1.x"`

Using -r12345 will take a copy at a specific point.
