[Type and package guidance](https://stackoverflow.com/questions/42859693/golang-custom-struct-undefined-cant-import-correctly)
- Don't define types in main (usually)
- Don't try to import main in other packages
- Don't try to import both ways (import cycle)
- Always import from a lower level into a higher one (so mypkg into main)
- All folders are packages, put related data/functions in them and name them well