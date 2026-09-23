```bash
rg [OPTIONS] PATTERN [PATH ...]
rg [OPTIONS] -e PATTERN ... [PATH ...]
rg [OPTIONS] -f PATTERNFILE ... [PATH ...]
rg [OPTIONS] --files [PATH ...]
rg [OPTIONS] --type-list
command | rg [OPTIONS] PATTERN
rg [OPTIONS] --help
rg [OPTIONS] --version
```

- `-e REGEX` 
- `-f PATTERNFILE`
- `-s, --case-sensitive`
- `-i, --ignore-case`
- `-v, --invert-match`
- `-U, --multiline # Ripgrep will lift the restriction that a match cannot include a line terminator.`
- `--no-ignore`
- `-t TYPE, --type=TYPE # run with --type-list to see all filetypes`