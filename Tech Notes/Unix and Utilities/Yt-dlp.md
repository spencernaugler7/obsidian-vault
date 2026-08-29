---
source: https://www.ditig.com/yt-dlp-cheat-sheet
---
Basic download
```bash
yt-dlp https://www.example.com/watch?v=example
```

Download entire playlist
```bash
yt-dlp -o "%(playlist_index)s - %(title)s.%(ext)s" https://www.example.com/playlist?list=example
```

Download chapters as separate files
```
yt-dlp --split-chapters "URL" -o "%(title)s - %(chapter)s.%(ext)s"
```

Batch download from file
```bash
yt-dlp -a urls.txt #Each URL must be on its own line.
```

Download only audio
```bash
yt-dlp -x --audio-format mp3 https://www.example.com/watch?v=example
```


Add random delays to avoid bans
```bash
yt-dlp --sleep-interval 5 --max-sleep-interval 10 "URL"
```