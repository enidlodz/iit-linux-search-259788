> This is the demonstration how to use Linux commands to process strutured text data.

### 0. How many lines are in fullnames_with_age.txt?

Put screenshot from Codespaces illustrating the result here.
Correct screenshot should contain your github username in the shell, a command and the result.

Example:

![task 0](task0.png)

**Explanation** Write the explanation why the specific command was used.

Example: wc command is to count data in a given file. -l parameter is for counting lines.

### 1. How many lines in access_small.log have path /login?

![Task 1](task1.png)

**Explanation**

`grep "/login"` grabs all the lines with `/login` in them.

`wc -l` counts all the lines (note `-l` flag for lines)

### 2. How many different ages are in fullnames_with_age.txt?

![Task 2](task2.png)

**Explanation**

`grep -oP "age=\K[^ ]+` returns only the matching string (`-o`) after `=` (`\K`), finds any non-space character (`[^ ]`) as many times as it can (`+`). `-P` for PCRE.

`sort` sorts the returned data.

`uniq` grabs only the unique occurences of the users. Without `sort`, `uniq` does not work properly.

`wc -l` counts the returned lines (note `-l` flag for lines).

### 3. How many unique first names are in fullnames_with_age.txt?

![Task 3](task3.png)

**Explanation** 

`grep -oP "^\S+"` returns only the matching string (`-o`) from the beginning of a line (`^`), finding as many non-whitespace characters (`\S`) as it can (greedy, `+`).

`sort` sorts the returned data.

`uniq` grabs only the unique occurences of the users. Without `sort`, `uniq` does not work properly.

`wc -l` counts the returned lines (note `-l` flag for lines).

### 4. Which age is most frequent in fullnames_with_age.txt?

![Task 4](task4.png)

**Explanation**

`grep -oP "age=\K.*"` grabs lines that match the Perl-compatible regex pattern (`-p`), grab only the pattern word (`age=19`, `age=30`, etc). `\K` acts as a meta return, shifting the start of the returned string to that position (`age=19` becomes `19`, `age=30` becomes `30`, etc.). `.*` indicates "any character (`.`) any times (`*`) until whitespace".

The first `sort` arranges everything in order.

`uniq -c` counts all the occurences and returns the count in front of the value. Without the initial `sort`, `uniq -c` does not work properly.

`sort -nr` sorts numerically (`-n`) by the first value, and then reverses the order (`-r`) from increasing to decreasing.

`head -n 1` grabs the first (`-n 1`) line from the returned value.

### 5. Which username failed login most often in auth_small.csv?

![Task 5](task5.png)

**Explanation**

`grep -oP "^[^,]+,\K[^,]+(?=,[^,]+,FAIL$)"` returns only the string matching (`-o`) the Perl-compatible regex expression (`-P`) given. `^` sends the "cursor" to the beginning of the line, `[^,]+` finds any character that isn't a comma (`[^,]`) as many times as it can (`+`), `,\K[^,]+` meta returns the grep value to the position of the name and finds the name (`[^,]+`). We then use a positive lookahead that checks (`?=`), whether the rest of the line contains the structure of `,[^,]+,FAIL` (comma, any non-comma character as many times as possible, comma, `FAIL`), ending the checked line with a `$`. 

The first `sort` arranges everything in order.

`uniq -c` counts all the occurences and returns the count in front of the value. Without the initial `sort`, `uniq -c` does not work properly.

`sort -nr` sorts numerically (`-n`) by the first value, and then reverses the order (`-r`) from increasing to decreasing.

`head -n 1` grabs the first (`-n 1`) line from the returned value.

### 6. How many lines in system_small.log have ok=true?

![Task 6](task6.png)

**Explanation**

`grep "ok=true"` finds all the lines that contain `"ok=true"` in them.

`wc -l` counts the returned lines (note `-l` flag for lines).

### 7. Which level (INFO, WARN, ERROR) appears most often in system_small.log?

![Task 7](task7.png)

**Explanation**

`grep -oP "level=\K[^ ]+"` returns only the matching string (`-o`) after `=` (`\K`), finds any non-space character (`[^ ]`) as many times as it can (`+`). `-P` for PCRE.

The first `sort` arranges everything in order.

`uniq -c` counts all the occurences and returns the count in front of the value. Without the initial `sort`, `uniq -c` does not work properly.

`sort -nr` sorts numerically (`-n`) by the first value, and then reverses the order (`-r`) from increasing to decreasing.

`head -n 1` grabs the first (`-n 1`) line from the returned value.

### 8. What is the top 3 most common actions in app_small.log?

![Task 8](task8.png)

**Explanation**

`grep -oP "action=\K[^ ]+"` returns only the matching string (`-o`) after `=` (`\K`), finds any non-space character (`[^ ]`) as many times as it can (`+`). `-P` for PCRE.

The first `sort` arranges everything in order.

`uniq -c` counts all the occurences and returns the count in front of the value. Without the initial `sort`, `uniq -c` does not work properly.

`sort -nr` sorts numerically (`-n`) by the first value, and then reverses the order (`-r`) from increasing to decreasing.

`head -n 3` grabs the first three (`-n 3`) lines from the top of the returned values.

### 9. How many unique users are in app_small.log?

![Task 9](task9.png)

**Explanation**

`grep -oP "user=\K[^ ]+"` returns only the matching string (`-o`) after `=` (`\K`), finds any non-space character (`[^ ]`) as many times as it can (`+`). `-P` for PCRE.

The first `sort` arranges everything in order.

`uniq` returns only unique occurences (removes duplicates).

`wc -l` counts the returned lines.