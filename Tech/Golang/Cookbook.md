### Get lines from a text file.

```go
bytes, err := os.ReadFile("./dayTwo/dayTwoInput.txt")
if err != nil {
	fmt.Println(err.Error())
	os.Exit(1)
}
lines := strings.Lines(string(bytes))
```