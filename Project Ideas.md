## Make which-key for the shell.
- assign commands to emacs like key chords.
- create a tui that displays the keyboard.
- should look like
- prepopulate the tui with existing commands not created in config.

### Questions
- should I build it like zellij/tmux/screen, create a ui shell to host the actual keyboard runner.
- which lang should I use?
	- use rust + ratatui
___
## Make a groupme clone
- use asp.net core
- use sqlite
- use datastar
- make a rest endpoint
### Questions
- how do I use frontend libraries with datastar. For example tabulator
	- can I have tabulator read from a datastar signal?
- how should I handle authentication/autorization

___
## My own custom Speed reading application.

### Requirements
- Speed read text from a pdf
- demo in this video intro: [rsv app](https://www.youtube.com/watch?v=0UDhADj2Ljk)
- read text from some file and speed read content
	- txt file content
	- pdf content
	- docx content
### Domain info
- [RSVP](https://en.wikipedia.org/wiki/Rapid_serial_visual_presentation)
### Dependency docs
- [pdfpig](https://github.com/UglyToad/PdfPig/wiki)
- [webui frontend](https://webui.me/docs.html#/)
  - [Csharp lib](https://github.com/salvadordf/WebUI4CSharp)
___
## File include obsidian plugin
Want to use this to edit config files from multiple sources from one easy place obsidian.

- Make an obsidian plugin that can embed a file in a markdown note from any directory on the filesystem. 
- We can also signify a line number range or several ranges to embed the file. 
- We can also edit this file directly from the markdown note.
___
## Git source obsidian plugin.
Want to create an obsidian plugin that can pull a markdown file from some git repo. 
this file is then downloaded and automatically updates from the source with a command. uses the "source" frontmatter tag to descied the location to pull form.

- git url is specified in frontmatter. I run one command and it pulls the latest version of that file from repo and inserts the contents into the note. If contents already exist it updates the existing
- perhaps implement with git submodules?
- expand functionality to handle user edits with some kind of merge editor.