### Git remove files/folders that are are already tracked but ignored
```shell
git rm -r --cached <target> # wipe out file/folder from index (not working tree)
git add .
git commit -m "fix: stop tracking ignored files"
```
tldr wipe out all the files and restore the entire file tree from git.

### Have git normalize line endings
add `.gitattributes` file to repo directory with these contents
```
* text=auto
```
this won't immediately have an effect after committing this file.
force an update with
```shell
git add --renormalize .
```
