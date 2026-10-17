### Get lines from a text file.

```go
bytes, err := os.ReadFile("./dayTwo/dayTwoInput.txt")
if err != nil {
	fmt.Println(err.Error())
	os.Exit(1)
}
lines := strings.Lines(string(bytes))
```

### Join an array of strings

```go
reg := []string{"a", "b", "c"}
fmt.Println(strings.Join(reg, ","))
// a,b,c
```


## Parse a whole directory of template files and render one of them

```go
page := template.Must(template.ParseGlob("./fragments/*.html"))
fmt.Println(page.DefinedTemplates())
page.ExecuteTemplate(os.Stdout, "test.html", map[string]string { })
```