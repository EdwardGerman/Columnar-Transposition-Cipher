# Problem about *`Columnar Transposition Cipher`* (CTC)
#### The solve problem of *Columnar Transposition Cipher* without *keyword* and with *unknown split size*
This solve based on ***`Natural Language Processing`*** (NLP)
---
---
#### ***Contents***
- About
- Solution
- Description of project files and folders
- How to run
---
## **About**

More details about Columnar Transposition can be found [here](https://en.wikipedia.org/wiki/Transposition_cipher#Columnar_transposition)
And in particular about CTC [here](https://en.wikipedia.org/wiki/Transposition_cipher#Columnar_transposition)

### Problel conditions:
There is a text that encode as follows: 
- All letters are converted to lowercase
- All characters except (including 'space' and '\n') letters are removed from the text
At this stage, we get all text in one string
- The resulting string split on pieces same length. 
- This pieces are recorded graduatly in the table one under the other (we get **'pieces table'**).
- The columns of this table are shuffled
- Then in the same way table graduatly are converted to string.
This string is a encoded text.

**It is necessary**:  restore the original text sequence.

---
## **Solution**
### ***Main idea***
The main idea of this solution is that in natural language the frequency of different letter combinations (pairs of letters) is different. Therefore, even if the text length is small, it is quite simple to identify the correct pairs from the mixed columns.

This problem is about finding the correct order of columns in a `shuffled pieces table`. It is clear that if you solve this problem by brute-force search, it will take a lot of time, so you need to use a different method.

#### How we do it:
Based on the choised texts we compilated *`parity tables`* - tables that show number of each letter pairs in the text. 
We know that in natural language, different letter pairs occur in different numbers. And we can build corresponding tables of pair coefficients (as will be show). Accordingly, the more a pair occurs, the greater its value in the table. 

Obviously, when we select columns from the **`pieces table`**, the product of *pair coefficients* for a correct column pair will be much larger than for an incorrect pair. So we need to generate a table called the **`Parity Factor Table`** (PFT), which contains all the products of the *pair coefficients* for all column combinations from the *shuffled pieces table*. In this table, there are exactly ***`split size - 1`*** factors that have values that are much larger than others (you can see this on the *Heatmap* and *3D visualization*). These factors correspond to the correct order of columns in the pieces table. 

Based on the PFT, we form a **`column pairs list`** (CPL) what contain column pairs with the highest Parity Factors. Then, based on the CPL, we restore the correct order of the columns by chain.



### ***Solution stages***
1. Parity tables compilation
    - Search and preparation of texts on which will be creation `Parity tables`
    - Processing of this texts for further use.
    - Compilation of the general text from the existing ones
    - Creationt of the basis parity table that contain quantitivity of letter pairs in general text
    - Compilation of the defferent variants of ***quantitivity***, ***frequency*** and ***biased*** *`parity tables`*
    
    Note! For Parity tables compilation we use texts with `spaces`
   
2. Text encoding
    - Text spliting
    - Making table (matrix), that contain columns of spliting text.
    - Shuffeling of the table columns.
    - Reconctruction text stucture from the shuffled table.
    
3. Decoding text when we know the **`split size`**.
    - Splitting encoded text.
    - Creating **`Parity Factor Table`** (PFT) (described in the notebook).
    - Detection of a column pairs with the largest PFT - ***`column pairs list`*** (CPL). It must contain **`split size - 1`** column pairs.
    - The restore of initial order of columns in text based on the CPL.
    - Text recovery.
  
4. Decoding text when **`split size`** is unknown.
    - In a for loop we do decoding operation with known the **`split size`** for each probable value of split size.
    - Checking of a CPL for correctness (must be like chain)
    - If CPL is correct, we restore initial order of columns and recovere the text.

---
## **Description of project files and folders**
! Note ! The file description was done in the order of their creation
- **preprocessing notebooks**:
    - Letters_pairs_preproc_for_test.ipynb - processes the text for `test`
    - Letters_pairs_preproc_for_train.ipynb -  processes the text for `train` and creates of `parity tables`. Contains some statistics on text files

- **Noteboks for parity tables**:
    - Letters_pairs_Creating_tables.ipynb - notebook for creation and compilation of the defferent variants the *`parity tables`*
    - Letters_pairs_Stat_Visual.ipynb - notebook for statistics and visualization on the *`parity tables`*

- **Notebooks with solutions (main notebooks)**
    - Letters_pairs_Encoding_Decoding.ipynb - problem solution with known ***split size***
    - Letters_pairs_Unknown_SplitSize.ipynb - problem solution without ***split size***

- **Additional notebooks (not used in this project)**
    - Letters_pairs_preproc.ipynb - nb for processesing
    - Letters_pairs_preproc_Hamlet.ipynb - nb for processesing
    - Letters_pairs_Examples.ipynb - contains examples of algorithm codes, that used in project
    - Letters_pairs_functions.ipynb - contains several program functions, that used in project. Due to the complexity of using functions in Colab, that places in separate notebooks, we not use it.

- **Folders**:
    - Data - initial (natural) text files for `train` and `parity tables`
    - Data_pp - text files for `train` after preprocessing
    - Data_test - initial (natural) text files for `test`
    - Data_test_pp - text files for `test` after preprocessing
    - Data_add - additional text files (not used in this project)
    - Parity_tables - contain `.csv` tables,  in particular `parity tables`

---
## **How to run**

1. Open **Google Colab** [here](https://colab.research.google.com/)
2. Open `File -> Open notebook` (this can open automatically)
3. In the opened window go to section **`GitHub`**
4. Enter a GitHub **`URL`** into correspond field (line) and press *`find`* icon.
5. Under this line will appear a list with repository notebooks.
6. Open notebook what you want to run.
7. Run this notebook in Colab: `Runtime -> Run All`.  Associated data files are mounted automatically (in 2nd cell)

You can load this notebook on your resourse or change this code in a current session, but you don't can write changes in GitHub.














