### Git remove files/folders that are are already tracked but ignored
`git rm -r --cached .`
> [!note]
> **-f** force git clean won't run by default when config option `clean.requireForce` is set.
> **-d** by default git clean will not recurse into untracked directories, setting d will make git recurse into these directories.
> **-x** remove only files ignored by git.
