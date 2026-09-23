```bash
fd
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
-s, --case-sensitive
-e, --extension ext
-j, --threads num
-x, --exec command
	Execute command for each search result in parallel (use --threads=1 for sequential command execution).
```
