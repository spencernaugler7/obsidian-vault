## Make which-key for the shell.
- assign commands to emacs like key chords.
- create a tui that displays the keyboard.
- should look like
- pre-populate the tui with existing commands not created in config.

### Questions
- should I build it like zellij/tmux/screen, create a ui shell to host the actual keyboard runner.
- which lang should I use?
	- use rust + ratatui
___
## Make a groupme clone
- use asp.net core
- use sqlite
- use datastar
### Questions
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
Want to use this to edit config files from multiple sources from one easy place: obsidian.

- Make an obsidian plugin that can embed a file in a markdown note from any directory on the filesystem. 
- We can also signify a line number range or several ranges to embed the file. 
- We can also edit this file directly from the markdown note.
___
## Note auto population from source obsidian plugin.
Want to create an obsidian plugin. This plugin reads a  "source" frontmatter tag. the plugin then downloads the raw version of the source. Depending on the current contents of the note the plugin can do a copule things
1. Empty note: simply dump the raw contents into the note.
2. Note already has content? If the content in the note is the same as the pulled content do nothing. If the contents are different open a merge edit and resolve conflicts.
Plans for features.
- Initially just work with git repositories.
- Expand functionality to handle user edits with some kind of merge editor.
___
# Expand/Collapse all headings Obsidian plugin.
Add the ability to expand/collapse all headers in the current note.
Ways to run
1. command pallet item to expand/collapse all
2. right click in note option

More features
1. add option to automatically collapse all headers when first opening a note.