# Group symbol

- `*` - any sequence (последовательность) of any characters

	- **Example:**

		- `*` - all name file

		- `*g` - all name begin g
		
- `?` - any one character

	- **Example:**

		- `Data???` - name started from 'Data' next three any symbol

- `[characters]` - any one character from  specified range

	- **Example:**

		- `[abc]*` - all name started from symbols: "a", "b", "c"
 
- `[!characters]` - any one character out of specified range

- `[[:class]]` - any one character belonding to thr specified class

- `.[!.]?*` - beggin on `.` next any other symbol next any different symbols

- `$((exprassions))` - mathematic exprassion

## Use the braces(фигурные скобки)

- `{1..5}` - 1,2,3,4,5

- `{A{1..3},B{3..5}}` - A1B3, A2B4, A3B5  

## Expansion of environment

- `$USER` - variable of environment username

- `printenv` - print list of environment

## Use expassion of command 

- `echo $(ls)`

## Quoting

- `"word word"` - qupoting only space

- `word_word`- quoting only space

- `'$(environment)'`- ignoring all expansion

- `\` - escape character
