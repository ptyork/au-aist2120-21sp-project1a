# Project 1a: Word Mirror 

This is a simple little utility with a twist. I can't really think of a useful purpose for this particular script in real life, but the general concept of parsing and modifying a file word-by-word is VERY useful. Regardless, the goal is to reverse the letters of each individual word in a given input file. 

The script, `reversi.py`, should: 

1. Open the file specified as the first argument to the script (see below)
2. Read the file one line at a time (i.e., for line in file)
3. Split the contents of each line into words (no argument passed to split so you split on whitespace)
4. Iterate over each word in the line
    4a. Reverse the word (i.e., call your `mirror_word` function)
    4b. Append the reversed word (and a blank space) to a string
5. Print the entire reversed line to the screen (and continue to the next line)

Pay *VERY* close attention to these considerations. This is not intended to be as simple as just reversing a word or a sentence. Turning in a project that just does this will result in a very disappointing grade.

Be sure to read all of these instructions carefully. The hints at the bottom will also really help if you're feeling a little unsure.

## CONSIDERATIONS

1. If a "word" is empty or just whitespace, return nothing.

2. When mirroring a "word", be careful to check for punctuation and deal with that correctly. Especially words followed by periods, commas, etc. But also words starting or ending with quotation marks. Pay attention to periods, question marks, exclamation points, commas, quotation marks, semi-colons, and dashes. E.g.:
    - battle, ==> elttab,
        * __not__ ,elttab
    - "rejoicing ==> "gniciojer
        * __not__ gniciojer"
    - tribulation," ==> noitalubirt,"
        * __not__ ",noitalubirt __or__ "noitalubirt,

3. If a "word" is __JUST__ punctuation (like em dash "--"), then just return the word unscrambled.

## REQUIRED IMPLEMENTATION NOTES 

1. You MUST abstract your most useful logic by creating a function named `mirror_word` that takes a "word" and returns the reversed version (properly implementing the considerations above). This function must be "called" as your step 4a above, which will make the main script much cleaner. In other words, the *main* part of your script should open the file, loop through each line, split each line into "words", and call the following function for each individual "word": 

``` 
        def mirror_word(the_word): 
          ... REVERSE THE WORD ...
          return reversed_word   # or whatever variable contains the reversed "word"
``` 

2.  You MUST modify kennedy.txt, replacing John F. Kennedy's name with your own. __JUST edit and save the file using Mimir, VS code, or any another text editor. No Python code required here.__

3.  You MUST then reverse `kennedy.txt` and redirect the output to `mirror_kennedy.txt`. In other words, you should run `python reversi.py kennedy.txt > mirror_kennedy.txt`. This mirrored file should be in your final submission. __DO NOT WRITE TO A FILE INSIDE OF YOUR SCRIPT. ONLY READ AND PRINT. WRITING OCCURS HERE BY REDIRECTING OUTPUT.__

    *Note: If you do output redirection in Windows Powershell (the default shell for VS Code), it outputs writes the file using Unicode, which can cause issues. Use a standard Command Prompt (cmd.exe) if running this in Windows. Should not have any issues on Mac or Linux (and thus Mimir).*

When done, be sure to test the heck out of this and then submit the __project1 directory__ in Mimir.

## OPTIONAL CHALLENGES 

1. If the original word was title case, make the reversed word title case, as well. In other words "Kennedy" would become "Ydennek".

2. Create a second version of the script, `reversi2.py`. This version should import the mirror_word function from wmirror (`from reversi import mirror_word`). Instead of requiring a file name and reading the text from the file, instead read in the text line-by-line from sys.stdin. This should allow you to run it interactively AND to pipe in text from another command (e.g., `type kennedy.txt | python wmirror2.py`).

## HINTS 

1. The "arguments" to a python program are in the sys.argv list. The first element in the list is the name of the script and the rest are any additional words (arguments) added to the end. [See here for explanation](https://www.tutorialspoint.com/python/python_command_line_arguments.htm). The code needed may look as follows:
    ```
    import sys

    filename = sys.argv[1]
    ```

2.  For consideration #2 above, you might start off your mirror_word function by creating prefix and suffix strings. Start each as an empty string. Then "move" each punction character from the beginning of the word to the prefix string and any from the end to the suffix string. Then at the end, just concatenate and return the prefix, the word, the suffix and a space. The first part (moving the prefix characters) may look similar to:
    ```
        reversed_word = the_word    # make a copy of the function parameter to modify
        punctuation = '.?!,"\';:-'

        # String the prefix chars
        prefix = ''
        while len(reversed_word) > 0 and reversed_word[0] in punctuation:
            prefix = prefix + reversed_word[0]
            reversed_word = reversed_word[1:]
    ```
    The suffix is a LITTLE different--removing letters from the end of the word (i.e., `reversed_word[-1]` instead of `reversed_word[0]`), slicing all but the LAST letter (i.e., `reversed_word = reversed_word[:-1]`), and being careful to append them in the right order. But very similar.
