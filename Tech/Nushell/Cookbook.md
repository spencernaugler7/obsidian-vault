## Find Command

```nu
help commands | where name like <search string>
```

## Declare variables

```nu
let a = "Hello"
mut b = 3
const c = 4
```

## Arrays

```nu
let sampleArray = [22,5,10,8,12,9,80]
let sampleArray = ["Blah","Foo","Bar","Baz"]
```

## Get the Type of the return value of an object

```nu
ls | describe
# => table<name: string, type: string, size: filesize, modified: datetime> (stream)
```

## Comparison Operators

```nu
(1 == 1) and (1 == 2)   # Result is False
```

## Get All Drives On Computer

```nu
sys disks
```

## Get Available Disk Space

```nu
sys disks | first | get device mount free
```

## Get Local Time

```nu
date now
```

## Select Property on File

```nu
ls | get modified
```

## Change Property on File

```powershell
Get-ChildItem .\test.txt | %{ $_.LastWriteTime = '09/20/2026 06:00:36' }
## ----------- or ------------
(Get-Item .\test.txt).LastWriteTime = '01/11/2002 06:00:36'

```

## Get Property Value from File

```powershell
Get-ChildItem .\test.txt | %{ $_.CreationTime, $_.LastWriteTime }
# ------------- or ------------
(Get-ChildItem .\test.txt).CreationTime
```

## Write To A File

```nu
sys mem | save mem.txt
open mem.txt
```

## String Interpolation

```nu
let name = "Smith"
let message = $"Hello, ($name)! Welcome to NuShell."
```

## Select property in pipeline

```nu
date | select modified
```

## Functions (Custom commands)

### Basic Function Definition

```nu
# def <name> [<parameters>]: <input type> -> <output type> { <body> }
def add [a: int, b: int] { $a + $b }

# <input type> is optional
# <output type> is optional
```

| Syntax in `[ ]`            | Meaning                                                 | Value when not given |
| -------------------------- | ------------------------------------------------------- | -------------------- |
| `name`, `name: type`       | Required positional parameter                           | (error)              |
| `name?`, `name?: type`     | Optional positional parameter                           | `null`               |
| `name = value`             | Optional positional parameter with a default            | the default          |
| `--flag`, `--flag (-f)`    | Switch (a `bool`; no type annotation allowed)           | `false`              |
| `--flag: type`             | Flag that takes a value                                 | `null`               |
| `--flag: type = value`     | Flag with a default value                               | the default          |
| `...rest`, `...rest: type` | Any number of remaining positional arguments, as a list | `[]`                 |

### Take Pipeline input

```nu
def testBlah [..] { $in * 2 }
# 4 | testBlah => 8
```
