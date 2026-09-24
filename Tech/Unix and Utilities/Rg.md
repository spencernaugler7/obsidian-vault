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
- `-g GLOB,--glob=GLOB`
	- match files that match glob
	- prepend glob with `!` to exclude example: ` rg -g "*.cs" -g !"*.aspx.cs" DateTime.Now`
- `-f PATTERNFILE`
- `-s, --case-sensitive`
- `-i, --ignore-case`
- `-v, --invert-match`
- `-U, --multiline # Ripgrep will lift the restriction that a match cannot include a line terminator.`
- `--no-ignore`
- `-t TYPE, --type=TYPE`
	- run with --type-list to see all filetypes
- `--type-add=TYPESPEC`
	- example: `rg --type-add 'foo:*.foo' -t foo PATTERN`
- `--no-messages`
	- remove "Permission denied" messages
- `-g GLOB, --glob=GLOB`
	- example: `rg '123456789012' -g '*.tf'`