# Redirect std

- `cat` - redirect stdin to stdout

Merging files(Объединение файлов)
```
cat one.txt  > two.txt
```

- `sort` - sorting strings of text

- `uniq` - message about duplicates files and remove them.

- `wc` - out number symbol feed line, words and byts in every selected files.

- `grep` - find and print string, correspond of sample.

- `head` - out a  first string of file.

- `tail` - out a lasr string of file.

- `tee` - read std in and print std out together write to file

- `>` - redirect stdout to other file(rewrite file).

- `>>` - redirect stdout to file, but don't rewrite this file

- `2>` - redirect stderr to file 

Redirect stdout and syderr to one file

```
ls -l /home > example.txt 2>&1
``` 

- `&>` - redirect stdout and and stderr to one file

Delete output, just redirect ot /dev/null

- `> /dev/null`

- `<` - redirect stdin

Redirect stdint from file
```
cat < test.txt
```
