# System Project
Nischal DHUNGANA  
Antoine CHARVIN

## SEARCH ENGINE

### ABOUT
This script will browse through a file tree of text files to search for sentences corresponding to keywords entered by users in
the graphical interface.

### PREREQUISITES
customtkinter installation: `pip install customtkinter`  
PIL installation: `pip install pillow`  
scikit-learn installation: `pip install -U scikit-learn`  
stanza installation: `pip install stanza`

### USAGE
You must have a tree structure of text files in the same directory as the script.
The script will extract all sentences from the files and index them. It will then keep only the significant words, that is,
words longer than 4 letters and those starting with a capital letter.
It will then return the corresponding sentence(s) and the number of the files they belong to.

### STRUCTURE AND METHODS
The core of the program is located in the file `parse.py`. It contains the methods:
#### PARSE
This method allows separating all the sentences contained in the documents. It generates a `.json` file to view the separated sentences.

#### INDEX
This method allows indexing each sentence. It returns a dictionary with the sentences and their indexes.

#### WORDINDEX
This method allows generating a dictionary of significant words according to the sentences passed as an argument. Significant words are filtered as follows: a TF-IDF, words less than 4 letters are removed, and we keep all the words starting with a capital letter. It returns a `.json` file with the retained keywords.

#### LESSTHAN, STARTCAPITAL, TFIDF
These methods allow implementing the filters mentioned above. The tfidf is carried out using the scikit-learn package.

#### SEARCH
This method will be called by the graphical interface to search for matches between the user's keywords and the significant words. In the end, the method returns the sentence(s) that match with the keyword(s) as well as the documents to which these sentences belong. Thanks to the stanza package, the user can enter, for example, a verb in the infinitive, and the method will also search for all the conjugations of this verb. The same goes for plurals.  
Example:  
keywords entered: "manger" (to eat)  
words that can match with "manger": "mangeait" (was eating), "manges" (you eat), "mangeons" (we eat), etc.

The user-facing part of the program is the file `gui.py`. It allows for more convenient use than a terminal for someone not accustomed to it. Several keywords can be entered; they will be separated by a split to conduct the search. Example:  
keywords entered: "légers brebis" (light sheep)  
keywords retained by the program: "Fromage" (Cheese), "Camembert"  

## ADDITION SINCE THE PRESENTATION ON THE MACHINE TUESDAY, DECEMBER 13
Added the "tfidf" method in the file `parse.py` to perform tfidf on documents, thanks to the scikit-learn package.  
Added stanza to manage cases of singulars/plurals and verb conjugations.
