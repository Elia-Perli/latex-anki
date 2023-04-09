#LATEX-ANKI
A simple script to enable using a normal tex editor to typeset you anki questions.

###usage
#####summary:

######preparing everything
0. Copy the file `parser_latex→anki.py` in a folder, let's say it has absolute path `FOLDR` 
1. Create special  `note type`  in Anki
2. Allow new import on Anki
3. Add a bash script to your bin folder
######actually convert into cards
4. type the latex document
5. run the command
6. import the .txt file


#####Non-summary

1. You should create on you anki a `note type` two new types:
  
  - The first one should be called "Basic-math", 
  to do this, from the anki home window Add→ Type→Manage→Add→"Add:Basic"→Type the name "Basic-math"
  Then, follow Add→Fields→Add→ Type the name "ID"→ Reposition → 1
  - For the second one:
    Add→ Type→Manage→Add→"Add:Cloze"→Type the name "Basic-cloze".
    Add→Fields→Add→ Type the name "ID"→ Reposition → 1
2. Just follow: Tools→Preferences→Basic→"New import/export handling" should be ON
3.  This is optional. At this point you can use the command by typing in the terminal `python parser_latex→anki.py dmd_DECK.tex` and it should work.
Nonetheless it's easier if you create a bash command like the one called `latex→anki` and replace *"/home/ape/Scrivania/Programming/Python/latex_anki/latex→anki/parser_latex→anki.py"* with your the `FOLDR` path where you have put the script.

##### The actual use
4. The format should be the following
``` 
	\begin{itemize}
		\item 1→Qual è la definizione di semigruppo? → p.23b
		\item 2→Qual è la definizione di monoide? → p.23b
		\item 3→Qual è la definizione di gruppo? → p.23b
		\item 4→Qual è la definizione di elemento invertibile a dx/sx; invertibile ? → p.24
		\item 5→Se un elemento di un semigruppo è invertibile {{c1::allora il suo inverso è unico}}. → clz

	\end{itemize}
 ```

You can put anything you want in the preamble of the document. The important is that you have only one "itemize" in all the file. Remember to add the new commands to anki as well.
Also, as you can see each question is defined by the format "tabtab \item {number} → QUESTION→ANSWER" . You can change in the code, pehearps the "→" might not be suitable for you (But on Ubunutu it's easy to type since you just have to press `AltGr+i`)
5. Assuming you are in a directory X, assuming in this directory there is a file called "dmd_DECK1.tex", to get the ankified version you just have to run `anki→latex dmd_DECK1.tex` . This should generate the file "dmd_DECK1_to_be_imported.txt", that you can import to anki
