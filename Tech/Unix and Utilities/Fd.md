## Summary
```bash
-t, --type filetype
   f, fileregular files  
   d, dir, directory  
		  directories  
   l, symlink  
		  symbolic links  
   b, block-device  
		  block devices  
   c, char-device  
		  character devices  
   s, socket  
		  sockets  
   p, pipenamed pipes (FIFOs)  
   x, executable  
		  executable (files)  
   e, empty  
		  empty files or directories
-I, --no-ignore
-H, --hidden
-g, --glob #  Perform a glob-based search instead of a regular expression search.
-s, --case-sensitive
-e, --extension ext
-E, --exclude <glob>
	Examples:
		--exclude '*.pyc'
		--exclude node_modules
-j, --threads num
-x, --exec command
	Execute command for each search result in parallel (use --threads=1 for sequential command execution).
```

## Find all powershell scripts in directory recursively.
```bash
fd -t f -e ps1
```

## Find all powershell scripts in directory recursively. and exclude files that have '/packages' in their location
```bash
fd -t f -e ps1 -E '**/packages/**'
```
