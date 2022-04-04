# Redirect std

- `cat` - redirect stdin to stdout

Merging files(Объединение файлов)
```
cat one.txt  > two.txt
```

- `sort` - sorting strings of text by alphabet

- `uniq` - message about duplicates files and remove them.

	- `-d` - delete not duplicats

- `wc` - (word count)out number symbol feed line, words and byts in every selected files.

	- `ls /bin /usr/bin | sort | uniq | wc -l` - print number of elements in output

- `grep` - find and print string, correspond of sample.

	- `grep` *sample* *file*

	- `-i` -  without case sensitive

	- `-v` - reverse print, outputing no match

- `head` - out a  first 10 string of file.

- `tail` - out a lasr 10 string of file.

	- `-n` - specify the number of words

	- `-f` - whatch last string in real time

- `tee` - read std in and print std out together write to file

- `>` - redirect stdout to other file(rewrite file).

- `>>` - redirect stdout to file, but don't rewrite this file

- `2>` - redirect stderr to file 

Redirect stdout and syderr to one file

```
ls -l /home > example.txt 2>&1
``` 

- `&>` - redirect stdout and and stderr to one file

*Delete output, just redirect ot /dev/null*

- `> /dev/null`

- `<` - redirect stdin

Redirect stdint from file
```
cat < test.txt
```

- `|` - symbol of conveyor. Stdout first command redirect to stdin second command

