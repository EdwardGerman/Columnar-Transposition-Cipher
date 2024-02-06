# Problem about *`Columnar Transposition Cipher`* (CTC)
#### The solve problem of *Columnar Transposition Cipher* without *keyword* and with *unknown split size*
This solve based on ***`Natural Language Processing`*** (NLP)

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
At first 
Ця задача зводиться до пошуку правильного порядку стовпців в shuffled pieces table. Зрозуміло, що якщо розв'язувати цю задасу повним перебором, то на це піде дуже багато часу, тому треба застосувати інший метод.
Відомо, що в natural language різні пари літер зустріаються в різній кількості. І ми можемо побудувати відповідні таблиці парних коєфіцієнтів (що буде продемонстровано). Відповідно, чим пара більше зустрічається, тим значення для неї в таблиці більше. 
В очевидь, коли ми підбираємо стовпці з pieces table, то для коректрой пари стовпців добуток парних коєфіцієнтів буде набагато бульше, ніж для некоректної. Таким чином ми повинні згенерувати таку таблицю - Parity Factor Table (PFT), яка містить всі добутки парних коєфіцієнтів явсіх комбінацій стовпців з shuffled pieces table. В цій таблиці рівно **`split size - 1`** факторів, які мають значення що набагато більші за інщі (це можна буде побачити на Heatmap та 3D visualization). Саме ці фактори відповідаю коректному порядку стовпців в pieces table. 
На основі PFT формуємо `column pairs list` (CPL) який містить пари стовпчиків з набільшими Parity Factors. Потім на основі CPL ланцюжком відновлюємо правильний порядок стовпців.

#### How we do it:
Based on the choised texts we compilated *`parity tables`* - tables that show number of each letter pairs in the text. 

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
## **Description of project files and directories**

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














