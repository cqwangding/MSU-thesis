# Modifications for latex package msu-thesis

## Motivation

The latex package [msu-thesis](https://ctan.org/pkg/msu-thesis) produced by [Alan Munn](https://ctan.org/author/munn) helps lots of students in their thesis writing. The provided template may not fully support some format requirements. Therefore, I have summarized some of the modifications needed to meet these format requirements. 

## Modifications

The modifications are based on version 2.9c

1. There will be page number missing if you disabled both \makecopyrightpage and \makededicationpage. To address this issue, add one line of code \pagestyle{plain}.

   ```
   % \makecopyrightpage
   % \makededicationpage
   \pagestyle{plain}
   ```

2. The copyright page is not formatted correctly. It should be all left aligned. You can modify the msu-thesis.cls file as follows:

   ```
   % make the copyright page
   \newcommand*{\makecopyrightpage}{%
   	\pagestyle{plain}
   	\clearpage
   	\thispagestyle{empty}
   	\vspace*{4in}
   	{\raggedright Copyright by\\\MakeUppercase{\theauthor}\\\thedate\\}% Author now uppercase 6/5/12
   	\clearpage}
   ```

3. If you have algorithms in your thesis, you need to have a LIST OF ALGORITHMS in the preliminary pages and add an entry to the TABLE OF CONTENTS for LIST OF ALGORITHMS. You can modify the latex template as follows:

   ```
   \let\oldlistofalgorithms\listofalgorithms
   \let\oldnumberline\numberline
   \newcommand{\algnumberline}[1]{Algorithm~#1:\hspace{1em}}
   \renewcommand{\listofalgorithms}{
     \let\numberline\algnumberline
     \oldlistofalgorithms
     \let\numberline\oldnumberline
   }
   \SingleSpacing
   \tableofcontents*
   \clearpage
   \listoftables
   \clearpage
   \listoffigures
   \clearpage
   \listofalgorithms
   \addcontentsline{toc}{chapter}{List of Algorithms}
   \clearpage
   ```

   
