# Python

* branch dev-python

## Algorithm

### main program:
- clean_up(source): clean up file manually (or with small code) beforehand
- read_source(source): load file and store all lines in a list
- set_types(): read each line and determine its type
- process_lines(): read each line and break person blocks if needed
- store_result(target): store all modified lines in target file

*Notes: "lines", "types" and "current" are global variables, so the "core" functions have not arguments*

### clean_up(source):
- clean up text so that it can be predictably/easily be processed (do it manually and/or with small add hoc functions using regular expressions) so that at the end:
    - person name should be on a separate line, all in uppercase (with no punctuation)
    - directions must be within parenthesis, on a separate line
    - transitions should be on separate lines and contain one the "keyword" : [TITLE, TITRE, SCENE, ACT, FIN, END]
    - apart from first line, all main lines should have an empty line before them
    - there should not be several empty lines following each other

### read_source(source):
- read and analyse "source" text file and store it into "lines" (list of strings):
    - open source and store in "file" object
    - read all lines from file and store in "lines"

### set_types():
- For each "line" in lines, determine its type and store it into "types" (a list of string):
    - a type is assigned to each line based on the following rules:
        - directions: if line starts with "("
        - transition: if line contains a keyword
        - person: if it is all caps
        - blank: if it is empty
        - script : in all other cases
    - use append to add to "types", so that both "lines" and "types" end up with equal length

### process_lines():
- For each line in lines, do the following depending on the corresponding line "type":
    - <u>transition</u>:
        - set "current" to null (ie: we are not in a person block)
    - <u>person</u>:
        - set "current" to that name (ie: we are starting a person block)
    - <u>direction</u>:
        - if (current is null) or (previous line is name) or (next line is blank and following line is main) then: pass (do nothing)
        - else **insert** (= insert blank line + line with current named before it)
    - <u>script</u>:
        - if current is null then **error** (= add a line with "ERROR" before it - to be processed manually afterwards)
        - else if previous line is script then **insert**
        - else **process_script(line)** *(see below : break it if more than 200 characters, and process the 2nd part recursively)*

### store_result(target):
- Store result in "target" text file
    - open target file
    - write all lines to file

### process_script(txt):
- if txt contains less than 200 characters then
    - return txt
- else, for each symbol in ".?!;:, ":
    - if there are at least 70 characters txt before and after that symbol then:
        - "before" = txt until and including that symbol
        - "insert" = blank line + line with current name
        - "after" = txt after (excluding) that symbol
        - return process_script(before) + insert + process_script(after)
