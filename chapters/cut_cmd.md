# Column/Field Selection (cut)

`cut` allows user to select a range of character columns or fields from a text file.

## Character Selection
Specific column selection can be used to extract columns from Fixed Record Length files.

#### General format of `cut` with character selection:
```bash
$ cut -cCCC,CCC... < file
```
* CCC: one or more column ranges to select.  A range is either a single column number or range of columns in the form `a-b`.

#### Character Selection Examples:
```bash
$ head -4 input_users.txt
USER_ID:ACCT_NUM:USER_NAME
3:5555:David
5:789:Carol
11:5555:Carol

$ head -4 input_users.txt | cut -c2-6
SER_I
:5555
:789:
1:555

$ head -4 input_users.txt | cut -c1,3,5
UE_
355
579
1:5
```
It also comes in handy when you need to crop wide output of program.
```bash
$ ps -aef  | cut -c1-75
.... (output will now fit on screen without wrapping) ...
```

## Field Selection
#### General format of `cut` with field selection:
```bash
$ cut -dD -fFFF,FFF,... < file
```
* D: field delimiter character.
* FFF: one or more field ranges to select.  A range is either a single field number or range of fields in the form `a-b`.

#### Field Selection Examples:
```bash
$ head -4 input_users.txt | cut -f1,3 -d:
USER_ID:USER_NAME
3:David
5:Carol
11:Carol
```

## Known Issues
* Does not handle fields separated by multiple spaces.
* Not all implementations can handle field reordering (e.g. `$ cut -f2,1`)
