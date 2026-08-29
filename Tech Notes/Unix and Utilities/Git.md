### Git remove files/folders that are are already tracked but ignored
`git rm -r --cached .` clear the whole cache (this will wipe out the physical directory files but keep the git files in tact.)
```shell
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
